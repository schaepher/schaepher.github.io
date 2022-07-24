# MySQL InnoDB 并发控制之 MVCC


MySQL 的多版本并发控制（Multiversion Concurrency Control，MVCC）解决了 InnoDB 事务隔离级别中读已提交和可重复读的读和写冲突问题。MVCC 使事务中执行普通的 SELECT 读取数据不需要对记录加锁，同时又能根据需要避免脏读、不可重复读、幻读的问题，提高了系统整体效率。

MVCC 要放在事务的框架中学习，因此下文会尽可能多地使用包含了“事务”的表述，用来增强读者脑中的“一个事务包含一条以上的 SQL”的印象。在此基础上要清楚如果没有显示地执行 `BEGIN` 开启事务或者 `set autocommit = 0` ，执行的单条 SQL 语句都会被 MySQL 作为一个事务执行。因此就可以通过事务的结构来统一地理解多条语句和单条语句的情况。

> 注：下文提到数据库中的“行”的概念时，会使用“记录”这一表述代替。

## 疑问有哪些？

在对 InnoDB 了解得很少时，会有以下的疑问：

1. 一条记录的多个版本是用什么区分的？是使用更新时间么？是使用版本号么？
2. 一条记录应该保留多少个版本？
3. 更新数据还未提交的时候，是不是有另外一块区域存放新数据，等到提交的时候才覆盖到数据页里原先的位置上？
4. 在启动事务后，另一个事务更新了数据，那么旧数据会存放在哪？
5. 是不是为每条记录都设置了独享的一块放置该数据的多个版本的内存或外存区域？
6. 如果两个事务都想修改同一个数据，会怎么处理？

## 记录与事务

如果思考的视角是记录本身，就会往记录本身的更新时间和版本号去思考。但是正如前文强调的，无论是 MVCC 还是 SQL 语句对记录的修改都离不开事务。既然如此，就可以把视角转移到记录和事务的关系上。一旦明确这个关系，就可以考虑将事务的 ID 作为记录的版本号了。

在记录上引入事务 ID 字段表示最近一次变更该记录的事务。当一个事务更新该记录或标记删除的时候，将记录的版本号更新为这个事务的 ID。

```c++
static inline void row_upd_rec_sys_fields(
    rec_t *rec,                /* 记录（record） */
    page_zip_des_t *page_zip,
    const dict_index_t *index, /* 聚集索引 */
    const ulint *offsets,
    const trx_t *trx,          /* 事务 */
    roll_ptr_t roll_ptr)
{
  if (page_zip) {
    // ... 省略
  } else {
    ulint offset = index->trx_id_offset;
    // ... 省略
    trx_write_trx_id(rec + offset, trx->id);  // <-- 就是这里
    // ... 省略
  }
}
```

## 未提交的更新存放在哪

通常情况下，如果数据没有提交，我们会认为它应该放在一个单独的地方。只有提交的时候，才把这些数据拿去覆盖原先的数据，否则其他事务在读取的时候，就会读取到未提交的数据。

MVCC 工作在读已提交和可重复读这两个事务级别上，说明使用 MVCC 的情况下不会出现读到未提交的数据。但是 MVCC 没有将未提交的数据单独存放，而是直接写入数据页，甚至会刷入磁盘。

> 见回答及其评论区：  
> [https://www.zhihu.com/question/278643174/answer/522384191](https://www.zhihu.com/question/278643174/answer/522384191)  
> 源码以后再找。

## 旧数据存放在哪

既然未提交的更新直接写入到数据页，那么原先的数据要怎么办？必然需要有一个地方存储旧数据的备份。

了解 InnoDB 的同学会知道 undo 日志的存在。undo 日志用于存储一个操作的反向操作，例如 insert 操作就是 delete；如果是 update，则产生一个更新回旧数据的 update。当事务回滚时执行 undo 日志中的操作达到恢复数据的效果。

## 旧数据会存多少个版本

与这个问题相关的是：如果两个事务同时修改一个记录，会如何处理？

其中一个事务会在记录上加锁，在其释放锁之前，另一个事务无法加锁，也就无法操作数据。于是不会出现 undo 日志中存在多个事务未提交的记录。由于 undo 日志存储的是逻辑日志，一个事务有可能多次修改同一个数据，那么一个记录就可能出现多次出现在 undo 日志中。

undo 日志是以事务为粒度划分区域还是全局呢？

undo 日志按事务划分，各自组成一条链。

MySQL 在初始化的时候会创建两个回滚表空间（undo_001 和 undo_002 这两个文件），每个表空间划分了 TRX_SYS_N_RSEGS = 128 个段（Segement），这些在回滚表空间的段又称为回滚段（Rollback Segment，源码中简写为 rseg）。undo 日志存储于回滚段中。

```c++
struct trx_t {
    // ... 省略
    UndoMutex undo_mutex;
    undo_no_t undo_no;
    space_id_t undo_rseg_space;
    trx_rsegs_t rsegs; /* 回滚段 */
    // ... 省略
}

struct trx_rsegs_t {
  trx_undo_ptr_t m_redo;   /* 系统崩溃后需要恢复的回滚日志 */
  trx_undo_ptr_t m_noredo; /* 系统崩溃后不需要恢复的回滚日志 */
};

struct trx_undo_ptr_t {
  trx_rseg_t *rseg;        /* 回滚段 */
  trx_undo_t *insert_undo; /* 插入操作的 undo 日志指针*/
  trx_undo_t *update_undo; /* 更新操作的 undo 日志指针*/
};
```



```c++
/** 事务系统中心内存数据结构 */
struct trx_sys_t {
  // ... 省略一些字段
  
  /** 多版本并发控制管理器 */
  MVCC *mvcc;

  /** serialisation_list 的互斥量 */
  TrxSysMutex serialisation_mutex;

  /** 追踪未提交的最小事务号 */
  UT_LIST_BASE_NODE_T(trx_t, no_list) serialisation_list;

  /** 为 MySQL 创建的事务列表 */
  UT_LIST_BASE_NODE_T(trx_t, mysql_trx_list) mysql_trx_list;

  /** 用于 MVCC 快照的一组读写事务 ID */
  trx_ids_t rw_trx_ids;

  // ... 省略一些字段
}
```

```c++
class ReadView {
  class ids_t {
    // ... 省略
    private:
      /** 大于等于此 ID 的事务修改的数据对该快照不可见 */
      trx_id_t    m_low_limit_id;

      /** 小于此 ID 的事务对数据的修改对该快照可见 */
      trx_id_t    m_up_limit_id;

      /** 创建该快照的事务 */
      trx_id_t    m_creator_trx_id;

      /** 当该快照被创建时，处于活动中的所有读写事务 */
      ids_t       m_ids;

      // ... 省略
  }

  // ... 省略
  public:
    bool changes_visible(trx_id_t id, const table_name_t &name) const {
    // ... 省略
    if (id < m_up_limit_id || id == m_creator_trx_id) {
      return (true);
    }

    check_trx_id_sanity(id, name);

    if (id >= m_low_limit_id) {
      return (false);

    } else if (m_ids.empty()) {
      return (true);
    }

    const ids_t::value_type *p = m_ids.data();

    return (!std::binary_search(p, p + m_ids.size(), id));
  }

}

void ReadView::prepare(trx_id_t id) {
  // ... 省略

  m_creator_trx_id = id;

  m_low_limit_no = trx_get_serialisation_min_trx_no();

  m_low_limit_id = trx_sys_get_next_trx_id_or_no();

  if (!trx_sys->rw_trx_ids.empty()) {
    copy_trx_ids(trx_sys->rw_trx_ids);
  } else {
    m_ids.clear();
  }

  m_up_limit_id = !m_ids.empty() ? m_ids.front() : m_low_limit_id;

  // ... 省略
}
```



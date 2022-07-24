# C 语言实现面向对象（一）：初步实现三个基本特征


这篇文章所使用代码的完整版见：[https://github.com/schaepher/c-objcet-oriented](https://github.com/schaepher/c-objcet-oriented)  

## 相关背景知识

### 面向对象

面向对象的三个基本特征是：封装、继承、多态。

<!-- more -->

- 封装  
    隐藏成员变量及成员方法。  
- 继承  
    子类可以使用现有类（父类）的所有功能，并在无需重新编写原来的类的情况下对这些功能进行扩展。  
- 多态  
    由继承而产生的相关的不同的类，其对象对同一消息会做出不同的响应。

### C 语言

C 语言的文件通常分为两种：用于声明的 `.h` 头文件，用于实现的 `.c` 文件。  

当我们要引用已有的功能时，会使用预编译指令 `#include` 将 `.h` 文件包含进来。由于 `.h` 文件仅包含定义的内容而不包含具体实现，因此客户端（调用者）无法了解和接触到具体的实现细节。  

C 语言的结构体在创建时会申请定长的内存空间，并按照结构体内部的结构体成员的声明顺序划分内存。在结构体指针做强制转换的时候，指针指向保持不变，内存保持不变。如果转为第一个成员的类型，则可以将其解释为第一个成员类型的指针。

## 实现三个基本特征

### 封装  

利用客户端无法访问到 `.c` 文件的内容来隐藏成员变量和成员方法。下面以隐藏成员变量为例，成员方法类似。

如果不考虑其他条件，那么可以很自然地想到把所有成员变量写在结构体中。例如：

```c
struct Animal
{
    char *type;
    char *name;
    int age;
};
```

如果把这段代码放到 `.h` 文件内部，则客户端引用 `.h` 后，可以在获取结构体指针后直接访问 type、name 和 age。

如果把这段代码放到 `.c` 中，`.h` 仅做声明 `struct Animal;`，那么客户端尝试访问内部属性时，就会碰到编译错误。  

> 为了方便和简洁，把该结构体的详细定义命名为 `_Animal`，然后使用 typedef 给结构体一个别名：  
> `typedef struct _Animal *Animal;`   
> 上面这部分见代码仓库里的 `incl/animal.h` 和 `src/animal.c`。

成员变量无法直接访问后，要提供简介访问这些变量的方法。先考虑最简单的方式：

`src/animal.c`:

```c
char *animalGetName(Animal this)
{
    return this->name;
}
```

### 继承

成员变量基于结构体存放元素时是按顺序的来做转换。  

```
 Animal    Human

+------+  +------+
| type |  | type |
+------+  +------+
| name |  | name |
+------+  +------+
| age  |  | age  |
+------+  +------+
          | id   |
          +------+
```

`src/animal.c`:

```c
struct _Animal
{
    char *type;
    char *name;
    int age;
};
```

而 Human 通过直接把 Animal 作为结构体的第一个成员，继承了 Animal 的属性。

`src/human.c`:

```c
struct _Human
{
    Animal animal;
    int id;
};
```

这时 `_Human` 相当于：

```c
struct _Human
{
    char *type;
    char *name;
    int age;
    int id;
};
```

而对于成员方法，则使用：

```c
char *humanGetName(Human this)
{
    return animalGetName((Animal)this);
}
```

因为此时 `src/human.c` 指 include 了 `src/animal.h`，所以还是不能直接接触 Animal 里 name 这个属性。

在将指针往父类转换后，实际上不会丢失子类的内容，内存还存在。因此指针还能再向子类转换。

## 多态

这里要做的是，当子类对象转换为父类的类型时，调用父类方法却得到子类方法的结果。

实现继承后，我们可以根据需要修改方法的实现，达到不同子类对象得到不同的结果。如下：

```c
char *humanGetName(Human this)
{
    char *prefix = "name: ";
    char *name = animalGetName((Animal)this);
    char *result = (char *)malloc(strlen(prefix) + strlen(name));
    strcpy(result, prefix);
    strcat(result, name);
    return result;
}
```

但是这并没有实现转换为父类类型时也能得到子类方法的结果。  

解决方法就是在结构体里面加上一个专门用于存这些方法指针的结构体（以下称之为：虚函数表），父类对象可以使用这些指针来调用子类的方法。

`src/animal.h`:  

```c
typedef struct AnimalVtb {
    void (*say)(void *this);
} AnimalVtb;
```

然后在原先的结构体里面，把虚函数表加到最前面，这样使得其与直接子类互相转换的时候比较方便。

`src/animal.c`:

```c
struct _Animal
{
    AnimalVtb *vptr;
    char *type;
    char *name;
    int age;
};

void animalInit(Animal this, AnimalVtb *vptr, char *type, char *name, int age)
{
    this->vptr = vptr;
    this->type = type;
    this->name = name;
    this->age = age;
}
```

子类在创建对象时，将虚函数表传到父类结构体。

`src/human.c`:

```c
void humanSay(void *this)
{
    Human human = (Human)this;
    printf("Hi, my name is %s, and my ID is %d!\n", humanGetName(human), humanGetId(human));
}

AnimalVtb humanVtb = {humanSay};

Human humanCreate(char *name, int age, int id)
{
    Human this;
    this = (Human)malloc(sizeof(Human));
    animalInit((Animal)this, &humanVtb, "human", name, age);
    this->id = id;
    return this;
}
```

这样调用父类方法时，可以直接使用这个函数指针：

`src/animal.c`:

```c
void animalSay(Animal this)
{
    (*this->vptr->say)(this);
}
```

客户端代码为：  

`src/main.c`：

```c
int main(void)
{
    Animal animal;
    Human human = humanCreate("ZhangSan", 25, 111);
    animal = (Animal)human;
    animalSay(animal);

    return 0;
}
```

# 问题

1. 多层级继承的情况下，没法再添加更多虚函数定义  
    例如有基类 Object，虚函数列表里有 A B C 三个函数指针。类 ObjectA 继承 Object，类 ObjectB 继承 ObjectA。此时类 ObjectA 无法再往虚函数列表里添加更多定义了。

2. 如果要添加接口，转换不了

要解决这些问题，需要有 Map 这种数据结构，将函数指针存放到 Map 里面。

# 参考资料

- C语言：春节回家过年，我发现只有我没有对象！  
  https://mp.weixin.qq.com/s/2ivQ9hcRvZnhk89jzAppSg
- 用C实现OOP面向对象编程（1）  
  https://www.cnblogs.com/findumars/p/6350092.html
- C语言的不完整类型和前置声明  
  https://blog.csdn.net/astrotycoon/article/details/41286413
- C语言实现多态  
  https://blog.csdn.net/dumpling5232/article/details/52632060

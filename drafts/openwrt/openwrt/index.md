# OpenWRT 软件安装和配置


注：如果提示软件无法安装，一般是因为没有执行 `opkg update`


目录：  

1. 支持 U 盘
2. U 盘扩容
3. 内网穿透
4. 科学学习
5. Supervisor


## 安装 supervisor

```sh
opkg update
opkg install curl
opkg install python3
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py
pip install supervisor
mkdir /var/log/supervisor
```



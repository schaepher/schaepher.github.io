# CentOS7 编译 Git


```bash
yum install -y make autoconf gcc zlib-devel gettext-devel
make config
./configure --prefix=/usr
make all
make install
```

https://git-scm.com/book/en/v2/Getting-Started-Installing-Git

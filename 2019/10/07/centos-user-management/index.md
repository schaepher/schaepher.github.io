# CentOS7 用户管理



## 基础操作

添加用户：  
`useradd -m username`  

`-m` 参数是为了给用户创建 home 目录。例如 /home/username

<!-- more -->

设置密码或修改密码：  
`passwd username`

用户加组：  
`gpasswd -a username groupname`

组移除用户：
`gpasswd -d username groupname`

删除用户：  
`userdel username`

## 允许用户执行 sudo

系统允许在 wheel 用户组内的用户执行 sudo：  
`gpasswd -a username wheel`


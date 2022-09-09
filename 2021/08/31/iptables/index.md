# iptables


https://www.digitalocean.com/community/tutorials/how-to-list-and-delete-iptables-firewall-rules#:~:text=Deleting%20Rules%20by%20Specification.%20One%20of%20the%20ways,the%20rules%20list%2C%20iptables%20-S%2C%20for%20some%20help.

## 禁止所有网卡访问 9093 端口

iptables -I INPUT -p tcp --dport 9093 -j DROP

--dport 一定要加在 -p tcp 后面，否则会提示没有该选项。

## 放行所有访问本机某个网卡的 9093 端口

iptables -I INPUT -d 192.168.1.101 -p tcp --dport 9093 -j ACCEPT

## 列出所有规则

iptables -L

## 列出 INPUT 链的所有规则

iptables -L INPUT

## 列出 INPUT 链的所有规则，带上序号

iptables -L INPUT --line-numbers

## 删除 INPUT 链的指定序号的规则

iptables -D INPUT 2


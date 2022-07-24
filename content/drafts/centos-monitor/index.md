---
title: CentOS Monitor
date: 2019-10-25 14:54:50
updated: 2019-10-25 14:54:50
tags:
---

`top -b -n 1 -c -H`

top -b -n 1 -c -H

cat c.txt |  sort -k3,3nr | less -S

cat c.txt | awk '{ sum+=$3 } END { print sum }'
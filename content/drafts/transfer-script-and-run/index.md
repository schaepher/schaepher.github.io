---
title: transfer-script-and-run
date: 2019-12-17 23:52:05
updated: 2019-12-17 23:52:05
tags:
---

```bash
filename=""
base64_script=$(base64 /usr/local/src/${filename})

cmd="echo '---run---'; mkdir -p /usr/local/src; echo '${base64_script}' | base64 -di > /usr/local/src/${filename}; bash /usr/local/src/${filename}; echo '---end---'"

bash -c "${cmd}"
```
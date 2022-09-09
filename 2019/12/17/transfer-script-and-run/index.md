# transfer-script-and-run


```bash
filename=""
base64_script=$(base64 /usr/local/src/${filename})

cmd="echo '---run---'; mkdir -p /usr/local/src; echo '${base64_script}' | base64 -di > /usr/local/src/${filename}; bash /usr/local/src/${filename}; echo '---end---'"

bash -c "${cmd}"
```

# 

vimajax

```bash
#!/bin/bash

onlyRead=''

while getopts ':R' optchar; do
    case "${optchar}" in
        R)
            onlyRead='-R'
            ;;
        *)
            break
            ;;
    esac
done

shift $((OPTIND-1))

act=$1

result=$(grep -n "act=='$act'" /path/to/dir)

fileName=$(echo "$result" | awk -F ':' '{print $1}')
line=$(echo "$result" | awk -F ':' '{print $2}')

vim $onlyRead +$line $fileName
```


```bash
echo -e "$counts" | sort -n -k 1 -r | column -t -s ' ' | cat -n
```


```bash

```










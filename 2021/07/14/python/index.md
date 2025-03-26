# Python


## 子进程

通过 Shell 执行：

```python
# -*- coding: utf-8 -*-
from subprocess import Popen, PIPE
p = Popen(["echo '1+1' | bc"], shell=True, stdout=PIPE, stderr=PIPE)
stdout, stderr = p.communicate()
print(stdout, stderr)
```

不通过 Shell 执行：

```python
# -*- coding: utf-8 -*-
from subprocess import Popen, PIPE
p1 = Popen(["echo", "1+1"], shell=False, stdout=PIPE, stderr=PIPE)
# p1.stdout 作为 p2.stdin
p2 = Popen(["bc"], shell=False, stdin=p1.stdout ,stdout=PIPE, stderr=PIPE)
# 在 p2 先于 p1 退出时，p1 能够接收到 SIGPIPE 信号
p1.stdout.close()
stdout, stderr = p2.communicate()
print(stdout, stderr)
```

## 时间转换

```python
# -*- coding: utf-8 -*-
from datetime import datetime, timezone, timedelta

# 如果在生成 date 的时候，没有指定 tz，则应该在后续通过 replace 设置时区
# date: 'datetime = datetime.fromisoformat("2021-05-05 16:00:00").replace(tzinfo=timezone.utc)'
date: 'datetime = datetime.now(tz=timezone.utc)'

# astimezone 默认把时区转换为本地时区
# 对于 Asia/Shanghai 时区，等同于 date.astimezone(timezone(timedelta(hours=8)))
tz_aware_date = date.astimezone()
# 通过设置 timespec="seconds"，把毫秒去掉
iso8601format = tz_aware_date.isoformat(timespec="seconds")
print(iso8601format)
```

## 时间计算

```python
datetime.now() + timedelta(days=1)
```

## 时间比较

```python
if datetime.now() < datetime.now():
    return
```

## 打印一天内的每一分钟

```python
[print("%02d:%02d:00" % (hour, minute)) for hour in range(0,24) for minute in range(0,60)]
```

## Excel xls

```python
# -*- coding: utf-8 -*-
from xlwt.Workbook import Workbook
from xlwt.Worksheet import Worksheet

wb = Workbook()
sheet = wb.add_sheet("test")
i = 1
for r in range(1, 100):
    for c in range(1, 100):
        sheet.write(r, c, i)
        i += 1

wb.save("test.xls")
```

## Excel xlsx

```python
# -*- coding: utf-8 -*-
from openpyxl import Workbook,utils
from openpyxl.worksheet.worksheet import Worksheet

wb = Workbook()
wb.remove(wb.active)
sheet = wb.create_sheet("test")

i = 1
for r in range(1, 100):
    for c in range(1, 100):
        sheet.cell(r, c, i)
        i += 1

wb.save("test.xlsx")
```

自适应：

```python
def columns_best_fit(ws: Worksheet):
    column_letters = tuple(utils.get_column_letter(col_number + 1) for col_number in range(ws.max_column))
    for column_letter in column_letters:
        ws.column_dimensions[column_letter].auto_size = True
        if column_letter == "A" or column_letter == "B":
            ws.column_dimensions[column_letter].width = 20
```

## 获取公网 IP

```python
# https://stackoverflow.com/a/28950776
# https://stackoverflow.com/a/166589
def get_local_ip():
    s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    try:
        # doesn't even have to be reachable
        s.connect(('8.8.8.8', 80))
        ip = s.getsockname()[0]
    except Exception, e:
        ip = '127.0.0.1'
    finally:
        s.close()
    return ip
```

```python
import re
import subprocess

# https://stackoverflow.com/a/28532296
def is_ip_private(ip):
    # https://en.wikipedia.org/wiki/Private_network

    priv_lo = re.compile("^127\.\d{1,3}\.\d{1,3}\.\d{1,3}$")
    priv_24 = re.compile("^10\.\d{1,3}\.\d{1,3}\.\d{1,3}$")
    priv_20 = re.compile("^192\.168\.\d{1,3}.\d{1,3}$")
    priv_16 = re.compile("^172.(1[6-9]|2[0-9]|3[0-1]).[0-9]{1,3}.[0-9]{1,3}$")

    res = priv_lo.match(ip) or priv_24.match(ip) or priv_20.match(ip) or priv_16.match(ip)
    return res is not None

def get_local_ip_by_hostname():
    process=subprocess.Popen(['hostname', '-I'], stdout=subprocess.PIPE)
    ips, error = process.communicate()
    if error != None:
        return "127.0.0.1"
    
    for ip in ips.split(" ")[:-1]:
        if not is_ip_private(ip):
            return ip
        
    return "127.0.0.1"
```


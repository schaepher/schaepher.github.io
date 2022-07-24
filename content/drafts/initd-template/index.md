---
title: init 脚本模板
date: 2019-12-22 12:21:15
updated: 2019-12-22 12:21:15
tags:
---


其中，PROG变量为所要运行的可执行程序的名称， PROG_PATH为可执行文件所在的目录，PROG_ARGS为执行程序的各个参数。
```bash
#!/bin/bash
### BEGIN INIT INFO
#
# Provides:	 location_server
# Required-Start:	$local_fs  $remote_fs
# Required-Stop:	$local_fs  $remote_fs
# Default-Start: 	2 3 4 5
# Default-Stop: 	0 1 6
# Short-Description:	initscript
# Description: 	This file should be used to construct scripts to be placed in /etc/init.d.
#
### END INIT INFO
 
## Fill in name of program here.
PROG="location_server"
PROG_PATH="/opt/location_server" ## Not need, but sometimes helpful (if $PROG resides in /opt for example).
PROG_ARGS="" 
PID_PATH="/var/run/"
 
start() {
    if [ -e "$PID_PATH/$PROG.pid" ]; then
        ## Program is running, exit with error.
        echo "Error! $PROG is currently running!" 1>&2
        exit 1
    else
        ## Change from /dev/null to something like /var/log/$PROG if you want to save output.
        $PROG_PATH/$PROG $PROG_ARGS 2>&1 >/var/log/$PROG &
	$pid=`ps ax | grep -i 'location_server' | sed 's/^\([0-9]\{1,\}\).*/\1/g' | head -n 1`
 
        echo "$PROG started"
        echo $pid > "$PID_PATH/$PROG.pid"
    fi
}
 
stop() {
    echo "begin stop"
    if [ -e "$PID_PATH/$PROG.pid" ]; then
        ## Program is running, so stop it
	pid=`ps ax | grep -i 'location_server' | sed 's/^\([0-9]\{1,\}\).*/\1/g' | head -n 1`
	kill $pid
        
        rm -f  "$PID_PATH/$PROG.pid"
        echo "$PROG stopped"
    else
        ## Program is not running, exit with error.
        echo "Error! $PROG not started!" 1>&2
        exit 1
    fi
}
 
## Check to see if we are running as root first.
## Found at http://www.cyberciti.biz/tips/shell-root-user-check-script.html
if [ "$(id -u)" != "0" ]; then
    echo "This script must be run as root" 1>&2
    exit 1
fi
 
case "$1" in
    start)
        start
        exit 0
    ;;
    stop)
        stop
        exit 0
    ;;
    reload|restart|force-reload)
        stop
        start
        exit 0
    ;;
    **)
        echo "Usage: $0 {start|stop|reload}" 1>&2
        exit 1
    ;;
esac
```
# phicomm-n1


TTL 救砖和刷机看这篇：  
https://linan.blog/2019/N1-Burn-img/

注意！！
擦除 flash 和 擦除 bootloader 是要 **取消勾选**！！！眼瞎看成 **勾选** 导致多花了些时间。  
见：https://www.right.com.cn/forum/thread-308485-2-1.html

官改固件作者发的贴子：  
https://www.znds.com/tv-1118656-1-1.html


OPENWRT：  
https://www.znds.com/tv-1151977-1-1.html

https://github.com/coolsnowwolf/lede

https://www.znds.com/tv-1034311-1-1.html

http://www.epinv.com/post/12289.html


https://www.mivm.cn/phicomm-n1-unofficial/

工具包：

https://share.weiyun.com/5t9zqaO

刷 armbian ：

下载包：

https://yadi.sk/d/pHxaRAs-tZiei

配置时间：

https://yuerblog.cc/2019/10/23/%e6%96%90%e8%ae%afn1-%e5%ae%8c%e7%be%8e%e5%88%b7%e6%9c%baarmbian%e6%95%99%e7%a8%8b/

看起来舒服：

https://mivm.cn/phicomm-n1-linux

参数和统计：

https://github.com/kasicass/blog/blob/master/debian/2018_11_19_armbian_on_n1_box.md

软件安装：

https://post.smzdm.com/p/a25gpgx7/

freerdp：

https://blog.csdn.net/Pipcie/article/details/84955347

xfreerdp --sound alsa -f --audio-mode 0 --disable-wallpaper --disable-themes --enable-fonts --disable-menu-anims --network lan --enable-clipboard --sec nla -w 1920 -h 1080 -u 用户邮箱 -v ip地址

xfreerdp -wallpaper -themes +clipboard +fonts -menu-anims /compression-level:0 /sound:alsa /sec:nla /w:1920 /h:1080 /network:lan /u:用户邮箱 /v:192.168.1.102:3389

## 安装 CUPS

```
    1  apt upgrade
    2  armbian-config 
    3  apt install cups
    4  apt install hplip
    5  vim /etc/cups/cupsd.conf 
    6  systemctl restart cups
    7  vim /etc/cups/cupsd.conf 
    8  systemctl restart cups
    9  rebooot
   10  reboot
   11  hp-scan
   12  systemctl restart cups
   13  avahi-daemon 
   14  vim /etc/init.d/cups 
   15  systemctl enable cups
   16  systemctl enable avahi-daemon
   17  reboot
   18  lsusb 
   19  reboot
   20  lsusb 
   21  ls /dev/usbmon
   22  lsusb 
   23  hp-config_usb_printer 
   24  lsusb
   25  hp-config_usb_printer 001:002
   26  lsusb
   27  hp-config_usb_printer 001:002
   28  lsusb
   29  hp-config_usb_printer 001:002
   30  lsusb
   31  lsusb 
   32  lsusb
   33  systemctl restart cups
   34  lpinfo -l --v
   35  lpinfo -l -v
   36  lsusb 
   37  cd /dev
   38  ls
   39  ls usbmon1
   40  systemctl restart cups
   41  dmesg 
   42  dmesg  | less
   43  tail /var/log/dmesg
   44  less /var/log/dmesg
   45  less /var/log/dmesg.0 
   46  dmesg
   47  lsmod 
   48  lsmod  | grep ehci
   49  hp-plugin-ubuntu 
   50  lsusb
   51  shutdown -h now
   52  lsusb
   53  dmesg
   54  tail -f /var/log/cups/access_log 
   55  tail -f /var/log/cups/error_log 
   56  less /var/log/cups/error_log 
   57  vim /usr/share/dbus-1/services/org.freedesktop.systemd1.service 
   58  less /var/log/cups/error_log 
   59  tail -f /var/log/cups/error_log 
   60  dmesg
   61  apt purge ippusbxd
   62  cd /etc/cups/
   63  ls
   64  vim cupsd.conf 
   65  vim cupsd.conf.0
   66  cp cupsd.conf /root/
   67  apt remove cups
   68  apt install cups
   69  apt install cups-bsd cups-pdf foomatic-db-compressed-ppds
   70  lsusb
   71  reboot
   72  lsusb
   73  dmesg
   74  armbian-install 
   75  lsusb
   76  ls
   77  cp cupsd.conf /etc/cups/cupsd.conf
   78  systemctl restart cups
   79  apt install hplip
   80  hp-plugin
   81  systemctl 
   82  systemctl status avahi~
   83  systemctl status avahi-daemon.socket 
   84  systemctl restart avahi-daemon.socket 
   85  lsusb 
   86  poweroff 
   87  lsusb 
   88  hp-plugin
   89  hp-info
   90  hp-testpage 
   91  dmesg
   92  dmesg | grep print
   93  dmesg | grep usb
   94  hp-testpage 
   95  dmesg
   96  tail /var/log/dmesg
   97  tail /var/log/cups/access_log 
   98  tail /var/log/cups/error_log 
   99  tail -f /var/log/cups/error_log 
  100  dmesg
  101  hp-check
  102  apt install libcups2
  103  apt install libcups2 libdbus-1-dev libjpeg-dev libcups2-dev cups-bsd cups-client libcupsimage2-dev libusb-1.0.0-dev libusb-0.1-4 libsane-dev libavahi-client-dev libavahi-core-dev libavahi-common-dev libsnmp-dev snmp-mibs-downloader openssl python3-dev libtool libtool-bin 
  104  apt update
  105  apt install libcups2 libdbus-1-dev libjpeg-dev libcups2-dev cups-bsd cups-client libcupsimage2-dev libusb-1.0.0-dev libusb-0.1-4 libsane-dev libavahi-client-dev libavahi-core-dev libavahi-common-dev libsnmp-dev snmp-mibs-downloader openssl python3-dev libtool libtool-bin 
  106  apt install libcups2 libdbus-1-dev libjpeg-dev libcups2-dev cups-bsd cups-client libcupsimage2-dev  libusb-0.1-4 libsane-dev libavahi-client-dev libavahi-core-dev libavahi-common-dev libsnmp-dev snmp-mibs-downloader openssl python3-dev libtool libtool-bin 
  107  hp-check
  108  apt install libcups2
  109  apt install libusb-0.1-4
  110  apt install libusb-1.0.0-dev
  111  apt upgrade
  112  hp-testpage 
  113  reboot
  114  hp-testpage 
  115  lsusb 
  116  systemctl restart avahi-daemon.socket 
  117  crontab -e
  118  fg
  119  cd /usr/lib/cups/
  120  ls
  121  cd filter/
  122  ls
  123  du -sh .
  124  sz hpcups
  125  apt install lrzsz
  126  ls
  127  sz hpcups
  128  history | less
  129  cd /etc/
  130  ls
  131  cd avahi/services/
  132  ls
  133  cd ..
  134  ls
  135  vim avahi-daemon.conf 
  136  ls
  137  cat avahi-autoipd.action 
  138  ls
  139  cat hosts 
  140  ls
  141  cd services/
  142  ls
  143  cd ..
  144  ls
  145  sz avahi-autoipd.action 
  146  sz avahi-daemon.conf 
  147  history
```

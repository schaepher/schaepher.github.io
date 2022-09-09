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

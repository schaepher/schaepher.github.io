# Ubuntu一些常用的软件安装及配置


# 软件

1. 安装 Vim

    - `echo "y" | sudo apt-get install vim`

1. 安装搜狗输入法
    这个我在虚拟机里面尝试了好多遍，不断恢复备份然后重试。终于有了这个纯靠命令安装的做法。

    - `wget -O $HOME/Downloads/sogou.deb http://cdn2.ime.sogou.com/dl/index/1475147394/sogoupinyin_2.1.0.0082_amd64.deb?st=bt76tTmCNyR7z8AF3TSnuQ&e=1491123967&fn=sogoupinyin_2.1.0.0082_amd64.deb`
    - `echo "y" | sudo apt install $HOME/Downloads/sogou.deb`
    - `gnome-session-quit --no-prompt`
        此时会退出当前用户，需要重新输入密码进入桌面
    - `sed -i 's/sogoupinyin:False/sogoupinyin:True/g' $HOME/.config/fcitx/profile`
    - `fcitx-remote -r`
    - `fcitx-remote -s sogoupinyin`

1. 安装网易云音乐

    - `wget -O $HOME/Downloads/netease-cloud-music.deb http://s1.music.126.net/download/pc/netease-cloud-music_1.0.0_amd64_ubuntu16.04.deb`
    - `sudo apt install $HOME/Downloads/netease-cloud-music.deb`
    - `netease-cloud-music &`
        这一句是启动网易云音乐

1. 连上 google 

    - 下载 hosts 文件到 $HOME/Downloads 下面 -> hosts 文件自己找（逃
    - `sudo cp $HOME/Downloads/hosts /etc/`
    - `sudo systemctl restart NetWorkManager`

1. 下载 chrome

    - `wget -O $HOME/Downloads/google-chrome.deb https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb`
    - `echo "y" | sudo apt install $HOME/Downloads/google-chrome.deb`
    - `google-chrome-stable &`
    - 此时弹出对话框，询问是否设置 chrome 为默认浏览器(default brower)
    - 接下去就是登陆(sign in)

1. 安装 git 

    - `echo "y" | sudo apt install git` 

1. tmux 多窗口

# 配置

## 显示配置

1. launcher 放到底部
    - `gsettings set com.canonical.Unity.Launcher launcher-position Bottom`
        如果参数为 Left 则还原为默认

1. 修改 launcher 的大小
    - bash 中执行： `unity-control-center` 打开系统设置
    - 选择 Appearance ，这个页面包含 Look 和 Behavior 两个子页面
    - Look 页面最底下的 `Launcher icon size` 改为 34 

1. SystemSettings/Appearance/Behavior  
    - 勾选 `Add show desktop icon to the launcher` ：在 launcher 上显示一个图标，和 windows 的 “显示桌面” 按钮一样。
    - 勾选 `Always displayed` ：总是显示当前窗口的菜单
    - 勾选 `In the windows's title bar` ： 将菜单显示在当前窗口的顶部。另一项则是显示在系统桌面顶部那一栏。

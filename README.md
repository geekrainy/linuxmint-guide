# Linux Mint 配置向导及应用


目录
=================

* [Linux Mint 配置向导及应用](#linux-mint-配置向导及应用)
     * [基本配置](#基本配置)
         * [联网](#联网)
         * [终端](#终端)
         * [内核回退](#内核回退)
         * [字体](#字体)
         * [美化](#美化)
         * [输入法](#输入法)
            * [输入法词库](#输入法词库)
         * [Java 开发环境配置](#Java-开发环境配置)
     * [应用软件](#应用软件)
         * [浏览器](#浏览器)
         * [Chrome Apps](#Chrome-Apps)
         * [编辑器](#编辑器)
         * [Markdown 写作](#markdown-写作)
         * [效率](#效率)
         * [开发环境](#开发环境)
         * [同步工具](#同步工具)
         * [代理工具](#代理工具)
         * [文档阅读](#文档阅读)
         * [办公教育](#办公教育)
         * [下载工具](#下载工具)
         * [系统管理](#系统管理)
     * [Windows 兼容](#Windows-兼容)
         * [CrossOver](#CrossOver)
         * [Microsoft Office](#Microsoft-Office)
         * [虚拟机方案及优化](#虚拟机方案及优化)

## 基本配置

### 联网

1. 锐捷官方客户端

   ```bash
   sudo chmod +x ./rjsupplicant.sh
   sudo ./rjsupplicant.sh --help # 配置使用
   ```

2. Mentohust

   安装 [mentohust_0.3.4-1_amd64.deb](https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/mentohust/mentohust_0.3.4-1_amd64.deb) 包。

   Mentohust 使用 `notify-osd` `libnotify-dev` 提供气泡提示（Unity 桌面默认通知方式，Cinnamon 桌面需要手动安装包）。关于通知的文档：https://wiki.archlinux.org/index.php/Desktop_notifications

   ```bash
   # 修复提示 “！！打开libnotify失败，请检查是否已安装该库文件。”
   sudo ln -s /usr/lib/x86_64-linux-gnu/libnotify.so.4.0.0 /usr/lib/libnotify.so.1
   ```

   配置文件位置 `/etc/mentohust.conf`:

   组播地址：标准

   DHCP 方式：二次认证

### 终端

安装 zsh:

```bash
sudo apt-get install zsh
```

切换默认 zsh:

```bash
chsh -s /bin/zsh
```

安装 `oh-my-zsh`:

```bash
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

配置文件 `~/.zshrc`:

```bash
# 定义 zsh 主题
ZSH_THEME="ys"

# 设置别名
alias sudo="sudo "                # 授予 sudo 别名权限
alias rj="mentohust"              # 联网
alias qrj="mentohust -k"          # 退出联网
# alias xl="docker start xware"   启动讯雷下载容器
# alias qxl="docker stop xware"   停止讯雷远程下载容器
```

### 内核回退



### 字体

下载符号字体解决 wps 符号字体缺失：

[symbol-fonts_1.2_all.deb](https://pan.baidu.com/share/link?uk=505215462&shareid=3369982571)

下载全套 Windows 字体：

[winfonts_1.3_all.deb](https://pan.baidu.com/share/link?uk=505215462&shareid=1223565760)

同时使用 Infinality 优化字体渲染：

> 参考文章：http://www.webupd8.org/2013/06/better-font-rendering-in-linux-with.html

```bash
sudo add-apt-repository ppa:no1wantdthisname/ppa
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install fontconfig-infinality
```

设置风格为 `Infinality`：

```bash
sudo bash /etc/fonts/infinality/infctl.sh setstyle
```

设置渲染风格：

```bash
# 修改 USE_STYLE 为 UBUNTU
sudo vim /etc/profile.d/infinality-settings.sh
```

启用 `Hinting full`。

### 美化

1. 壁纸

   安装所有 Linux Mint 历史版本自带壁纸：

   ```bash
   sudo apt-get install mint-backgrounds-*
   ```

2. 图标

   1. 经典 Numix-Circle 图标适配全，更新快：

      ```bash
      sudo add-apt-repository ppa:numix/ppa
      sudo apt-get update
      sudo apt-get install numix-icon-theme-circle
      ```

   2. 扁平化 Paper 图标，适合扁平化主题：

      ```shell
      sudo add-apt-repository ppa:snwh/pulp
      # update repository info
      sudo apt-get update
      # install icon theme
      sudo apt-get install paper-icon-theme
      # install gtk theme
      sudo apt-get install paper-gtk-theme
      # install cursor theme
      sudo apt-get install paper-cursor-theme
      ```

3. 主题

   1. 添加 Numix PPA 后，安装 gtk 主题：

      ```bash
      sudo apt-get install numix-gtk-theme
      ```

      对于 Cinnamon 桌面而言，改变 Panel 主题可下载 `Numix-Cinnamon-2` 主题设置使用。

   2. 添加 Adapta PPA 后，安装主题：

      ```shell
      sudo apt-get install adapta-gtk-theme
      ```

4. 登录窗口

   同样选择 Numix 主题来统一风格，自定义背景修改 `/usr/share/mdm/html-themes` 路径下主题文件。

### 输入法

Fcitx 搭配 Cinnamon 会产生一个僵尸进程，搜狗输入法容易导致概率性 CPU 占用 100%。所以使用[小小输入法](http://yongim.ys168.com/)。

解压到主目录 `~/.yong`:

```bash
sudo chmod +x ./yong-tool.sh
sudo ./yong-tool.sh --install
```

#### 输入法词库

小小输入法内置词库少，可使用工具将其他词库转换后导入：https://github.com/studyzy/imewlconverter

导入说明：https://github.com/studyzy/imewlconverter/wiki/Xiaoxiao

### Java 开发环境配置

默认 JDK 安装：

```shell
sudo apt-get update
sudo apt-get install default-jre
```

Oracle JDK 安装：

```shell
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java6-installer # JDK 6
sudo apt-get install oracle-java7-installer # JDK 7
sudo apt-get install oracle-java8-installer # JDK 8
```

版本之间切换：

```shell
update-alternatives --config java
update-alternatives --config javac
```

## 应用软件

### 浏览器

1. Chrome

   ```bash
   wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
   ```


2. Firefox Dev

   ```bash
   # 使用 Umake 安装
   umake web firefox-dev 
   ```

### Chrome Apps

1. Google Keep
2. 豆瓣电台
3. Enjoy Music Player
4. Polarr
5. All-in-One
6. Postman

### 编辑器

Visual Studio Code - https://code.visualstudio.com/

### Markdown 写作

```bash
# optional, but recommended
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE
# add Typora's repository
sudo add-apt-repository 'deb https://typora.io ./linux/'
sudo apt-get update
# install typora
sudo apt-get install typora
```

### 效率

1. 白噪音 `ANoise`:

   ```bash
   sudo add-apt-repository ppa:costales/anoise
   sudo apt-get update
   sudo apt-get install anoise
   ```

2. 剪贴板管理 `Diodon`:

   ```bash
   sudo add-apt-repository ppa:diodon-team/stable
   sudo apt-get update
   sudo apt-get install diodon
   ```

3. 截图 `Shutter`:

   ```bash
   sudo apt-get install shutter
   ```

   设置快捷键命令 `shutter -s`，实现矩形选区截图。

4. 护眼 `Redshift`:

   ```bash
   sudo apt-get install redshift
   ```

   初次启动可能提示缺少 `Geoclue` 组件，安装后可以使用自动网络定位。

   手动配置文件 `~/.config/redshift.conf`:

   ```bash
   temp-day=6500        # 适应可设为 5500
   temp-night=5500      # 适应可设为 4100

   gamma=0.8            # 纠正笔记本大白屏幕的好方式
   ```

5. 录屏 GIF 工具: [peek](https://github.com/phw/peek)

   ```shell
   sudo add-apt-repository ppa:peek-developers/stable
   sudo apt update
   sudo apt install peek
   ```



### 开发环境

1. [NVM](https://github.com/creationix/nvm)

2. [Docker](https://docs.docker.com/engine/installation/linux/ubuntulinux/)

3. Umake

   Umake 是 Ubuntu 官方的一款用来安装开发环境及开发工具的工具，同样在 Linux Mint 下可用。预装已有 Umake 工具，但支持较少，通过 ppa 来升级。

   ```bash
    $ sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
    $ sudo apt-get update
    $ sudo apt-get upgrade
   ```

4. [DBeaver](http://dbeaver.jkiss.org/): 跨平台数据库管理工具。

5. [DiffMerge](https://sourcegear.com/diffmerge/): 跨平台 GUI 代码比较工具。

6. [Wireshark](https://www.wireshark.org/): 跨平台抓包工具

   ```shell
   sudo add-apt-repository ppa:wireshark-dev/stable
   sudo apt-get update
   sudo apt-get install wireshark
   ```

   将本地用户加入 `wireshark` 用户组：

   ```shell
   sudo usermod -a -G wireshark rainy
   ```

7. [Code::Blocks](http://www.codeblocks.org/)

   Daily Builds:

   ```shell
   sudo add-apt-repository ppa:damien-moore/codeblocks
   sudo apt-get update
   sudo apt-get install codeblocks
   ```

   Release Builds:

   ```shell
   sudo add-apt-repository ppa:damien-moore/codeblocks-stable
   sudo apt-get update
   sudo apt-get install codeblocks codeblocks-contrib
   ```

### 同步工具

1. [坚果云](https://www.jianguoyun.com/)

2. [Dropbox](https://www.dropbox.com/)

   安装过程中需要联网下载，故需使用 `Proxychains` 来启动安装。

   Dropbox 默认目录在 `~/Dropbox` 进行同步，备份目录只需要创建一个软链接到此目录即可。

### 代理工具

1. Shadowsocks

   推荐使用 [Shadowsocks-qt5](https://github.com/shadowsocks/shadowsocks-qt5) 来设置。

   ```bash
   sudo add-apt-repository ppa:hzwhuang/ss-qt5
   sudo apt-get update
   sudo apt-get install shadowsocks-qt5
   ```

   在 Shadowsocks 启动后，会运行一个 `8123` 端口的 http 本地代理，不支持 socks 代理的可以使用此 http 代理方式。

2. Proxychains

   代理终端命令中的网络请求。在源中安装：

   ```bash
   sudo apt-get install proxychains
   ```

   然后配置文件 `/etc/proxychains.conf`。

3. [Lantern](https://getlantern.org/)

4. polipo

   polipo 是一个轻量级的缓存web代理程序，将 socks 代理转换为 http 代理。

   ```bash
   sudo apt-get install polipo
   ```

   配置文件 `/etc/polipo/config`：

   ```bash
   # This file only needs to list configuration variables that deviate
   # from the default values.  See /usr/share/doc/polipo/examples/config.sample
   # and "polipo -v" for variables you can tweak and further information.

   logSyslog = true
   logFile = /var/log/polipo/polipo.log

   proxyAddress = "0.0.0.0"

   socksParentProxy = "127.0.0.1:1080"
   socksProxyType = socks5

   chunkHighMark = 50331648
   objectHighMark = 16384

   serverMaxSlots = 64
   serverSlots = 16
   serverSlots1 = 32
   ```

   默认运行在 8123 端口，启动服务并为当前会话配置代理：

   ```bash
   sudo service polipo start
   export http_proxy="http://127.0.0.1:8123/"
   ```

### 文档阅读

1. [Zeal](https://zealdocs.org/)

   ```bash
   $ sudo add-apt-repository ppa:zeal-developers/ppa
   $ sudo apt-get update
   $ sudo apt-get install zeal
   ```

2. Calibre

   ```bash
   sudo -v && wget -nv -O- https://raw.githubusercontent.com/kovidgoyal/calibre/master/setup/linux-installer.py | sudo python -c "import sys; main=lambda:sys.stderr.write('Download failed\n'); exec(sys.stdin.read()); main()"
   ```

### 办公教育
1. [QtiPlot](http://www.qtiplot.com/)

   可以替代 OriginLab.

   ```shell
   sudo apt-get install qtiplot
   ```

2. [WPS Office](http://linux.wps.cn/)

   许久未见更新，半死不活的样子。Linux 版本无法编辑公式，无法正确显示公式。只适合阅读不适合编辑。

### 下载工具

1. [Xware](https://github.com/yinheli/docker-thunder-xware)

   会用 Docker 的一看就懂。

2. [You-Get](https://github.com/soimort/you-get)

   视频下载神器，同样地，下载 Youtube 视频用 Proxychains 代理。

### 系统管理

1. Gparted

   图形化磁盘分区管理工具。

   ```shell
   sudo apt-get install gparted
   ```

## Windows 兼容

Linux 平台下的应用虽然数量多，但质量也参差不齐。许多应用需要进行虚拟机或 wine 等方式来曲线救国。

1. [CrossOver](https://www.codeweavers.com)

   作为 wine 项目的商业支持版本，可以很方便安装一系列 Windows 平台软件。对于 Deepin Linux 用户已经预装在系统中，包含批量授权。其他发行版用户需要购买。

2. Microsoft Office

   鉴于 WPS for Linux 功能有限且字体各方面显示不尽人意，借助 CrossOver 可以完美安装 Microsoft Office 系列。但为了消除字体等造成的差异，还是选择在虚拟机下使用 Office。

3. 虚拟机方案及优化

   （待编辑）
# 1_通用

## 1-1_更新软件源

- 更新软件源

    ```bash
    sudo apt-get update
    ```

- 拉取最新的软件包

    ```bash
    sudo apt-get upgrade
    ```

## 1-2_基础开发工具

### 1-2-1_常见嵌入式开发工具套装

- 安装网络工具

    ```bash
    sudo apt install net-tools
    ```

- 安装 ssh 用于远程操作

    ```bash
    sudo apt install ssh
    ```

- 安装 git

    ```bash
    sudo apt install git
    ```

- 安装 vim

    ```bash
    sudo apt install vim
    ```

- 安装 make

    ```bash
    sudo apt install make
    ```

- 安装 gcc

    ```bash
    sudo apt install gcc
    ```

### 1-2-2_安装 windterm

#### 1-2-2-1_详情

- windterm：一款 ubuntu 下的 ssh，debug 等串口工具。

- 下载
    - 官方下载地址：[官方版本下载](https://github.com/kingToolbox/WindTerm/releases/tag/2.5.0)

    - 个人维护版本：[个人维护版本下载](https://zyb-software-center.oss-cn-chengdu.aliyuncs.com/linux/ubuntu/WindTerm_2.5.0_Linux_Portable_x86_64.tar.gz?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701421000&Signature=VH1eKcnRxHDOqPft7d5LOl2eHP4%3D)


- 普通安装引发问题
    - 解决问题：使用 WindTerm 打开 tty 设备等串口时，不加 sudo 命令就会碰到权限问题
    - 方便使用：在 Ubuntu 左侧启动栏点击鼠标就启动 WindTerm

#### 1-2-2-2_安装指南

##### 1-2-2-2-1_下载并解压软件

- 1st 下载软件安装包至 ~/Download

- 2nd 解压软件安装包至 ～/software

    ```bash
    tar -zxvf ~/software WindTerm_2.5.0_Linux_Portable_x86_64.tar.gz
    ```

##### 1-2-2-2-2_解决权限问题

执行如下命令将用户放入组（diaout、tty 即可），注意用户名 username 根据个人实际情况做改动

```bash
sudo newgrp dialout tty
```

```bash
sudo usermod -a -G dialout username
```

```bash
sudo usermod -a -G tty username
```

##### 1-2-2-2-3_将软件放入侧边栏

- 新建文件目录：/usr/share/applications

- 新建文件名：windterm.desktop

- 新建文件内容如下: （注意修改配置文件路径，文件中的目录一定要根据个人开发实际情况变更）

    ```shell
    [Desktop Entry]
    Name=WindTerm
    Comment=A professional cross-platform SSH/Sftp/Shell/Telnet/Serial terminal
    GenericName=Connect Client
    Exec=/home/username/software/WindTerm_2.5.0/WindTerm
    Type=Application
    Icon=/home/zyb/software/WindTerm_2.5.0/windterm.png
    StartupNotify=false
    StartupWMClass=Code
    Categories=Application;Development
    Actions=new-empty-window
    Keywords=windterm
    
    [Desktop Action new-empty-window]
    Name=New Empty Window
    Icon=/home/username/software/WindTerm_2.5.0/windterm.png
    Exec=/home/username/software/WindTerm_2.5.0/WindTerm
    ```

- 增加文件的可执行权限

    ```bash
    sudo chmod +x /usr/share/applications/windterm.desktop
    ```

- 启动软件（没有`./`）

    ```bash
    /home/username/software/WindTerm_2.5.0/WindTerm
    ```

- 最终效果如下图：

    ![安装windterm成功启动效果](https://zyb-pic-center.oss-cn-chengdu.aliyuncs.com/note-pic/ubuntu%E5%AE%89%E8%A3%85%E5%B8%B8%E7%94%A8%E8%BD%AF%E4%BB%B6/1.2-1.2.2-1.2.2.2-1.2.2.2.3-1%E5%AE%89%E8%A3%85windterm%E6%88%90%E5%8A%9F%E5%90%AF%E5%8A%A8%E6%95%88%E6%9E%9C.png?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001704176000&Signature=3K0fAaVkfMlSQzbZKjToiG7YyHo%3D)

### 1-2-3_安装程序猿计算器

```bash
sudo snap install uno-calculator
```

## 1-3_安装常用办公软件

### 1-3-1_安装搜狗输入法

[安装指南](https://shurufa.sogou.com/linux/guide)

### 1-3-2_安装谷歌浏览器

#### 1-3-2-1_下载源

- 官网版本：[chroom浏览器官网版本下载](https://www.google.com/chrome/)
- 个人维护版本：[chroom浏览器个人维护版本下载](https://zyb-tools.oss-cn-chengdu.aliyuncs.com/ubuntu-software/google-chrome-stable_current_amd64.deb?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001692695000&Signature=jLyc7P4luOxkVjcmiwil1wcd%2F1M%3D)

#### 1-3-2-2_下载并安装

- 1st 下载至指定目录

- 2nd 使用 dpkg 安装

    ```bash
    sudo dpkg -i deb包名
    ```

### 1-3-3_安装qq音乐

#### 1-3-2-1_下载源

- 官网版本：[qq音乐官方版本下载](https://y.qq.com/download/download.html)
- 个人维护版本：[qq音乐个人维护版本下载](https://zyb-tools.oss-cn-chengdu.aliyuncs.com/ubuntu-software/qqmusic_1.1.5_amd64.deb?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001692695000&Signature=dDW%2F24vpW%2FbMB5FLYXQJzd6hEL4%3D)

#### 1-3-2-2_下载并安装

- 1st 下载至指定目录

- 2nd 使用 dpkg 安装

    ```bash
    sudo dpkg -i deb包名
    ```

#### 1-3-3-3_设置启动指令

- 1st 编辑 ~/.bashrc 文件，添加如下内容

    ```bash
    ###############################
    ####      qq音乐 启动      ####
    ###############################
    alias qqmusic-start='qqmusic --no-sandbox'
    ```

- 2nd 执行 source 使能

    ```bash
    source ~/.bashrc
    ```

#### 1-3-3-4_启动qq音乐

```bash
qqmusic-start
```

- 此处执行指令需要根据个人在 ~/.bashrc 中设置的 alias 而定。

# 2_ubuntu22专属

ubuntu22使用`sudo apt-get install gcc`安装的 gcc 版本默认为 8.5，但是在日常开发过程中，大多数公司依旧选择 ubuntu18 作为稳定的开发环境，同时老系统的代码环境以及编译环境外加各种乱七八糟的东西都来自于 ubuntu18。本章节

## 2-1_gcc_7-5

- 1st：修改软件源列表

  ```bash
  sudo vim /etc/apt/sources.list
  ```

  在文件最后新增源：`deb [arch=amd64] http://archive.ubuntu.com/ubuntu focal main universe`

- 2nd：更新软件源`sudo apt-get update`

- 3rd：安装 7.5 版本的 gcc

  ```bash
  apt-get -y install gcc-7 g++-7
  ```

- 4th：变更软连接

  ```bash
  update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 50
  ```

- 5th：使用`gcc --version`查看 gcc 版本发现已经是 gcc-7.5。

## 2-2_pahole_1-21

- 1st：安装编译源码必须的包

  ```bash
  sudo apt-get install build-essential pkg-config libdw-dev libdwarf-dev elfutils cmake
  ```

- 2nd：下载源码，默认在 ~/software/pahole 下

  ```bash
  git clone https://git.kernel.org/pub/scm/devel/pahole/pahole.git
  ```

- 3rd：进入源码根目录 ~/software/pahole/pahole1.21，同时在当前编译终端导出 lib 库

  ```bash
  export LD_LIBRARY_PATH=/usr/local/lib
  ```

- 4th：在源码根目录下切换 pahole 源码至 1.21 的 tag

  ```bash
  git checkout v1.21
  ```

- 5th：源码根目录 ~/software/pahole/pahole1.21 下创建 build 目录并进入

  ```bash
  mkdir build && cd build
  ```

- 6th：编译

  ```bash
  cmake -D__LIB=lib ..
  ```

- 7th：安装

  ```bash
  make install
  ```

- 8th：查看版本`pahole --version`

## 2-3_python3-colcon-common-extensions

这个 deb 包在 ROS 中，使用 apt 安装之前必须要先添加适当的签名才可以，安装步骤如下：

- 1st：安装必要包

  ```bash
  sudo apt-get install -y lsb-release gnupg2 curl
  ```

- 2nd：下载相关签名并将其写入本地（如果网络不好就多尝试几次）

  ```bash
  curl https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | gpg --dearmor --yes --output /etc/apt/trusted.gpg.d/ros.gpg 
  ```

- 3rd：将软件包源写入本地 list

  ```bash
  sh -c 'echo "deb [arch=amd64,arm64] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros-latest.list'
  ```

- 4h：更新软件源

  ```bash
  sudo apt-get update
  ```

- 5th：安装应用

  ```bash
  export DEBIAN_FRONTEND=noninteractive
  ```

  ```bash
  echo -e "6\n70" | apt-get install -y python3-colcon-common-extensions
  ```

## 2-4_pip2

ubuntu 22.04 默认不带 python2，因为 python2 已于 2020 年 1 月 正式停止支持。

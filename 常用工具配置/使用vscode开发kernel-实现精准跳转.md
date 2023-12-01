# 1-软件安装

## 1-1_基础软件安装

- 安装并配置 git：参考 [git 快捷配置](https://github.com/zyb-prj/note-center/blob/main/%E5%B8%B8%E7%94%A8%E5%B7%A5%E5%85%B7%E9%85%8D%E7%BD%AE/git%E5%BF%AB%E6%8D%B7%E9%85%8D%E7%BD%AE.md)。
- 安装 bear 工具（用于生成钩子）：`sudo apt install bear`
- 安装 vscode 及其插件，详情参考 vscode 插件安装。

## 1-2_安装vscode及其插件

- 客户端/服务端最好均安装
- 客户端必须安装（后续使用 ssh 连接至服务端再同步至服务端）。

### 1-2-1_安装vscode

- 官网下载：https://code.visualstudio.com/
- 个人维护
    - windows 点击此处下载
    - [mac 点击此处下载](https://zyb-software-center.oss-cn-chengdu.aliyuncs.com/mac/vscode/VSCode-darwin-arm64.zip?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701337000&Signature=DPsVDGIlMSuIP4agVHgf45es1EE%3D)
    - linux 点击此处下载

### 1-2-2_vscode插件安装

- 客户端/服务端均安装。
- 客户端必须安装（后续可使用 ssh 连接至服务端再同步至服务端）。

#### 1-2-2-1_安装插件目录

- c 技术栈类：`C/C++`    `C/C++ Extension Pack`    `C/C++ Snippets`    `Clangd`     `Code Runner`  


- linux 开发工具类：`Remote SSH`    `DeviceTree`    `Arm Assembly`    `Hex Editor`


- 软件开发工具类：`Code Spell Checker`     `compareit`    `Tabnine AI Autocomplete` 


​									`Bracket Pair Colorization Toggler` 

- 辅助开发工具类：`Chinese`     `vscode-icons`    `One Dark Pro`


​                                     `Rainbow Highlighter` ： 高亮文字：shift + alt + z     取消高亮：shift + alt + a            

- markdown类：`Markdown All in One`    `Markdown Preview Enhanced`

#### 1-2-2-2_插件确认

具体必备插件安装如下图（vscode开发kernel所需插件合集图）所示。

![vscode开发kernel所需插件合集图](https://zyb-pic-center.oss-cn-chengdu.aliyuncs.com/note-pic/%E4%BD%BF%E7%94%A8vscode%E5%BC%80%E5%8F%91kernel-%E5%AE%9E%E7%8E%B0%E5%86%85%E6%A0%B8%E4%BB%A3%E7%A0%81%E7%B2%BE%E5%87%86%E8%B7%B3%E8%BD%AC/1-1.2-1.2.2-1.2.2.2-1-vscode%E5%BC%80%E5%8F%91kernel%E6%89%80%E9%9C%80%E6%8F%92%E4%BB%B6%E5%90%88%E9%9B%86%E5%9B%BE.png?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701340000&Signature=DguVyfN7TjO3KSUfvWMRYELepdQ%3D)

## 1-3_安装clangd

vscode 安装 clang 插件后，它的使用还需要一个运行在 Linux 服务器上的 clangd 程序。我们以后使用 vscode 打开 c 文件时，会提示你安装 clangd 程序，它会安装最新版本(版本15)，但是这个版本有一些 Bug，所以我们手工安装版本 13。

### 1-3-1_下载源

- 官方下载地址：[Clang13.0官方版本下载](https://github.com/clangd/clangd/releases/tag/13.0.0)
- 个人维护版本：[Clang13.0个人维护版本下载](https://zyb-software-center.oss-cn-chengdu.aliyuncs.com/linux/ubuntu/clangd-linux-13.0.0.zip?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701340000&Signature=OXsecHyMZlRu2VKVjLg%2Fi3E6Dvs%3D)

### 1-3-2_下载并安装（一定要在服务端安装）

- 1st 需要安装 clang 插件

- 2nd 下载 clang13.0 版本至指定目录

- 3rd 把下载到的 clangd-linux-13.0.0.zip 放到指定目录下，此处为 ~/software

    ```bash
    unzip -d ~/software clangd-linux-13.0.0.zip
    ```

# 2-使用vscode远程连接

## 2-1_基本要求

- 确保 ubuntu 服务端安装了 ssh 以及 net-tools

    ```bash
    sudo apt-get install ssh net-tools
    ```

- 确保 ubuntu 服务端 ubuntu 下的 vscode 安装了 Remote SSH 插件，同时客户端的 vscode 也安装了 Remote SSH 插件。

- linux 内核开发建议使用 ubuntu 操作系统来做开发，下面我们称其为服务端。同时 windows 或 mac 操作系统更具有可操作性，下面称其为客户端，因此我们可以在 win 或 mac 下使用 vscode 远程连接服务器来做开发。

## 2-2_vscode使用ssh连接

- 1st 获取服务端 IP，假设为 xx.xx.xx.x。

- 2nd 打开服务端 vscode，点击左下角的远程连接按钮，操作流程如下图（vscode打开远程连接界面演示图）所示。

    ![vscode打开远程连接界面演示图](https://zyb-pic-center.oss-cn-chengdu.aliyuncs.com/note-pic/%E4%BD%BF%E7%94%A8vscode%E5%BC%80%E5%8F%91kernel-%E5%AE%9E%E7%8E%B0%E5%86%85%E6%A0%B8%E4%BB%A3%E7%A0%81%E7%B2%BE%E5%87%86%E8%B7%B3%E8%BD%AC/2-2.2-1-vscode%E6%89%93%E5%BC%80%E8%BF%9C%E7%A8%8B%E8%BF%9E%E6%8E%A5%E7%95%8C%E9%9D%A2%E6%BC%94%E7%A4%BA%E5%9B%BE.png?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701400000&Signature=qW3y9iKrq04Zk0Nf4YUcrUUTOOQ%3D)

- 3rd 新增连接，操作流程如下图（vscode打开远程连接按钮后新增配置界面操作展示图）所示。

    ![vscode打开远程连接按钮后新增配置界面操作展示图](https://zyb-pic-center.oss-cn-chengdu.aliyuncs.com/note-pic/%E4%BD%BF%E7%94%A8vscode%E5%BC%80%E5%8F%91kernel-%E5%AE%9E%E7%8E%B0%E5%86%85%E6%A0%B8%E4%BB%A3%E7%A0%81%E7%B2%BE%E5%87%86%E8%B7%B3%E8%BD%AC/2-2.2-2-vscode%E6%89%93%E5%BC%80%E8%BF%9C%E7%A8%8B%E8%BF%9E%E6%8E%A5%E6%8C%89%E9%92%AE%E5%90%8E%E6%96%B0%E5%A2%9E%E9%85%8D%E7%BD%AE%E7%95%8C%E9%9D%A2%E6%93%8D%E4%BD%9C%E5%B1%95%E7%A4%BA%E5%9B%BE.png?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701400000&Signature=8lMK7HavmRbbBOB3esZMO%2B28SYI%3D)

- 4th 按要求配置远程连接指令：`ssh user@xx.xxx.xxx.x -A`，输入完成后按回车确定。操作流程如下图（vscode具体ssh配置展示图）所示。

    ![vscode具体ssh配置展示图](https://zyb-pic-center.oss-cn-chengdu.aliyuncs.com/note-pic/%E4%BD%BF%E7%94%A8vscode%E5%BC%80%E5%8F%91kernel-%E5%AE%9E%E7%8E%B0%E5%86%85%E6%A0%B8%E4%BB%A3%E7%A0%81%E7%B2%BE%E5%87%86%E8%B7%B3%E8%BD%AC/2-2.2-3-vscode%E5%85%B7%E4%BD%93ssh%E9%85%8D%E7%BD%AE%E5%B1%95%E7%A4%BA%E5%9B%BE.png?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701400000&Signature=KVlJyDR%2BFcd8glSxYL4mWV8hFTY%3D)

- 5th 重新按照 1st & 2nd & 3rd 的方式走到 3rd 所示途中的位置会出现添加的配置，如下图（vscode连接ssh最后一步展示图）所示：

    ![vscode连接ssh最后一步展示图](https://zyb-pic-center.oss-cn-chengdu.aliyuncs.com/note-pic/%E4%BD%BF%E7%94%A8vscode%E5%BC%80%E5%8F%91kernel-%E5%AE%9E%E7%8E%B0%E5%86%85%E6%A0%B8%E4%BB%A3%E7%A0%81%E7%B2%BE%E5%87%86%E8%B7%B3%E8%BD%AC/2-2.2-4-vscode%E8%BF%9E%E6%8E%A5ssh%E6%9C%80%E5%90%8E%E4%B8%80%E6%AD%A5%E5%B1%95%E7%A4%BA%E5%9B%BE.png?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701400000&Signature=r%2FVsBitMgqnsLKH6Jo9fuZ7hqTI%3D)


- 6th 客户端登录免密登陆。


    - 参考 [git 快捷配置中生成公钥密钥](https://github.com/zyb-prj/note-center/blob/main/%E5%B8%B8%E7%94%A8%E5%B7%A5%E5%85%B7%E9%85%8D%E7%BD%AE/git%E5%BF%AB%E6%8D%B7%E9%85%8D%E7%BD%AE.md#2-1_%E7%94%9F%E6%88%90%E5%85%AC%E9%92%A5%E5%AF%86%E9%92%A5)章节内容在客户端生成公钥。

    - 使用`ssh-copy-id -p 端口号 user@hostname`指令（端口号默认22可以不用写）将本地客户端公钥复制到服务端的`~/.ssh/authorized_keys` 文件中。

    - 回到 4th 步，打开 vscode 在 4th 中设置的 config 文件，对应配置方式如下

        ```shell
        Host xx.xxx.xx.xx
          HostName xx.xxx.xx.xx
          User 主机名
          Port 端口号
          IdentityFile ~/.ssh/id_rsa
        ```

    - 配置完成之后保存即可。

- 7th 远程连接成功之后一定将插件在远程也安装一份，直接打开插件然后在本地模块往下来，看到黄色感叹号点击即可安装在远端，详情如下图（vscode客户端插件安装至服务端展示图）所示。

    ![vscode客户端插件安装至服务端展示图](https://zyb-pic-center.oss-cn-chengdu.aliyuncs.com/note-pic/%E4%BD%BF%E7%94%A8vscode%E5%BC%80%E5%8F%91kernel-%E5%AE%9E%E7%8E%B0%E5%86%85%E6%A0%B8%E4%BB%A3%E7%A0%81%E7%B2%BE%E5%87%86%E8%B7%B3%E8%BD%AC/2-2.2-5-vscode%E5%AE%A2%E6%88%B7%E7%AB%AF%E6%8F%92%E4%BB%B6%E5%AE%89%E8%A3%85%E8%87%B3%E6%9C%8D%E5%8A%A1%E7%AB%AF%E5%B1%95%E7%A4%BA%E5%9B%BE.png?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701403000&Signature=hvGnmQNaMo3j%2BkMYcu1qY5yJHxY%3D)

# 3_服务端配置

- 1st 确保 clang13.0 插件完成安装（[clang13.0安装](#1-3_安装clangd)），并获取其安装路径（此处为 ～/software/clangd_13.0.0/bin）。


- 2nd 修改服务端设置文件，客户端 vscode 连接到服务端之后打开 vscode 服务器配置文件 settings.json 做适当调整。操作流程如下图（vscode服务端配置文件settings.json流程示意图）所示。

    ![vscode服务端配置文件settings.json流程示意图](https://zyb-pic-center.oss-cn-chengdu.aliyuncs.com/note-pic/%E4%BD%BF%E7%94%A8vscode%E5%BC%80%E5%8F%91kernel-%E5%AE%9E%E7%8E%B0%E5%86%85%E6%A0%B8%E4%BB%A3%E7%A0%81%E7%B2%BE%E5%87%86%E8%B7%B3%E8%BD%AC/3-1-vscode%E6%9C%8D%E5%8A%A1%E7%AB%AF%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6settings.json%E6%B5%81%E7%A8%8B%E7%A4%BA%E6%84%8F%E5%9B%BE.png?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701403000&Signature=ZcDkgFRopbkmr%2B0vSGaaQVeH6lc%3D)

- 3rd settings.json 基本设置内容

    ```json
    {
    	"C_Cpp.default.intelliSenseMode": "linux-gcc-arm",
    	"C_Cpp.intelliSenseEngine": "Disabled",
    	"clangd.path": " /.../clangd_13.0.0/bin/clangd",
    	"clangd.arguments": [
    		"--log=verbose",
    	],
    }
    ```


# 1 软件安装

## 1.1 基础软件安装

- 安装并配置 git：参考 [git 快捷配置](https://github.com/zyb-prj/note-center/blob/main/%E5%B8%B8%E7%94%A8%E5%B7%A5%E5%85%B7%E9%85%8D%E7%BD%AE/git%E5%BF%AB%E6%8D%B7%E9%85%8D%E7%BD%AE.md)。
- 安装 bear 工具（用于生成钩子）：`sudo apt install bear`
- 安装 vscode 及其插件，详情参考 vscode 插件安装。

## 1.2 安装 vscode 及其插件

- 客户端/服务端最好均安装
- 客户端必须安装（后续使用 ssh 连接至服务端再同步至服务端）。

### 1.2.1 安装 vscode

- 官网下载：https://code.visualstudio.com/
- 个人维护
    - windows 点击此处下载
    - [mac 点击此处下载](https://zyb-software-center.oss-cn-chengdu.aliyuncs.com/mac/vscode/VSCode-darwin-arm64.zip?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701337000&Signature=DPsVDGIlMSuIP4agVHgf45es1EE%3D)
    - linux 点击此处下载

### 1.2.2 vscode 插件安装

- 客户端/服务端均安装。
- 客户端必须安装（后续可使用 ssh 连接至服务端再同步至服务端）。

#### 1.2.2.1 安装插件目录

- c 技术栈类：`C/C++`    `C/C++ Extension Pack`    `C/C++ Snippets`    `Clangd`     `Code Runner`  


- linux 开发工具类：`Remote SSH`    `DeviceTree`    `Arm Assembly`    `Hex Editor`


- 软件开发工具类：`Code Spell Checker`     `compareit`    `Tabnine AI Autocomplete` 


​									`Bracket Pair Colorization Toggler` 

- 辅助开发工具类：`Chinese`     `vscode-icons`    `One Dark Pro`


​                                     `Rainbow Highlighter` ： 高亮文字：shift + alt + z     取消高亮：shift + alt + a            

- markdown类：`Markdown All in One`    `Markdown Preview Enhanced`

#### 1.2.2.2 插件确认

具体必备插件安装如下图（vscode开发kernel所需插件合集图）所示。

![vscode开发kernel所需插件合集图](https://zyb-pic-center.oss-cn-chengdu.aliyuncs.com/note-pic/%E4%BD%BF%E7%94%A8vscode%E5%BC%80%E5%8F%91kernel-%E5%AE%9E%E7%8E%B0%E5%86%85%E6%A0%B8%E4%BB%A3%E7%A0%81%E7%B2%BE%E5%87%86%E8%B7%B3%E8%BD%AC/1-1.2-1.2.2-1.2.2.2-1-vscode%E5%BC%80%E5%8F%91kernel%E6%89%80%E9%9C%80%E6%8F%92%E4%BB%B6%E5%90%88%E9%9B%86%E5%9B%BE.png?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701340000&Signature=DguVyfN7TjO3KSUfvWMRYELepdQ%3D)

## 1.3 安装 clangd

vscode 安装 clang 插件后，它的使用还需要一个运行在 Linux 服务器上的 clangd 程序。我们以后使用 vscode 打开 c 文件时，会提示你安装 clangd 程序，它会安装最新版本(版本15)，但是这个版本有一些 Bug，所以我们手工安装版本 13。

### 1.3.1 下载源

- 官方下载地址：[Clang13.0官方版本下载](https://github.com/clangd/clangd/releases/tag/13.0.0)
- 个人维护版本：[Clang13.0个人维护版本下载](https://zyb-software-center.oss-cn-chengdu.aliyuncs.com/linux/ubuntu/clangd-linux-13.0.0.zip?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701340000&Signature=OXsecHyMZlRu2VKVjLg%2Fi3E6Dvs%3D)

### s1.3.2 下载并安装（一定要在服务端安装）

- 1st 需要安装 clang 插件

- 2nd 下载 clang13.0 版本至指定目录

- 3rd 把下载到的 clangd-linux-13.0.0.zip 放到指定目录下，此处为 ~/software

    ```bash
    unzip -d ~/software clangd-linux-13.0.0.zip
    ```

# 
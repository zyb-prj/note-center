

# 1_基本要求

当前阶段，ubuntu18 LTS 依旧为主力。使用 vim 需要各种插件，在配置文件中设置的插件更新也会默认获取最新版。官网安装的 ubuntu18 LTS 默认自带 python3.6，同时使用 `sudo apt-get install vim` 安装的 vim 版本是 8.0。在后续安装插件时会各种报错。以下为老夫亲自含泪整理的一些踩坑说明：

- 要求 vim版本是 8.0+（亲自踩坑 8.0 不行）。
- 安装代码自动补全插件 YouCompleteMe
    - 安装此插件需要获取最新版编译之后做配置。
    - 编译过程至少需要 python3.8+。
    - 需要支持 c++17 的 gcc 以及 g++。
- cmake 至少需要安装版本至少是 3.15。此为通过源码安装高版本 python（python3.10）时的要求。 具体哪个版本之后满足条件没有尝试过，反正下载最新版就对了。
- python（版本必须要大于 3.8）
    - python 用于编译  YouCompleteMe 时要用到；python 在设置 .vimrc 配置文件中要用到。
    - ubuntu18 LTS 自带 python3.6，且其中各种依赖较多，因此千万不要动 python3 这个软连接。用户安装完高版本 python（假设为 python3.10）之后直接做一个 python3.10 的软连接，然后相对应的在 .vimrc 中修改并编译插件即可。

因此若您使用 ubuntu18.04，则要安装相对较新的 gcc、cmake、python 以及 vim 再做下文配置。详情参考[安装指定版本的软件](#2_安装指定版本的软件)部分。若您使用 ubuntu22.04，则完全不需要折腾，直接参考[配置 vim 章节](#3_配置vim)操作即可。

# 2_安装vim

## 2-1_说明

我们这么折腾的目的是为了安装一些好用的插件，其中最神奇的为安装代码自动补全插件 YouCompleteMe，恰好这个安装最折腾人，几乎所有的坑都是在这个插件的安装上面。首先 vim 本身的版本必须要 8.0+ 且 8.0 不行。

## 2-2_安装

- 1st 添加一个包含最新Vim版本的软件源

  ```bash
  sudo add-apt-repository ppa:jonathonf/vim
  ```

- 2nd 更新软件包列表

  ```bash
  sudo apt update
  ```

- 3rd 执行安装指令

  ```bash
  sudo apt install vim
  ```

# 3_配置vim

此模块偏讲解，如果想直接使用，[请移步至此](#4_快速配置并使用)。

## 3-1_自动安装插件并对插件做使用快捷键配置

- 自动化过程放入 ~/.vimrc 中，这是 linux 发行版的特性做到的，不再赘述原理，直接开始即可。


- 新增 ～/.vimrc（注意位置在 home 目录下）文件并添加配置，内置默认设置以及各种插件。
- 启动 vim 时自动加载。

### 3-1-1_vim基本配置

```bash
set nocompatible												
set backspace=indent,eol,start
set guifont=Monospace\ 14
set nu!
syntax enable
syntax on
colorscheme desert
```

- 第 1 行，禁用兼容模式，为了使 vim 无线贴近 vi。
- 第 2 行，在 vim 中使用 "set backspace=indent,eol,start" 命令可以配置 backspace 键的行为，以删除缩进、行尾和行首字符。这个命令可以在Vim的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。通过设置 backspace 选项，您可以根据自己的喜好和编辑习惯来配置 vim 中 backspace 键的行为。运行该命令后，backspace 键将具有以下行为：
  - "indent"：可以使用 backspace 键删除缩进，即将光标退回到当前行的前一个非空白字符。
  - "eol"：可以使用 backspace 键删除行尾字符，即将光标退回到当前行的最后一个字符。
  - "start"：可以使用 backspace 键删除行首字符，即将光标退回到当前行的第一个字符。

- 第 3 行，vim 的 GUI 界面将使用 Monospace 字体，并将字体大小设置为 14。请注意，**在设置字体时，需要使用反斜杠来转义空格字符**。
- 第 4 行，vim 显示行号。
- 第 5 行，在 vim 中，使用`syntax enable`命令可以启用语法高亮功能。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将会根据当前文件类型自动启用相应的语法高亮规则。语法高亮可以让不同的代码元素以不同的颜色或样式进行显示，从而提高代码的可读性和可视化效果。
  - 通过启用语法高亮，您可以更清晰地看到代码的结构和语法，并更方便地进行编辑和调试。这对于编程和编辑各种类型的文本文件都非常有用。
- 第 6 行，在 vim 中，使用`syntax on`命令可以打开语法高亮功能。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将会根据当前文件类型自动打开相应的语法高亮规则。语法高亮可以使不同的代码元素以不同的颜色或样式进行显示，从而提高代码的可读性和可视化效果。
  - 通过打开语法高亮，您可以更清楚地看到代码的结构和语法，并更方便地进行编辑和调试。这对于编程和编辑各种类型的文本文件都非常有用。
- 第 7 行，在 vim 中，使用`colorscheme desert`命令可以应用 "desert" 颜色方案。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 的编辑器界面将使用 "desert" 颜色方案进行渲染。"desert" 是 vim 自带的一种颜色方案，它使用了深色背景和适宜的文本颜色，以提供舒适的编辑体验。
  - 如果您想使用其他颜色方案，可以替换 "desert" 为您所喜欢的颜色方案的名称。vim 提供了多种预定义的颜色方案供选择，也可以通过自定义配置来创建自己的颜色方案。

### 3-1-2_vim进阶设置

```bash
set autowrite   " 自动保存
set foldmethod=marker
set foldlevel=100  " 启动vim时不要自动折叠代码
set textwidth=80
set formatoptions+=t
set cindent
set smartindent
set noerrorbells
set showmatch
set nobackup 
set noswapfile
```

- 第 1 行，在 vim 中，使用`set autowrite`命令可以开启自动写入（autowrite）功能。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将会自动在某些事件发生时（例如切换文件、退出vim等）自动保存当前的文件。这样可以确保在这些事件发生时，对文件的修改会被自动写入到磁盘上，以避免意外丢失修改。
  - 自动写入功能在某些情况下非常有用，特别是在您频繁切换文件或者在退出 vim 之前忘记保存文件的情况下。它可以提供更好的编辑流畅性和文件保护。
- 第 2 行，在 vim 中，使用`set foldmethod=marker`命令可以设置折叠方法为标记（marker）。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将会使用标记作为折叠的方法。您可以在代码中使用特定的标记来定义折叠的起始和结束位置。例如，在 C 语言中，您可以使用"{ {"作为折叠的起始标记，使用"} }"作为折叠的结束标记。
  - 使用折叠可以将代码中的一部分隐藏起来，以便更好地组织和浏览大型文件。标记折叠方法允许您自定义折叠的起始和结束标记，以适应不同的语言和文件结构。
- 第 3 行，在 vim 中，使用`set foldlevel=100`命令可以设置折叠级别为 100。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将会将折叠级别设置为 100，这意味着所有可折叠的代码块都将被折叠起来。
  - 折叠级别控制着哪些代码块应该被折叠。较小的折叠级别会导致更多的代码块被折叠起来，而较大的折叠级别则会展开更多的代码块。
  - 使用折叠功能可以在编辑大型文件时更好地组织和浏览代码。通过设置折叠级别，您可以根据自己的喜好和需求来控制代码块的折叠和展开。
- 第 4 行，在 vim 中，使用`set textwidth=80`命令可以设置文本行的宽度为 80 个字符。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将会自动将文本行限制在 80 个字符的宽度范围内。当您在编辑文本时，如果输入的内容超过 80 个字符，vim 会自动将其换行。
  - 通过设置文本行宽度，可以帮助您在编辑文本文件时保持一致的格式和可读性。80个字符的宽度在许多编程语言和文本格式中是常见的标准，同时也有助于适应不同的屏幕和打印布局。
- 第 5 行，在 vim 中，使用`set formatoptions+=t`命令可以将`t`选项添加到格式选项中。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将会在格式选项中启用`t`选项。`t`选项表示在使用文本自动换行时，在新行的开始位置保留一个缩进。这对于保持段落的缩进和文本的格式化很有用。
  - 通过设置格式选项，您可以定制 vim 的文本编辑行为，以满足您的需求和喜好。添加`t`选项可以帮助您在编辑文本时保持一致的缩进和格式，提高可读性和编辑效率。
- 第 6 行，在 vim 中，使用`set cindent`命令可以启用 C 样式的自动缩进。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将会根据 C 语言的语法规则自动缩进代码。这可以帮助您在编写C语言代码时保持一致的缩进风格，提高代码的可读性。
  - 自动缩进功能会根据代码中的语法结构和大括号的位置自动调整缩进级别。这样，您可以专注于编写代码，而无需手动调整缩进。
  - 请注意，启用 C 样式的自动缩进可能不仅适用于 C 语言，还可以适用于其他使用类似语法的编程语言，如 C++ 和 Java。
- 第 7 行，在 vim 中，使用`set smartindent`命令可以启用智能缩进功能。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将会根据上一行的缩进来自动调整下一行的缩进。这可以帮助您在编写代码时保持一致的缩进风格，提高代码的可读性。
  - 智能缩进功能会根据上下文和语法规则自动调整缩进级别。它适用于许多编程语言，并且可以在多种代码编辑环境下使用。
  - 值得注意的是，vim 还提供了其他缩进选项，如`autoindent`和`cindent`，以适应不同的编码风格和语言要求。您可以根据需要选择适合您的选项来实现最佳的缩进行为。
- 第 8 行，在 vim 中，在 vim中，使用`set noerrorbells`命令可以禁用错误提示音。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将不再发出错误提示音，无论是在编辑过程中还是在执行命令时出现错误。
  - 禁用错误提示音可以提供更加安静和无干扰的编辑环境，尤其当您在处理大量代码或进行复杂编辑时，避免不必要的干扰声是很有帮助的。
  - 如果您希望重新启用错误提示音，可以使用`set errorbells`命令。
- 第 9 行，在 vim 中，使用`set showmatch`命令可以启用匹配括号高亮显示功能。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将会在您输入括号时，自动高亮显示相匹配的括号。这样可以帮助您更清楚地看到代码中的括号匹配情况，避免出现括号不匹配的错误。
  - 高亮显示匹配括号可以提高代码的可读性，并且对于编写复杂的嵌套代码尤为有用。当您在输入括号时，vim 会自动将光标跳转到相匹配的括号位置，方便您进行编辑。
  - 如果您希望禁用括号匹配的高亮显示功能，可以使用`set noshowmatch`命令。
- 第 10 行，在 vim 中，使用`set nobackup`命令可以禁用备份文件的创建。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将不再创建备份文件。备份文件通常以文件名后跟一个波浪线`~`的形式存在，它们是原始文件的副本，用于恢复意外丢失的修改。
  - 禁用备份文件的创建可以避免在文件系统中产生大量的备份文件，同时也可以节省磁盘空间。
  - 如果您希望重新启用备份文件的创建，可以使用`set backup`命令。
- 第 11行，在 vim 中，使用`set noswapfile`命令可以禁用交换文件的创建。
  - 这个命令可以在 vim 的命令模式下使用，通过在正常模式下按下`:`来访问命令模式。
  - 运行该命令后，vim 将不再创建交换文件。交换文件是为了在发生意外关闭或崩溃时，能够恢复未保存的修改而创建的临时文件。
  - 禁用交换文件的创建可以避免在文件系统中产生多余的临时文件，同时也可以节省磁盘空间。
  - 请注意，在禁用交换文件的情况下，如果 vim 在编辑过程中意外关闭或崩溃，您可能会丢失未保存的修改。因此，建议定期手动保存文件以确保数据的安全性。
  - 如果您希望重新启用交换文件的创建，可以使用`set swapfile`命令。

### 3-1-3_设置光标移动（上下左右）

#### 3-1-3-1_禁止键盘的上下左右按键

```bash
" disable 
" noremap <Up> <Nop>
" noremap <Down> <Nop>
" noremap <Left> <Nop>
" noremap <Right> <Nop>
```

- 上述代码是在 vim 中使用注释`disable`和`noremap`命令来禁用上、下、左、右方向键的映射。
- 使用双引号`"`在 vim 中表示注释，这意味着相关行的代码将被忽略，不会执行。
- `noremap`命令用于创建非递归映射。在这种情况下，"Up"、"Down"、"Left" 和 "Right" 被映射为 "Nop"，这意味着按下这些方向键时不会有任何操作。
- 这种做法可以帮助您禁用方向键在 vim 中的默认功能，以防止误操作或改为其他快捷键。但请注意，禁用方向键可能会影响您在编辑和导航文件时的体验，请确保您有其他方式进行光标移动和滚动页面。

#### 3-1-3-2_设置窗口切换

```bash
" remap control + arrow key to select windows
noremap <C-Down>  <C-W>j
noremap <C-Up>    <C-W>k
noremap <C-Left>  <C-W>h
noremap <C-Right> <C-W>l
noremap <C-J> <C-W>j
noremap <C-K> <C-W>k
noremap <C-H> <C-W>h
noremap <C-L> <C-W>l
```

- 上述代码是在 vim 中使用`noremap`命令将`Ctrl+`方向键映射为选择窗口的操作。
- `noremap`命令用于创建非递归映射。在这种情况下，"Up"、"Down"、"Left" 和 "Right" 被映射为 "j"、"k"、"h" 和 "l"，分别用于在不同的窗口之间进行切换。
- 此外，还有将`Ctrl+j`、`Ctrl+k`、`Ctrl+h`和`Ctrl+l`映射为相同的窗口选择操作的快捷键。这样您就可以使用不同的组合键进行窗口之间的切换，而不仅限于方向键。
- 通过这些映射，您可以更快速和方便地在不同窗口之间进行切换，提高编辑和导航的效率。

## 3-2_插件安装

下面各种配置均需要写入 ~/.vimrc 中。

### 3-2-1_安装插件管理工具Vundle

#### 3-2-1-1_说明

这步是必须的，有插件管理器才能通过配置文件安装插件。

Vundle 插件可以在 .vimrc 中跟踪、管理和自动更新插件内容。 

#### 3-2-1-2_安装

- 1st 创建插件目录（关键，固定文件夹）

  - 跳转至用户根目录

    ```shell
    cd ~
    ```

  - 创建指定文件夹（固定格式，不要更改）

    ```shell
    mkdir .vim && cd .vim && mkdir bundle && cd bundle
    ```

- 2nd 在指定目录`~/.vim/bundle`中下载插件

  ```bash
  git clone https://github.com/VundleVim/Vundle.vim.git
  ```

#### 3-2-1-3_配置

做法：写入配置文件中 ~/.vimrc 中。

- 1st：打开文件

  ```bash
  vim ~/.vimrc
  ```

- 2nd：将以下内容写入

  ```bash
  " Vundle manage
  set nocompatible              " be iMproved, required
  filetype off                  " required
  
  " set the runtime path to include Vundle and initialize
  set rtp+=~/.vim/bundle/Vundle.vim
  ```

  - 第 1 | 5 行，`"`在 .vimrc 中用于做注释。
  - 第 2 行，设置 vim 以非兼容模式运行，使用`set nocompatible`命令。这是为了确保 vim 支持更多的现代功能。
  - 第 3 行，使用`filetype off`命令，用于在加载插件之前禁用自动检测文件类型。这是因为 Vundle 插件管理器需要在 filetype 插件之前加载插件。
  - 第 6  行，将运行时路径 runtime path 设置为包含 Vundle 插件的路径。通过设置`set rtp+=~/.vim/bundle/Vundle.vim`，将 Vundle 插件的安装路径添加到运行时路径中。

### 3-2-2_插件安装与配置

在 vim 中使用 Vundle 插件管理器来配置和安装一系列插件，做法是现在 .vimrc 文件中做设置，然后打开 vim 执行 `:PluginInstall`命令即可自动安装插件。

```bash
call vundle#begin()

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
Plugin 'vim-airline/vim-airline' | Plugin 'vim-airline/vim-airline-themes' " Status line"
Plugin 'jiangmiao/auto-pairs'
Plugin 'mbbill/undotree'
Plugin 'gdbmgr'
Plugin 'scrooloose/nerdcommenter'
Plugin 'Yggdroot/indentLine' " Indentation level"
Plugin 'bling/vim-bufferline' " Buffer line"
"Plugin 'kepbod/quick-scope' " Quick scope
Plugin 'yianwillis/vimcdoc'
Plugin 'nelstrom/vim-visual-star-search'
Plugin 'mbbill/echofunc'
Plugin 'Yggdroot/LeaderF', { 'do': './install.sh' }
Plugin 'vim-scripts/taglist.vim'

Plugin 'majutsushi/tagbar' " Tag bar"
Plugin 'scrooloose/nerdtree'
Plugin 'Xuyuanp/nerdtree-git-plugin'
Plugin 'jistr/vim-nerdtree-tabs'
Plugin 'w0rp/ale'
Plugin 'ludovicchabant/vim-gutentags'
Plugin 'Valloric/YouCompleteMe'
" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
```

- 首先，使用 "call vundle#begin()" 函数开始 Vundle 插件管理器的配置。这个函数调用是必需的。
- 然后，列出了一系列要安装的插件。每个插件都以`Plugin '`插件名称'"的形式指定，可以根据需要添加或删除插件。
- 插件列表中包括了一些常用的插件，例如 YouCompleteMe、NerdTree、Tagbar、Airline、Auto Pairs 等等。每个插件都以注释的形式附带了简短的说明
- 在插件列表的最后，使用 "call vundle#end()" 函数结束 Vundle 插件管理器的配置。
- 最后，设置了`filetype plugin indent on`，用于启用文件类型检测、插件和自动缩进功能。

通过这些设置，您可以使用 Vundle 插件管理器来自动下载、安装和更新所列出的插件。确保将这些设置添加到Vim的配置文件（通常是~/.vimrc）中，并准备好在安装过程中遵循相关插件的额外安装说明。

#### 3-2-2-1_不需要做特殊配置的插件

安装插件配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置相关插件的安装：

```bash
Plugin 'vim-airline/vim-airline' | Plugin 'vim-airline/vim-airline-themes' " Status line"
Plugin 'jiangmiao/auto-pairs'
Plugin 'mbbill/undotree'
Plugin 'gdbmgr'
Plugin 'scrooloose/nerdcommenter'
Plugin 'Yggdroot/indentLine' " Indentation level"
Plugin 'bling/vim-bufferline' " Buffer line"
"Plugin 'kepbod/quick-scope' " Quick scope
Plugin 'yianwillis/vimcdoc'
Plugin 'nelstrom/vim-visual-star-search'
Plugin 'mbbill/echofunc'
Plugin 'Yggdroot/LeaderF', { 'do': './install.sh' }
Plugin 'vim-scripts/taglist.vim'
```

#### 3-2-2-2_大纲生成插件Tagbar

- 作用：用源代码文件生成大纲，包括类、方法、变量以及函数名等，可以选中并快速跳转到目标位置。

- 安装插件配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置 Tagbar 的安装：

  ```bash
  Plugin 'majutsushi/tagbar' " Tag bar"
  ```

- 为了方便使用，使 vim 打开源码自动生成列表，需要做自动化配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置。

  ```bash
  " Tagbar
  let g:tagbar_width=25
  autocmd BufReadPost *.cpp,*.c,*.h,*.cc,*.cpp,*.cxx call tagbar#autoopen()
  ```

- 设置快捷键开关 F1 做开关切换。在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置。

  ```bash
  " 自定义Tagbar快捷键为F1
  nnoremap <F1> :TagbarToggle<CR>
  ```

#### 3-2-2-3_文件浏览插件NerdTree

- 作用：显示树状目录。

- 安装插件配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置 NerdTree 的安装：

  ```bash
  Plugin 'Xuyuanp/nerdtree-git-plugin'
  ```

- 为了方便使用，需要做自定义配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置。

  ```bash
  "======= NetRedTree=========
  "->NERDTree目录树插件---配置选项=====================================================         
  let g:NERDTreeDirArrowExpandable = '▸'  "目录图标                                                           
  let g:NERDTreeDirArrowCollapsible = '▾'
  "autocmd vimenter * NERDTree                "自动打开目录树
  "vim【无文件】也显示目录树 
  "vim打开目录文件也显示目录树？
  autocmd StdinReadPre * let s:std_in=1
  autocmd VimEnter * if argc() == 1 && isdirectory(argv()[0]) && !exists("s:std_in") | exe 'NERDTree' argv()[0] | wincmd p | ene     | endif
  "CRTL+N开关目录树
  map <C-n> :NERDTreeToggle<CR>
  "关闭最后一个文件，同时关闭目录树
  autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif
  "<-NERDTree目录树插件---配置选项===============================================================
  let NERDTreeWinSize=20
  "let NERDTreeShowLineNumbers=1
  let NERDTreeAutoCenter=1
  let NERDTreeShowBookmarks=1
  let g:winManagerWindowLayout='TagList'
  nmap wm :WMToggle<cr>
  ```

  - 第 3 行，设置展开目录时候的图标。
  - 第 4 行，设置关闭目录时候的图标。
  - 第 5 行，注释掉的，不自动打开目录树。
  - 第 8 行，配置无文件时或打开目录文件也显示目录树。
  - 第 11 行，配置使用`Ctrl + n`手动打开目录树。
  - 第 13 行，配置关闭最后一个文件时自动关闭 NerdTree 的设置。
  - 第 15 行，`let NERDTreeWinSize=20` 设置NerdTree窗口的宽度。
  - 第 17 行，`let NERDTreeAutoCenter=1` 设置NerdTree窗口自动居中。
  - 第 18 行，`let NERDTreeShowBookmarks=1` 是用于配置 NerdTree 插件是否显示书签的选项。
    - 当将`NERDTreeShowBookmarks`的值设置为1时，NerdTree 插件将在目录树中显示您添加的书签。书签是一种方便的方式，可以将特定的文件或目录标记为书签，以便快速导航。
    - 要使用书签功能，您可以按下 `m` 键，然后选择一个字母作为书签的标识。例如，按下 `ma` 将在当前选定的文件或目录上创建一个名为 `a` 的书签。然后，您可以按下 `go` 来打开 NerdTree 插件，并在目录树中查看和导航到添加的书签。
    - 请注意，为了使这个设置生效，您需要确保已经安装了 NerdTree 插件，并在 Vim 配置文件（通常是 `~/.vimrc`）中包含了对 NerdTree 插件的正确配置。
    - 通过将 `NERDTreeShowBookmarks` 设置为1，您可以启用 NerdTree 插件的书签功能，并在目录树中显示您的书签。根据需要和喜好，您可以调整和使用这个功能来提高代码的导航和浏览效率。
  - 第 19 行，`let g:winManagerWindowLayout='TagList'` 这行代码是为了配置 NerdTree 插件与 TagList 插件之间的窗口布局。
    - NerdTree 插件是一个用于显示和导航文件目录结构的插件，而 TagList 插件是一个用于显示代码的标签列表的插件。
    - 通过设置 `g:winManagerWindowLayout` 变量的值为 `'TagList'`，您将配置 NerdTree 插件和 TagList 插件以一种分割窗口的方式共存。在这种布局中，NerdTree 插件将显示在左侧窗口，而 TagList 插件将显示在右侧窗口。
    - 请注意，为了使此设置生效，您需要确保已经安装了 TagList 插件，并在 Vim 配置文件（通常是 `~/.vimrc`）中正确配置了 TagList 插件。这样配置之后，您可以同时使用 NerdTree 插件和 TagList 插件，并在右侧窗口中显示代码的标签列表。
  - 第 20 行，`nmap wm :WMToggle<cr>` 这行代码是用于创建一个快捷键映射，将 `wm` 映射为执行 `:WMToggle` 命令的快捷键。
    - 在这个快捷键映射中，`nmap` 表示创建一个普通模式的快捷键映射，`wm` 是您选择的快捷键，`:WMToggle` 是您要执行的命令，`<cr>` 是表示按下回车键的指令。
    - `:WMToggle` 命令是由插件 WinManager 提供的，它用于切换窗口布局。具体来说，该命令会在可用布局之间进行切换，例如 NERDTree、TagList 和其他布局。
    - 通过将快捷键 `wm` 映射为执行 `:WMToggle` 命令，您可以更方便地切换不同的窗口布局。只需按下 `wm` 快捷键即可自动切换到下一个布局。
    - 请注意，为了使这个快捷键映射生效，您需要确保已经安装了 WinManager 插件，并在 Vim 配置文件（通常是 `~/.vimrc`）中正确配置了 WinManager 插件。
    - 通过这个快捷键映射，您可以轻松切换不同的窗口布局，以适应您的编辑需求和工作流程。根据需要和喜好，您可以修改或添加其他快捷键映射来进一步定制 Vim 的操作。

#### 3-2-2-4_动态语法检测工具ale

- 作用：编辑代码过程中检测出语法错误，不用等到编译或者运行。光标移动在当前行会显示错误原因。

- 安装插件配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置 ale 的安装：

  ```bash
  Plugin 'w0rp/ale'
  ```

- 为了方便使用，需要做自定义配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置。

  通过这些配置，您可以自定义 ALE 插件的静态语法检测行为和显示选项。请将这些设置添加到 Vim 配置文件（通常是 `~/.vimrc`）中，并根据您的需求进行适当的修改。确保已经安装了 ALE 插件，并按照其文档中的说明进行配置。

  ```bash
  " ======ALE静态语法检测========
  let g:ale_sign_column_always = 1
  let g:ale_sign_error = '✗'
  let g:ale_sign_warning = 'w'
  let g:ale_statusline_format = ['✗ %d', '⚡ %d', '✔ OK']
  let g:ale_echo_msg_format = '[%linter%] %code: %%s'
  let g:ale_lint_on_text_changed = 'normal'
  let g:ale_lint_on_insert_leave = 1
  "let g:airline#extensions#ale#enabled = 1
  let g:ale_c_gcc_options = '-Wall -O2 -std=c99'
  let g:ale_cpp_gcc_options = '-Wall -O2 -std=c++14'
  let g:ale_c_cppcheck_options = ''
  let g:ale_cpp_cppcheck_options = ''
  ```

  - 第 2 行，`let g:ale_sign_column_always = 1` 设置了错误和警告的符号列总是可见。
  - 第 3 & 4 行，`let g:ale_sign_error = '✗'` 和 `let g:ale_sign_warning = 'w'` 分别设置了错误和警告的显示符号。
  - 第 5 行，`let g:ale_statusline_format` 设置了状态栏的格式，显示了错误数、警告数和检查通过的数量。
  - 第 6 行，`let g:ale_echo_msg_format` 设置了错误和警告信息的格式。
  - 第 7 行，`let g:ale_lint_on_text_changed = 'normal'` 和 `let g:ale_lint_on_insert_leave = 1` 分别设置了 ALE 插件在文本更改和插入模式离开时执行语法检测。
  - 第 10 & 11 行，`let g:ale_c_gcc_options` 和 `let g:ale_cpp_gcc_options` 设置了 C 和 C++ 的编译选项。
  - 第 12 & 13 行，`let g:ale_c_cppcheck_options` 和 `let g:ale_cpp_cppcheck_options` 设置了 C 和 C++ 的静态检测选项。

#### 3-2-2-5_自动索引插件vim-gutentags

- 作用：异步生成 tags 索引。

- 安装插件配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置 ale 的安装。

  ```bash
  Plugin 'ludovicchabant/vim-gutentags'
  ```

- 为了方便使用，当我们修改一个文件时，vim-gutentags 会在后台帮助我们更新 tags 数据索引库，为了方便使用，需要做自定义配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置。

  ```bash
  " ===========gutentags=============
  " 搜索工程目录的标志，碰到这些文件/目录名就停止向上一级目录递归
  let g:gutentags_project_root = ['.root', '.svn', '.git', '.hg', '.project', '.gitignore']
  
  " 添加ctags额外参数，会让tags文件变大
  " let g:gutentags_ctags_extra_args = ['--fields=+niazlS', '--extra=+q']
   let g:gutentags_ctags_extra_args = ['--fields=+lS']
  " let g:gutentags_ctags_extra_args += ['--c++-kinds=+px']
  " let g:gutentags_ctags_extra_args += ['--c-kinds=+px']
  
  if isdirectory("kernel/") && isdirectory("mm/")
          let g:gutentags_file_list_command = 'find arch/arm/ mm/ kernel/ include/ init/ lib/'
  endif
  ```

#### 3-2-2-6_自动补全插件YouCompleteMe

##### 3-2-2-6-1_安装插件

- 1st：安装插件配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置 YouCompleteMe 的安装。

  ```
  Plugin 'Valloric/YouCompleteMe'
  ```

- 2nd：终端启动 vim，vim 进入命令行模式，输入`PluginInstall`即可自动安装插件。

  - 安装速度与网速有关，可能需要科学上网，后续我回上传一份做维护。
  - YouCompleteMe 的安装回直接报错，别紧张，有后续措施。

注：直接安装的完全不能用，会报错，看下面操作即可。

##### 3-2-2-6-2_安装加载此插件所需的软件

此步骤专门用于ubuntu18，更高版本的 ubuntu 发行版不需要此步骤。请按照[安装指定版本的软件](#5_安装指定版本的软件)所示的步骤安装完成。

##### 3-2-2-6-3_拉取并编译源码

- 1st 进入 YCM 源码根目录 ~/.vim/bundle/YouCompleteMe（执行自动化安装后会自行下载旧版本）。

  ```bash
  cd ~/.vim/bundle/YouCompleteMe
  ```

- 2nd 拉取最新代码。

  ```bash
  git submodule update --init --recursive
  ```

  

- 2nd 在 YCM 源码根目录编译源码，一定要用做好软连接的 python3.10 编译。

  ```bash
  python3.10 install.py --clang-completer
  ```

  - --clang-completer 表示对 C/C++ 提供支持。

##### 3-2-2-6-4_安装产物

- 将 YCM 源码根目录编译产物放至 ~/.vim 下。

  ```bash
  cp third_party/ycmd/examples/.ycm_extra_conf.py ~/.vim
  ```

- 确保 ~/.vimrc 文件下有如下配置

  ```bash
  let g:ycm_server_python_interpreter='/usr/bin/python3.10'					“ 一定要注意软连接
  let g:ycm_global_ycm_extra_conf='~/.vim/.ycm_extra_conf.py'
  ```

- 再次使用`:PluginInstall`指令重新安装插件，详情参考[自动化安装插件](#3-2-2-2_自动化安装插件)部分。

##### 3-2-2-6-5_同步环境

该步骤用于解决在低版本 ubuntu 中通过编译源码安装 python3 执行编译引起 vim 启动提示错误信息的问题。

错误信息为：

```bash
The ycmd server SHUT DOWN (restart with ':YcmRestartServer'). Unexpected exit code 1.
```

解决方式如下：

- 1st 一定要确保在 ～/.vimrc 中配置的 python3 版本与编译 YouCompleteMe 的版本一致，此处为 python3.10

- 2nd 跳转至 YouCompleteMe 源码根目录

  ```bash
  cd ~/.vim/bundle/YouCompleteMe
  ```

- 3rd 执行如下指令

  ```bash
  python3.10 install.py
  ```

## 3-3_其它必备工具安装

#### 3-3-1_跳转工具ctags

##### 3-3-1-1_说明

- 作用：用于扫描指定的源文件，找出其中包含的语法元素，并把找到的相关内容记录下来，这样在浏览和查找代码时就可以利用这些记录实现查找和跳转功能。

- 为了方便使用，在 .vimrc 中已经做了配置。为了方便使用，需要做自定义配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置。

    ```bash
     "--------------------------------------------------------------------------------
    "  自动加载ctags: ctags -R
    if filereadable("tags")
          set tags=tags
    endif
    ```
    
- 常用快捷键

    |  快捷键  |                用法                |
    | :------: | :--------------------------------: |
    | Ctrl + ] | 跳转到光标处的函数或变量定义的位置 |
    | Ctrl + T |        返回到跳转之前的地方        |

##### 3-3-1-2_安装并使用

- 安装

    ```bash
    sudo apt-get install universal-ctags
    ```

- 使用

    - 在使用 ctags 工具之前需要手动生成索引文件，在需要 vim 打开的源码跟目录下执行如下指令，指令如下：

        ```bash
        ctags -R .
        ```

    - 上述指令会在当前目录下生成一个 tags 文件。启动 vim 之后需要加载这个 tags 文件，**vim 中使用如下指令实现加载**：

        ```bash
        :set tags=tags
        ```

#### 3-3-2_安装查询调用位置工具cscope

##### 3-3-2-1_说明

- 作用：查找函数在哪里被调用。

- 在 .vimrc 中已经做了配置，为了方便使用，需要做自定义配置，在您的 vim 配置文件（通常是 ~/.vimrc）中，添加以下行来配置。

    ```bash
    "--------------------------------------------------------------------------------
    " cscope:建立数据库：cscope -Rbq；  F5 查找c符号； F6 查找字符串；   F7 查找函数定义； F8 查找函数谁调用了，
    "--------------------------------------------------------------------------------
    if has("cscope")
      set csprg=/usr/bin/cscope
      set csto=1
      set cst
      set nocsverb
      " add any database in current directory
      if filereadable("cscope.out")
          cs add cscope.out
      endif
      set csverb
    endif
    
    
    :set cscopequickfix=s-,c-,d-,i-,t-,e-
    
    nmap <C-_>s :cs find s <C-R>=expand("<cword>")<CR><CR>
    nmap <C-_>g :cs find g <C-R>=expand("<cword>")<CR><CR>
    nmap <C-_>c :cs find c <C-R>=expand("<cword>")<CR><CR>
    nmap <C-_>t :cs find t <C-R>=expand("<cword>")<CR><CR>
    nmap <C-_>e :cs find e <C-R>=expand("<cword>")<CR><CR>
    nmap <C-_>f :cs find f <C-R>=expand("<cfile>")<CR><CR>
    nmap <C-_>i :cs find i ^<C-R>=expand("<cfile>")<CR>$<CR>
    nmap <C-_>d :cs find d <C-R>=expand("<cword>")<CR><CR>
    
    
    "nmap <C-_>s :cs find s <C-R>=expand("<cword>")<CR><CR>
    "F5 查找c符号； F6 查找字符串；   F7 查找函数定义； F8 查找函数谁调用了，
    nmap <silent> <F5> :cs find s <C-R>=expand("<cword>")<CR><CR> :botright copen<CR><CR> 
    nmap <silent> <F6> :cs find t <C-R>=expand("<cword>")<CR><CR> :botright copen<CR><CR>
    "nmap <silent> <F7> :cs find g <C-R>=expand("<cword>")<CR><CR> 
    nmap <silent> <F7> :cs find c <C-R>=expand("<cword>")<CR><CR> :botright copen<CR><CR>
    ```
    
    
    
- 快捷键如下

    | 快捷键 |           功能           |
    | :----: | :----------------------: |
    |   F5   |     查找 C 语言符号      |
    |   F6   |      查找指定字符串      |
    |   F7   | 查找哪些函数调用了本函数 |

##### 3-3-2-2_安装并使用

- 安装

    ```bash
    sudo apt-get install cscope
    ```

- 使用

    - 在使用 scope 工具之前需要为源码生成索引库，指令如下（在源码根目录下执行）：

        ```bash
        cscope -Rbq
        ```

    - 上述指令会生成 3 个文件，cscope.cout、scope.in.out 和 scope.po.out。其中 scosse.cout 是基本索引，后面两个文件是是使用`-q`选项生成的，用于加快 scope 索引加快速度。

# 4_快速配置并使用

## 4-1_安装8.0+版本的vim

- 1st 添加源

  ```bash
  sudo add-apt-repository ppa:jonathonf/vim
  ```

- 2nd 更新源

  ```bash
  sudo apt update
  ```

- 3rd 安装 vim

  ```bash
  sudo apt-get install vim
  ```

## 4-2_安装插件管理器Vundle

### 4-2-1_说明

这步是必须的，有插件管理器才能通过配置文件安装插件。

Vundle 插件可以在 .vimrc 中跟踪、管理和自动更新插件内容。 

### 4-2-2_安装

- 1st 创建插件目录（关键，固定文件夹）

  - 跳转至用户根目录

    ```shell
    cd ~
    ```

  - 创建指定文件夹（固定格式，不要更改）

    ```shell
    mkdir .vim && cd .vim && mkdir bundle && cd bundle
    ```

- 2nd 在指定目录`~/.vim/bundle`中下载插件

  ```bash
  git clone https://github.com/VundleVim/Vundle.vim.git
  ```

## 4-3_填充配置文件

- 1st 创建 ~/.vimrc

  ```bash
  touch ~/.vimrc
  ```

- 2nd 打开并编辑

  ```bash
  vim ~/.vimrc
  ```

- 将谢列内容放置其中

  ```bash
  " ==============vim基本配置==============
  set nocompatible
  set backspace=indent,eol,start
  set guifont=Monospace\ 14
  set nu!             " 显示行号
  syntax enable
  syntax on
  colorscheme desert
  
  set autowrite   " 自动保存
  
  set foldmethod=marker
  set foldlevel=100  " 启动vim时不要自动折叠代码
  set textwidth=80
  set formatoptions+=t
  set cindent
  set smartindent
  set noerrorbells
  set showmatch
  set nobackup 
  set noswapfile
  " set cursorline
  
  " disable 
  " noremap <Up> <Nop>
  " noremap <Down> <Nop>
  " noremap <Left> <Nop>
  " noremap <Right> <Nop>
  
  " remap control + arrow key to select windows
  noremap <C-Down>  <C-W>j
  noremap <C-Up>    <C-W>k
  noremap <C-Left>  <C-W>h
  noremap <C-Right> <C-W>l
  noremap <C-J> <C-W>j
  noremap <C-K> <C-W>k
  noremap <C-H> <C-W>h
  noremap <C-L> <C-W>l
  
  " ==============Vundle插件管理==============
  " Vundle manage
  set nocompatible              " be iMproved, required
  filetype off                  " required
  
  " set the runtime path to include Vundle and initialize
  set rtp+=~/.vim/bundle/Vundle.vim
  call vundle#begin()
  
  " let Vundle manage Vundle, required
  Plugin 'VundleVim/Vundle.vim'
  Plugin 'Valloric/YouCompleteMe'
  Plugin 'scrooloose/nerdtree'
  Plugin 'majutsushi/tagbar' " Tag bar"
  Plugin 'Xuyuanp/nerdtree-git-plugin'
  Plugin 'jistr/vim-nerdtree-tabs'
  Plugin 'vim-airline/vim-airline' | Plugin 'vim-airline/vim-airline-themes' " Status line"
  Plugin 'jiangmiao/auto-pairs'
  Plugin 'mbbill/undotree'
  Plugin 'gdbmgr'
  Plugin 'scrooloose/nerdcommenter'
  Plugin 'Yggdroot/indentLine' " Indentation level"
  Plugin 'bling/vim-bufferline' " Buffer line"
  "Plugin 'kepbod/quick-scope' " Quick scope
  Plugin 'yianwillis/vimcdoc'
  Plugin 'nelstrom/vim-visual-star-search'
  Plugin 'ludovicchabant/vim-gutentags'
  Plugin 'w0rp/ale'
  Plugin 'mbbill/echofunc'
  Plugin 'Yggdroot/LeaderF', { 'do': './install.sh' }
  Plugin 'vim-scripts/taglist.vim'
  
  " All of your Plugins must be added before the following line
  call vundle#end()            " required
  filetype plugin indent on    " required
  
  
  " ==============YCM==============
  let g:ycm_server_python_interpreter='/usr/bin/python3.10'
  let g:ycm_global_ycm_extra_conf='~/.vim/.ycm_extra_conf.py'
  let g:ycm_confirm_extra_conf = 0
    " YCM 查找定义
  let mapleader=','
  nnoremap <leader>gl :YcmCompleter GoToDeclaration<CR>
  nnoremap <leader>gf :YcmCompleter GoToDefinition<CR>
  nnoremap <leader>gg :YcmCompleter GoToDefinitionElseDeclaration<CR>
  let g:ycm_collect_identifiers_from_tags_files = 1
  
  " 语法关键字补全
  let g:ycm_seed_identifiers_with_syntax = 1
  
  set completeopt=menu,menuone   
  let g:ycm_add_preview_to_completeopt = 0  " 关闭函数原型提示
  
  let g:ycm_show_diagnostics_ui = 0 " 关闭诊断信息
  let g:ycm_server_log_level = 'info'
  let g:ycm_min_num_identifier_candidate_chars = 2  " 两个字符触发 补全
  let g:ycm_collect_identifiers_from_comments_and_strings = 1 " 收集
  let g:ycm_complete_in_strings=1
  
  " noremap <c-z> <NOP>
  " let g:ycm_key_invoke_completion = '<c-z>'   " YCM 里触发语义补全有一个快捷键
  " let g:ycm_max_num_candidates = 15  " 候选数量
  
  let g:ycm_semantic_triggers =  {
                          \ 'c,cpp,python,java,go': ['re!\w{2}'],
                          \ }
  
  
  " ===========gutentags=============
  " 搜索工程目录的标志，碰到这些文件/目录名就停止向上一级目录递归
  let g:gutentags_project_root = ['.root', '.svn', '.git', '.hg', '.project', '.gitignore']
  
  " 添加ctags额外参数，会让tags文件变大
  " let g:gutentags_ctags_extra_args = ['--fields=+niazlS', '--extra=+q']
   let g:gutentags_ctags_extra_args = ['--fields=+lS']
  " let g:gutentags_ctags_extra_args += ['--c++-kinds=+px']
  " let g:gutentags_ctags_extra_args += ['--c-kinds=+px']
  
  if isdirectory("kernel/") && isdirectory("mm/")
          let g:gutentags_file_list_command = 'find arch/arm/ mm/ kernel/ include/ init/ lib/'
  endif
  
  
  " =======echodoc 显示函数参数===========
  " ctags -R --fields=+lS .
  
  "======= NetRedTree=========
  "->NERDTree目录树插件---配置选项=====================================================         
  let g:NERDTreeDirArrowExpandable = '▸'  "目录图标                                                           
  let g:NERDTreeDirArrowCollapsible = '▾'
  "autocmd vimenter * NERDTree                "自动打开目录树
  "vim【无文件】也显示目录树 
  "vim打开目录文件也显示目录树？
  autocmd StdinReadPre * let s:std_in=1
  autocmd VimEnter * if argc() == 1 && isdirectory(argv()[0]) && !exists("s:std_in") | exe 'NERDTree' argv()[0] | wincmd p | ene     | endif
  "CRTL+N开关目录树
  map <C-n> :NERDTreeToggle<CR>
  "关闭最后一个文件，同时关闭目录树
  autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif
  "<-NERDTree目录树插件---配置选项===============================================================
  let NERDTreeWinSize=25
  "let NERDTreeShowLineNumbers=1
  let NERDTreeAutoCenter=1
  let NERDTreeShowBookmarks=1
  let g:winManagerWindowLayout='TagList'
  nmap wm :WMToggle<cr>
  
  " ======ALE静态语法检测========
  let g:ale_sign_column_always = 1
  let g:ale_sign_error = '✗'
  let g:ale_sign_warning = 'w'
  let g:ale_statusline_format = ['✗ %d', '⚡ %d', '✔ OK']
  let g:ale_echo_msg_format = '[%linter%] %code: %%s'
  let g:ale_lint_on_text_changed = 'normal'
  let g:ale_lint_on_insert_leave = 1
  "let g:airline#extensions#ale#enabled = 1
  let g:ale_c_gcc_options = '-Wall -O2 -std=c99'
  let g:ale_cpp_gcc_options = '-Wall -O2 -std=c++14'
  let g:ale_c_cppcheck_options = ''
  let g:ale_cpp_cppcheck_options = ''
  
  " ========airline状态栏=========  
  let g:airline#extensions#tabline#enabled = 1
  let g:airline_section_b = '%-0.10{getcwd()}'
  let g:airline_section_c = '%t'
  let g:airline#extensions#tagbar#enabled = 1
  let g:airline_section_y = ''
  
  "--------------------------------------------------------------------------------
  " cscope:建立数据库：cscope -Rbq；  F5 查找c符号； F6 查找字符串；   F7 查找函数定义； F8 查找函数谁调用了，
  "--------------------------------------------------------------------------------
  if has("cscope")
    set csprg=/usr/bin/cscope
    set csto=1
    set cst
    set nocsverb
    " add any database in current directory
    if filereadable("cscope.out")
        cs add cscope.out
    endif
    set csverb
  endif
  
  
  :set cscopequickfix=s-,c-,d-,i-,t-,e-
  
  nmap <C-_>s :cs find s <C-R>=expand("<cword>")<CR><CR>
  nmap <C-_>g :cs find g <C-R>=expand("<cword>")<CR><CR>
  nmap <C-_>c :cs find c <C-R>=expand("<cword>")<CR><CR>
  nmap <C-_>t :cs find t <C-R>=expand("<cword>")<CR><CR>
  nmap <C-_>e :cs find e <C-R>=expand("<cword>")<CR><CR>
  nmap <C-_>f :cs find f <C-R>=expand("<cfile>")<CR><CR>
  nmap <C-_>i :cs find i ^<C-R>=expand("<cfile>")<CR>$<CR>
  nmap <C-_>d :cs find d <C-R>=expand("<cword>")<CR><CR>
  
  
  "nmap <C-_>s :cs find s <C-R>=expand("<cword>")<CR><CR>
  " F5 查找函数或变量的定义； F6 查找字符串；   F8 查找函数谁调用了，
  nmap <silent> <F5> :cs find s <C-R>=expand("<cword>")<CR><CR> :botright copen<CR><CR> 
  " F6 在光标下搜索当前单词
  nmap <silent> <F6> :cs find t <C-R>=expand("<cword>")<CR><CR> :botright copen<CR><CR>
  " F7 搜索光标下的符号的引用（使用该函数或访问该变量的地方）；
  nmap <silent> <F7> :cs find g <C-R>=expand("<cword>")<CR><CR> :botright copen<CR><CR>
  " F8 光标下搜索当前单词的定义
  nmap <silent> <F8> :cs find c <C-R>=expand("<cword>")<CR><CR> :botright copen<CR><CR>
  
  
   "--------------------------------------------------------------------------------
  "  自动加载ctags: ctags -R
  if filereadable("tags")
        set tags=tags
  endif
  
  "--------------------------------------------------------------------------------
  " global:建立数据库
  "--------------------------------------------------------------------------------
  if filereadable("GTAGS")
          set cscopetag
          set cscopeprg=gtags-cscope
          cs add GTAGS
          au BufWritePost *.c,*.cpp,*.h silent! !global -u &
  endif
  
  " Tagbar
  let g:tagbar_width=25
  autocmd BufReadPost *.cpp,*.c,*.h,*.cc,*.cpp,*.cxx call tagbar#autoopen()
  nnoremap <F1> :TagbarToggle<CR>
  
  "->taglist浏览插件配置=========================================
  "taglist窗口显示在右侧，缺省为左侧
  let Tlist_Use_Right_Window=1
  "设置ctags路径"将taglist与ctags关联
  let Tlist_Ctags_Cmd = '/usr/bin/ctags'
  "启动vim后自动打开taglist窗口
  let Tlist_Auto_Open = 1
  "不同时显示多个文件的tag，只显示当前文件的
  "不同时显示多个文件的tag，仅显示一个
  let Tlist_Show_One_File = 1
  "taglist为最后一个窗口时，退出vim
  let Tlist_Exit_OnlyWindow = 1
  "let Tlist_Use_Right_Window =1
  "设置taglist窗口大小
  "let Tlist_WinHeight = 100
  "let Tlist_WinWidth = 40
  "设置taglist打开关闭的快捷键F8
  noremap <F2> :TlistToggle<CR>
  "更新ctags标签文件快捷键设置
  noremap <F3> :!ctags -R<CR>
  "<-taglist=========================================
  ```

## 4-4_安装插件

### 4-4-1_普通插件安装

- 1st 启动 vim
- 2nd vim 进入命令行模式，输入指令`PluginInstall`即可自动安装。

### 4-4-2_YCM的安装

#### 4-4-2-1_安装加载此插件所需的软件

此步骤专门用于ubuntu18，更高版本的 ubuntu 发行版不需要此步骤。请按照[安装指定版本的软件](#5_安装指定版本的软件)所示的步骤安装完成。

#### 4-4-2-2_拉取并编译源码

- 1st 进入 YCM 源码根目录 ~/.vim/bundle/YouCompleteMe（执行自动化安装后会自行下载旧版本）。

  ```bash
  cd ~/.vim/bundle/YouCompleteMe
  ```

- 2nd 拉取最新代码。

  ```bash
  git submodule update --init --recursive
  ```

  

- 2nd 在 YCM 源码根目录编译源码，一定要用做好软连接的 python3.10 编译。

  ```bash
  python3.10 install.py --clang-completer
  ```

  - --clang-completer 表示对 C/C++ 提供支持。

#### 4-4-2-3_安装产物

- 将 YCM 源码根目录编译产物放至 ~/.vim 下。

  ```bash
  cp third_party/ycmd/examples/.ycm_extra_conf.py ~/.vim
  ```

- 确保 ~/.vimrc 文件下有如下配置

  ```bash
  let g:ycm_server_python_interpreter='/usr/bin/python3.10'					“ 一定要注意软连接
  let g:ycm_global_ycm_extra_conf='~/.vim/.ycm_extra_conf.py'
  ```

- 再次使用`:PluginInstall`指令重新安装插件，详情参考[自动化安装插件](#3-2-2-2_自动化安装插件)部分。

#### 4-4-2-4_同步环境

该步骤用于解决在低版本 ubuntu 中通过编译源码安装 python3 执行编译引起 vim 启动提示错误信息的问题。

错误信息为：

```bash
The ycmd server SHUT DOWN (restart with ':YcmRestartServer'). Unexpected exit code 1.
```

解决方式如下：

- 1st 一定要确保在 ～/.vimrc 中配置的 python3 版本与编译 YouCompleteMe 的版本一致，此处为 python3.10

- 2nd 跳转至 YouCompleteMe 源码根目录

  ```bash
  cd ~/.vim/bundle/YouCompleteMe
  ```

- 3rd 执行如下指令

  ```bash
  python3.10 install.py
  ```

## 4-5_其它必备工具安装

#### 4-5-1_跳转工具ctags

##### 4-5-1-1_说明

- 作用：用于扫描指定的源文件，找出其中包含的语法元素，并把找到的相关内容记录下来，这样在浏览和查找代码时就可以利用这些记录实现查找和跳转功能。

- 常用快捷键

  |  快捷键  |                用法                |
  | :------: | :--------------------------------: |
  | Ctrl + ] | 跳转到光标处的函数或变量定义的位置 |
  | Ctrl + T |        返回到跳转之前的地方        |

##### 4-5-1-2_安装并使用

- 安装

  ```bash
  sudo apt-get install universal-ctags
  ```

- 使用

  - 在使用 ctags 工具之前需要手动生成索引文件，在需要 vim 打开的源码跟目录下执行如下指令，指令如下：

    ```bash
    ctags -R .
    ```

  - 上述指令会在当前目录下生成一个 tags 文件。启动 vim 之后需要加载这个 tags 文件，**vim 中使用如下指令实现加载**：

    ```bash
    :set tags=tags
    ```

#### 4-5-2_安装查询调用位置工具cscope

##### 4-5-2-1_说明

- 作用：查找函数在哪里被调用。

- 快捷键如下

  | 快捷键 |           功能           |
  | :----: | :----------------------: |
  |   F5   |     查找 C 语言符号      |
  |   F6   |      查找指定字符串      |
  |   F7   | 查找哪些函数调用了本函数 |

##### 4-5-2-2_安装并使用

- 安装

  ```bash
  sudo apt-get install cscope
  ```

- 使用

  - 在使用 scope 工具之前需要为源码生成索引库，指令如下（在源码根目录下执行）：

    ```bash
    cscope -Rbq
    ```

  - 上述指令会生成 3 个文件，cscope.cout、scope.in.out 和 scope.po.out。其中 scosse.cout 是基本索引，后面两个文件是是使用`-q`选项生成的，用于加快 scope 索引加快速度。

## 4-6_使用

# 5_安装指定版本的软件


## 5-1_安装指定版本的gcc

### 5-1-1_说明

此处特指在 ubuntu18 下折腾的情况。ubuntu18 自带的 gcc 为 7.5 版本，无法支持 c++17，无法满足 vim 插件 YCM 的编译。我们需要对其做升级。要求 gcc 以及 g++ 的版本至少为 8.0。第一种方式为官网下载然后编译、安装、使用，此方法坑太多，不建议使用。第二种方式直接使用命令行安装更新即可。

### 5-1-2_安装

- 1st 删除旧版本

  ```bash
  sudo apt-get remove gcc g++
  ```

- 2nd 使用命令行安装，此处你可以使用 Tab 键来补充指定的 gcc 以及 g++ 版本，亲测最新是 8.4 版本，满足要求。

  ```bash
  sudo apt install gcc-8
  ```

  ```bash
  sudo apt install g++-8
  ```

- 2nd 配置新版本全局可用

  - 链接 gcc

    ```bash
    sudo ln -s /usr/bin/gcc-8 /usr/bin/gcc
    ```

  - 链接 g++

    ```bash
    sudo ln -s /usr/bin/g++-8 /usr/bin/g++
    ```

## 5-2_安装指定版本的cmake

### 5-2-1_方式1

#### 5-2-1-1_下载资源

官网全版本资源下载地址：[cmake官网全版本资源下载](https://cmake.org/download/)

个人维护版本（3.27）：[cmake3.27下载](https://zyb-tools.oss-cn-chengdu.aliyuncs.com/ubuntu-software/cmake/cmake-3.27.7.tar.gz?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001696735000&Signature=zwJzsjK90Fby7%2B5kYziieyhzRfA%3D)。若下载失效，请联系我，邮箱地址为 zyb_2457@outlook.com。

#### 5-2-1-2_软件安装

- 1st 查看当前版本

  ```bash
  cmake --version
  ```

- 2nd 下载指定 cmake 源码至自定义目录，假设下载 cmake-3.27.7.tar.gz

  ```bash
  wget https://cmake.org/download/cmake-3.27.7.tar.gz
  ```

- 3rd 解压源码至指定目录（此处为 ~/tools）

  ```bash
  tar -c ~/tools -zxvf cmake-3.27.7.tar.gz
  ```

- 4th 编译安装

  - 进入源码根目录

    ```bash
    cd ~/tools/cmake-3.27.7
    ```

  - 执行配置

    ```bash
    ./bootstrap
    ```

  - 执行编译`make`

  - 执行安装

    ```bash
    sudo make install
    ```

  - 配置环境变量

    ```bash
    source ~/.bashrc
    ```

- 5th 验证

  ```bash
  cmake --version
  ```

### 5-2-2_方式2

- 1st 安装 snap 工具

  ```bash
  sudo apt install snapd
  ```

- 安装最新版本 cmake

  ```bash
  sudo snap install cmake --classic
  ```

## 5-3_安装指定版本的python3.10

### 5-3-1_源码包下载

- 官网版本下载地址（全版本）：[python官网版本下载](https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz)
- 个人维护版本（3.10）：[python3.10个人维护版本下载](https://zyb-tools.oss-cn-chengdu.aliyuncs.com/ubuntu-software/Python-3.10.0.tgz?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=3678160358&Signature=mvvAqI%2BoaxH3byjQdbrbv2ZqBWE%3D)。若下载失效，请联系我，邮箱地址为 zyb_2457@outlook.com。

### 5-3-2_编译python源码

- 1st 确认编译器及其中已经安装了 gcc（>8.0版本） 以及 cmake（>3.15版本）。

- 2nd 解压下载后的源码至自定义目录，本文以 ~/software 为例。

  ```bash
  tar -C ~/software/ -zxvf Python-3.10.0.tgz
  ```

- 3rd 安装必备工具

  ```bash
  sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev libbz2-dev wget
  ```

- 4th 进入源码根目录 ~/software/Python-3.10.0 打配置

  ```bash
  ./configure xxx
  ```

  - xxx = "**--enable-shared**" 仅用这个配置即可，因为需要动态库，此正好满足
  - xxx = "**--enable-optimiza**" 编译完成之后安装完毕是静态库，无法编译 YCM，此处为说明一下，不用就对了。

- 6th 在源码根目录 ~/software/Python-3.10.0 下执行编译

  ```bash
  make -j${nproc}
  ```

### 5-3-3_安装python3.10

此小节涉及到的目录详情见[编译python源码](#2-4-2_编译python源码)章节。

- 1th 在源码根目录 ~/software/Python-3.10.0 下执行安装指令

  ```bash
  sudo make install
  ```

- 2th 在源码根目录 ~/software/Python-3.10.0 下执行更新动态链接库缓存

  ```bash
  sudo ldconfig
  ```


- 3rd 操作过安装指令后，可执行文件位于 /usr/local/bin 中，我们需要做个 python3.10 的软连接方便后续操作。千万不要直接链接到 python3，否则后面很痛苦，详情[点击此处查看](#1_基本要求)。


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

# 2_安装指定版本的软件

## 2-1_安装vim

### 2-1-1_说明

我们这么折腾的目的是为了安装一些好用的插件，其中最神奇的为安装代码自动补全插件 YouCompleteMe，恰好这个安装最折腾人，几乎所有的坑都是在这个插件的安装上面。首先 vim 本身的版本必须要 8.0+ 且 8.0 不行。

### 2-1-2_安装

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


## 2-2_安装指定版本的gcc

### 2-2-1_说明

此处特指在 ubuntu18 下折腾的情况。ubuntu18 自带的 gcc 为 7.5 版本，无法支持 c++17，无法满足 vim 插件 YCM 的编译。我们需要对其做升级。要求 gcc 以及 g++ 的版本至少为 8.0。第一种方式为官网下载然后编译、安装、使用，此方法坑太多，不建议使用。第二种方式直接使用命令行安装更新即可。

### 2-2-2_安装

- 1st 删除旧版本

    ```bash
    sudo apt-get remove gcc g++
    ```

- 2nd 使用命令行安装，此处你可以使用 Tab 键来补充指定的 gcc 以及 g++ 版本，亲测最新是 8.4 版本，满足要求。

    ```bash
    sudo apt install gcc-8
    ```

    ```
    sudo apt install gcc+8
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

## 2-3_安装指定版本的cmake

### 2-3-1_下载资源

官网全版本资源下载地址：[cmake官网全版本资源下载](https://cmake.org/download/)

个人维护版本（3.27）：[cmake3.27下载](https://zyb-tools.oss-cn-chengdu.aliyuncs.com/ubuntu-software/cmake/cmake-3.27.7.tar.gz?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001696735000&Signature=zwJzsjK90Fby7%2B5kYziieyhzRfA%3D)。若下载失效，请联系我，邮箱地址为 zyb_2457@outlook.com。

### 2-3-2_软件安装

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

## 2-4_安装指定版本的python3.10

### 2-4-1_源码包下载

- 官网版本下载地址（全版本）：[python官网版本下载](https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz)
- 个人维护版本（3.10）：[python3.10个人维护版本下载](https://zyb-tools.oss-cn-chengdu.aliyuncs.com/ubuntu-software/Python-3.10.0.tgz?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=3678160358&Signature=mvvAqI%2BoaxH3byjQdbrbv2ZqBWE%3D)。若下载失效，请联系我，邮箱地址为 zyb_2457@outlook.com。

### 2-4-2_编译python源码

- 1st 确认编译器及其中已经安装了 gcc（>8.0版本） 以及 cmake（>3.15版本）。

- 2nd 解压下载后的源码至自定义目录，本文以 ~/software 为例。

    ```bash
    tar -C ~/software/ -zxvf Python-3.10.0.tgz
    ```

- 3rd 安装必备工具

    ```bash
    sudo apt update
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

### 2-4-3_安装python3.10

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

# 3_配置vim

## 3-1_安装插件管理工具Vundle

### 3-1-1_说明

这步是必须的，有插件管理器才能通过配置文件安装插件。

Vundle 插件可以在 .vimrc 中跟踪、管理和自动更新插件内容。 

### 3-1-2_安装

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

## 3-2_自动安装插件并对插件做使用快捷键配置

自动化过程放入 ~/.vimrc 中，这是 linux 发行版的特性做到的，不再赘述原理，直接开始即可。

### 3-2-1_添加配置vimrc

#### 3-2-1-1_说明

新增 ～/.vimrc（注意位置在 home 目录下）文件并添加配置，内置各种插件。

#### 3-2-1-2_内容

注意第78行，python软连接根据个人设置操作。内容如下：

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
let NERDTreeWinSize=20
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
"F5 查找c符号； F6 查找字符串；   F7 查找函数定义； F8 查找函数谁调用了，
nmap <silent> <F5> :cs find s <C-R>=expand("<cword>")<CR><CR> :botright copen<CR><CR> 
nmap <silent> <F6> :cs find t <C-R>=expand("<cword>")<CR><CR> :botright copen<CR><CR>
"nmap <silent> <F7> :cs find g <C-R>=expand("<cword>")<CR><CR> 
nmap <silent> <F7> :cs find c <C-R>=expand("<cword>")<CR><CR> :botright copen<CR><CR>


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
noremap <F8> :TlistToggle<CR>
"更新ctags标签文件快捷键设置
noremap <F6> :!ctags -R<CR>
"<-taglist=========================================
```

### 3-2-2_安装插件

- 已经安装 8.0+ 版本的 vim
- 已经安装 3.10+ 版本的 python 并链接至 python3.10
- 已经安装 cmake make git

#### 3-2-2-1_说明

##### 3-2-2-1-1_大纲生成插件Tagbar

- 作用：用源代码文件生成大纲，包括类、方法、变量以及函数名等，可以选中并快速跳转到目标位置。
- 安装插件配置详情见[.vimrc 内容](#3-2-1-2_内容)第 53 行。
- 为了方便使用，使 vim 打开源码自动生成列表，需要做自动化配置，详情见[.vimrc 内容](#3-2-1-2_内容)第 221~223 行。

##### 3-2-2-1-2_文件浏览插件NerdTree

- 作用：显示树状目录。
- 安装插件配置详情见[.vimrc 内容](#3-2-1-2_内容)第 54 行。
- 为了方便使用，需要做自定义配置，配置详情见[.vimrc 内容](#3-2-1-2_内容)第 127～146 行。

##### 3-2-2-1-3_动态语法检测工具

- 作用：编辑代码过程中检测出语法错误，不用等到编译或者运行。光标移动在当前行会显示错误原因。
- 安装插件配置详情见[.vimrc 内容](#3-2-1-2_内容)第 67 行，打开 vim 使用`:PluginInstall`指令安装插件。
- 为了方便使用，使 vim 任意时刻均提示错误，需要做自动化配置，详情见[.vimrc 内容](#3-2-1-2_内容)第 148~160 行。

##### 3-2-2-1-4_自动索引插件vim-gutentags

- 作用：异步生成 tags 索引。
- 安装插件配置详情见[.vimrc 内容](#3-2-1-2_内容)第 66 行。
- 为了方便使用，当我们修改一个文件时，vim-gutentags 会在后台帮助我们更新 tags 数据索引库。需要做自定义配置，配置详情见[.vimrc 内容](#3-2-1-2_内容)第 109～121 行。

##### 3-2-2-1-5_自动补全插件YouCompleteMe

- 作用：YCM 插件的作用是编辑代码自动补全。
- 安装插件配置详情见[.vimrc 内容](#3-2-1-2_内容)第 51 行。
- 安装完成效果是在`~/.vim/bundle/`目录下安装了 YCM 源码，但是 YCM 无法使用，需要重新编译并将产物配置复制到 ~/.vim 目录下做配置后重新使用`:PluginInstall`指令安装插件。
- 为了方便使用，做自动化配置使得 vim 在任一时刻编辑都会产生自动补全的效果，配置详情见[.vimrc 内容](#3-2-1-2_内容)第 77～106 行。
- YouCompleteMe 插件比较奇葩，需要拉取最新的做编译并将产物复制到指定位置，详情参考[安装自动补全插件YouCompleteMe](#3-2-2-3_安装自动补全插件YouCompleteMe)部分。

#### 3-2-2-2_自动化安装插件

##### 3-2-2-2-1_必要前提（必做）

- 插件管理工具 Vundle 安装成功，详情参考[安装插件管理工具 Vundle](#3-1_安装插件管理工具Vundle)部分。
- 配置文件.vimrc编辑完成，详情参考[添加配置 .vimrc](#3-2-1_添加配置vimrc)部分。

##### 3-2-2-2-2_安装插件

- 1st：终端启动 vim
- 2nd：vim 进入命令行模式，输入`PluginInstall`即可自动安装插件。
    - 安装速度与网速有关，可能需要科学上网，后续我回上传一份做维护。
    - YouCompleteMe 的安装回直接报错，别紧张，有后续措施。

#### 3-2-2-3_安装自动补全插件YouCompleteMe

##### 3-2-2-3-1_必要前提（必做）

- 必须安装 8.0+ 版本的 vim，3.15+ 版本的 cmake，8.0+ 版本的 gcc&g++，3.8+ 版本的 python3，详情请参考[安装指定版本软件](#2_安装指定版本的软件)处，此步骤必做。

- 其它必备软件安装。

    ```bash
    sudo apt-get install git make build-essential python3-dev
    ```

- 必须执行过自动化安装插件这一步，详情参考[自动化安装插件](#3-2-2-2_自动化安装插件)部分。

##### 3-2-2-3-2_拉取并编译源码

- 1st 进入 YCM 源码根目录 ~/.vim/bundle/YouCompleteMe（执行自动化安装后会自行下载旧版本），拉取最新代码。

    ```bash
    git submodule update --init --recursive
    ```

- 2nd 在 YCM 源码根目录编译源码，一定要用做好软连接的 python3.10 编译。

    ```bash
    python3.10 install.py --clang-completer
    ```

    - --clang-completer 表示对 C/C++ 提供支持。

##### 3-2-2-3-3_安装产物

-  将 YCM 源码根目录编译产物放至 ~/.vim 下。

    ```bash
    cp third_party/ycmd/examples/.ycm_extra_conf.py ~/.vim
    ```

- 确保 ~/.vimrc 文件下有如下配置

    ```bash
    let g:ycm_server_python_interpreter='/usr/bin/python3.10'
    let g:ycm_global_ycm_extra_conf='~/.vim/.ycm_extra_conf.py'
    ```

- 再次使用`:PluginInstall`指令重新安装插件，详情参考[自动化安装插件](#3-2-2-2_自动化安装插件)部分。

## 3-3_其它必备工具安装

#### 3-3-1_跳转工具ctags

##### 3-3-1-1_说明

- 作用：用于扫描指定的源文件，找出其中包含的语法元素，并把找到的相关内容记录下来，这样在浏览和查找代码时就可以利用这些记录实现查找和跳转功能。

- 为了方便使用，在 .vimrc 中已经做了配置，详情见[.vimrc 内容](#3-2-1-2_内容)第 205～209 行。常用快捷键

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

- 在 .vimrc 中已经做了配置，详情见[.vimrc 内容](#3-2-1-2_内容)第 169～202 行，生成 3 条快捷指令

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
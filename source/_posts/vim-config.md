---
title: vim配置
date: 2018-06-08 16:18:33
tags:
- vim
categories:
- Linux
comments:
---

# 配置文件
vim的配置是在用户主目录下的 ~/.vimrc 文件中完成的，如果没有的话，需要自己新建一下：
```
cd ~
touch .vimrc
```

# 基础配置
```
"多窗口操作
"+:扩大窗口
map + <C-W>+
"-:缩小窗口
map - <C-W>-
"C-l移动到右侧窗口
map <C-l> <C-W>l
"C-h移动到左侧窗口
map <C-h> <C-W>h
"C-j移动到下方窗口
map <C-j> <C-W>j
"C-k移动到上方窗口
map <C-k> <C-W>k

"代码折叠，zc折叠，za打开
set foldmethod=indent
set foldlevel=99
```
# 安装Vundle
Vundle 是 Vim bundle 的简称,使用git来管理vim插件，有了它，安装其它插件就方便很多。
项目地址:https://github.com/VundleVim/Vundle.vim
首先下载源码：
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```
如果~/.vim/bundle目录不存在，则新建目录：
```
cd ~
mkdir .vim
cd .vim
mkdir bundle
```
然后将下列配置放在.vimrc文件的开头：
```
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
```
如果想下载某个插件，比如自动缩进indentpython.vim插件，需要将
```
Plugin 'vim-scripts/indentpython.vim'
```
置于call vundle#begin()和call vundle#end()之间，保存配置后在vim中执行
```
:PluginInstall
```
即可以自动下载indentpython.vim插件了。
bundle可以管理下载几种不同的插件,方式如下：
```
github上的插件
Plugin 'tpope/vim-fugitive'
来自于http://vim-scripts.org/vim/scripts.html的插件
Plugin 'L9'
非github上的git插件
Plugin 'git://git.wincent.com/command-t.git'
本地插件
Plugin 'file:///home/gmarik/path/to/plugin'
" The sparkup vim script is in a subdirectory of this repo called vim.
" Pass the path to set the runtimepath properly.
" Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
有旧插件的情况下，下载新的插件并重命名以避免冲突
Plugin 'ascenator/L9', {'name': 'newL9'}
```
下载方式除了在vim中运行:PluginInstall外，还可以在命令行中运行：
```
vim +PluginInstall +qall
```
其它常用的命令：
```
:PluginList       - lists configured plugins
:PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
:PluginSearch foo - searches for foo; append `!` to refresh local cache
:PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
```

# .vimrc example
下面展示一个vim配置实例：
 ```
 "Vundle配置文件
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
Plugin 'jiangmiao/auto-pairs'
Plugin 'scrooloose/nerdtree'
Plugin 'majutsushi/tagbar'
"Plugin 'Yggdroot/indentLine'
" The following are examples of different formats supported.
" Keep Plugin commands between vundle#begin/end.
" plugin on GitHub repo
" Plugin 'tpope/vim-fugitive'
" Git plugin not hosted on GitHub
" Plugin 'git://git.wincent.com/command-t.git'
" git repos on your local machine (i.e. when working on your own plugin)
" Plugin 'file:///home/gmarik/path/to/plugin'
" The sparkup vim script is in a subdirectory of this repo called vim.
" Pass the path to set the runtimepath properly.
" Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
" see :h vundle for more details or wiki for FAQ


"插件配置
"let g:indentLine_char='┆'
"let g:indentLine_enabled = 1
"打开目录树
nmap <silent> <F3> :NERDTreeToggle<CR>
nmap <silent> <F4> :TagbarToggle<CR>


"set mouse=a  "启用鼠标
set wildmenu "按TAB键时命令行自动补齐
"Ctrl-A 选中所有内容
map <silent>  <C-A>  gg v G
set pastetoggle=<F11> "F11来支持切换paste和nopaste状态
autocmd BufNewFile,BufRead *.py,*.pl,*.sh,*.R,.vimrc set tabstop=4 softtabstop=4 shiftwidth=4 textwidth=79 expandtab autoindent fileformat=unix
"tabstop 设定 tab 长度为 4
"softtabstop 使得按退格键时可以一次删掉 4 个空格
"shiftwidth 设定 << 和 >> 命令移动时的宽度为 4
"textwidth 行最大宽度
"expandtab tab替换为空格键
"autoindent 自动缩进
"fileformat=unix 保存文件格式
set nowrapscan "禁止在搜索到文件两端时重新搜索
set incsearch "输入搜索内容时就显示搜索结果

"多窗口操作
"+:扩大窗口
map + <C-W>+
"-:缩小窗口
map - <C-W>-
"C-l移动到右侧窗口
map <C-l> <C-W>l
"C-h移动到左侧窗口
map <C-h> <C-W>h
"C-j移动到下方窗口
map <C-j> <C-W>j
"C-k移动到上方窗口
map <C-k> <C-W>k

"代码折叠，zc折叠，za打开
set foldmethod=indent
set foldlevel=99

"一键执行代码
map <F5> :call Run()<CR>
func! Run()
    exec "w"
    if &filetype == 'python'
        exec '!time python %'
    elseif &filetype == 'perl'
	exec '!time perl %'
    elseif &filetype == 'sh'
	exec '!time bash %'
    endif
endfunc

"自动插入文件头
autocmd BufNewFile *.py,*.pl,*.sh exec ":call SetTitle()"
func! SetTitle()
    if &filetype == 'sh'
        call setline(1, "\#!/bin/bash")
        call append(line("."),"\#########################################################################")
        call append(line(".")+1, "\# File Name: ".expand("%"))
        call append(line(".")+2, "\# Author: samson-xu")
        call append(line(".")+3, "\# mail: xy_xu@foxmail.com")
        call append(line(".")+4, "\# Created Time: ".strftime("%c"))
        call append(line(".")+5, "\#########################################################################")
        call append(line(".")+6, "")
        call append(line(".")+7, "")
    elseif &filetype == 'perl'
        call setline(1, "\#!/usr/bin/env perl")
        call append(line("."),"\#########################################################################")
        call append(line(".")+1, "\# File Name: ".expand("%"))
        call append(line(".")+2, "\# Author: samson-xu")
        call append(line(".")+3, "\# mail: xy_xu@foxmail.com")
        call append(line(".")+4, "\# Created Time: ".strftime("%c"))
        call append(line(".")+5, "\#########################################################################")
        call append(line(".")+6, "")
        call append(line(".")+7, "use strict;")
        call append(line(".")+8, "use warnings;")
        call append(line(".")+9, "use File::Basename;")
        call append(line(".")+10, "use Getopt::Long;")
        call append(line(".")+11, "use Data::Dumper;")
        call append(line(".")+12, "")
        call append(line(".")+13, "")
    elseif &filetype == 'python'
        call setline(1, "\# -*- coding: utf-8 -*-")
        call append(line("."),"\#########################################################################")
        call append(line(".")+1, "\# File Name: ".expand("%"))
        call append(line(".")+2, "\# Author: samson-xu")
        call append(line(".")+3, "\# mail: xy_xu@foxmail.com")
        call append(line(".")+4, "\# Created Time: ".strftime("%c"))
        call append(line(".")+5, "\#########################################################################")
        call append(line(".")+6, "")
        call append(line(".")+7, "")
    endif
    normal G
endfunc
 ```

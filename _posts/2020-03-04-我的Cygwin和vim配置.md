---
layout:     post                    # 使用的布局（不需要改）
title:      备份我的cygwin和vim配置           # 标题 
subtitle:   cygwin+vim #副标题
date:       2020-03-04              # 时间
author:     DJFML                      # 作者
header-img: img/wallhaven-Matrix.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - 终端
    - terminal
    - cygwin
    - vim
    
---

# 备份我的cygwin配置

## 终端配置 
![](img/cygwin_terminal.png)

## .bashrc配置 
```
# 我的配置
set -o vi

export LESSCHARSET=utf-8
alias less='/bin/less -r'
alias ls='/bin/ls --color'
export LC_ALL=en_US.UTF-8
export LC_CTYPE=en_US.UTF-8
export LANG=en_US.UTF-8
export OUTPUT_CHARSET="UTF8"

alias vi='/usr/bin/vim'
alias grep='grep --color'alias grep='grep --color'

alias cdgit='cd "/cygdrive/c/MyGit"'
alias cdsit='cd "/cygdrive/c/MySync/Study-IT/"'
alias cdxtk='cd "/cygdrive/c/MyWork"'
alias cdgithub='cd "/cygdrive/c/MySync/Study-IT/myGitHub"'

```  
## .vimrc配置 
```
" General {{{
set nu
set ruler
set encoding=utf-8
set fileformat=unix
" }}}

" Lang & Encoding {{{
set fileencodings=utf-8,gbk2312,gbk,gb18030,cp936
set encoding=utf-8
set langmenu=zh_CN
let $LANG = 'en_US.UTF-8'
"language messages zh_CN.UTF-8
" }}}

" Format {{{
set expandtab     " 使用空格代替tab.
set tabstop=4     " 空格数量是4。
set shiftwidth=4  " 自动缩进的宽度。
syntax on
" }}}
```  

## 右键打开cygwin

打开注册表（regedit）并定位到
`HKEY_CLASSES_ROOT\Directory\shell`

然后右击**shell->新建->项**，然后名字随便起，比如RunCygwin
在其下**再新建一项,叫做command**,表示要执行的命令,command下会有一个图标是ab字样的键值，名称是(默认)，类型是`REG_SZ`，
双击其会弹出一个"修改字符串"的窗口,修改数据数值为:
```
C:\cygwin64\bin\mintty.exe C:\cygwin64\bin\bash -login -c "cd '%1'; exec bash -rcfile ~/.bashrc"
```   
其中
C:\cygwin64\
是我此处Cygwin安装路径下的bash和mintty的的位置，其下会存在bash工具：bin\bash和bin\mintty.exe




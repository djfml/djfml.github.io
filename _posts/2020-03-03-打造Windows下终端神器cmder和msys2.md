---
layout:     post                    # 使用的布局（不需要改）
title:      打造Windows下终端神器           # 标题 
subtitle:   cmder+msys2 #副标题
date:       2020-03-03              # 时间
author:     DJFML                      # 作者
header-img: img/wallhaven-Matrix.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - 终端
    - terminal
    - cmder
    - msys2
    
---

# 打造Windows下终端神器
>cmder+msys2

## Step 1 : 安装Cmder
http://cmder.net/
下载mini版，full版均可。
full版比mini版多了GitforWindows

## Step 2 : 安装MSYS2
https://www.msys2.org/

### MSYS2 镜像配置
进入 `C:\msys64\etc\pacman.d` ， 下面有3个文件：
mirrorlist.mingw32
mirrorlist.mingw64
mirrorlist.msys

分别编辑3个文件 
mirrorlist.mingw32 内容如下：
```
##
## 32-bit Mingw-w64 repository mirrorlist
##

## Primary
## 清华大学软件镜像
Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/i686/
## 中科大镜像
Server = http://mirrors.ustc.edu.cn/msys2/mingw/i686/
## msys2.org
Server = http://repo.msys2.org/mingw/i686/
Server = https://sourceforge.net/projects/msys2/files/REPOS/MINGW/i686/
Server = https://www2.futureware.at/~nickoe/msys2-mirror/mingw/i686/
Server = https://mirror.yandex.ru/mirrors/msys2/mingw/i686/
Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/i686
Server = http://mirrors.ustc.edu.cn/msys2/mingw/i686
Server = http://mirror.bit.edu.cn/msys2/REPOS/MINGW/i686
```

mirrorlist.mingw64 内容如下：
```
##
## 64-bit Mingw-w64 repository mirrorlist
##

## Primary
## 清华大学软件镜像
Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/x86_64/
## 中科大镜像
Server = http://mirrors.ustc.edu.cn/msys2/mingw/x86_64/
## msys2.org
Server = http://repo.msys2.org/mingw/x86_64/
Server = https://sourceforge.net/projects/msys2/files/REPOS/MINGW/x86_64/
Server = https://www2.futureware.at/~nickoe/msys2-mirror/mingw/x86_64/
Server = https://mirror.yandex.ru/mirrors/msys2/mingw/x86_64/
Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/x86_64
Server = http://mirrors.ustc.edu.cn/msys2/mingw/x86_64
Server = http://mirror.bit.edu.cn/msys2/REPOS/MINGW/x86_64
```

mirrorlist.msys 内容如下：
```
##
## MSYS2 repository mirrorlist
##

## Primary
## 清华大学软件镜像
Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/msys/$arch
## 中科大镜像
Server = http://mirrors.ustc.edu.cn/msys2/msys/$arch
## msys2.org
Server = http://repo.msys2.org/msys/$arch/
Server = https://sourceforge.net/projects/msys2/files/REPOS/MSYS2/$arch/
Server = https://www2.futureware.at/~nickoe/msys2-mirror/msys/$arch/
Server = https://mirror.yandex.ru/mirrors/msys2/msys/$arch/
Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/$arch/
Server = http://mirrors.ustc.edu.cn/msys2/msys/$arch
Server = http://mirror.bit.edu.cn/msys2/REPOS/MSYS2/$arch
```

安装完, 修改好镜像之后，更新一下软件：
```
pacman -Syu
```

注意：
如果更新失败，可能会锁库。删除db.lck文件，然后重新更新即可。

## Step3 ： 集成 MSYS2 MinGW64 与 Cmder

### 1. 新建Tasks
Settings -> Startup -> Tasks -> +  增加一个Task配置:
名字： `zsh::MinGW64`
Task parameters 处设置一下默认启动目录, 我这里以 C:\Users\djfml\Documents\MinGW64home 为例：
```
/dir "C:\Users\djfml\Documents\MinGW64home"
```
Commands 这里是shell的启动命令（请写成一行）:
```
set MSYSTEM=MINGW64 & set MSYSCON=conemu64.exe & set MSYS2_PATH_TYPE=inherit & set CHERE_INVOKING=1 & "%ConEmuDir%\..\..\..\msys64\usr\bin\bash.exe" --login -i -new_console:n
```
保存

### 2. 更换默认shell
General -> General settings -> 更换 -> 保存

### 3. 更换字体
General -> Fonts
推荐字体 https://github.com/tonsky/FiraCode

### 4. 关闭新建tab的confirm标签
General -> Confirm -> 取消 Confirm creating new console/tab

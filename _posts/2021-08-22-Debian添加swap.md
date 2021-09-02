---
layout: mypost
title:   Debian添加swap
categories: [Debian,swap]
---
查看下Swap的大小

    free -m
创建一个存放Swap文件的文件夹

    mkdir /opt/swap


生成一个大小为1G，名字是swapfile的文件

    cd /opt/swap && dd if=/dev/zero of=swapfile bs=1024 count=1048576

文件转换成swap并且激活

    mkswap swapfile && swapon /opt/swap/swapfile

设置开机自动挂载 nano /etc/fstab 添加

    /opt/swap/swapfile swap swap defaults 0 0
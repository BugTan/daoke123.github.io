---
layout: mypost
title:  ArmBian做ZeroTier内网穿透
categories: [ArmBian,ddns,ZeroTier]
---
Linux最简单的安装方法：

    curl -s https://install.zerotier.com/ | sudo bash

无任何报错显示：

    *** Waiting for identity generation...

*** Success! You are ZeroTier address [ d56f99571f ].
把zerotier服务复制到系统服务目录并激活

    systemctl daemon-reload
    systemctl start zerotier-one
    systemctl enable zerotier-one //开机启动

察看状态：

    zerotier-cli info

演示：

[root@instance-1 ~]# `zerotier-cli info`
200 info d56f99571f 1.2.12 ONLINE
最后加入zerotier网络：

    zerotier-cli join <network> //你的Zeroiter网络ID

**彻底卸载Zerotier-one**
通过dpkg删除zerotier-one服务

    sudo dpkg -P zerotier-one

删除zerotier-one文件夹，该文件夹存储了address地址，删除后再次安装会获得新的address地址

    sudo rm -rf /var/lib/zerotier-one/


服务**

    sudo dpkg -P zerotier-one

删除zerotier-one文件夹，该文件夹存储了address地址，删除后再次安装会获得新的address地址

    sudo rm -rf /var/lib/zerotier-one/



---
layout: mypost
title:  Linux VPS流量查看/监测工具 -- vnStat
categories: [vnStat,Debian,vps命令]
---
vnstat安装步骤，软件包和编译安装任选一种方法即可
使用yum/apt-get 软件包管理工具进行安装：（建议使用此方法）

CentOS需要先安装EPEL第三方源，安装好EPEL后执行命令：yum install vnstat 即可安装上vnstat，安装过程可能会要求输入y 进行确认。
Fedora安装命令：yum install vnstat 或 dnf install vnstat
Debian/Ubuntu安装命令：`apt-get install vnstat`
可以`ifconfig`看看自己的网卡是否是eth0
执行一下：`vnstat -u -i eth0` 创建上对应网卡的数据库，eth0根据前面的说明自己修改网卡。
首先，停止 vnStat 服务

    systemctl stop vnstat

再启动 vnStat 服务

    systemctl start vnstat

vnstat基本使用命令

    vnstat -l    #显示实时流量
    vnstat -h    #按小时查询
    vnstat -d    #按天数查询
    vnstat -m    #按月数查询
    vnstat -w    #按周数查询
    vnstat -t    #查询TOP10

更多命令帮助信息可以 `vnstat --help` 进行查看。
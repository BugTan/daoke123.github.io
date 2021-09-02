---
layout: mypost
title:   n1用的mini docker openwrt
categories: [N1,docker,openwrt]
---
基于openwrt官方19.07.5固件打包制作。

请勿当路由使用（不包含路由组件），适合做有管理界面的mini Linux跑一些小应用比如京东签到。

启用混杂模式

    ip link set eth0 promisc on

创建虚拟macvlan网卡(IP、网关请根据自己的网络修改)

    docker network create -d macvlan --subnet=192.168.11.0/24 --gateway=192.168.11.1 -o parent=eth0 macnet

创建openwrt容器

    docker run -d --restart always --name openwrt --network macnet --privileged 99010/openwrt /sbin/init
    docker run --restart always --name openwrt -d --network macnet --privileged sulinggg/openwrt-mini:arm64 /sbin/init

进入容器并修改相关参数

    docker exec -it openwrt bash
执行此命令后我们便进入 OpenWrt 的命令行界面，首先，我们需要编辑 OpenWrt 的网络配置文件：

    vi /etc/config/network

我们需要更改 Lan 口设置：

    config interface 'lan'
            option type 'bridge'
            option ifname 'eth0'
            option proto 'static'
            option ipaddr '192.168.3.88'
            option netmask '255.255.255.0'
            option ip6assign '60'
            option gateway '192.168.3.1'
            option broadcast '192.168.3.255'
            option dns '192.168.3.1'

6.重启网络

    /etc/init.d/network restart

京东签到的ipk下载

https://github.com/jerrykuku/luci-app-jd-dailybonus

https://hub.docker.com/r/sulinggg/openwrt-mini
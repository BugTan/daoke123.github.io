---
layout: mypost
title:  N1 Armbian 安装 docker 并启用 OpenWrt
categories: [N1,docker,Armbian,OpenWrt]
---
1. 安装 docker（这一步建议处于低调上网环境，否则可能会下载慢甚至失败）

    curl -fsSL https://get.docker.com | bash


2. 拉取镜像
这里使用的 F 大的镜像，感谢！原帖地址

    docker pull unifreq/openwrt-aarch64


默认拉取最新的镜像

3. 打开网卡的混杂模式

    ip link set eth0 promisc on

复制代码

4. 创建 macvlan 网络

    docker network create -d macvlan --subnet=192.168.x.0/24 --gateway=192.168.x.1 -o parent=eth0 macnet

复制代码
注意：这里需要根据实际网络来填写网关和子网掩码，如果主路由的 ip 地址为 192.168.0.1，则将上面的 192.168.x 改为 192.168.0

5. 运行 OpenWrt

    docker run --name op --restart always -d --network macnet --privileged unifreq/openwrt-aarch64 /sbin/init



6. 修改 OpenWrt 的网络设置

    docker exec -it op bash

复制代码

    nano /etc/config/network



修改图中两处红框，
第一处修改为需要访问 OpenWrt 的 ip 地址（前三未数字需要和主路由相同，最后一位数字随意修改，不要和其他设备冲突就行）
第二出修改为主路由 ip 地址

退出，保存：
（按 ESC 键，输入

    :wq

，回车）

7. 重启 OpenWrt 的网络

    /etc/init.d/network restart

复制代码


8. 此时可以在浏览器访问第 6 步中第一个红框处填写的地址访问 OpenWrt
默认账户：root，默认密码：password

9. 设置 OpenWrt
9.1 关闭 DHCP
网络 -> 接口 -> LAN/修改

基础设置

9.2 关闭桥接
物理设置

保存即可





到这里 OpenWrt 安装并且已经设置完毕，可以日用了，下面还有一些附加设置可以选择。

1. 设置 armbian 访问 OpenWrt
在 armbian 下修改 /etc/network/interfaces 文件，替换为以下内容
auto eth0
iface eth0 inet static
address 192.168.0.x
netmask 255.255.255.0
gateway 192.168.0.1

x 代表的是你需要设置的 n1 armbian 系统的 Ip 地址
然后重新载入 networking
systemctl reload networking
复制代码
如果重载失败，请使用
systemctl status networking


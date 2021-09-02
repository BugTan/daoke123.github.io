---
layout: mypost
title:  N1 ARMBIAN 固定MAC
categories: [N1,arnbian]
---
winscp编辑网卡etc/network/interfaces，在iface eth0 inet dhcp下添加一行并保存

    pre-up ifconfig eth0 hw ether 1A:33:E6:90:1F:27
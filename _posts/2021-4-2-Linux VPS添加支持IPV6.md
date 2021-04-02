---
layout: mypost
title:  Linux VPS添加支持IPV6
categories: [ipv6,vps]
---
### Linux VPS添加支持IPV6

**一、注册he.net的账号**
1. 打开注册链接：https://www.tunnelbroker.net/register.php
![这是图片](tunnel1.jpg)

Linux下借助TunnelBroker(he.net)让不支持IPV6的VPS添加支持IPV6

**2. 对英文阅读有困难的朋友可以看一下这个翻译对照**
![这是图片](tunnel2.jpg)

Linux下借助TunnelBroker(he.net)让不支持IPV6的VPS添加支持IPV6

3. 除了公司名，其他都要填写，国家选China即可，好像没有对IP和注册地址的验证。

**二、登录TunnelBroker创建Tunnel**
1. 打开链接：https://www.tunnelbroker.net/

2. 使用前面注册的账号密码登录

3. 登录后点Create Regular Tunnel
![这是图片](tunnel3.jpg)


Linux下借助TunnelBroker(he.net)让不支持IPV6的VPS添加支持IPV6

或直接打开链接：https://www.tunnelbroker.net/new_tunnel.php

4. 填写你的公网IPV4，选择一个离你VPS最近的节点，点Create Tunnel
![这是图片](tunnel4.jpg)

Linux下借助TunnelBroker(he.net)让不支持IPV6的VPS添加支持IPV6

**三、VPS中开启IPV6配置**
1. 修改/etc/sysctl.conf，在底下加上下列代码

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

2. 执行`sysctl -p`使其生效

**四、VPS中配置Tunnel**
1. Tunnel创建完成后的页面是这样的，点`Example Configurations`
![这是图片](tunnel5.jpg)

Linux下借助TunnelBroker(he.net)让不支持IPV6的VPS添加支持IPV6

2. 选择`Linux-net-tools`
![Alt text](tunnel6.jpg)

Linux下借助TunnelBroker(he.net)让不支持IPV6的VPS添加支持IPV6

3. 复制配置代码
![Alt text](tunnel7.jpg)

Linux下借助TunnelBroker(he.net)让不支持IPV6的VPS添加支持IPV6

4. 在SSH执行上面复制的代码

**五、测试ipv6**
用ping6或者ping -6测试ipv6是否能用

```
ping6 www.google.com
ping-6 www.google.com
```

转至：https://haoduck.com/685.html

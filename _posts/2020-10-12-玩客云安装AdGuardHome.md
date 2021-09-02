---
layout: mypost
title:  玩客云安装AdGuardHome
categories: [玩客云,AdGuardHome]
---
安装 AdGuard Home

二进制版本
wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_armv7.tar.gz

tar -zxvf AdGuardHome_linux_armv7.tar.gz

cd AdGuardHome

./AdGuardHome -s install

# Linux 下使用的服务管理器是 systemd 、Upstart 或 SysV，macOS 下使用的服务管理器是 Launchd。
AdGuardHome -s install
服务安装后好，你可以使用以下命令来管理它。
#启动
systemctl start AdGuardHome
#开机自启
systemctl enable AdGuardHome
#重启
 restart AdGuardHome
#停止
systemctl stop AdGuardHome
# 卸载 AdGuardHome 服务
systemctl uninstall AdGuardHome 

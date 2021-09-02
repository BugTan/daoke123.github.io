---
layout: mypost
title:  Debian CentOS修改时区
categories: [Linux,Debian,CentOS]
---
Debian CentOS修改时区
Debian修改时区：

`dpkg-reconfigure tzdata`


CentOS修改时区：

timedatectl set-timezone Asia/Shanghai
1.首先查看当前语言环境
`env | grep LANG`	

2.开始第一步

`export LANG=en_US.UTF-8`
注意  en表示语言，US表示国家，UTF-8表示编码

第二步
`dpkg-reconfigure locales`
`reboot`
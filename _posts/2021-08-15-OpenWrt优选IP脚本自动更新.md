---
layout: mypost
title:   OpenWrt优选IP脚本自动更新
categories: [OpenWrt,优选IP]
---
https://github.com/Lbingyi/CloudflareST
路由器优选IP脚本设置定时更换优选ip
用ssh连接软件连接opewrt
# 进入root文件夹
cd /root

如果是第一次使用，则建议创建新文件夹（后续更新请跳过该步骤）

```
mkdir CloudflareST
```

进入文件夹（后续更新，只需要从这里重复下面的下载、解压命令即可）
```

cd CloudflareST
```

下载 CloudflareST 压缩包（自行根据需求替换 URL 中版本号和文件名）

```
wget -N https://cdn.jsdelivr.net/gh/Lbingyi/CloudflareST@main/cfst-DNS.tar.gz
```

解压（不需要删除旧文件，会直接覆盖，自行根据需求替换 文件名）
```

tar -zxf cfst-DNS.tar.gz
```

赋予执行权限

```
chmod +x CloudflareST
```

修改cfst-DNS.sh中的一处地方
修改微信/Telegram推送token
显示不了图片，开一下VPN吧
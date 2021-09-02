---
layout: mypost
title:   老毛子固件DNSMASQ优化：AdGuardHome外挂服务
categories: [Padavan,AdGuardHome]
---
#AdGuardHome
#表示对以下设置的所有server发起查询#选择回应最快的一条作为查询结果返回

    all-servers
    server=192.168.2.2#5533 #AdGuardHome
    dns-forward-max=1000 #AdGuardHome


 ![DNSMASQ][1]


  [1]: https://cdn.jsdelivr.net/gh/daoke123/pic/DNSMASQ.png
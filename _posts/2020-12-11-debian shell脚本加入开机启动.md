---
layout: mypost
title:  debian shell脚本加入开机启动
categories: [debian,shell]
---
问题：
debian shell脚本加入开机启动

解决：
编辑/etc/crontab，尾部加入：@reboot root /root/rules.sh即可，/root/rules.sh为脚本路径

样例：

   <pre> view source
    01
    # /etc/crontab: system-wide crontab
    02
    # Unlike any other crontab you don't have to run the `crontab'
    03
    # command to install the new version when you edit this file
    04
    # and files in /etc/cron.d. These files also have username fields,
    05
    # that none of the other crontabs do.
    06
     
    07
    SHELL=/bin/sh
    08
    PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
    09
     
    10
    # m h dom mon dow user  command
    11
    17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
    12
    25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
    13
    47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
    14
    52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
    15
    #
    16
    @reboot root /root/rules.sh</pre>
     
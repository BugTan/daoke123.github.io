---
layout: mypost
title:  Debian8小内存环境安装Caddy+PHP5+SQLite3
categories: [Debian,Caddy]
---
**Debian8小内存环境安装Caddy+PHP5+SQLite3**
**0、前言**
最近入手了<code>Gullo</code>的<code>128M</code>内存小鸡，因为内存太小，故一直在找<code>Debian8</code>能用的一键环境安装脚本，
LNMP肯定是安装不上了，编译安装一半的时候，就已经报错了，所以编译安装这条路算是走不通了。

经过多次尝试，发现<code>Caddy-Web-Server-Installer</code>整体来说做的比较好，故研究了下。
这个脚本除了没有<code>SQlite3</code>，装好了<code>Caddy+PHP5</code>可以直接用，无需额外设置。

在<code>Github</code>上，给的脚本安装多次尝试无法成功，重新改了，复制下面的命令行，粘贴到<code>SSH</code>里面回车即可。
仅测试了<code>Debian 8 64bit</code>，理论上<code>Debian8 32bit</code>、<code>Debian7 32bit</code>都可以运行这个脚本，
包括安装下面的<code>PHP</code>组件和<code>SQLite3</code>数据库，有对应环境的可以尝试下。
**1、精简系统，你可以选择性尝试执行，并不是强制性这么做，但是的确可以清理少许的内存和磁盘占用，这对小内存vps来说，是很有帮助的，在SSH执行下面的命令即可。**
<pre><code>apt-get -y update&amp;&amp;apt-get -y upgrade&amp;&amp;apt-get dist-upgrade -y&amp;&amp;apt-get -y purge apache2-* bind9-* xinetd samba-* nscd-* portmap sendmail-* sasl2-bin&amp;&amp;apt-get -y purge lynx memtester unixodbc python-* odbcinst-* sudo tcpdump ttf-*&amp;&amp;apt-get -y autoremove &amp;&amp; apt-get clean
</code></pre>
**2、使用Caddy-Web-Server-Installer安装Caddy+PHP5，既然一键能做的事情，就让脚本完成吧。**
<pre><code>bash &lt;(curl -L -s https://git.io/JvNd7)</code></pre>
如果提示：<code>-bash: curl: command not found</code>
请先执行：<code>apt-get -y update&amp;&amp;apt-get install curl -y</code>

脚本安装完成后，在SSH输入 <code>caddy install</code> 即可开始安装<code>Caddy+PHP5</code>，填入对应信息后，即可安装完成。
**3、根据需要，安装SQLite3数据库**
等全部安装成功后，在<code>SSH</code>里面执行：<code>apt-get install -y sqlite php5-sqlite</code> 即可安装<code>SQLite3</code>数据库。
**4、上传PHP源码路径，和权限设置。**
安装完成后，上传代码到<code>/caddy</code>，即可通过绑定的域名访问。
如果是<code>php</code>程序需要安装提示没有权限，那么执行：<code>chown -R caddy:caddy /caddy</code>
每次更换了源码后或者更新了这个文件夹的文件后，都需要执行<code>chown -R caddy:caddy /caddy</code>
**5、PHP的一些设置（仅Debian8）**
取消<code>php</code>已禁用的函数：<code>sed -i 's@^disable_functions.*@disable_functions = passthru,exec,system,chroot,chgrp,chown,shell_exec,proc_open,proc_get_status,ini_alter,ini_restore,dl,openlog,syslog,readlink,symlink,popepassthru,stream_socket_server,fsocket,popen@' /php.ini</code>
修改时区：<code>sed -i 's@^;date.timezone.*@date.timezone = /Shanghai@' /php.ini</code>
脚本占用最大内存16M：<code>sed -i "s@^memory_limit.*@memory_limit = 16M@" /php.ini</code>
**6、多域名绑定**
使用<code>FinalShell</code>或者<code>WinSCP</code>等可视化<code>SSH</code>工具，编辑<code>/Caddyfile</code>这个文件。
每个域名用英文状态下的中括号包裹着，就能简单的配置多域名绑定，比<code>Nginx</code>看起来简单多了。
演示下：
<pre><code> {
    root /
    gzip
    log /access.log
    errors /error.log
    fastcgi / 127.0.0.1:9000 php
    rewrite {
        if {path} not_match ^/admin
        to {path} {path}/ /index.php?{query}
     }
}
:80 {
    gzip
    proxy / 
}
:443 {
    root /caddy
    gzip
    log /access.log
    errors /error.log
    fastcgi / 127.0.0.1:9000 php
    tls .crt .key
    proxy /ws localhost:10000 {
        websocket
        header_upstream -Origin
    }
}
</code></pre>
简单说下<code>root</code>代表代码存放路径，<code>gzip</code>就是开启<code>gzip</code>压缩，<code>log</code>和<code>errors</code>是日志和错误日志，
<code>fastcgi</code>是网关接口，简单说要能解析<code>php</code>，这行就不能少，单纯的反代这行就可以不要。
<code>tls</code> 后面可以跟域名的<code>whois</code>邮箱，这样它能帮助你自动申请<code>SSL</code>证书，你也可以填写证书的绝对路径，来获取本地证书。
<code>proxy</code>是反向代理， <code>/ws</code> 代表路径，你也可以反代为主页，取消<code>ws</code>即可。/ws 后面可以跟本地地址+端口，也可以<code></code>外网网址。
<code>v2</code>一键脚本安装后，在<code>v2</code>的配置文件里面有一个端口，你就填在这里面即可。

注意事项
不管是修改了<code>/Caddyfile</code>还是修改了<code>/php.ini</code> ，都需要重启<code>caddy</code>服务才能生效。
Caddy重启命令：<code>caddy restart</code>

你可以通过<code>caddy help</code>来查看<code>caddy</code>的状态并管理它。
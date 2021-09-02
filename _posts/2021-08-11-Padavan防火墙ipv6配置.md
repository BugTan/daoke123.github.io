---
layout: mypost
title:   Padavan防火墙ipv6配置
categories: [Padavan,ipv6]
---
防火墙ipv6配置
关闭ipv6防火墙

    ip6tables -F
    ip6tables -X
    ip6tables -P INPUT ACCEPT
    ip6tables -P OUTPUT ACCEPT
    ip6tables -P FORWARD ACCEPT

本机下允许ipv6防火墙特定端口转发

    ip6tables -A FORWARD -p tcp --dport 11899 -j ACCEPT
    ip6tables -A FORWARD -p udp --dport 11899 -j ACCEPT

本机开放ipv6防火墙特定端口80/443

    ip6tables -A INPUT -p tcp --dport 80 -j ACCEPT
    ip6tables -A OUTPUT -p tcp --sport 80 -j ACCEPT
    ip6tables -A INPUT -p tcp --dport 443 -j ACCEPT
    ip6tables -A OUTPUT -p tcp --sport 443 -j ACCEPT
#本机服务端口开放 SSH:8622 HTTPS:8623

    iptables -I INPUT -p tcp --dport 8622 -j ACCEPT
    iptables -I OUTPUT -p tcp --sport 8622 -j ACCEPT
    iptables -I INPUT -p tcp --dport 8623 -j ACCEPT
    iptables -I OUTPUT -p tcp --sport 8623 -j ACCEPT
    ip6tables -I INPUT -p tcp --dport 8622 -j ACCEPT
    ip6tables -I OUTPUT -p tcp --sport 8622 -j ACCEPT
    ip6tables -I INPUT -p tcp --dport 8623 -j ACCEPT
    ip6tables -I OUTPUT -p tcp --sport 8623 -j ACCEPT


#NAS服务端口开放 88

    #iptables -I FORWARD -p tcp -d 192.168.9.10 --dport 88 -j ACCEPT
    #iptables -I FORWARD -p tcp -s 192.168.9.10 --sport 88 -j ACCEPT
    ip6tables -I FORWARD -p tcp -d 240e:XXXX:XXXX:XXXX:1a8b:15ff:fe16:5f01 --dport 88 -j ACCEPT
    ip6tables -I FORWARD -p tcp -s 240e:XXXX:XXXX:XXXX:1a8b:15ff:fe16:5f01 --sport 88 -j ACCEPT

#值班台服务端口开放 80,8080

    #iptables -I FORWARD -p tcp -d 192.168.9.209 --dport 80 -j ACCEPT
    #iptables -I FORWARD -p tcp -s 192.168.9.209 --sport 80 -j ACCEPT
    #iptables -I FORWARD -p tcp -d 192.168.9.209 --dport 8080 -j ACCEPT
    #iptables -I FORWARD -p tcp -s 192.168.9.209 --sport 8080 -j ACCEPT
    ip6tables -I FORWARD -p tcp -d 240e:XXXX:XXXX:XXXX:f017:f31f:6d5c:79ee --dport 80 -j ACCEPT
    ip6tables -I FORWARD -p tcp -s 240e:XXXX:XXXX:XXXX:f017:f31f:6d5c:79ee --sport 80 -j ACCEPT
    ip6tables -I FORWARD -p tcp -d 240e:XXXX:XXXX:XXXX:f017:f31f:6d5c:79ee --dport 8080 -j ACCEPT
    ip6tables -I FORWARD -p tcp -s 240e:XXXX:XXXX:XXXX:f017:f31f:6d5c:79ee --sport 8080 -j ACCEPT
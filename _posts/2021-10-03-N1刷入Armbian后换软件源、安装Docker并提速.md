---
layout: mypost
title:  N1 arnbian 前期基本操作管理
categories: [N1,arnbian,docker]
---
网络环境所限，在使用Armbian的时候经常下载软件出问题，下载不到或者下载中断，所以找来了国内的源，更换一下，下载会变快很多。

假定armbian已经安装完成

1、打开putty，输入N1的IP地址连接并登陆


2、输入命令

    nano /etc/apt/sources

复制代码
3、在原先的源前面加#号注释掉，并将国内源复制过去

```
    deb http://mirrors.ustc.edu.cn/debian stretch main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian stretch-updates main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian stretch-backports main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian-security/ stretch/updates main contrib non-free
```


复制代码
改 armbian 源

    nano /etc/apt/sources.list.d/armbian.list

将里面的那行注释掉（在前面添加 # ）然后添加这行

    deb https://mirrors.tuna.tsinghua.edu.cn/armbian bionic main bionic-utils bionic-desktop

4、ctrl+x退出编辑，按y回车保存
5、执行

    apt update && apt upgrade -y

复制代码
至此，软件源更换完毕。

6、安装docker

    curl -fsSL https://get.docker.com -o get-docker.sh

    sh get-docker.sh --mirror Aliyun

复制代码
使用上述命令安装会调用阿里云的镜像，安装速度较快。

7、配置docker镜像加速
登陆

    dev.aliyun.com

复制代码
进入容器镜像服务，得到镜像加速器地址



8、putty下执行

    mkdir -p /etc/docker

    tee /etc/docker/daemon.json <<-'EOF'
    {
     "registry-mirrors": [
     "https://kfwkfulq.mirror.aliyuncs.com",
     "https://2lqq34jg.mirror.aliyuncs.com",
     "https://pee6w651.mirror.aliyuncs.com",
     "https://registry.docker-cn.com",
     "http://hub-mirror.c.163.com"]
    }
    EOF

    systemctl daemon-reload

    systemctl restart docker

复制代码

9、安装docker图形化管理Portainer  

在putty下执行

    docker volume create portainer_data

    docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer:linux-arm64

复制代码
10、安装完成后可访问N1ip:9000查看图形化界面
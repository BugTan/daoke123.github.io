---
layout: mypost
title:   修改宝塔OneDrive插件API为自己的E5续命
categories: [宝塔,OneDrive,E5]
---
地址：https://portal.azure.com/#home

1：使用@xxx.onmicrosoft.com账号登陆。

2：点击左边的应用注册

3：新注册。名称：随意，类型：任何组织目录（两个都可以），重定向 URI：http://localhost/login/authorized

4：返回主页，点击打开刚注册好的应用，复制：应用程序(客户端) ID

5：点击客户端凭据，+客户端密码，名称：随意，截至日期：24个月

6：复制刚新建的客户端密码里面的值

7：返回主页，打开第3步注册的应用，点击API 权限，点击代表XXX授权管理员同意

8：宝塔安装好OneDrive插件。已登录的退出登录。

9：编辑文件/www/server/panel/plugin/msonedrive/credentials.json

10：修改onedrive-international下面的client_id为第4步复制的应用程序(客户端) ID，修改client_secret为第6步复制的值

11：保存文件后，正常登录即可。
https://hostloc.com/forum.php?mod=viewthread&tid=879895&highlight=e5
---
layout: post
title: 搭建Nginx proxy manager.md
date: 2022-4-01
author: 曲淡歌
color: rgb(2485,195,205)
cover: 'https://cdn.jsdelivr.net/gh/dangehub/ImgData/27cb10003a58f65a27f36078579b1aca.jpg'



tags: 反向代理 数码
---

# 参考资料
- [Docker系列 搭建密码管理应用bitwarden - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/506369199)
- [反向代理神器——Nginx Proxy Manager_蒟蒻颖的博客-CSDN博客](https://blog.csdn.net/zy440458/article/details/122090513)
- [反向代理服务器nginx-proxy-manager_杨浦老苏的博客-CSDN博客_免费反向代理服务器](https://blog.csdn.net/wbsu2004/article/details/122533684)
- [Nginx Proxy Manager](https://nginxproxymanager.com/guide/#hosting-your-home-network)

# 过程记录
```
version: '2'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '10000:80'
      - '10001:81'
      - '10002:443'
    volumes:
      - /www/wwwroot/NginxProxyManager/data:/data
      - /www/wwwroot/NginxProxyManager/letsencrypt:/etc/letsencrypt
```

使用默认用户名与密码登录后修改为
email: ‹邮箱›
full name: ‹全名›
nickname: ‹昵称›
password: ‹密码›


但是如果这样使用的话，反代之后的网址还是需要加上端口，十分的不美观，分析得出应该让npm接管网站的80/443端口，于是需要先解放安装了宝塔的服务器的80/443端口
	解除80占用：
		1. 在网站的nginx配置文件中修改监听的端口
		2. 在nginx配置文件中注释掉最后的默认文件[使用宝塔面板时80端口被占用的解决方法_亓根火柴的博客-CSDN博客_宝塔让出80端口](https://blog.csdn.net/qigenhuochai/article/details/82347560)


先停止npm的dcoekr `docker-compose down`


然后按照之前启动npm的方法，把端口修改好之后再启动

```
version: '2'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - /www/wwwroot/NginxProxyManager/data:/data
      - /www/wwwroot/NginxProxyManager/letsencrypt:/etc/letsencrypt
```

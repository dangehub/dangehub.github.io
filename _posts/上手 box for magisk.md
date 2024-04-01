---
share: true 
title: 安卓透明代理，上手 box for magisk
tags: 
- geek
- Android 
- magisk 
- proxy
categories:
- geek
---
# 前言
在使用安卓设备的时候也有科学上网的需求，而直接使用app层级的代理会遇见以下几种问题：
1. 部分app会检测代理：比如soul微调，检测代理的主要原因都是为了防破解/防抓包
2. vpn app不稳定，容易被杀后台
3. 在使用命令行时无法通过app代理 
综上所述，需要实现透明代理。目前有两个项目是比较符合的我的需求，同时又有着比较低的上手门槛的：
1. 神秘盒子：基于singbox的代理模块，无法使用自定义的分流配置，但是上手简单，有app作为图形化界面
2. box for magisk：支持诸如v2ray和clash等核心，支持自定义配置，~~目前没有图形化界面~~ 可以用app管理，但是不能在app里设置订阅。
# 项目实践
- 项目地址：[taamarin/box_for_magisk: Transparent Proxy for Android(root)](https://github.com/taamarin/box_for_magisk)
- 文档地址：[box_for_magisk/docs/index_cn.md at master · taamarin/box_for_magisk](https://github.com/taamarin/box_for_magisk/blob/master/docs/index_cn.md)
- 配套的配置app[taamarin/box: box manager](https://github.com/taamarin/box)

## 安装记录
1. 下载并刷入模块 
2. 在刷入时用`音量+`选择下载内核，或者刷入后使用命令行
   `su -c /data/adb/box/scripts/box.tool upcore`（此命令为更新指定的内核，需要先确认配置文件）
3. 
```
   # 更新 Clash 管理面板
su -c /data/adb/box/scripts/box.tool upyacd
```
4. 配置`/data/adb/box/settings.ini`
```
interva_update="@daily"  #更新频率
run_crontab="true"  #开启定时更新
subscription_url_clash="<订阅地址>"  #配置clash订阅地址，如果handshake报错可以把https改为http
renew=true  #采用订阅文件中的分流规则
```
5. 终端中运行命令`  su -c /data/adb/box/scripts/box.tool subs`  
6. 如果有需要更新Geo数据库，可以采用`su -c /data/adb/box/scripts/box.tool geox`
7. 如果需要同时更新订阅与Geo，可以使用`su -c /data/adb/box/scripts/box.tool subs`
---
{"title":"密码管理器：从bitwarden迁移到keepass","date":"2024-04-24","lastmod":"2024-12-16","creation date":"2024-04-24 19:19","modification date":"星期一 2024 十二月16日 12:25:42","tags":["自托管"],"categories":["geek"],"alases":null,"dg-publish":true,"created":"2025-03-08T11:35","updated":"2025-04-15T21:50","dg-path":"自托管折腾/密码管理器：从bitwarden迁移到keepass.md","permalink":"/自托管折腾/密码管理器：从bitwarden迁移到keepass/","dgPassFrontmatter":true,"noteIcon":""}
---



# bitwarden到keepass的迁移

bitwarden和keepass同为开源的支持自托管的密码管理器，keepass可以做到无服务端，因此我决定将我的密码库迁移到keepass，但是bitwarden直接导出的备份文件是不能把附件和totp等导入到keepass的，因此我们需要借助第三方项目来完成。

项目地址：https://hub.docker.com/r/rogsme/bitwarden-to-keepass#!

本项目在github上也有python版本，但是我更喜欢用docker解决这种有运行环境的东西。

这里我采用windows的docker desktop，需要注意是本地文件挂载的写法

下面附上我的启动命令：
```
docker run --rm -it -e BITWARDEN_URL="https://bitwarden.your.com/" -v C:\Users\username\Documents\keepass:/exports rogsme/bitwarden-to-keepass
```

其中`BITWARDEN_URL`是自托管的项目地址，如果不设置这个环境变量，则是从官方项目获取。

启动docker后，需要手动输入新建keepass的密码、bitwarden的邮箱、bw的密码，然后等待完成后，就可以在挂载的目录下找到对应的kpdb文件，导入到keepass即可。

# 多平台客户端的选择 

迁移之后就要考虑如何使用了，如何选择客户端，我主要参考了下面这篇文章。

下表转自文章 [不只为了省钱：开源密码管理器可用性报告](https://client.sspai.com/prime/story/opensource-password-managers-compared#!)


| 平台            | 推荐客户端                                                                                                                                                                                                                                                                                                                                                                                |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Windows/Linux | [KeePassXC](https://client.sspai.com/link?target=https%3A%2F%2Fkeepassxc.org%2F) (开源免费，Qt 框架)                                                                                                                                                                                                                                                                                        |
| macOS         | [Strongbox](https://client.sspai.com/link?target=https%3A%2F%2Fgithub.com%2Fstrongbox-password-safe%2FStrongbox) (开源，高级功能 €15/年或 €60 买断)<br><br>KeePassXC<br><br>[KeePassium](https://client.sspai.com/link?target=https%3A%2F%2Fgithub.com%2Fkeepassium%2FKeePassium) (开源，高级功能 $20/年或 $80 买断)                                                                                       |
| iOS           | Strongbox<br><br>KeePassium                                                                                                                                                                                                                                                                                                                                                          |
| Android       | [Keepass2Android](https://client.sspai.com/link?target=https%3A%2F%2Fgithub.com%2FPhilippC%2Fkeepass2android) (开源免费)<br><br>[KeePassDX](https://client.sspai.com/link?target=https%3A%2F%2Fgithub.com%2FKunzisoft%2FKeePassDX) (开源免费，有[捐赠版](https://client.sspai.com/link?target=https%3A%2F%2Fplay.google.com%2Fstore%2Fapps%2Fdatasafety%3Fid%3Dcom.kunzisoft.keepass.pro)，$10 买断) |
| 浏览器           | [Strongbox 自带](https://client.sspai.com/link?target=https%3A%2F%2Fstrongbox.reamaze.com%2Fkb%2Fautofill%2Fare-there-any-browser-plugins-for-strongbox) (Chromium、Firefox 和 Safari)<br><br>[KeePassXC-Browser](https://client.sspai.com/link?target=https%3A%2F%2Fgithub.com%2Fkeepassxreboot%2Fkeepassxc-browser) (Chromium 和 Firefox)                                               |
| 命令行           | [KeePassXC 自带](https://client.sspai.com/link?target=https%3A%2F%2Fkeepassxc.org%2Fdocs%2FKeePassXC_UserGuide%23_command_line_tool)                                                                                                                                                                                                                                                   |



## 安卓端


我对比了Keepass2Android和KeePassDX，前者界面比较古老，后者界面更好看，但是只有k2a支持多种云服务，而kpdx只支持本地文件（并且作者声明这是他的选择，为了更安全），云同步得自己用第三方软件实现。

最后我选择使用了[KeePassDX](https://play.google.com/store/apps/details?id=com.kunzisoft.keepass.free&hl=en)，然后采用[Foldersync app](https://play.google.com/store/apps/details?id=dk.tacit.android.foldersync.lite&hl=en)实现同步，云盘使用我自己搭建的webdav。

## win端

最后我选择了KeePassXC这个客户端，因为它也比较好看，功能也全面。不过它有一个缺点：中英文混排时，部分英文字母会变的很奇怪。

桌面：[KeePassXC Password Manager](https://keepassxc.org/)

浏览器装对应插件 


# 云同步的实现和备份 

## 采用Obcsapi的webdav


## 将obcsapi同步到onedrive

目录1:/mnt/onedrive
目录2:/data/compose/obcsapi

~~然后写个脚本，一直保活在后台监控~~ <font color="#ff0000">此方法已被废弃。</font>

```
#!/bin/bash

  

# 源目录和目标目录

SOURCE_DIR="/data/compose/obcsapi"

DESTINATION_DIR="/mnt/onedrive/obcsapi"

  

# 从源目录到目标目录的同步

rsync -av --delete "$SOURCE_DIR/" "$DESTINATION_DIR/"

  

# 从目标目录到源目录的同步

rsync -av --delete "$DESTINATION_DIR/" "$SOURCE_DIR/"
```

现在采用的备份方法是定期压缩并同步到onedrive，使用1panel自带的备份工具。
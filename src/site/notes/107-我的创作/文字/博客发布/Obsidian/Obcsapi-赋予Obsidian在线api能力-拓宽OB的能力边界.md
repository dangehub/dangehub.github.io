---
{"uid":20241230193952,"title":"Obcsapi：一个赋予Obsidian在线api能力，再次拓宽OB的能力边界的超级工具","tags":["geek","obsidian插件","obsidian","obsidian同步","memos"],"description":"这是一个基于S3 存储/CouchDb/本地存储的后端 API 项目，可以对外提供WebDAV服务，可借助 Obsidian 的 Remotely-Save 或 Self-hosted LiveSync插件同步，支持多种api方法保存消息到 Obsidian 库。","author":"曲淡歌","modified":20250212225527,"dg-publish":true,"created":"2025-03-08T11:35","updated":"2025-04-15T22:24","dg-path":"Obsidian/Obcsapi-赋予Obsidian在线api能力-拓宽OB的能力边界.md","permalink":"/Obsidian/Obcsapi-赋予Obsidian在线api能力-拓宽OB的能力边界/","dgPassFrontmatter":true,"noteIcon":""}
---


# 前言

为什么很多人会纠结用 notion 还是 obsidian？因为 notion 具有强大的在线功能，一旦使用场景超越了单设备，obsidian 用户就不得不面临诸如“同步”、“发布”和“跨设备”的问题。

我使用 obsidian 三年有余，尝试了几乎所有同步方式，最终得出结论：目前现成的解决方法不可能得到完美体验（指对标原生在线的笔记应用，如 notion）。

因此首先需要厘清自己的需求，再因地制宜去改造 obsidian，这也是 obsidian 最大的优点：客制化潜力巨大（来源于它使用 md 格式文件和它繁荣的插件社区）。

比如我的工作流包括以下场景：

1. 在 pc 上使用 obsidian 客户端写笔记
2. 在手机上看 b 站视频、浏览器网页的时候想要分享我看的东西
3. 在手机上记录 memos
4. 在手机上查看我的 obsidian 笔记库并编辑

其中最麻烦的事是如何在手机上得到良好体验，obsidian 虽然有官方的 app，但是体验不佳。而且在手机端进行复杂编辑还想要好体验本身就是一个伪命题（除非外接显示器和键盘），因此我选择使用网页（当然这里做出了妥协，即放弃了 ob 各种强大的功能，网页上只做简单的文字编辑），这样直接解决了跨平台的问题。

通过上面的分析后，拆解我的工作流来分析需求，可以得到三个版块

1. 同步
2. 信息输入
3. web 发布

而 [obcsapi](https://github.com/kkbt0/obcsapi-go) 几乎完美的符合了我的需求，下面我将正式开始介绍 obcsapi 这个开源项目。

obcsapi 是由中国 obsidian 用户 [恐咖兵糖](https://github.com/kkbt0) 开发的一款 obsidian 工具，其官方介绍如下：

> 基于 Obsidian S3 存储， CouchDb ，本地存储和 WebDAV 的后端 API ,可借助 Obsidian 插件 Remotely-Save 插件，或者 Self-hosted LiveSync (ex:Obsidian-livesync) 插件 CouchDb 方式，保存消息到 Obsidian 库。或者支持本地文件夹的文本编辑器。特点
>
> - 前端添加 Memos / 简答编辑 ， 支持指令模式，有黑暗主题 ，是 PWA 应用
> - 微信测试号 微信到 Obsidian
> - 支持简悦 SimpRead Webook 裁剪网页文章
> - 支持 fv 悬浮球文字图片分享保存
> - 静读天下 MoonReader 高亮标注 仿 ReadWise API
> - 通用 http api
> - 使用 Lua & Bash 拓展功能。用户可以处理任何请求
> - WebDAV 服务
> - 一个简易图床，附带命令行上传工具。
> - 云函数 或者 Dokcer 部署

可以看到 obcsapi 的使用前提是需要自己部署，我个人是采用自租 vps 部署，当然也可以使用云函数 + 对象存储，Nas+ 内网穿透等方法。

它可以做到包括但不限于如下功能：

- 部署一个 web 页面，可以访问、搜索并修改 obsidian 整个库
	- web 页面类 memos，可以快速记录灵感想法 ![图片](https://github.com/kkbt0/obcsapi-go/raw/master/obcsapi-docs/docs/images/Snipaste_2023-05-09_21-21-34.png)
- 支持 api 输入，可以使用任何支持 http quest 的工具集成，如 fv 悬浮球/静读天下/简悦/ios 的捷径/tasker/Windows Quicker 等
- 支持微信公众号测试号、企业微信，可以从微信端传入信息
- 自带 webdav 服务，可以把 obsidian 库作为 webdav 的目录，这样就能与 remotely-save 等插件集成，进行同步
- 支持 couchDB，可与 livesync 插件联动
- 自带图床，web 上传图片自动存到图床并插入笔记
- 支持分钟级待办提醒（微信推送、邮件提醒），邮件提醒可以自动识别最近三天日记中的所有待办并且每天早上发送邮件提醒，即每日提醒功能

还有更多功能见文档 [Obcsapi使用说明](https://www.ftls.xyz/docs/obcsapi/)

最后实际的使用效果见我的 b 站视频：[Obcsapi：如何让obsidian和notion打擂台？【元知识】_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1iT421k7aq/)

## 功能展示

### 同步功能

#### remotely-save 联动

#### livesync 联动

### api与各种软件联动

### 邮件提醒

### web 页面，随时随地使用 Obsidian

### 企业微信

![assets/img-20250212223540293.png|assets/Pasted image 20241219204451.png](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/img-20250212223540293.png)

# 现有 Bug 记录

## 101 被识别为 707

obcsapi 设置选项中的 `Obsidian Daily 设置`，如果把文件夹名称设置为 `101 日记`，最后的实际效果是 `707 日记`，这个 bug 很奇怪

## 微信待办提醒文档有误

[4. 功能使用 | Obcsapi](https://www.ftls.xyz/docs/obcsapi/md/go-version/4-%E5%8A%9F%E8%83%BD%E4%BD%BF%E7%94%A8.html)

> [登录微信测试号](https://mp.weixin.qq.com/debug/cgi-bin/sandboxinfo?action=showinfo&t=sandbox/index),模板消息接口新增测试模板，标题随意。内容处包含 `\{\{content.DATA\}\}` 即可。如
>
> plain
>
> ```
> 待办任务： \{\{content.DATA\}\}
> ```
>
> 创建完成后，模板 ID 复制到配置文件，作为 `wechat_template_id` 的值。

测试日期 2024 年 07 月 16 日，微信测试号的内容变量要求为 `待办任务：{{content.DATA}}`，如果加入斜杠会导致模板失效。

这一点在配置文件中是正确的，但是项目文档还没改

## 微信语音转文字失效

[4. 功能使用 | Obcsapi](https://www.ftls.xyz/docs/obcsapi/md/go-version/4-%E5%8A%9F%E8%83%BD%E4%BD%BF%E7%94%A8.html)

> #### 微信公众号说明
> - 支持消息类型: 文字，图片，链接 (收藏中的)，地图位置，语音消息 (直接调用微信转文字存储)

实测语音转文字功能失效，昨天请教过作者，即便打开测试号的 `接收语音识别结果` 功能再重启也无法启效。

- [x] 换一个测试号测试 ✅ 2024-07-16
我换了一个测试号，换了一个微信号测试依然无法识别

## 通过 api 发送的图片无法在 web 中显示

web 直接上传图片，图片会上传到图床

通过 api 发送会放到 ob 库中，以 `!()[]` 格式引用，在 ob 中正常显示，但在 web 中无法显示

## 文档中关于企业微信配置有误

配置文件中有这样一段：

```
# work wechat 企业微信自建应用
work_wechat_receiverid: xxxxxxxxxxxxxx # 企业ID
work_wechat_corpid: xxxxxxxxxxxxxx #企业ID
```

可以看到第一个 `receiverid` 的备注也是企业 id，这明显是错误的，实际上这一行不应该被配置，而是要被注释留空，原因是见此文：[个人开发者的receiveid填什么？ - 开发者社区 - 企业微信开发者中心](https://developer.work.weixin.qq.com/community/question/detail?content_id=16321548993000405078)，即

> 个人主体的第三方应用的 ReceiveId 是一个空字符串
>
> https://developer.work.weixin.qq.com/document/path/91144#%E9%99%84%E6%B3%A8%EF%BC%9Areceiveid-%E5%90%AB%E4%B9%89

同时文档中也没有给出回调 api 的地址，而它应该这么填写

![assets/img-20250212223540415.png|assets/Pasted image 20241219201940.png](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/img-20250212223540415.png)

即 `obcsapi地址/api/workwechat`

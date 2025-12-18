---
{"uid":20250117163348,"title":"在移动端设备上管理Obsidian待办和备忘的方法探讨","tags":["Obsidian","android","ios","笔记软件"],"description":null,"author":"曲淡歌","draft":false,"editable":false,"modified":20250121185659,"dg-publish":true,"created":"2025-03-08T11:35","updated":"2025-10-07T18:04","dg-path":"Obsidian/在移动端设备上管理Obsidian待办和备忘的方法探讨.md","permalink":"/Obsidian/在移动端设备上管理Obsidian待办和备忘的方法探讨/","dgPassFrontmatter":true,"noteIcon":""}
---


# 前言

虽然我不提倡 all in one，但是我一直希望能使用 Obsidian 管理我的待办。虽然可以用 tasks、reminder 之类的插件来实现 Obsidian 内部的待办管理，但是对于普通人来说，手机才是真正有提醒功能的终端，而移动端 Obsidian 不能调用系统级的通知，即便它能，也会受到启动缓慢且无法常驻后台的短板的制约，因此我们需要更轻量而稳定的实现方法。

好在 Obsidian 是基于 md 开放格式的软件，我们完全可以用其他软件来读取笔记，然后按照对应规则来解析笔记的待办。除了自行实现外，我也发现了一些应用在努力完成这样的目标。后文会介绍现有的第三方应用与自行实现的方法，宥于个人能力与精力的有限，难以做到全面准确，如有错漏，欢迎批评指正。

# 省流

- 三星手机用户推荐用obsidian mstodo sync
- 全平台用户可以用tickticksync+滴答清单
- Google生态用户且愿意折腾可以用tasknotes
- 不想同步信息给大厂的用taskforge（会员买断30美元）

# 第三方应用解析ob笔记


## QuickCapture-forObsidian

支持平台：ios，android

## Supasend

支持平台：ios

## Quick Draft

支持平台：ios


## TaskForge

支持平台：ios，Android

功能介绍：
- 识别笔记中的任务，并且可以调用系统提醒
- 支持tasks与tasknote语法

## Obsidian小部件

支持平台：ios

## Sriptable

支持平台：ios

这是一个支持自定义脚本的小部件工具，可以去Reddit上找关于ob的脚本，就能把笔记解析出来
## MarkdownWidget

支持平台：ios

自定义脚本的小部件工具
## Capsidian

支持平台：android

下载地址：[Google play商店](https://play.google.com/store/apps/details?id=com.devindie.keepsidian&pli=1)

功能介绍：
- 读写笔记中的任务
- 写日记
- 使用语音写日记
	- 使用离线模型转录并写入日记，还能保存时间轴（但是只支持英文和某外语）
	- 同一天记两次，会生成两个日记
- 支持拍照OCR（离线），但是也不支持中文
- 不知道为什么，一天输入两次笔记都会创建两个文件

## notifian

支持平台：android

下载地址：[Google play 商店](https://play.google.com/store/apps/details?id=com.notifian&hl=en)

功能介绍：扫描本地的 Obsidian 库，提取其中的待办提醒，然后在对应时间点发起提醒。

[fold]

-  ![../../../../105-极客/写作工具/Obsidian/assets/Pasted image 20250117193514.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/Pasted%20image%2020250117193514.png)

细节：

- 支持两种待办格式
	- frontmatter
		- `remind at` 为提醒时间，支持精确到分钟
		- `repeat` 为重复规则，支持
			- 每月的第 x 天
			- 每 x 分钟/小时/天/周
	- 兼容 tasks 语法（因此只支持到按天提醒，不能精确到小时分钟）

## obsi

支持平台 ：android

下载地址：[Google play商店](https://play.google.com/store/apps/details?id=com.scanworks.obsi&hl=en)

功能介绍：扫描本地的 Obsidian 库，提取其中的待办提醒，将其渲染为可视化 todo，同时可以用图形 UI 创建新的待办，支持设置截止日期、属性和种类。

![../../../../105-极客/写作工具/Obsidian/assets/Pasted image 20250117193049.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/Pasted%20image%2020250117193049.png)

细节：

- 通过 `obsi` app 创建的待办都会被放到 `obsi.md` 文件中，目前无法分散保存待办
- 目前无法发出提醒，只能由用户自行查看

## ObsidianAndroidWidget

支持平台：android

下载地址：[GitHub仓库](https://github.com/Irony95/ObsidianAndroidWidget)

功能介绍：

细节：

- 只能手动选定链接的文件，无法按照一定的规则自动切换文件（比如根据当天日期切换当天的日记）

## QuickMDCapture

[通过 Android 主屏幕上的小部件添加注释：r/ObsidianMD --- Adding notes through a widget on the Android home screen : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1flev91/adding_notes_through_a_widget_on_the_android_home/)

## Kvaesitso

支持平台：android

下载地址：[GitHub仓库](https://github.com/MM2-0/Kvaesitso)

功能介绍：这是一个开源的安卓桌面 app，它有一个自带的小组件，可以链接到一个 md 文件，然后就可以在桌面编辑这个 md 文件


![../../../../105-极客/写作工具/Obsidian/assets/Screenshot_20250117_234412_Kvaesitso.jpg](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/Screenshot_20250117_234412_Kvaesitso.jpg)

细节：

- 只能手动选定链接的文件，而且这个文件必须由这 app 新建（当然可以手动替换）

# 将ob待办同步到待办app

## obsidian mstodo sync

支持在ob内一键同步待办到微软todo中 ![PixPin_2025-11-30_10-43-52-1764470655555.webp](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/PixPin_2025-11-30_10-43-52-1764470655555.webp)


优点：微软todo大厂软件，跑路可能性低，国内网络能正常同步，免费。如果用的是三星手机，可以与系统待办集成。

缺点：ob-->微软todo单向同步，且无法自动同步，需手动触发

分析：适合只需要手动挑选重要待办在移动端获取提醒的用户，三星用户额外加分

注：插件未上架，仓库地址：[LumosLovegood/obsidian-mstodo-sync: microsoft-todo for obsidian.md](https://github.com/LumosLovegood/obsidian-mstodo-sync "LumosLovegood/obsidian-mstodo-sync: microsoft-todo for obsidian.md")


## tickticksync

实现ob与滴答清单的双向同步

## tasknotes

实现ob与Google日历/task的双向同步

缺点：配置繁琐，要走google的开发者控制台


# 自行实现

## 使用 tasker

### 网友分享的思路

- [来自 Android 的快速添加注释：r/ObsidianMD --- Quick add note from Android : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/qj7nct/quick_add_note_from_android/)
- [Guy-92/QuickNote: A way to take Quick Notes in Obsidian on Android](https://github.com/Guy-92/QuickNote)
	- 另一个网友以此为基础进行了修改
- [使用 Tasker 为 Android 创建“即时笔记”小部件：r/ObsidianMD --- Using Tasker To Create An "Instant Note" Widget For Android : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1h9tgqh/using_tasker_to_create_an_instant_note_widget_for/)
- 一个网友分享的 tasker 创建的思路，但是没有分享具体文件 [使用 Tasker 为 Android 创建“即时笔记”小部件：r/ObsidianMD --- Using Tasker To Create An "Instant Note" Widget For Android : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1h9tgqh/using_tasker_to_create_an_instant_note_widget_for/)

## obcsapi

obcsapi可以扫描库里的待办，然后用微信/邮件来发送提醒

![PixPin_2025-11-30_11-20-20-1764472827938.webp](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/PixPin_2025-11-30_11-20-20-1764472827938.webp)

### 我的 tasker widget

## 使用 ios 捷径

[iOS 快捷方式 ： r/ObsidianMD --- iOS Shortcut : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1i4zpom/ios_shortcut/)

## fv 悬浮球记笔记（偏题）

[安卓利用FV悬浮球实现不打开ob进行文本快捷输入（包括图片自动上传图床后的外链） - 经验分享 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/5687/2)

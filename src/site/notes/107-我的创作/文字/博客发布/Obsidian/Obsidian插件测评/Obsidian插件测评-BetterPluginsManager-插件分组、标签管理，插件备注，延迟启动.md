---
{"uid":20250109102534,"title":"Obsidian插件测评——BetterPluginsManager：插件分组、标签管理，插件备注，延迟启动","tags":["obsidian插件"],"description":null,"author":"曲淡歌","draft":false,"editable":false,"modified":20250109112404,"dg-publish":true,"created":"2025-03-08T11:35","updated":"2025-04-15T22:24","dg-path":"Obsidian/Obsidian插件测评/Obsidian插件测评-BetterPluginsManager-插件分组、标签管理，插件备注，延迟启动.md","permalink":"/Obsidian/Obsidian插件测评/Obsidian插件测评-BetterPluginsManager-插件分组、标签管理，插件备注，延迟启动/","dgPassFrontmatter":true,"noteIcon":""}
---


# 插件简介

Better Plugins Manager (BPM)是一款 Obsidian 插件管理工具，功能包括：插件分组、标签管理、备注和延迟启动，提升插件管理效率和用户体验。

## 使用示例

### 插件分组&延迟启动

![assets/Pasted image 20250109111415.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/Pasted%20image%2020250109111415.png)

### 标签管理

![assets/Pasted image 20250109111841.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/Pasted%20image%2020250109111841.png)

### 插件备注

![assets/Pasted image 20250109112029.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/Pasted%20image%2020250109112029.png)

## 项目情况

是否上架官方市场：✅️

[项目地址链接](https://github.com/0011000000110010/obsidian-manager)

# 使用教程

在OB插件市场中搜索安装，然后点击OB左侧的 ![assets/Pasted image 20250109113033.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/Pasted%20image%2020250109113033.png) 图标即可启动管理页面。

在管理页面里可以完成以下工作：
- 设置分组
- 分配标签
- 自定义插件名称与描述
- 设置插件的启动延迟时间
- 筛选插件：支持按分组、标签、名称筛选

管理页面各部件使用说明请参照下图：

![assets/betterpluginmanager图解.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/betterpluginmanager%E5%9B%BE%E8%A7%A3.png)

因为插件的操作逻辑很简单，没必要再把图中的说明复述一遍，不过我要强调几个重点：
1. 首次使用此插件时，建议复制当前库，以便在副本中测试插件功能，确保无误后再在主力库中启用（或者说首次使用任何插件时，都推荐这样做）
2. 使用本插件管理 Obsidian 插件后，请避免使用 Obsidian 自带的插件管理器开关插件，以免引发未知错误
3. 一键开关功能仅针对当前视图中的插件生效。通过分组或标签筛选，可以批量开关特定插件（也就是说如果你没有开启任何筛选功能的话，一键开关插件就是把你的OB中的所有插件一键开关，**目前0.0.4版本的插件描述有误，请以本文为准**）。

如果需要调整分组、标签和延迟，则需要前往BPM的设置页面中添加。（可选）点击取色工具来自定义元素的颜色，然后输入id（推荐使用纯英文）和名称，点击加号即可添加。

- 添加分组：
![assets/Pasted image 20250109132739.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/Pasted%20image%2020250109132739.png)

- 添加标签：
![assets/Pasted image 20250109132811.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/Pasted%20image%2020250109132811.png)

- 添加延迟：
![assets/Pasted image 20250109132831.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/Obsidian/assets/Pasted%20image%2020250109132831.png)

# 闲谈

有一段时间我一直想优化我的Obsidian启动速度，一个常用的方案就是让一部分插件在Obsidian启动后再启动。于是我尝试了很多方案，一开始我使用templater脚本来实现插件延迟启动，但是这种方案依赖于代码，不方便随时修改，然后我使用了 [PluginGroups](https://github.com/Mocca101/obsidian-plugin-groups) 和 [LazyPlugins](https://github.com/alangrainger/obsidian-lazy-plugins)，前者已经停更两年，并且分组操作窗口小而不直观，后者专注于插件的延迟启动，但在我使用的时候有奇怪的bug。

直到我朋友02开发了这款插件，几乎能满足我的所有需求。直观的插件分类管理，可视化的操作，多组别延迟启动。因此我想把它推荐给你们。
---
{"dg-publish":true,"dg-permalink":"I-modded-Anchor-Link-Display-Text","title":"解决“Obsidian wiki链接采用相对路径模式时会显示冗长的相对路径”的问题","created":"2025-12-18T11:51","updated":"2025-12-18T11:51","dg-path":"Obsidian/解决“Obsidian wiki链接采用相对路径模式时会显示冗长的相对路径”的问题.md","permalink":"/I-modded-Anchor-Link-Display-Text/","dgPassFrontmatter":true,"noteIcon":""}
---


我修改了 [[003-功能页面/BPM/Anchor Link Display Text\|Anchor Link Display Text]] 来解决这个问题。已经给原作者提 PR 了，在他合并我的 PR 之前，可以去我 fork 的仓库下载：[Release 1.3.1 · dangehub/anchor-link-display-text](https://github.com/dangehub/anchor-link-display-text/releases/tag/1.3.1)

需要在插件设置中打开 `Auto alias note links` 选项。

效果展示：
![image-1766030740267.webp](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/image-1766030740267.webp)

这样就能让带有一长串相对路径的链接仅显示笔记名称本身。

这样既能保证使用相对路径这种最强兼容性能的书写格式，又不会在书写时增加摩擦力。
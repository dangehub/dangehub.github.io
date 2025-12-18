---
{"dg-publish":true,"dg-permalink":"I-modded-Anchor-Link-Display-Text","title":"正文","created":"2025-12-18T11:51","updated":"2025-12-18T11:51","dg-path":"Obsidian/解决“Obsidian wiki链接采用相对路径模式时会显示冗长的相对路径”的问题.md","permalink":"/I-modded-Anchor-Link-Display-Text/","dgPassFrontmatter":true,"noteIcon":""}
---


# 正文

我修改了 [[003-功能页面/BPM/Anchor Link Display Text\|Anchor Link Display Text]] 来解决这个问题。已经给原作者提 PR 了，在他合并我的 PR 之前，可以去我 fork 的仓库下载：[Release 1.3.1 · dangehub/anchor-link-display-text](https://github.com/dangehub/anchor-link-display-text/releases/tag/1.3.1)

需要在插件设置中打开 `Auto alias note links` 选项。

效果展示：

![image-1766030740267.webp](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/image-1766030740267.webp)

这样就能让带有一长串相对路径的链接仅显示笔记名称本身。

这样既能保证使用相对路径这种最强兼容性能的书写格式，又不会在书写时增加摩擦力。

# 吐槽

在搜索“相对链接太长”这个话题时，发现 2020 年就有人反馈过这个问题，而官方在 2023 年给出的答复是“会在 1.2”版本中解决这个问题，而快三年过去了，Obsidian 都更新到 1.11 了，这个问题依然存在。

而我现在的实现方式也是不够完美的，如果链接的对象被修改了，Obsidian 会自动更新链接，但是 `display text` 不会被自动更新。

所以可能目前最好的方式还是使用 `尽可能简短的形式`，并且在未来有需求的时候，使用脚本/插件转换之。
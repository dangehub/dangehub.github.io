---
{"dg-publish":true,"dg-permalink":"I-modded-Anchor-Link-Display-Text","title":"解决“Obsidian wiki链接采用相对路径模式时会显示冗长的相对路径”的问题","created":"2025-12-18T11:51","updated":"2025-12-18T11:51","dg-path":"Obsidian/解决“Obsidian wiki链接采用相对路径模式时会显示冗长的相对路径”的问题.md","permalink":"/I-modded-Anchor-Link-Display-Text/","dgPassFrontmatter":true,"noteIcon":""}
---


我修改了 [[003-功能页面/BPM/Anchor Link Display Text\|Anchor Link Display Text]] 来解决这个问题。

在插件设置中打开 "Auto alias note links" 就可以将

`[[../../../003-功能页面/BPM/VCF Contacts]]`

自动补全成

`[[../../../003-功能页面/BPM/VCF Contacts|VCF Contacts]]`

最终显示的效果就是

`[[VCF Contacts]]`

这样既能保证使用相对路径这种最强兼容性能的书写格式，又不会在书写时增加摩擦力。
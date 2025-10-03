---
{"uid":20250207201714,"title":"Thino与Mac软件popclip联动，实现系统级全局划词摘录","tags":["obsidian","obsidian插件"],"description":null,"author":"曲淡歌","modified":20250207202127,"dg-publish":true,"关联笔记":["[[../../../../105-极客/写作工具/我的工作流之如何快速记录灵感Memos|我的工作流之如何快速记录灵感Memos]]","[[memos]]","[[obcsapi]]"],"created":"2025-04-17T18:43","updated":"2025-04-17T18:43","dg-path":"Obsidian/Thino与Mac软件popclip联动-实现系统级全局划词摘录.md","permalink":"/Obsidian/Thino与Mac软件popclip联动-实现系统级全局划词摘录/","dgPassFrontmatter":true,"noteIcon":""}
---


简单介绍一下 popclip：

>  PopClip 是一款 macOS 效率工具，选中文本后弹出快捷工具栏，支持复制、粘贴、搜索等操作，并可通过扩展插件实现翻译、格式化、笔记保存等功能。

popclip 有一个插件可以把选中的文本发送到 Obsidian 中，如果是在浏览器中选中文本，还可以用 md 格式把标题与链接插入到笔记中，很适合摘录。

![assets/Clipboard-20250207-121434-348.gif](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/Clipboard-20250207-121434-348.gif)

但是原有插件不支持插入当前时间戳，也就是 thino 需要的那个 `- 18:34 ` 前缀，因此我修改了插件，并且提交了 PR，现在可以在插件市场下载

使用方法：

1.在 Obsidian 中安装 `advanced url` 插件，启用后无需任何设置

2.在 popclip 中安装 [黑曜石 - popclip扩展 --- Obsidian — PopClip Extensions](https://www.popclip.app/extensions/x/wfhk0x) 插件

3.在 popclip 中设置库名称

4.勾选 `include timestamp`

![assets/Pasted image 20250207201859.png](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/Pasted%20image%2020250207201859.png)

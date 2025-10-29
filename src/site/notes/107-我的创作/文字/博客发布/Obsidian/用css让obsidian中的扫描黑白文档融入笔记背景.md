---
{"title":"用css让obsidian中的扫描黑白文档融入笔记背景","date":"2025-01-06","lastmod":"2025-01-06","creation date":"2025-01-06 21:14","modification date":"星期一 2025 一月6日 21:18:28","categories":null,"tags":["CSS","obsidian","美化"],"alases":null,"dg-publish":true,"cssclasses":["has-scan"],"created":"2025-04-17T18:43","updated":"2025-04-18T02:00","dg-path":"Obsidian/用css让obsidian中的扫描黑白文档融入笔记背景.md","permalink":"/Obsidian/用css让obsidian中的扫描黑白文档融入笔记背景/","dgPassFrontmatter":true,"noteIcon":""}
---



从[• Discord | "Diff geom notes :D" | Obsidian Members Group (OMG)](https://discord.com/channels/686053708261228577/1283153363864911982/1283153363864911982)学习到的小技巧

新建一个css文件：
```
.has-scan img {
    mix-blend-mode : multiply
}
```

然后在笔记属性中添加：
```
---
cssclasses: has-scan
---
```

然后就可以在笔记的`阅读视图`下看到会跟随obsidian主题背景变化的图片了。

据作者说如果需要在`实时视图`中生效（但是在我这里没有生效， 原因未知），可以把css改为：
```
.has-scan .internal-embed.media-embed.image-embed.is-loaded {
    background: var(--background-primary);
}
```

下面是效果展示：

| 未启用效果                                       | 启用后效果                                       |
| ------------------------------------------- | ------------------------------------------- |
| ![assets/Pasted image 20250106211727.png](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/Pasted%20image%2020250106211727.png) | ![assets/Pasted image 20250106211742.png](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/Pasted%20image%2020250106211742.png) |
|                                             |                                             |



这种方式特别适合扫描产生的黑白线稿图片。
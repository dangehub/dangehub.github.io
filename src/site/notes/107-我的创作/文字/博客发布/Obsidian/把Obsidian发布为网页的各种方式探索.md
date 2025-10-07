---
{"title":"把Obsidian发布为网页的各种方式探索","date":"2024-08-26","lastmod":"2024-12-16","creation date":"2024-08-26 13:24","modification date":"星期一 2024 十二月16日 13:21:55","tags":["网站建设","Obsidian","Obsidian插件","自建博客"],"categories":null,"alases":null,"dg-publish":true,"created":"2025-04-17T18:43","updated":"2025-10-05T21:18","dg-path":"Obsidian/把Obsidian发布为网页的各种方式探索.md","permalink":"/Obsidian/把Obsidian发布为网页的各种方式探索/","dgPassFrontmatter":true,"noteIcon":""}
---


# Obsidian发布方式汇总


| 方式汇总           | 优点          | 缺点                                |
| -------------- | ----------- | --------------------------------- |
| 官方publish      | 官方支持，稳定     | 要花钱，数据非私有                         |
| digital garden | 更新稳定，支持功能多  | 静态页面，无法即时渲染                       |
| Quartz框架       | 开发文档全面，可以自行 | 静态页面，无法即时渲染                       |
| perlite        | 实时渲染，无需等待   | 不支持dataview excalidraw等插件功能，需要服务器 |

对于不想折腾的用户来说，只有一种方案：花钱买官方的publish。本文不再讨论这种方法。

其实目前主流的Obsidian发布方案就是两种：
- 通过后端支持实现实时渲染，只需要把ob的md源码上传就能马上看到最终效果
- 通过渲染器把md源码编译成一个静态网页，然后把静态网页文件托管到某个平台，好处是网页加载快，缺点是每次增删改笔记都要重新编译，往往需要等待数分钟才能看到新的结果。

因此如果发布前能保证已经完成了最终稿，那么静态发布是很好的选择。但是如果发布后还需要频繁修改，最好采用可即时编辑的工具。

# 静态页面类

如果你想要找一个能免费且私有数据的发布obsidian笔记的方案，这可能是最好也是唯一的选择。

可以简单的把静态页面的发布方式理解为即食食品，只需要拿到这个“静态页面”就可以开袋即食，与之相对的，非静态页面的方法，需要服务器进行渲染操作，因此一般是很难找到支持非静态页面的、大公司提供的、免费的方案。

其实静态页面发布博客的方法浩如星海，较为出名如Jekyll、Hugo、Hexo、Vuepress、Docsdify都是很成熟且有较多主题可以选择的，不过考虑到我们要发布obsidian笔记，当然需要支持obsidian的wiki链接功能，因此之后不再考虑这些没有针对obsidian优化的框架。

## Digital Garden插件

项目地址：此插件已上架官方市场。

优点：
- 更新勤快，后续有支持
- 功能多样
	- 支持导入ob主题
	- 支持excalidraw
	- 支持dataview

缺点：
- 依赖vercel（其实是可以使用github action的，不过需要一定动手能力）
- 发布文章需要填写frontmatter，体验不够丝滑（可以使用模板来优化流程）

## Quartz框架

项目地址：[jackyzha0/quartz: 🌱 a fast, batteries-included static-site generator that transforms Markdown content into fully functional websites](https://github.com/jackyzha0/quartz)

优点：
- 原生美观程度是比digital garden高
- 原生支持i18n，如果你需要发布多言语版本的文章，这点很重要

缺点：
- 不支持excalidraw
- 不支持dataview

## Obcsapi+对象存储

项目地址：[kkbt0/obcsapi-go: 基于 WebDAV，S3 存储或 CouchDb 的后端 API ，Obsidian 笔记的 API](https://github.com/kkbt0/obcsapi-go)

此方案来自和[和恐咖兵糖的聊天](https://www.ftls.xyz/posts/2024-12-09-hugo-obsidian-wenku/?atk_comment=155&atk_notify_key=GCFXN#:~:text=%E9%9D%99%E6%80%81%E5%8D%9A%E5%AE%A2%E7%A1%AE%E5%AE%9E,%E5%8F%AF%E8%83%BD%E8%BF%9B%E8%A1%8C%E4%BC%98%E5%8C%96%E3%80%82)

obcsapi在对象存储模式下可以把渲染好的页面放在对象存储中，obsidian 额外生成一个索引并同步

# 实时渲染类

## Perlite

项目地址：[secure-77/Perlite: A web-based markdown viewer optimized for Obsidian](https://github.com/secure-77/Perlite)

优势：
- 实时，无需渲染
- 可以直接把整个库复制进去，保留原库文件树

缺点：
- 支持的功能较少
	- html标签不支持
	- canvas不支持
	- task语法不支持
	- todo语法不支持
- 上次更新是7个月之前，疑似停更，支持力度更小

## Obcsapi-publish功能

obcsapi自带一个简易的publish页面，可以把指定目录的下笔记暴露在公开网络上。不过这个功能我并没有成功启动，暂时先记在这里。

据说能配合lua脚本。

## Obsiflask


<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



- 13:54 #Obsidian插件  一个把Obsidian发布到网上的新工具，类似obcsapi ， [bahleg/OBSIFLASK: Simple web service for Obsidian vaults](https://github.com/bahleg/OBSIFLASK)，目前主打功能是编辑、搜索、支持excalidraw 

</div></div>




# 采用第三方服务

如果能接受把上述两种方案的幕后工作交与第三方进行，我们也可以使用一些方案，但是请注意，你使用其他人提供的免费服务，可能面临对方突然停止服务或数据丢失（如果发布后本地不再留档）的风险，因此我只建议将这些方式作为临时发布方案。


已上架官方市场的插件：
- Share Note
- Obsius Publish
- Friday
- ……

如果你想探索那些没有上架官方市场的插件，可以在github搜索obsidian，然后去topics里面查看，印象中前5页就有好几个发布用的项目。

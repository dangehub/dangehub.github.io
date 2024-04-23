---
share: true 
title: wordpress导入rss以同步全平台
git_title: 2024-04-23-wordpress导入rss以同步全平台
tags: 
- geek
- wordpress 
- 网站
categories:
- geek
---

使用`Feedzy`插件，注意两点：
1. rss链接最后跟上`/?feed_author=1`，最后的数字是`wordpress user ID`，这样可以指定这个rss的作者是谁，1就是我的admin账号。如果不加的话，所有rss搬运过来会变成空用户，还得手动修改作者。
2. 发布时间选择`item_date`，这样rss的搬运内容会和原平台的发布时间同步，比如2024-04-23在wp搬运了一条2024-02-02的，就会变成在wp的2-2发布，而不是4-23，这样可以防止时间乱序。
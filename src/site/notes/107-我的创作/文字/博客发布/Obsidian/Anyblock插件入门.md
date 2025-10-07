---
{"title":"Anyblock插件入门","date":"2024-10-03","lastmod":"2024-10-03","creation date":"2024-10-03 19:33","modification date":"星期四 2024 十月3日 19:42:36","tags":["obsidian插件"],"categories":null,"alases":null,"dg-publish":true,"created":"2025-03-08T11:35","updated":"2025-04-15T22:25","dg-path":"Obsidian/Anyblock插件入门.md","permalink":"/Obsidian/Anyblock插件入门/","dgPassFrontmatter":true,"noteIcon":""}
---



# 插件简介

Anyblock是一个【无语法、可扩展、灵活强大、多平台】 的 Markdown 块扩展渲染插件。能实现无语法入侵的前提下，为obsidian实现更多渲染效果，例如表格、折叠、滚动、思维导图等。

# 官方文档

作者的博客： [README | Linc 的小站](https://linczero.github.io/MdNote_Public/ProductDoc/AnyBlock/README.show.html)

作者自荐的帖子：[列表转表格、树目录、思维导图、时间线、表格合并 —— Any Block V3（Ob/Md-it/VuePress/VitePress通用） - 经验分享 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/38352)

插件的开源地址：[LincZero/obsidian-any-block.](https://github.com/LincZero/obsidian-any-block)


# 使用说明

使用info语法召唤说明文档，如果你想看到渲染后的效果，应该在安装插件后，输入下面这段文字：

```
[info]
- 这是any block的文档
```

然后应该会渲染出下面的效果：

![assets/Pasted image 20241003193747.png](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/Pasted%20image%2020241003193747.png)



## 各效果器展示

我只会在这里展示我常用的效果，更多内容参见插件自身的文档。

### 文件树

#### 技巧 ：
1. 分隔左右侧的逗号是中文逗号
2. 逗号后有一个空格

#### 源代码 ：

```
[list2dt]

- vue-demo/
  - build/， 项目构建(webpack)相关代码
  - config/， 配置目录，包括端口号等。我们初学可以使用默认的
  - node_modules/， npm 加载的项目依赖模块
  - src/， 这里是我们要开发的目录
    - assets/， 放置一些图片，如logo等
    - components， 目录里面放了一个组件文件，可以不用
    - App.vue， 项目入口文件，我们也可以直接将组件写这里，而不使用 components 目录
    - main.js， 项目的核心文件。
  - static/， 静态资源目录，如图片、字体等
  - test/， 初始测试目录，可删除
  - .eslintignore
  - .gitignore， git配置
  - .index.html， 首页入口文件，你可以添加一些 meta 信息或统计代码啥的
  - package.json， 项目配置文件
  - READED.md， 项目的说明文档，markdown 格式<br>手动换行测试<br>自动换行测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试k
  - ...
```

#### 效果展示 ：
![assets/Pasted image 20241003193848.png](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/Pasted%20image%2020241003193848.png)



### 超出折叠

#### 技巧 ：使用(300)这样的参数控制显示范围

#### 源代码：

```
[overfold(300)]
- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
```

#### 效果展示：![assets/Pasted image 20241003193954.png](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/Pasted%20image%2020241003193954.png)

### 滚动

#### 技巧：滚动也适用(300)这样的长度控制参数

#### 源代码：

```
[scroll(300)]

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
```


#### 效果展示：![assets/Pasted image 20241003194039.png](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/Pasted%20image%2020241003194039.png)

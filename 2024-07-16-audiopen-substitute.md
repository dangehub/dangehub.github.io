---
title: 语音笔记AudioPen的“平替”
git_title: 2024-07-16-audiopen-substitute
tags:
  - geek
  - 元知识
  - 笔记软件
  - 知识管理
  - 效率工具
categories:
  - geek
---


# 前言 

在b站发出AudioPen的视频后，有网友问有没有能自己部署的项目做平替，那今天就来分析一下如何找到AudioPen的平替。

# 现有项目 

AudioPen的工作原理其实并不复杂，语音转文字-->文字发给LLM，也就是说它并没有核心技术，只是现有技术的整合，因此如果去google以`audio notes`为关键词搜索，能找到好几个类似的软件，但是他们的定价策略甚至还比不过AudioPen，因此不考虑这类软件。

## 语音输入法+LLM

最简单的办法就是用语音输入法输入一段文字，然后发给任何一个大语言模型（比如ChatGPT），然后告诉它：“你现在是速录员，请把下面的口语整理为通顺的书面表达”，通过微调提示词，可以得到不同的效果。


## Alog：ios平台+需要网络

如果使用的苹果设备，可以去app store搜索`alog`，这是一个可以使用自己的LLM key的软件，同时还支持apple watch端，是一个我比较看好的软件，它采用ios内置的本地语音转文字功能，仅需要自己去解决第二步的问题，而互联网上有很多免费的key获取途径。

## OralPen：ios平台+需要网络

[Allwillcome/OralPen: 出口， AI 成章| Record voice and refine it into language ChatGPT understands.](https://github.com/Allwillcome/OralPen)

这是一个使用ios的快捷指令实现的脚本，也是通过ios内置的本地语音转文字，然后将转录稿发送给自定义的LLM，其实只要读懂了这个脚本，几乎就可以在任何一种设备上复刻AudioPen。


![[assets/Pasted image 20240716175420.png|assets/Pasted image 20240716175420.png]]

## whisper+llm本地离线：任何平台+无需网络

通过上面的两个例子，我们完全可以通过whisper本地模型来转录语音，再用LLM来处理文字，如果本地算力足够，可以通过如ollama等服务在本地部署自己的LLM并通过api来使用它。

# 小结 

看上去有很多方法，但殊途同归，他们都是采用的同样一套原理。但是AudioPen的效果出奇的好，可能作者在某些细节进行了处理，因此，如果想得到最好的效果，目前来看，我还是推荐付费使用产品。如果只是想尝鲜，完全可以用语音输入法那个方案，同时像ChatGPT本身就支持语音输入，也可以直接让它帮你总结。 







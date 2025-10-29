---
{"uid":20250203004253,"title":"ollama离线运行AI模型+反思翻译法+沉浸式翻译=免费又好用的翻译？最具性价比的选择！","tags":["LLM","ai","翻译","自托管","反思翻译法"],"description":null,"author":"曲淡歌","modified":20250205194018,"dg-publish":true,"created":"2025-04-17T18:43","updated":"2025-04-18T02:00","dg-path":"效率工具/ollama离线运行AI模型-反思翻译法-沉浸式翻译-免费又好用的翻译.md","permalink":"/效率工具/ollama离线运行AI模型-反思翻译法-沉浸式翻译-免费又好用的翻译/","dgPassFrontmatter":true,"noteIcon":""}
---


# 前言

## 设备需求与劝退

本文中我使用的设备是 `2020 M1 macbook pro 16g`

如果你想学习本文的操作，建议先检查自己的设备是否满足以下任一要求：

- mac 平台：M 系芯片的 mac，内存 16g 起步
- windows 平台：使用显存大于 8g 的显卡
- linux 平台：都用 linux 了，不用我教

## 起因

我们不能回避的一个现状是：大部分领域的英文语料都是相当有价值的，因此阅读英文依然是我们的必修课。但所幸我们已经有很多工具来减轻英语阅读的负担，以我个人为例，我最常用的两个工具是 `沉浸式翻译` 和 `bob` （macos 上的一个全局划词翻译软件）。

其中沉浸式翻译是我在 mac、win、ios、android 四端都在使用的插件。一般我会先用沉浸式翻译的机翻来粗读文章，遇见低质翻译或长难句等需要精读英文时会使用划词翻译 + [[107-我的创作/文字/博客发布/效率工具/用反思翻译法提升大语言模型翻译的质量\|反思翻译法]]。因为现在 LLM api 的价格、并发限制与延迟，我一般不会在全局使用 LLM 翻译。粗读时往往会在沉浸式翻译自带的、开箱即用的微软翻译与 google 翻译里来回切换（因为频繁翻译会被限制，需要二者切换使用）。

最近因为 deepseek 的开源，又开始折腾起本地部署 LLM，突然又萌生起使用本地 LLM 来做翻译的想法，测试了一下，发现 2b 的小模型做段落级翻译居然也相当不错，于是写下本文。

# 配置教程

1. 安装 ollama
2. （保证网络畅通）拉取模型 `ollama run gemma2:2b`
3. 在沉浸式翻译中增加一个 LLM 服务，接口为 `http://127.0.0.1:11434/v1/chat/completions` ，key 为 `ollama` ，模型为 `gemma2:2b`
4. enjoy it

# 效果展示

因为发现 2b 的模型其实翻译效果也还可以，比机翻要好一点。而使用在线 LLM api 既不稳定还贵。下面我们做一下对比。

![assets/img-20250208161613150.jpeg](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/%E6%95%88%E7%8E%87%E5%B7%A5%E5%85%B7/assets/img-20250208161613150.jpeg)

依次分别为微软翻译、google 翻译、gemma2:2b、deepseek-v3（在线 api）

为了未来对比效果，我也把原文放在这里

```
Is the UK about to ban running LLMs locally?

The UK government is targetting the use of AI to generate illegal imagery, which of course is a good thing, but the wording seems like any kind of AI tool run locally can be considered illegal, as it has the *potential* of generating questionable content. Here's a quote from the news:

"The Home Office says that, to better protect children, the UK will be the first country in the world to make it illegal to possess, create or distribute AI tools designed to create child sexual abuse material (CSAM), with a punishment of up to five years in prison." They also mention something about manuals that teach others how to use AI for these purposes.

It seems to me that any uncensored LLM run locally can be used to generate illegal content, whether the user wants to or not, and therefore could be prosecuted under this law. Or am I reading this incorrectly?

```

可以看到在线的 deepseek 确实爆杀了，但是 api 是要额外花钱的，还需要时间来反应。而在我的 mac 上跑 2b 的小模型，速度比在线 api 快一点，效果介于机翻和 api 之间。而机翻使用的太频繁也会触发限制，相比之下我用 ollama 跑一个 2b 的小模型，电脑也不卡，翻译速度也能接受，还不收费，岂不美哉？

（单个网页用本地 LLM 是可以的，但是如果快速翻页 or 多个网页，本地 LLM 的速度还是不够，需要更强的配置，另外可能还要再配置一下 ollama 的同时加载模型数与单模型的并发处理数）

因此我还是很推荐的这样做的。

最后放上更多翻译工具的结果：

DeepL 翻译：

> [!DeepL 翻译]
> 英国即将禁止在本地开办法律硕士课程？
>
> 英国政府正在打击利用人工智能生成非法图像的行为，这当然是件好事，但从措辞上看，似乎任何一种在本地运行的人工智能工具都可以被视为非法，因为它有*可能*生成有问题的内容。以下是新闻中的一段话：
>
> “内政部表示，为了更好地保护儿童，英国将成为世界上第一个规定拥有、创建或分发旨在创建儿童性虐待材料（CSAM）的人工智能工具为非法的国家，最高可判处五年监禁。” 他们还提到了一些关于教他人如何为这些目的使用人工智能的手册。
>
> 在我看来，无论用户是否愿意，在本地运行的任何未经审查的 LLM 都可以用来生成非法内容，因此可以根据该法律进行起诉。还是我理解错了？

使用反思翻译法 +deepseek-v3 得到的翻译：

> [!使用反思翻译法 +deepseek-v3 得到的翻译]
> 英国政府正在打击利用人工智能生成非法图像的行为，这当然是件好事，但措辞似乎暗示任何本地运行的 AI 工具都可能被视为非法，因为它们有*潜在*生成不良内容的可能。
>
> 以下是新闻中的一段引述：
>
> “内政部表示，为了更好地保护儿童，英国将成为世界上第一个将拥有、创建或分发旨在制作儿童性虐待材料（CSAM）的 AI 工具定为非法的国家，最高可判处五年监禁。”他们还提到了一些关于教别人如何使用 AI 进行这些目的的指南。
>
> 在我看来，任何未经审查的本地运行的大型语言模型都可以用来生成非法内容，无论用户是否有意为之，因此可能会根据这项法律被起诉。还是我理解错了？

在 n8n 中的 AI-agent 使用反思翻译法 +deepseek-v3 得到的翻译：

> [!在 n8n 中的 AI-agent 使用反思翻译法 +deepseek-v3 得到的翻译]
> 英国政府正在针对使用人工智能生成非法图像的行为进行打击，这当然是件好事，但措辞似乎暗示任何本地运行的 AI 工具都可能被视为非法，因为它们有生成可疑内容的*潜力*。以下是新闻中的一段引述：
>
> 内政部表示，为了更好地保护儿童，英国将成为世界上第一个将拥有、创建或分发旨在创建儿童性虐待材料（CSAM）的 AI 工具定为非法的国家，最高可判处五年监禁。他们还提到了一些关于教别人如何使用 AI 达到这些目的的手册。
>
> 在我看来，任何本地运行的未经审查的大型语言模型（LLM）都可能被用来生成非法内容，无论用户是否有意，因此可能会根据这项法律被起诉。或者我理解错了？

可以看到传统机器翻译的天花板 DeepL 的翻译结果也不尽人意，LLM 具备的上下文感知功能在翻译领域真的太强了。另外同样使用 deepseek-v3 ，不同的 prompt 也会产生不同的效果，因此 prompt 工程也很重要。
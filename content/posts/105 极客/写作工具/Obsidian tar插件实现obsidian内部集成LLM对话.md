---
{"title":"Obsidian tar插件实现obsidian内部集成LLM对话","git_title":"2024-08-11-obsidian-tars","tags":["geek"],"categories":["Github"],"dg-publish":true,"permalink":"/105 极客/写作工具/Obsidian tar插件实现obsidian内部集成LLM对话/","dgPassFrontmatter":true,"noteIcon":""}
---

# Tars插件简介

通过大语言模型（LLM）api，把AI集成到obsidian内部，使用方法为使用ob内部的tag标记触发对应AI即可。#

# 示例

#新对话 #我 : 你好，请介绍你自己

#qwen : 你好，我是来自阿里云的大规模语言模型，我叫通义千问。我可以生成各种类型的文本，如文章、故事、诗歌、故事等，并能够根据不同的场景和需求进行变换和扩展。此外，我还能够回答问题、提供信息和与用户进行交互，帮助解决疑惑和提供有益的建议。如果你有任何问题或需要帮助，欢迎随时向我提问！

# 使用教程

1. 安装插件并配置api
2. 输入 `新对话` `我`
3. 再输入 `#qwen` 回车即可触发 （此处的qwen为自定义项）
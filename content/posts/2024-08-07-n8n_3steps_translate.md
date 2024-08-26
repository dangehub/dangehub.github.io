---
title: 用 n8n 实现三步翻译
git_title: 2024-08-07-n8n_3steps_translate
tags:
  - geek
  - 翻译
categories:
  - geek
---


用 defy 搭建三步翻译老是报错，想自托管发现 defy 的配置要求很高，于是准备先用之前的 n 8 n 试试。

更新 n 8 n：1.0.4 更新到 1.44.1

![](https://github.com/dangehub/github2wp/blob/main/_posts/assets/Pasted%20image%2020240806214536.png)

采用这样的结构时，会报错 `Expected to find the prompt in an input field called 'chatInput' (this is what the chat trigger node outputs). To use something else, change the 'Prompt' parameter`

感觉像是个 bug，明明已经能读取前两个节点的输出，但是 n 8 n 还是提示无法读取到上上个节点。然后细查日志发现报错
```
NodeOperationError: No prompt specified at getPromptInputByType (/usr/local/lib/node_modules/n8n/node_modules/@n8n/n8n-nodes-langchain/dist/utils/helpers.js:71:15) at Object.execute (/usr/local/lib/node_modules/n8n/node_modules/@n8n/n8n-nodes-langchain/dist/nodes/chains/ChainLLM/ChainLlm.node.js:412:65) at Workflow.runNode (/usr/local/lib/node_modules/n8n/node_modules/n8n-workflow/dist/Workflow.js:728:19) at /usr/local/lib/node_modules/n8n/node_modules/n8n-core/dist/WorkflowExecute.js:673:51 at /usr/local/lib/node_modules/n8n/node_modules/n8n-core/dist/WorkflowExecute.js:1086:20
```

后面我发现问题来自于 `prompt` 的设置，原来每个 llm chain 一开始就有一个 prompt 设置，而默认是继承自上一个节点，而我的第一个 llm chain 节点就没设置它。
![](https://github.com/dangehub/github2wp/blob/main/_posts/assets/Pasted%20image%2020240806221817.png)

搞定后展示一下翻译效果：

> 原文：
> It’s so creepy and weird. I’ll go back and play DoDS and HL 2 DM etc and it’s still like a chat room while you play, it makes gaming so much more casual and enjoyable. I play this game and try to engage in any way and get literally no response from anyone. Is it just because this is a newer game so it’s full of antisocial teenagers who don’t know how to talk to each other? I just honestly don’t get it. It’s not that you’re obligated to chat, but it seems very weird to pretend that you’re not playing with other human beings.
> 
> Edit: I actually think this is why I lose interest in this game so quickly. In the old school games my team could be getting destroyed but it doesn’t bother me because we’re all chatting and having a good time. In this game it’s just silence anyway, doesn’t even feel like I’m playing against actual people so I don’t feel bad leaving in the middle of a match if we’re getting rolled.

> Google 翻译：
> 这太令人毛骨悚然和奇怪了。我会回去玩 DoDS 和 HL 2 DM 等游戏，玩的时候它仍然像一个聊天室，它让游戏变得更加休闲和愉快。我玩这个游戏并尝试以任何方式参与，但几乎没有得到任何人的回应。难道只是因为这是一款较新的游戏，所以里面充满了不知道如何与对方交谈的反社会青少年？老实说我不明白。这并不是说你有义务聊天，但假装你没有和其他人一起玩似乎很奇怪。
> 编辑：我实际上认为这就是我这么快对这款游戏失去兴趣的原因。在老式的学校比赛中，我的球队可能会被摧毁，但这并不困扰我，因为我们都在聊天，玩得很开心。无论如何，在这款游戏中，一切都是沉默，甚至感觉不到我是在和真人比赛，所以如果我们被淘汰，我不会因为在比赛中途离开而感到难过。

> 三步翻译：
> 实在是太奇怪而且让人有点不舒服了。回想当年玩《DoD:S》和《HL 2 DM》等游戏的时候，那种体验就像是在一间聊天室里面玩游戏，让整个游戏玩起来更加轻松且愉快。但当我玩这款游戏时，不管我怎么试图互动，却几乎得不到任何人的回应。难道仅仅因为这是一款新游戏，所以里面都是些不太愿意交流彼此的社恐少年吗？我真的搞不清楚是怎么回事。我不是说大家必须聊天，但完全假装没有和其他玩家一起玩的感觉总是让人觉得有点别扭。
> 编辑：我想这可能是导致我对这款游戏兴趣迅速消退的原因之一吧。在游戏中，即便是我们队伍大败亏输，我也不至于特别沮丧，因为我们那时都在愉快地聊天。但在这款游戏中，整个世界就像是一片寂静，根本感受不到自己是在跟其他玩家对战，所以我们遭受挫败时，我中途退出时也就没有什么内疚感了。

下面展示一下三步翻译的过程：

> 直译：
> 真是太诡异又让人不舒服。我回到过去玩 DoDS 和 HL 2 DM 等游戏时，感觉就像在一个聊天室里游戏，这让整个游戏体验变得更加轻松愉快。然而玩这款游戏时，无论我怎样尝试互动，却几乎得不到任何人的回应。难道仅仅因为这是一款新游戏，所以满是那些不懂得彼此交谈的社交恐惧少年？我真的不明白这是怎么回事。我不是说大家非得聊天不可，只是假装没有和其他玩家一起游戏，总让我觉得有些奇怪。\n\n 编辑：我想明白了，这可能就是我迅速对这个游戏失去兴趣的原因。在以前的老游戏中，即使我的队伍被杀得人仰马翻，我也不会感到烦闷，因为我们都在欢快地聊天。而在这款游戏中，四周一片寂静，根本感受不到是在和真人对战，所以我们被碾压时，我中途离开也不会有丝毫的愧疚感。

> 然后是用 ai 进行反思：
> <直接翻译>中存在的问题:\n\n 1. **不符合中文的表达习惯:**\n   - "真是太诡异又让人不舒服"：中文通常不以"真是太..."这样的句式表达负面强烈的情感。\n   \n 2. **句子结构笨拙:**\n   - "我玩这款游戏时，无论我怎样尝试互动，几乎得不到任何人的回应"：应改为“当我玩这款游戏时，无论怎样尝试互动，几乎得不到任何人的回应”更加自然流畅。\n   \n 3. **表达含糊不清，难以理解：**\n   - "难道仅仅因为这是一款新游戏, 所以满是那些不懂得彼此交谈的社交恐惧少年?" : 整个句子表达过于生硬，不易于理解其意图。\n   - "而这款游戏中, 四周一片寂静, 根本感受不到是在和真人对战": 这里使用“真人”来指代其他在线玩家显得较为突兀且不自然。一般情况下，在这种语境中并不会强调对战的对象是否为真实的人，因为在网络游戏中默认就是与真人对战。\n\n 4. **表达不够地道：**\n   - "所以, 我们被碾压时, 我中途离开也不会有丝毫的愧疚感" : 愧疚感的表达在此处显得过于严肃，通常在网络游戏中玩家们会更倾向于用更加随意的语气来描述此类情况。\n\n 注: 以上指出的问题并未提供修改后的版本。

此处我采用的是通义千问的 qwen-long 模型，它的实力在目前的 llm 中算不上非常强劲，这正好能说明三步翻译的强劲实力。

# 做成 api 来配合划词翻译 

先启动 n 8 n 的测试模式，然后用划词翻译发送一次，得到划词翻译的发包格式 

```
"body": {

"model": "qwen-long",

"messages": [

{

"role": "user",

"content": "This is an embeddable Chat widget for n8n. It allows the execution of AI-Powered Workflows through a Chat window."

}
```

然后需要根据格式调整 n8n

n8n 自动翻译完之后的输出为

```
  
[

{

"text": "<改进翻译>\n\n这是一款专为 n8n 设计的、可嵌入式的聊天工具，它使用户能够在聊天窗口内执行由人工智能驱动的工作流程。\n\n在这个版本里解决了以下问题：\n1. 调整了“可嵌入式”的位置，使之更符合中文的语言习惯。\n2. 简化并调整了句子结构，将“它能让用户通过聊天窗口来运行由人工智能驱动的工作流程”改写为更贴合中文表达习惯和流畅度的表述：“它使用户能够在聊天窗口内执行由人工智能驱动的工作流程”。\n3. 增强了句子之间逻辑关系的连贯性。"

}

]
```

而划词翻译需要接受来自 openai 格式的json，因此需要把上面n8n 的输出转换一下。

openai 格式参考为:
```
{
  "id": "b3e86c70-bd28-995b-a6e9-c47ab55c6495",
  "model": "qwen",
  "object": "chat.completion",
  "created": 1722959731,
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hello! How can I assist you today?"
      },
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 1,
    "completion_tokens": 9,
    "total_tokens": 10
  }
}
```

注意，在http  request 中不能使用引号和换行。

在 prompt 中要求不要使用引号，然后用节点来处理换行符，最后得到效果如下：![](https://github.com/dangehub/github2wp/blob/main/_posts/assets/Pasted%20image%2020240807013225.png)

可以看到这个效果已经相当好了。

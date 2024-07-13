---
share: true
title: 安卓端用tasker实现ai总结b站
git_title: 2024-07-13-android_tasker_ai_summary
tags:
  - geek
  - android
  - ai
  - LLM
  - gpt
categories:
  - android
  - geek
---
# 前言 

本文的实现方式受到chrome拓展[ChatGPTBox](https://chromewebstore.google.com/detail/chatgptbox/eobbhoofkanlmddnplfhnmkfbnlhpbbo)的启发，原理是通过b站的api和cookie获得自动ai字幕，然后用大语言模型（LLM）来总结字幕，从而获得视频的总结。


此工具的功能是帮助用户快速总结视频内容，以提高信息获取的速度。诚然，b站自己也推出了ai总结功能，但是那个功能很不稳定，有时候对一个视频有详细而结构化的总结，有时却只能得到一句话的概括，即便LLM已经火了两三年了，b站仍没有在这块投入过多，因此只能自己动手，丰衣足食。


本工具的缺点：
1. 无法总结没有字幕的视频（但是像bibigpt和b站官方的ai总结有时候能总结没有字幕的视频，我怀疑是有其他途径获取字幕）
2. 对视频内容和音频内容非强相关的视频无效（例如一个ASMR催眠视频，如果只用声音来判断，可能整个视频都是没有意义的。我们期待在未来多模态的ai能解决这个问题）
3. 需要使用b站的cookie才能获取视频字幕，而cookie是动态变化的，因此需要cookie刷新机制，我的处理办法是使用cookiecloud（需要自己的服务器/托管在别人的服务器上）

# 安卓端利用tasker实现ai总结b站

## 工作原理

1. 如果视频是手机分享的短链接形式（https://b23.tv/xxxxx ），则通过域名重定向获取bid（BVxxxxxx）
2. 已知bid后，获取cid `https://api.bilibili.com/x/web-interface/view?bvid=%bid`
3. 已知bid和cid后，获取包含字幕链接subtitle_url的信息`https://api.bilibili.com/x/player/v2?cid=%cid&bvid=%bid`
4. 将字幕发送通过api发送给ai，让ai总结


## 案例：

以视频[【游戏试玩】杀戮尖塔+娃娃机=抓抓地牢？游戏实况](https://www.bilibili.com/video/BV1DC411J7Wy/) 为例，如果采用安卓端国内版bilibili应用分享链接，得到的链接为`【【游戏试玩】杀戮尖塔+娃娃机=抓抓地牢？-哔哩哔哩】 https://b23.tv/jpcq7rz`

（隐藏的第一步为获取最新的cookie，因为实现方法不唯一，在下一章节介绍）

因此第一步是要从文字中提取出链接，一般采用正则 

```
(https?|ftp|file)://[-A-Za-z0-9+&@#/%?=~_|!:,.;]+[-A-Za-z0-9+&@#/%=~_|]
```

得到结果为`https://b23.tv/jpcq7rz`，然后我们需要将短链接转为长链接，最简单的办法就是使用浏览器的重定向功能，最终将得到`https://www.bilibili.com/video/BV1DC411J7Wy/`

然后使用正则提取出bid，正则如下：
```
BV([^/?]+)
```
即得到`BV1DC411J7Wy`

然后执行`http get`  `https://api.bilibili.com/x/web-interface/view?bvid=BV1DC411J7Wy` 可以获取一个json文件，需要从中提取cid，因此执行两次正则 

正则1（先匹配cid）:
```
"cid":(\d+)
```
得到：`"cid":1524209082`

正则2（提取cid的值）：
```
(\d+)
```
得到`1524209082`

然后获取字幕url，执行`http get` `https://api.bilibili.com/x/player/v2?cid=1524209082&bvid=BV1DC411J7Wy`
注意，header中需要加入cookie，如 
```headers
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Cookie:%cookieString
```
然后会获得一个包含键为`subtitle_url`的json文件（前提是视频有字幕），因此这里为了避免不存在字幕产生的误会，需要做一个有无的判断 

用正则进行匹配 
```
//[-A-Za-z0-9+&@#/%?=~_|!:,.;]+[-A-Za-z0-9+&@#/%=~_|]
```
如果不匹配，则提示此视频无字幕，若满足则进行下一步 

对`subtitle_url`执行`http get`，获得json，提取键`content`

然后把`content`的内容`http post`给LLM 

headers：
```headers
Authorization: Bearer %api_key
```

body：
```
{
    "model": "%llm_model",
    "messages": [
        {
            "role": "user",
            "content": "用尽量简练的语言,采用markdown语法书写（不要用代码块包裹），联系视频标题,对视频进行内容摘要,同时仍要保留重要细节和标题信息,视频标题为:%bili_name,字幕内容为:%subtitle"
        }
    ],
    "use_search": true,
    "stream": false
}
```

然后就能获得ai总结的内容了


## 同步cookie

我选择使用开源项目[CookieCloud](https://github.com/easychen/CookieCloud)实现cookie的同步 

变量解释：
- `%cookiecloud_url`：`cookiecloud服务器域名`，例如：`https://cookiecloud.25wz.cn/`，注意，结尾没有`/`
- `%cookiecloud_uuid`：见cookiecloud插件文档
- `%cookiecloud_key`：见cookiecloud插件文档 

步骤详解：

执行`http get` `%cookiecloud_url/get/%cookiecloud_uuid`
请求的body如下：
```
password%cookiecloud_key
```
这一步会获得解码后的json，包括cookie和localdata 

然后通过JavaScriptlet来格式化cookie 
```JavaScript
var jsonData = JSON.parse(local('%http_data'));
var cookies = jsonData.cookie_data[".bilibili.com"];
var result = [];

for (var i = 0; i < cookies.length; i++) {
    var name = cookies[i].name;
    var value = cookies[i].value;
    result.push(name + "=" + value);
}

// 将结果存储在Tasker的全局变量中
setGlobal('cookieString', result.join(';'));
```

注：其实这一步理论上只需要`SESSDATA`，我为了省事这么写了。
格式化得到`a=1,b=2,c=3`格式的cookie信息，然后参见上一章完成目标即可。


---
share: true
title: 下载网易云音乐的双语歌词
git_title: 2024-07-13-how-to-download-the-lyrics
tags:
  - geek
  - 音乐
categories:
  - 音乐
---
原文地址：[下载网易云音乐的双语歌词](https://umi.im/cloud-music-lrc/

==网易云音乐==是国内最好的音乐平台，歌曲丰富，而且很多外语歌都有双语歌词。但是==网易云音乐==不提供歌词下载，用手机客户端可以一键获取，但是获取到的歌词并非 LRC 格式的，而且文件名是纯数字，不方便用。

在 PC 端，可以通过一段 JS 脚本直接获取到双语的歌词。

# 使用方法：

- 打开需要下载歌词的歌曲==网易云音乐==链接，通过地址栏 URL 获取到歌曲 ID 。

[![cloud-music-lrc-1](https://umi.im/wp-content/uploads/2016/03/cloud-music-lrc-1.png)](https://umi.im/wp-content/uploads/2016/03/cloud-music-lrc-1.png)

- 按 F12 打开审查元素（Chrome浏览器），点击 Console 。

[![cloud-music-lrc-3](https://umi.im/wp-content/uploads/2016/03/cloud-music-lrc-3.png)](https://umi.im/wp-content/uploads/2016/03/cloud-music-lrc-3.png)

- 把下面代码最后一行里面的歌曲 ID 替换成自己需要下载歌词的歌曲 ID ，复制粘贴并回车运行。

```
(function(songID){
    var xhr = new XMLHttpRequest();
    xhr.open('GET', 'http://music.163.com/api/song/lyric?lv=-1&tv=-1&id=' + songID, true);
    xhr.send();
    xhr.onload = function() {
        var data = JSON.parse(xhr.responseText);
        var lrc = data.lrc.lyric.match(/\[\d+:\d+\.\d+[^\[]+/g);
        var tLrc = data.tlyric.lyric.match(/\[\d+:\d+\.\d+[^\[]+/g);
        var newLrc = [];
        lrc.map(function() {
            newLrc.push(lrc[arguments[1]]);
            newLrc.push(tLrc[arguments[1]]);
        });
        window.open('', "_blank", '').document.write(newLrc.join('<br>'));
    };
}('28870317')); // 歌曲 ID
```

- 弹出阻止运行窗口请允许。

[![cloud-music-lrc-2](https://umi.im/wp-content/uploads/2016/03/cloud-music-lrc-2.png)](https://umi.im/wp-content/uploads/2016/03/cloud-music-lrc-2.png)

- 完美得到带时间轴的双语歌词，自行保存为 LRC 格式就好了，或者直接嵌入歌曲标签里面。

[![cloud-music-lrc-4](https://umi.im/wp-content/uploads/2016/03/cloud-music-lrc-4.png)](https://umi.im/wp-content/uploads/2016/03/cloud-music-lrc-4.png)

感谢 V2EX 用户 [demo](https://www.v2ex.com/member/demo) 贡献此脚本。

GitHub地址：anonymous/**[concat_163_music_lrc.js](https://gist.github.com/anonymous/a800677393bbb2dd113a)**
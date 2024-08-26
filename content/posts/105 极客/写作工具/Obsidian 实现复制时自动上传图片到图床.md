---
{"title":"Obsidian 实现复制时自动上传图片到图床","git_title":"2024-08-11-obsidian-pic-upload","tags":["geek"],"categories":["geek"],"dg-publish":true,"permalink":"/105 极客/写作工具/Obsidian 实现复制时自动上传图片到图床/","dgPassFrontmatter":true,"noteIcon":""}
---

# Obsidian 实现复制时自动上传图片到图床

[【QuickAdd脚本】带图复制-自动上传图片到图床 - 经验分享 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/34059/8)

我新开一个库可以用，但是在主力库里就不行，报错为

![assets/Pasted image 20240808164552.png](/img/user/105%20%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/assets/Pasted%20image%2020240808164552.png)

```
QuickAdd: (ERROR) failed to run user script 带
图复制.Error:
The “path" argument must be of type string.
Received undlefined
```

这个问题很奇怪，我在新开的空白ob库里没有遇见，但是在主力库就有这个问题。

怎么排查问题？

- 尝试删除js脚本后再执行命令，看看是不是脚本的问题——删除后报错找不到脚本，看来不是这个问题。

然后我想为什么空白库是对的，多半是插件或者设置的问题，然后我把脚本发给kimi，kimi分析到一个关键点，就是文件路径。

于是我发现问题了：试用的时候发现一个问题：

如果`内部链接类型`设置为`基于当前笔记的相对路径`，脚本会报错  
`QuickAdd: (ERROR) failed to run user script 带图 复制.Error: The “path" argument must be of type string. Received undefined`

采用绝对路径也会有同样问题。改为尽量短路径就正常了。

用chatgpt修复这个bug（还得是chatgpt哇），修复版的脚本为：

```
const path = require('path');
const quickAddApi = app.plugins.plugins.quickadd.api;
const { editor, file, containerEl } = app.workspace.activeEditor;
const url = "http://127.0.0.1:36677/upload";

module.exports = async () => {
  const files = app.vault.getFiles();
  let selection = "";
  let content = "";
  selection = editor.getSelection();
  console.log("Selected text:", selection);

  for (let line of selection.split("\n")) {
    let embed = "";
    if (line) {
      embed = matchSelectionEmbed(line);
    }
    console.log("Matched embed:", embed);

    if (embed && /\.(png|jpg|jpeg|gif|bmp)$/.test(embed)) {
      let wikiPath = getFilePath(files, embed); // 匹配Wiki链接
      if (!wikiPath) {
        new Notice(`❌无法找到文件: ${embed}`);
        console.log(`❌无法找到文件: ${embed}`);
        continue;
      }

      // 获取绝对路径
      const imgPath = app.vault.adapter.getFullPath(wikiPath);
      console.log("Image path:", imgPath);

      const data = await uploadFiles([imgPath], url);
      if (data.success) {
        const imgWiki = `![[${embed}]]`;
        const imgLink = `![${embed}](${data.result})`;
        line = line.replace(imgWiki, imgLink);
      } else {
        new Notice(`❌上传 ${path.basename(imgPath)} 图片失败`);
        console.log(`❌上传 ${path.basename(imgPath)} 图片失败`);
      }
    }
    content += line + "\n";
  }
  
  console.log("Final content:", content);
  copyToClipboard(content)
  new Notice(`✅复制成功`);
};

// 获取文件路径函数
function getFilePath(files, baseName) {
  let matchingFiles = files.filter(f => {
    const fullPath = f.path;
    console.log(`Comparing ${fullPath} with ${baseName}`);
    return fullPath.endsWith(baseName);
  });
  
  if (matchingFiles.length === 0) {
    console.log(`No files matched for: ${baseName}`);
    return undefined;
  }

  return matchingFiles[0].path;
}

function matchSelectionEmbed(text) {
  const regex = /!\[\[?([^\]]*?)(\|.*)?\]\]?\(?([^)\n]*)\)?/;
  const matches = text.match(regex);
  if (!matches) return;
  if (matches[3]) return decodeURIComponent(matches[3]);
  if (matches[1]) return decodeURIComponent(matches[1]);
}

async function uploadFiles(imagePathList, url) {
  const response = await requestUrl({
    url: url,
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ list: imagePathList }),
  });
  const data = response.json; // 直接访问 `json` 属性，而不是调用 `json()` 方法
  return data;
};

function copyToClipboard(extrTexts) {
  const txtArea = document.createElement('textarea');
  txtArea.value = extrTexts;
  document.body.appendChild(txtArea);
  txtArea.select();
  if (document.execCommand('copy')) {
      console.log('copy to clipboard.');
  } else {
      console.log('fail to copy.');
  }
  document.body.removeChild(txtArea);
}

```

## 使用方法 

1. 安装插件quickadd
2. 在quickadd中设置脚本存放目录 `Template Folder Path`，然后在对应目录下新建 `带图复制.js`，把代码粘贴进去
3. 新建一个宏，选择刚刚新建的脚本
4. 安装piclist，配置好图床
5. 在obsidian中选中要分享的文本，其中需要包含要上传的图片，然后ctrl+p使用脚本
6. 粘贴即可


# 直接把图片上传到github

用 github publisher 插件能把图片上传到 github，但是图片在文章中的格式是 `[[]]` 的 wiki 链接，因此我们需要通过正则的方式来转换格式。

参考这篇文章 [obsidian图片链接转换成markdown语法，不关闭wiki链接_obsidian图片显示变成链接-CSDN博客](https://blog.csdn.net/shinigami2/article/details/128516807)

同时上面这个方法还可以解决这个问题：obsidian 粘贴进来的图片名字会自动带空格，如 `Pasted image 20240806221817.png`

最后发布后就能看到在 github 是可以正常查看图片了，但是为了同步到其他平台，可以批量的在图片路径前面加上 `https://github.com/dangehub/github2wp/blob/main/_posts`

方法也很简单，就是搜索 `assets/`，然后替换为 `https://github.com/dangehub/github2wp/blob/main/_posts/assets/`

 - 但是为什么同步到 wordpress 的文章里图片没有了？

同步到 wp 的是 html 代码：
```
<p><img alt="" src="https://github.com/dangehub/github2wp/blob/main/_posts/assets/Pasted%20image%2020240806214536.png" /></p>
```

直接访问这个链接是对的，但是这段 html 代码不能正常工作。
比如放到 obsidian 中：

---
<p><img alt="" src="https://github.com/dangehub/github2wp/blob/main/_posts/assets/Pasted%20image%2020240806214536.png" /></p>

---
上面的分隔线中就是这段 html 代码，无法显示图像。为什么？

去调试台看了下，报错 `（失败）net::ERR_BLOCKED_BY_ORB`，~~这是跨域问题~~

但是都没人说 github 的图片会限制跨域，检查之后发现 `https://github.com/dangehub/github2wp/blob/b85405e3ef0c15a3caf57a038a545e0842d43996/_posts/assets/Pasted%20image%2020240806214536.png` 指向的不是图片本身，`https://github.com/dangehub/github2wp/blob/b85405e3ef0c15a3caf57a038a545e0842d43996/_posts/assets/Pasted%20image%2020240806214536.png?raw=true` 才是图片本身，替换为这个链接就好了。

即用 `png?raw=true` 替换 `png`
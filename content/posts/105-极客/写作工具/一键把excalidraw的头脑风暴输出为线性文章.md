---
{"title":"一键把excalidraw的头脑风暴输出为线性文章","date":"2024-09-07","lastmod":"2024-09-07","creation date":"2024-09-07 14:30","modification date":"星期六 2024 九月7日 14:30:27","tags":["obsidian","excalidraw","脚本"],"categories":["obsidian","geek"],"alases":null,"dg-publish":true,"permalink":"/105-极客/写作工具/一键把excalidraw的头脑风暴输出为线性文章/","dgPassFrontmatter":true,"noteIcon":""}
---

# 发散性思考与线性输出


我以前一直都是采用传统的笔记方法，从上往下写。

这种线性似乎是理所应当、浑然天成的，但是人在想问题的时候又喜欢在草稿上写写画画，这个时候思维的组织方式却是非线性的。

接近的概念就是头脑风暴之类的思考组织方式，无意掉书袋，因此本文不再就此概念做过多讨论，我们姑且定义两种方式，不再深究其描述是否准确：

1. 从上往下的一维：线性
2. 上下左右都有：发散性

这里就会引入一个问题，当你的大脑在发散性思考的时候，用线性的笔记辅助思考，就会出现脑子和手打架的窘境。

举例来说：我在写某个主题的时候，会突然联想到一个分支想法，它不适合放进当前的正文，但是与之又有关联。如果是传统的笔记方法，这里可以使用便签（callout），但这样终究不太适合内容组织。因此类似mindmap的工具都会提供二维的内容输出方式。

但是这会引入一个新问题——发散思考之后，如何输出高可读性的内容。

不知道大家有没有这样的体验：自己做的思维导图再烂也能看懂，而别人做的再好也看得很晕。

这就是非线性（发散性）内容的弊端，除非是自己生产（即已完成内化）的内容，否则非线性内容先天就更难理解。

因此我们需要找到一个允许我们发散性思考，但是又能快捷的输出线性内容的的方法。

# 线性输出脚本的前身


当我产生了这个需求的时候，我先是尝试用obsidian的引用功能来实现它，因为excalidraw本身是支持对外提供内容的嵌入的。但是很难做到方便快捷。

于是我在网上查询资料，了解到两位先驱者的探索：

-  [Note必利阀：从excalidraw视觉笔记到obsidian线性输出](https://www.bilibili.com/video/BV1D44y1P7uD/?p=1)
- [熊猫别熬夜：PKMer_自定义 Excalidraw 脚本 - 制作 Excalidraw 悬浮大纲以及一键生成线型笔记](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/excalidraw/%E8%87%AA%E5%AE%9A%E4%B9%89excalidraw%E8%84%9A%E6%9C%AC-%E5%88%B6%E4%BD%9Cexcalidraw%E6%82%AC%E6%B5%AE%E5%A4%A7%E7%BA%B2%E4%BB%A5%E5%8F%8A%E4%B8%80%E9%94%AE%E7%94%9F%E6%88%90%E7%BA%BF%E5%9E%8B%E7%AC%94%E8%AE%B0/#:~:text=%E8%87%AA%E5%AE%9A%E4%B9%89%20Excali)

学习了两位网友关于excalidraw笔记如何实现线性输出的思考，其中

- <u>Note必利阀</u>制作了一个脚本，可以把excalidraw中选中的文本和图像按编辑的时间顺序输出为文字与图像的引用，最终复制到剪贴板，我们只需要把这个粘贴到想要用的地方就行
- <u>熊猫别熬夜</u>制作了一套脚本，要求使用者在excalidraw编写好符合一定格式的标题，然后通过脚本把标题与对应的内容引用出来

前者的优势是输出的内容为文字与图片链接，是可以被标准md识别的，但缺少了excalidraw的强大图形能力（因为它要求把freedraw转成图片，后续再编辑也是很麻烦的）。另外因为excalidraw的Frame和Group还不支持嵌套，所以如果有画中画这样的展现形式，则无法用后者的脚本实现。

后者直接把excalidraw中的图形引用过来，能更好的保留excalidraw的功能，不过这样也导致如果有发布文章的需求，后续可能需要再手动去把excalidraw引用转换为图片。


在学习两位的过程中，我厘清了 `发散性思考` 、` 线性输出 ` 的概念，同时基于我自己的日记工作流，对熊猫别熬夜的脚本进行了修改，最终我的线性输出脚本诞生了。

# 线性输出脚本


## 脚本介绍

本脚本的全名应该叫 `excalidraw线性输出到同名笔记`，它的功能也很简单，一言以蔽之：通过识别规定格式的文本，把与文本组合的内容以excalidraw的嵌入链接形式输出到对应笔记的指定标题下。

如下图所示：
![assets/Pasted image 20240907152957.png](/img/user/105-%E6%9E%81%E5%AE%A2/%E5%86%99%E4%BD%9C%E5%B7%A5%E5%85%B7/assets/Pasted%20image%2020240907152957.png)

本脚本通过识别形如 `#1 标题` 的文本，解析为 `标题`，并将该文本所属的组合（优先级分别为：Frame>Group>Element）引用链接插入到标题之后。

脚本的优点：
1. 保留了excalidraw的图形能力
2. 将内容输出到指定文件并生成逐级标题，让思考输出的内容可以与文件本身融合，大纲可识别
3. 支持自定义在哪个标题后插入，并且会根据设置标题动态调整生成标题的层级（比如设置在 `#灵感` 后插入，则从二级标题开始生成，如果设置为 `##灵感`，则会从三级标题开始生成，确保生成内容为子内容）

## 脚本使用说明


### 下载

你可以在我的Github下载：[dangehub/aqu_ob_share: Share my Obsidian techniques](https://github.com/dangehub/aqu_ob_share)

或者在文末直接复制源代码，自己新建一个md文件粘贴进去就好。

### 安装使用

1. 把脚本放到excalidraw的script目录下
2. 前往excalidraw插件设置，在最后一项 `已安装脚本设置` 中修改 `Custom Misc Header`，设置为自己想要插入在哪个标题后，参考值 `## 1.3 杂记`
3. 点击脚本按钮or使用命令工具
4. `1.excalidraw` 的线性内容会被输出到 `1` 中的 `## 1.3 杂记` 标题下

视频教程见：[obsidian+excalidraw+线性输出脚本=快乐日记](https://www.bilibili.com/video/BV1X3pteUEU1/)

# 附脚本源代码

```


// 获取脚本设置

let settings = ea.getScriptSettings();

// 设置默认值（如果是首次运行）

if (!settings["Custom Misc Header"]) {

    settings = {

        ...settings,  // 保留现有设置

        "Custom Misc Header": {

            value: "## 1.3 杂记",

            description: "自定义杂记标题，用于插入 Excalidraw 内容"

        }

    };

    ea.setScriptSettings(settings);

}

  

// 使用设置中的自定义杂记标题

const customMiscHeader = settings["Custom Misc Header"].value;

// 计算customMiscHeader中的 #数量

const customHeaderLevel = (customMiscHeader.match(/^#+/) || [''])[0].length;

// 获取笔记的基本路径和笔记名

const currentFile = app.workspace.getActiveFile();

if (!currentFile) {

    new Notice("❌ 无法获取当前文件", 3000);

    return;

}

  
// 获取excalidraw文件路径、文件名，准备生成对应笔记
const filePath = currentFile.path;

const fileName = currentFile.name;

const fileBaseName = fileName.replace('.excalidraw', '');

  

// 初始化变量

let frameIds = [];

let extrTexts = '';

  

// 获取所有以'#'开头的文本元素（即标题）

let allEls = ea.getViewElements().filter(el => el.type === "text" && el.text.startsWith('#'));

  

// 对标题进行排序

allEls.sort((a, b) => {

    let aMatch = a.text.match(/^#([\d.]+)/);

    let bMatch = b.text.match(/^#([\d.]+)/);

    if (!aMatch || !bMatch) return 0;

    let aParts = aMatch[1].split('.').map(Number);

    let bParts = bMatch[1].split('.').map(Number);

    for (let i = 0; i < Math.max(aParts.length, bParts.length); i++) {

        if (aParts[i] === undefined) return -1;

        if (bParts[i] === undefined) return 1;

        if (aParts[i] !== bParts[i]) return aParts[i] - bParts[i];

    }

    return 0;

});

  

for (let i of allEls) {

    let elText = i.rawText.trim(); // 使用 rawText 而不是 text，以规避换行符问题

    let elID = i.id;

  

    let match = elText.match(/^#([\d.]+)\s+(.*)/);

    if (!match) continue;

  

    let numberPart = match[1];

    let titlePart = match[2];

  
    // 计算标题级别
    let levels = numberPart.split('.').length;
    let headLevel = Math.min(levels + customHeaderLevel, 6);  // 根据customMiscHeader的级别调整

  

    let heads = '#'.repeat(headLevel);

    let titleText = "";

    let titleLink = "";

    let embedlinks = [];

    let nums = 99;

  

    // 处理excalidraw中的Frame、Group

    if (i.frameId && !frameIds.includes(i.frameId)) {

        elID = i.frameId;

        frameIds.push(elID);

        titleLink = `${fileName}#^frame=${elID}`;

        for (let j of ea.getViewElements().filter(el => el.type === "embeddable")) {

            if (j.frameId == elID) {

                embedlinks.push(`\n!${j.link} `)

                let objectFrame = ea.getViewElements().filter(el => el.frameId === elID);

                nums = objectFrame.length;

            }

        }

    } else if (i.groupIds) {

        titleLink = `${fileName}#^group=${elID}`;

        for (let j of ea.getViewElements().filter(el => el.type === "embeddable")) {

            if (j.groupIds.some(groupId => i.groupIds.includes(groupId))) {

                embedlinks.push(`\n!${j.link} `)

                let objectFrame = ea.getViewElements().filter(el => el.groupIds.some(groupId => i.groupIds.includes(groupId)));

                nums = objectFrame.length;

            }

        }

    } else {

        titleLink = `${fileName}#^${elID}`;

    }

  

    // 生成标题文本

    if (embedlinks.length > 0) {

        let extrEmbedlinks = embedlinks.join('\r\n');

        titleText = `${heads} ${titlePart}\n${extrEmbedlinks}\n`;

        if (nums > 3) {

            titleText += `![[${titleLink}]]\n`;

        }

    } else {

        titleText = `${heads} ${titlePart}\n`;

        if (nums > 2) {

            titleText += `![[${titleLink}]]\n`;

        }

    }

  

    extrTexts += titleText;

}

  

// 构建输出文件路径

let outputFileName = `${fileBaseName}.md`;

let outputPath = filePath.replace('.excalidraw', '');

  

// 检查输出文件是否存在

let outputFile = app.vault.getAbstractFileByPath(outputPath);

if (!outputFile) {

    new Notice(`❌ 输出文件不存在：${outputPath}`, 3000);

    // 尝试创建文件

    try {

        await app.vault.create(outputPath, '');

        outputFile = app.vault.getAbstractFileByPath(outputPath);

        new Notice(`✅ 已创建新文件：${outputPath}`, 2000);

    } catch (error) {

        new Notice(`❌ 无法创建文件：${outputPath}`, 3000);

        return;

    }

}

  

// 读取输出文件内容

let outputContent = await app.vault.read(outputFile);



  

// 创建唯一标识符

let excalidrawIdentifier = `EXCALIDRAW_CONTENT_${fileName.replace(/[^a-zA-Z0-9]/g, "_")}`;

  

// 构建新的 Excalidraw 内容

let newExcalidrawContent = `<!-- BEGIN ${excalidrawIdentifier} -->\n${extrTexts}\n<!-- END ${excalidrawIdentifier} -->`;

  

// 检查是否已存在 Excalidraw 内容

let startMarker = `<!-- BEGIN ${excalidrawIdentifier} -->`;

let endMarker = `<!-- END ${excalidrawIdentifier} -->`;

let startIndex = outputContent.indexOf(startMarker);

let endIndex = outputContent.indexOf(endMarker);

  

// 辅助函数：获取标题级别

function getHeaderLevel(header) {

    return header.match(/^#+/)[0].length;

}

  

// 辅助函数：查找下一个相同或更高级别的标题

function findNextHeader(content, startIndex, currentLevel) {

    const headerRegex = /^#{1,6}\s/gm;

    headerRegex.lastIndex = startIndex;

    let match;

    while ((match = headerRegex.exec(content)) !== null) {

        if (getHeaderLevel(match[0]) <= currentLevel) {

            return match.index;

        }

    }

    return content.length;

}

  

if (startIndex !== -1 && endIndex !== -1) {

    // 如果存在，更新现有内容

    outputContent = outputContent.substring(0, startIndex) +

                   newExcalidrawContent +

                   outputContent.substring(endIndex + endMarker.length);

} else {

    // 如果不存在，在自定义杂记标题后插入新内容

    let miscIndex = outputContent.indexOf(customMiscHeader);

    if (miscIndex !== -1) {

        let currentHeaderLevel = getHeaderLevel(customMiscHeader);

        // 找到下一个相同或更高级别的标题或文件末尾

        let nextHeaderIndex = findNextHeader(outputContent, miscIndex + customMiscHeader.length, currentHeaderLevel);

        // 在自定义杂记标题和下一个标题之间插入新内容

        outputContent = outputContent.substring(0, nextHeaderIndex) +

                        "\n\n" + newExcalidrawContent + "\n\n" +

                        outputContent.substring(nextHeaderIndex);

    } else {

        // 如果没有找到自定义杂记标题，则在文件末尾添加

        outputContent += `\n\n${customMiscHeader}\n\n` + newExcalidrawContent;

    }

}

  

// 更新输出文件

await app.vault.modify(outputFile, outputContent);

  

new Notice(`✅ Excalidraw 内容已更新到文件：${outputPath}`, 2000);
```
---
{"uid":20241230193952,"title":"Obsidian技巧之用maoxian插件剪藏网络文章，同时把图片下载到本地","tags":["obsidian","网页剪藏"],"description":null,"author":"曲淡歌","type":"other","draft":false,"editable":false,"modified":20250108131402,"dg-publish":true,"dg-path":"Obsidian/obsidian技巧之用maoxian插件剪藏网络文章，同时把图片下载到本地.md","permalink":"/Obsidian/obsidian技巧之用maoxian插件剪藏网络文章，同时把图片下载到本地/","dgPassFrontmatter":true,"noteIcon":""}
---


# 前言

今天在学习隐写术的时候看到一篇挺有价值的文章，本来想用 ob 官方的剪藏工具保存下来，但是发现官方工具到现在还不能把网络图片下载下来，这对于剪藏防丢失这个目的来说，这种级别就是不可用的，于是还是换工具了，调研了一下，发现 maoxian 可能是最适合我的。

maoxian 的优势：

- 在浏览器环境下下载图片，可以使用浏览器的代理、cookie 等环境信息，做到所见即可得
- 开源
- 文件保存的名称、内容格式、路径高度可自定义

# maoxian web clipper 配置过程记录

Obsidian 库： `C:\Users\62300\Documents\livesync`

网摘入口：`C:\Users\62300\Documents\livesync\201-文章摘录`

浏览器默认下载地址：`C:\Users\62300\Downloads`

maoxian 根目录：`maoxian摘录`

你需要根据电脑的用户名、obsidian 库名称、剪藏存放的文件夹来替换部分内容。

创建软链接（路径有中文就必须要有引号）

```
mklink /D "C:\Users\62300\Downloads\maoxian摘录" "C:\Users\62300\Documents\livesync\201-文章摘录"
```

调整 maoxian 的设置，由于内容过多，我直接把我的配置文件贴在文章末尾，详见 [[107-我的创作/文字/博客发布/Obsidian/obsidian技巧之用maoxian插件剪藏网络文章，同时把图片下载到本地#我的maoxian配置文件\|Obsidian技巧之用maoxian插件剪藏网络文章，同时把图片下载到本地#我的maoxian配置文件]]

# 我的 maoxian 配置文件

使用方法：保存为 json 文件后到 maoxian 的备份中导入

[fold]

```
{
  "data": {
    "assistant.default-tag-status": "",
    "assistant.public-plan.default.20240502": [
      {
        "actions": [
          {
            "hide": [
              "div#toc",
              "table.infobox",
              "span.mw-editsection",
              "table.navbox",
              "div.thumb",
              "div.dablink",
              "table.metadata"
            ]
          },
          {
            "pick": "div.mw-parser-output"
          }
        ],
        "excludePattern": "https://*.m.wikipedia.org/*/",
        "name": "wikipedia.org",
        "pattern": "https://*.wikipedia.org/wiki/*",
        "tags": [
          "knowledge",
          "wiki"
        ],
        "version": 20240502
      },
      {
        "actions": [
          {
            "hide": [
              ".page-actions-menu",
              "#toc",
              ".mw-editsection",
              "h2 > div.mw-ui-icon",
              "table.box-Unreferenced",
              "table.box-More_citations_needed"
            ]
          },
          {
            "chAttr": {
              "attr": "style",
              "pick": "h2.section-heading",
              "sep": ";",
              "type": "split2list.add",
              "value": "width: 100%"
            }
          }
        ],
        "contributors": [
          "Altair Wei (author)"
        ],
        "name": "Wikipedia Mobile View",
        "pattern": "https://*.m.wikipedia.org/*/",
        "tags": [
          "knowledge",
          "wiki"
        ],
        "version": 20240502
      },
      {
        "actions": [
          {
            "hide": [
              ".avatar",
              ".avatar-parent-child",
              ".inline-comment-form-actions",
              ".flex-items-center.d-sm-flex.d-none",
              ".d-inline-block"
            ]
          },
          {
            "pick": [
              ".js-discussion",
              ".markdown-body"
            ]
          }
        ],
        "contributors": [
          "yzqzss (author)"
        ],
        "name": "Github",
        "pattern": "https://github.com/",
        "tags": [
          "IT",
          "geek",
          "git"
        ],
        "version": 20240502
      },
      {
        "actions": [
          {
            "pick": "#bodyContent"
          }
        ],
        "contributors": [
          "Mika"
        ],
        "name": "ArchWiki",
        "pattern": "https://wiki.archlinux.org/title/*",
        "tags": [
          "IT",
          "wiki",
          "doc"
        ],
        "version": 20240502
      }
    ],
    "assistant.public-plan.default.latest": "assistant.public-plan.default.20240502",
    "assistant.public-plan.default.text": "[\n  {\n    \"name\": \"wikipedia.org\",\n    \"pattern\": \"https://*.wikipedia.org/wiki/*\",\n    \"excludePattern\": \"https://*.m.wikipedia.org/*/\",\n    \"version\": 20240502,\n    \"actions\": [\n      {\n        \"hide\": [\n          \"div#toc\",\n          \"table.infobox\",\n          \"span.mw-editsection\",\n          \"table.navbox\",\n          \"div.thumb\",\n          \"div.dablink\",\n          \"table.metadata\"\n        ]\n      },\n      {\n        \"pick\": \"div.mw-parser-output\"\n      }\n    ],\n    \"tags\": [\n      \"knowledge\",\n      \"wiki\"\n    ]\n  },\n  {\n    \"name\": \"Wikipedia Mobile View\",\n    \"pattern\": \"https://*.m.wikipedia.org/*/\",\n    \"version\": 20240502,\n    \"actions\": [\n      {\n        \"hide\": [\n          \".page-actions-menu\",\n          \"#toc\",\n          \".mw-editsection\",\n          \"h2 > div.mw-ui-icon\",\n          \"table.box-Unreferenced\",\n          \"table.box-More_citations_needed\"\n        ]\n      },\n      {\n        \"chAttr\": {\n          \"type\": \"split2list.add\",\n          \"pick\": \"h2.section-heading\",\n          \"attr\": \"style\",\n          \"value\": \"width: 100%\",\n          \"sep\": \";\"\n        }\n      }\n    ],\n    \"tags\": [\n      \"knowledge\",\n      \"wiki\"\n    ],\n    \"contributors\": [\n      \"Altair Wei (author)\"\n    ]\n  },\n  {\n    \"name\": \"Github\",\n    \"pattern\": \"https://github.com/\",\n    \"version\": 20240502,\n    \"actions\": [\n      {\n        \"hide\": [\n          \".avatar\",\n          \".avatar-parent-child\",\n          \".inline-comment-form-actions\",\n          \".flex-items-center.d-sm-flex.d-none\",\n          \".d-inline-block\"\n        ]\n      },\n      {\n        \"pick\": [\n          \".js-discussion\",\n          \".markdown-body\"\n        ]\n      }\n    ],\n    \"tags\": [\n      \"IT\",\n      \"geek\",\n      \"git\"\n    ],\n    \"contributors\": [\n      \"yzqzss (author)\"\n    ]\n  },\n  {\n    \"name\": \"ArchWiki\",\n    \"pattern\": \"https://wiki.archlinux.org/title/*\",\n    \"version\": 20240502,\n    \"actions\": [\n      {\n        \"pick\": \"#bodyContent\"\n      }\n    ],\n    \"tags\": [\n      \"IT\",\n      \"wiki\",\n      \"doc\"\n    ],\n    \"contributors\": [\n      \"Mika\"\n    ]\n  }\n]",
    "assistant.public-plan.pointers": [
      "assistant.public-plan.default.20240502"
    ],
    "assistant.public-plan.subscription-urls": [
      "https://mika-cn.github.io/maoxian-web-clipper/assistant/plans/default/index.json"
    ],
    "assistant.public-plan.subscriptions": [
      {
        "description": "Default channel hosts plans that relative to international websites",
        "latestVersion": 20240502,
        "name": "default",
        "size": 4,
        "updateUrl": "https://mika-cn.github.io/maoxian-web-clipper/assistant/plans/default/20240502.json",
        "url": "https://mika-cn.github.io/maoxian-web-clipper/assistant/plans/default/index.json"
      }
    ],
    "config": {
      "allowFileSchemeAccess": true,
      "assetFileName": "$TIME-INTSEC-$MD5URL$EXT",
      "assetFolder": "$ROOT-FOLDER/assets",
      "assistantEnabled": false,
      "autoInputLastCategory": true,
      "autoInputLastTags": true,
      "autoRefreshHistory": false,
      "autoRunContentScripts": false,
      "autoUpdatePublicPlan": false,
      "autogenerateClippingJs": false,
      "backupAssistantData": true,
      "backupHistoryPageConfig": true,
      "backupSelectionData": true,
      "backupSettingPageConfig": true,
      "clippingFolderName": "$YYYY-$MM-$DD-$TIME-INTSEC",
      "clippingHandler": "Browser",
      "clippingJsPath": "$STORAGE-PATH/history/clippings.js",
      "communicateWithThirdParty": false,
      "defaultCategory": "default",
      "frameFileFolder": "$ROOT-FOLDER/frames",
      "frameFileName": "$TIME-INTSEC-$MD5URL.frame.html",
      "handlerBrowserEnabled": true,
      "handlerNativeAppEnabled": false,
      "handlerWizNotePlusEnabled": false,
      "htmlCaptureApplet": "remove",
      "htmlCaptureAudio": "remove",
      "htmlCaptureCssImage": "remove",
      "htmlCaptureCssRules": "saveUsed",
      "htmlCaptureEmbed": "saveImage",
      "htmlCaptureIcon": "remove",
      "htmlCaptureImage": "saveAll",
      "htmlCaptureObject": "saveImage",
      "htmlCaptureVideo": "remove",
      "htmlCaptureWebFont": "remove",
      "htmlCompressCss": false,
      "htmlCustomBodyBgCssEnabled": false,
      "htmlCustomBodyBgCssValue": "#000000",
      "htmlEmbedFilter": "<images>",
      "htmlObjectFilter": "<images>",
      "htmlSaveClippingInformation": false,
      "htmlWebFontFilterList": "woff2|woff|otf|ttf",
      "infoFileFolder": "$CLIPPING-PATH",
      "infoFileName": "index.json",
      "mainFileFolder": "$ROOT-FOLDER",
      "mainFileName": "$TITLE.$FORMAT",
      "markdownOptionBulletListMarker": "-",
      "markdownOptionCodeBlockStyle": "fenced",
      "markdownOptionEmDelimiter": "*",
      "markdownOptionFence": "```",
      "markdownOptionFormulaBlockWrapper": "padSameLine",
      "markdownOptionHeadingStyle": "atx",
      "markdownOptionHr": "- - -",
      "markdownOptionLinkReferenceStyle": "full",
      "markdownOptionLinkStyle": "inlined",
      "markdownOptionPreformattedCode": false,
      "markdownOptionStrongDelimiter": "**",
      "markdownTemplate": "\n{{content}}\n",
      "mouseModeEnabled": true,
      "offlinePageHandler": "Browser",
      "refreshHistoryHandler": "NativeApp",
      "rememberSelection": false,
      "requestCache": "default",
      "requestCacheCss": true,
      "requestCacheImage": true,
      "requestCacheWebFont": false,
      "requestCredentials": "same-origin",
      "requestMaxTries": 3,
      "requestReferrerPolicy": "strict-origin-when-cross-origin",
      "requestTimeout": 300,
      "rootFolder": "maoxian摘录",
      "saveDomainAsTag": false,
      "saveFormat": "md",
      "saveInfoFile": false,
      "saveTitleFile": false,
      "selectSaveFormatOnMenus": false,
      "shortcutSlot0": "_openLastClipping",
      "shortcutSlot1": "_clipAsDefault",
      "shortcutSlot2": "_clipAsHTML",
      "shortcutSlot3": "_clipAsMarkdown",
      "shortcutSlot4": "_doNothing",
      "shortcutSlot5": "_doNothing",
      "shortcutSlot6": "_doNothing",
      "shortcutSlot7": "_doNothing",
      "shortcutSlot8": "_doNothing",
      "shortcutSlot9": "_doNothing",
      "titleFileFolder": "$CLIPPING-PATH",
      "titleFileName": "a-title_$TITLE",
      "userCommandsText": "{\n  \"doNothing\": {\"exec\": \"doNothing\"}\n}",
      "version": "2.16"
    },
    "history.page.cache.enableAdvancedSearchMode": false,
    "history.page.cache.enableConfirmMode": true,
    "history.page.cache.localstorage.migrated": true,
    "history.page.cache.search.keyword": ""
  },
  "backupAt": "2024-12-17 16:25:24"
}
```
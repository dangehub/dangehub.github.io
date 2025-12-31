---
{"title":"解决vivaldi浏览器Crtl+E无法在Discord中唤出面板的问题","created":"2025-12-31T11:26","updated":"2025-12-31T11:30","dg-publish":true,"dg-permalink":"vivaldi-discord-hotkey-issue","dg-path":"浏览器技巧/解决vivaldi浏览器Crtl+E无法在Discord中唤出面板的问题.md","permalink":"/vivaldi-discord-hotkey-issue/","dgPassFrontmatter":true,"noteIcon":""}
---


我个人比较喜欢用的 chrome 系浏览器就是 [[Vivaldi\|Vivaldi]]，它有一个很好用的全局命令面板，默认使用 `Ctrl+E` 唤出，但是 [[Discord\|Discord]] 会劫持这个快捷键，并且设置中无法关闭。

这个时候我们可以使用 [[105-极客/TamperMonkey\|TamperMonkey]] 脚本来实现禁用网页快捷键，以下脚本使用 ChatGPT 编写

```
// ==UserScript==
// @name         Let browser Ctrl+E work on Discord
// @match        https://discord.com/*
// @run-at       document-start
// ==/UserScript==

window.addEventListener(
  "keydown",
  (e) => {
    if (e.ctrlKey && !e.altKey && !e.metaKey && e.key.toLowerCase() === "e") {
      // 关键：不要 preventDefault()，否则浏览器快捷键也被你取消了
      e.stopImmediatePropagation();
      // 可选：e.stopPropagation();
    }
  },
  true // capture
);


```
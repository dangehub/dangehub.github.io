---
{"uid":20250124130303,"title":"让Obsidian的光标丝滑移动","tags":["Obsidian美化","Obsidian","CSS"],"description":null,"author":"曲淡歌","draft":false,"editable":false,"modified":20250124133146,"dg-publish":true,"created":"2025-04-17T18:43","updated":"2025-04-18T02:00","dg-path":"Obsidian/让Obsidian的光标丝滑移动.md","permalink":"/Obsidian/让Obsidian的光标丝滑移动/","dgPassFrontmatter":true,"noteIcon":""}
---

# 更新版本

下面提到的 [[003-功能页面/BPM/Ninja Cursor\|Ninja Cursor]] 配合CSS会在一些情况下出现bug，现在我更推荐使用 [[003-功能页面/BPM/Animated Cursor\|Animated Cursor]] 插件，安装这个插件无须配合CSS。

** ↓↓下文已过时！↓↓**

# 前言

本文参考自 [光标平滑插入动画 - 插件创意|Cursor Smooth Caret Animation](https://forum.obsidian.md/t/cursor-smooth-caret-animation/31068/25)

效果展示：

![assets/PixPin_2025-01-24_13-14-53.gif](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/Obsidian/assets/PixPin_2025-01-24_13-14-53.gif)

# 使用方法

1. 在插件市场安装 `ninja cursor` 插件
2. 在 Obsidian 内添加并开启以下 css[^1]
3. enjoy it！

目前这个方案**有一定缺陷**：在部分插件/样式中，光标的显示位置会错位，不过实际位置是正确的

# 附录

[^1]: 新建文件 `丝滑光标.css` 并粘贴上面的代码，然后把文件放入 Obsidian 的 css 文件夹中并在 Obsidian 启用

```
/* Customization for the Ninja Cursor */ 
.x-cursor {
  position: inline block;
  background: var(--caret-color); /* Sets the Ninja Cursor Colour. */
  width: 1px; /* Sets the width of the Ninja Cursor. */ 
  transition: all 80ms !important; /* Sets the animation delay of the Ninja Cursor. Fast typers should use a higher delay to maintain the effect. */ 
  top: calc(0px - var(--header-height)); /* Ensures the cursor is inline with selected line. */ 
  --cursor-height: calc(var(font-size) - 2px); /* Sets Ninja Cursor Height. Font-Height variable used to ensure height matches current body text input. For a taller/shorter cursor alter the px. */ 
  max-height: calc(var(--font-ui-large) * 2); /* Caps the height of the Ninja Cursor to the span of two lines. Stops Ninja Cursor spanning several lines by capping it at two. It can be capped at one but the cursor is unable to change height to match headings. */ 
}

/* Hides the Default Cursor */
body:has(.x-cursor) * {
  caret-color: transparent;
}
.cm-cursorLayer {
  animation: none !important;
  display: none; 
}

/* Hides the Default Ninja Cursor Dashing Effect */ 
.cursorWrapper .x-cursor::after {
  display: none;
}

/* Applies the Caret Blinking Effect */
.cursorWrapper .x-cursor0 {
  animation: blink0 1s 1s both infinite;
}
.cursorWrapper .x-cursor1 {
  animation: blink1 1s 1s both infinite;
}

/* Keyframes for the Caret Blinking Effect */ 
@keyframes blink1 {
  0%   { opacity: 1; }
  45%  { opacity: 1; }
  50%  { opacity: 1;}
  95%  { opacity: 1; }
  100% { opacity: 1; }
}

@keyframes blink0 {
  0%   { opacity: 1; }
  45%  { opacity: 1; }
  50%  { opacity: 1;}
  95%  { opacity: 1; }
  100% { opacity: 1; }
}
```
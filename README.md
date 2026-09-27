# 视频速度控制器（Video Speed Controller）

[简体中文](README.md) | [English](README.en.md)

> **本仓库是 [igrigorik/videospeed][upstream-link] 的非官方简体中文分支**，基于上游 v0.11.1。
> 由社区维护，与原作者无关。上游官方版本见下方应用商店链接。

## 安装

**上游官方版本**（推荐大多数用户使用）：

[![Chrome Web Store][chrome-web-store-version]][chrome-web-store-link] [![Chrome Web Store Users][chrome-web-store-users-badge]][chrome-web-store-link] [![Chrome Web Store Users][chrome-web-store-stars]][chrome-web-store-link]

**本分支**（含汉化与浮窗改动）：尚未上架应用商店，需从源码构建后手动加载。

```bash
npm ci
npm run build
```

然后打开 `chrome://extensions`，启用「开发者模式」→「加载已解压的扩展程序」→ 选择 `dist/` 目录。

**视频速度控制器（Video Speed Controller）** 让你可以精细控制任意网站上的 HTML5 视频或音频元素。

## 本分支相对上游的改动

基于上游 v0.11.1。上游原有的功能、快捷键与设置项均未删改。

**新增**

- **调速 / 暂停时自动弹出浮窗** —— 按下提高速度、降低速度或暂停快捷键时，速度浮窗会自动显示，并在「自动隐藏」设定的秒数后自动消失。上游只有绑定到「显示/隐藏控制器」的按键才能改变浮窗可见性。
- **「自动隐藏」设置项** —— 位于设置页「高级」标签，控制上述浮窗保持显示的秒数，支持小数，默认 3 秒。

**修改**

- **显式隐藏不再压制临时反馈** —— 上游行为下，若启用了「默认隐藏控制器」或用户按过隐藏键，调速 / 暂停快捷键不会弹出浮窗；本分支让这类临时反馈始终可见，仅当媒体不可用时浮窗才完全不可见。浮窗的其他原有行为未改动。
- **浮窗闪现时长可配置** —— 由上游硬编码的 2 秒改为读取「自动隐藏」设置（默认 3 秒）。
- **界面汉化** —— 设置页、弹窗页面与本文档。

**修复**

- **设置页 / 弹窗中文乱码** —— 这两个页面缺少 `<meta charset="utf-8">`，在中文环境下浏览器回退到 GBK 解码导致乱码；已补上编码声明。

---

## 倍速播放的科学

**太长不看** —— 更快的播放速度意味着更高的参与度和更好的记忆效果。

普通成年人的阅读速度约为 [250-300 词/分钟][wpm-study]（wpm）。语音平均约 150 wpm；幻灯片演示往往接近 100 wpm。如果有选择，大多数观众会[把播放速度调到约 1.3-1.5 倍][ms-study] 来填补这一差距。加速观看能[让注意力保持更久][byu-study] —— 更快的传达带来更高的参与度。经过练习，许多人会稳定在 2 倍甚至更高，并发现[回到 1 倍反而不舒服][mit-study]。

[wpm-study]: http://www.paperbecause.com/PIOP/files/f7/f7bb6bc5-2c4a-466f-9ae7-b483a2c0dca4.pdf
[ms-study]: http://research.microsoft.com/en-us/um/redmond/groups/coet/compression/chi99/paper.pdf
[byu-study]: http://www.enounce.com/docs/BYUPaper020319.pdf
[mit-study]: http://alumni.media.mit.edu/~barons/html/avios92.html#beasleyalteredspeech

HTML5 媒体元素本身就提供了原生的播放速率 API，但大多数播放器会将其隐藏或人为限制。调速本应轻松且频繁：我们不会以固定的节奏阅读，自然也不该以单一速度观看。

## 功能特性

- **通用** —— 适用于任何包含 HTML5 媒体的网站：YouTube、Netflix、
  Coursera、播客、本地文件等。
- **视频与音频** —— 同时控制 `<video>` 和 `<audio>` 元素。
- **精细调速** —— 通过可配置的步进在 0.07x 到 16x 之间调整。
- **按站点速度规则** —— 为特定域名设置默认播放速度
  （例如讲座类网站始终使用 2 倍速）。
- **按站点禁用** —— 在你不希望显示控制器的网站上将其关闭。
- **记住速度** —— 可选地在会话与标签页之间保留你最后使用的速度。
- **速度回写（fightback）** —— 当网站的播放器试图重置你的速度时，自动重新应用。
- **可拖拽浮层** —— 将视频上的速度指示器拖动到任意位置。
- **完全可自定义快捷键** —— 重新映射每一个按键，添加修饰键组合
  （Ctrl、Shift、Alt），创建多个首选速度切换。
- **自定义控制器 CSS** —— 用你自己的 CSS 规则为浮层设置样式或调整位置。

## 默认键盘快捷键

- **S** —— 降低播放速度
- **D** —— 提高播放速度
- **R** —— 将播放速度重置为 1.0x
- **Z** —— 后退 10 秒
- **X** —— 前进 10 秒
- **G** —— 在当前速度与首选速度之间切换
- **V** —— 显示/隐藏控制器
- **M** —— 在当前位置设置标记
- **J** —— 跳回先前设置的标记

所有快捷键都可以在扩展的设置页面中完全自定义。你可以重新分配按键、添加修饰键组合，并定义多个具有不同数值的首选速度快捷键以便快速切换。在设置中点击 **新增** 即可创建更多绑定。修改后请刷新页面使其生效。

## 许可证

(MIT License) - Copyright (c) 2014 Ilya Grigorik  
Copyright (c) 2026 thomasfan（简体中文汉化与修改）

[chrome-web-store-version]: https://img.shields.io/chrome-web-store/v/nffaoalbilbmmfgbnbgppjihopabppdk?label=Chrome%20Web%20Store
[chrome-web-store-users-badge]: https://img.shields.io/chrome-web-store/users/nffaoalbilbmmfgbnbgppjihopabppdk
[chrome-web-store-stars]: https://img.shields.io/chrome-web-store/stars/nffaoalbilbmmfgbnbgppjihopabppdk
[github-release-badge]: https://img.shields.io/github/v/release/igrigorik/videospeed
[chrome-web-store-link]: https://chromewebstore.google.com/detail/video-speed-controller/nffaoalbilbmmfgbnbgppjihopabppdk
[github-release-link]: https://github.com/igrigorik/videospeed/releases
[upstream-link]: https://github.com/igrigorik/videospeed

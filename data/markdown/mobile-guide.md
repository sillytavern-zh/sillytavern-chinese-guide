---
title: "手机使用 SillyTavern 完整指南:iOS / Android / iPad"
description: "手机怎么用 SillyTavern?iOS、Android、iPad 三大平台的最佳方案完整对比和操作步骤,含 Termux 本地部署。"
slug: mobile-guide
category: getting-started
canonical: https://guide.sillytavern.one/getting-started/mobile-guide/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/getting-started/mobile-guide/](https://guide.sillytavern.one/getting-started/mobile-guide/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

"手机能用 SillyTavern 吗？" 是新手第二常问的问题。答案是：**能，但有讲究**。

这一篇梳理 iOS、Android、iPad 各自的最佳方案。

我自己用 iPad + 云端的组合用了很久,体感跟电脑没差多少——除了打字慢一点。

## 一张表看懂你该怎么选

| 设备 | 最佳方案 | 难度 |
|---|---|---|
| iPhone / iPad | 云端版（无替代） | 极低 |
| 普通 Android | 云端版 | 极低 |
| 高性能 Android + 喜欢折腾 | Termux 本地部署 | 中等 |
| 多设备并用（手机+电脑） | 云端版 + 数据同步 | 低 |

## iOS / iPad：只能用云端

iOS 系统封闭，**没办法在手机上跑 Node.js**——这是技术限制，不是软件做得差。所以 iOS 用户只有一条路：**用浏览器打开在线版部署**。

推荐流程：

1. 在 Safari / Chrome 打开在线版部署地址
2. 加到主屏幕（Safari → 分享 → 添加到主屏幕）
3. 像 App 一样使用

<div class="tip">

iPad 用户体验最好——大屏 + iOS 的稳定，加上云端版的统一同步，几乎和电脑无差。

</div>

## Android：两条路

### 路线 A：用云端（推荐 95% 的用户）
和 iOS 一样，浏览器打开即可。优点：

- 0 配置
- 自动同步其他设备
- 不吃电池、不发烫
- 不占存储

### 路线 B：Termux 本地部署（折腾党专属）

只有满足以下条件才推荐：

- 旗舰级 Android（8GB+ 内存）
- 熟悉命令行
- 介意数据放在别人服务器上
- 喜欢完全控制

核心步骤：

1. Google Play 装 Termux（或 F-Droid，更新更勤）
2. 进 Termux 跑：
```bash
pkg update && pkg upgrade
pkg install nodejs-lts git
git clone https://github.com/SillyTavern/SillyTavern.git
cd SillyTavern
npm install
node server.js
```
3. 在手机浏览器打开 `http://localhost:8000`

<div class="warn">

Termux 部署的酒馆**关掉应用就停止运行**。一般用一会就行，长期跑还是云端更省心。

</div>

## 移动端使用技巧

不管用哪种方案，这几个技巧让体验起飞：

### 1. 横屏使用
酒馆在窄屏下输入框会很小，横屏体验明显好。

### 2. 加到主屏幕
所有主流浏览器都支持「添加到主屏幕」，加完后像 App 一样独立打开，不再和其他网页混在浏览器里。

### 3. 关掉「移动端简化模式」
酒馆有的版本默认在手机上自动简化界面，把高级功能藏起来。在设置里关掉以使用全部功能。

### 4. 启用「连续模式」
让 AI 输出更长内容时不会被手机的省电策略中断。

## 常见手机问题

| 问题 | 原因 | 解决 |
|---|---|---|
| 输入法挡住输入框 | 移动浏览器问题 | 用横屏，或换 Edge / Firefox |
| 切到别的 App 回来对话丢了 | 浏览器后台被杀 | 用主屏幕模式启动 |
| 加载特别慢 | 4G 网或弱信号 | 切 WiFi，或关闭流式 |
| 总是被截断 | 移动端的连接断开 | 关闭流式输出（Stream 改 false） |

## 总结

> **大多数手机用户**：直接用云端版，5 分钟上手
> **iOS 用户**：没得选，云端版就是答案
> **折腾党 Android**：Termux 是好玩具，但日常推荐云端

---

## 相关阅读

- [在线版部署 vs 本地部署完整对比](/getting-started/cloud-vs-local/)
- [30 分钟极速上手](/getting-started/quickstart/)

---

## 📖 关于本文

- **原文**: [手机使用 SillyTavern 完整指南:iOS / Android / iPad](https://guide.sillytavern.one/getting-started/mobile-guide/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/getting-started/mobile-guide/) 为准。

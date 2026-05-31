---
title: "SillyTavern 1.17.0 升级后魔法棒按钮消失?一键修复"
description: "SillyTavern 1.17.0 升级后左下角魔法棒(扩展菜单)按钮不见了?这是新版默认隐藏导致。本文教你 30 秒一键恢复经典布局,附完整原因分析和 GitHub 开源扩展。"
slug: missing-wand-button-1170
category: troubleshooting
canonical: https://guide.sillytavern.one/troubleshooting/missing-wand-button-1170/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/troubleshooting/missing-wand-button-1170/](https://guide.sillytavern.one/troubleshooting/missing-wand-button-1170/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

# SillyTavern 1.17.0 升级后魔法棒按钮"消失"了?一键修复

> 🪄 30 秒解决 SillyTavern 1.17.0+ 左下角魔法棒(扩展菜单)按钮消失问题

## 你遇到这个问题吗?

升级到 SillyTavern 1.17.0 后,你可能发现:

- 左下角输入框旁的【🪄 魔法棒】按钮**不见了**
- 之前打开扩展菜单的【拼图】图标也找不到
- 想用扩展功能但找不到入口
- 即使重启、清浏览器缓存都没用

**这不是 bug,而是 1.17.0 改变了显示逻辑**。本文带你彻底搞懂 + 一键修复。

---

## ⚡ TL;DR(只想要解决方法)

### 方案 A: 入口移到了顶部栏

打开 SillyTavern → **顶部栏点击三个堆叠方块图标(扩展)** → 你会看到所有扩展菜单项。

### 方案 B: 装个扩展强制恢复经典左下角魔法棒

> ⭐ **推荐** - 30 秒安装,永久生效

详细安装步骤往下看 ⬇️ 第 4 节。

---

## 为什么 1.17.0 会"消失"按钮?(技术解析)

如果你想搞懂背后的原因,继续往下看。

### 真因:动态显示逻辑

SillyTavern 1.17.0 在 `scripts/extensions.js` 中加了这段代码:
javascript
function showHideExtensionsMenu() {
// 检查 #extensionsMenu 中【可见】的菜单项数量
const hasMenuItems = $('#extensionsMenu').children().filter((_, child) =>
$(child).css('display') !== 'none').length > 0;

// 有可见菜单项 → 显示按钮;没有 → 隐藏
$('#extensionsMenuButton').toggle(hasMenuItems);
}

// 每秒检查一次
setInterval(showHideExtensionsMenu, 1000);

### 触发条件

按钮被**隐藏**的情况:

| 场景 | 是否隐藏 |
|------|:-------:|
| 全新安装,还没装任何扩展 | 🔴 隐藏 |
| 装了酒馆助手等扩展 | ✅ 显示 |
| 装了扩展但所有菜单项都被禁用 | 🔴 隐藏 |
| 切换到某些场景导致菜单项被自动隐藏 | 🔴 偶发隐藏 |

### 官方设计意图

官方逻辑是:"没有可用扩展时,按钮就没意义,所以隐藏"。

但很多用户认为按钮应该作为**视觉锚点**保留——即使暂时没有菜单项,看到按钮也知道未来可以装扩展。

---

## 三种解决方案对比

| 方案 | 优点 | 缺点 | 推荐度 |
|------|------|------|:------:|
|**A. 用顶部栏入口**| 不需安装任何东西 | 改变操作习惯,反人类 | ⭐⭐ |
|**B. 装本扩展恢复**| 一键解决,可装可卸,完美兼容 | 需要安装一个扩展 | ⭐⭐⭐⭐⭐ |
|**C. 改 SillyTavern 源码**| 彻底解决 | 升级时会被覆盖,不推荐 | ⭐ |

---

## 详细安装教程(推荐方案 B)

### 第 1 步:打开扩展安装界面

进入 SillyTavern 后,点击**右上角顶部栏的"扩展图标"**(三个堆叠方块,鼠标悬停会显示 "Extensions")。

在弹出的菜单中点击**"Install extension"** 或 **"安装扩展"**(取决于你的语言设置)。

> 💡 如果顶部栏没有看到这个图标,可以直接在浏览器地址栏的 URL 后加 `#extensions` 访问。

### 第 2 步:粘贴仓库地址

在弹出的输入框中粘贴:
https://github.com/sillytavern-zh/sillytavern-classic-wand

点击 **Save / 保存** 按钮。

### 第 3 步:启用扩展

安装完成后,在 **"Manage extensions"(管理扩展)** 列表中找到 **`Classic Wand Button`**,确认它的开关是**启用状态**(打钩或绿色)。

### 第 4 步:刷新页面

按 **F5** 或 **Ctrl + Shift + R**(强制刷新)。

完成 ✅

输入框左下角应该立刻出现 🪄 魔法棒按钮(在【三】汉堡菜单旁边)。

### 第 5 步:验证

点击 🪄 按钮,应该看到扩展菜单从按钮**正上方**弹出(打开数据库 / 附加文件 / 生成图片 / 词符计数器 等)。

跟 SillyTavern 1.16.x 时代的体验完全一致。

---

## 这个扩展安全吗?会影响其他功能吗?

完全安全。我们公开了完整源代码:

-**核心代码**: 1 个 CSS 规则 + 30 行 JS
-**总大小**: < 2 KB
-**修改范围**: 仅强制显示按钮,**不修改 SillyTavern 任何业务逻辑**
-**协议**: MIT(可自由审计、修改、分发)

[GitHub 仓库](https://github.com/sillytavern-zh/sillytavern-classic-wand)
css
/整个扩展的核心就是这几行 CSS/

extensionsMenuButton {
display: flex !important;
width: auto !important;
height: auto !important;
visibility: visible !important;
opacity: 1 !important;
}

---

## 常见问题

### Q1: 安装后按钮还是没出现?

1.**强制刷新页面**: Windows `Ctrl+Shift+R` / Mac `Cmd+Shift+R`
2.**清浏览器缓存**: F12 → Network 标签 → 勾选 "Disable cache" → 刷新
3.**检查扩展是否启用**: Extensions → Manage Extensions → 看 `Classic Wand Button` 是否勾选
4.**重启 SillyTavern 服务**

### Q2: 任何 SillyTavern 用户都需要装吗?

是的,无论你是本地部署、Docker、还是用各种云端版,只要你在 SillyTavern 1.17.0+ 中**没看到左下角魔法棒**,就可以装这个扩展恢复。

### Q3: 升级 SillyTavern 后扩展失效?

进入 Extensions → Manage Extensions → 找到 `Classic Wand Button` → 点击【更新】按钮即可拉取最新版。

### Q4: 这个扩展未来会维护吗?

会。SillyTavern 中文教程站会跟进 SillyTavern 主要版本更新,确保兼容性。如果你发现 bug,直接在 [GitHub Issues](https://github.com/sillytavern-zh/sillytavern-classic-wand/issues) 反馈即可。

### Q5: 我能修改它吗?

当然!本扩展采用 MIT 协议,可自由使用、修改、分发。欢迎 PR。

---

## 总结

- 🪄 SillyTavern 1.17.0 的"按钮消失"是动态显示逻辑的副作用,不是 bug
- ⚡ 装本扩展 30 秒解决,永久生效
- 🔧 不修改 SillyTavern 核心代码,可装可卸
- 📦 [GitHub 仓库](https://github.com/sillytavern-zh/sillytavern-classic-wand) 开源,可审计

如果觉得有用,在 GitHub 给个 ⭐ 是最大的鼓励!

---

>**关于本文**: 由 SillyTavern 中文教程站维护,持续更新。如需引用请保留出处链接。

>**更多 SillyTavern 教程**: [guide.sillytavern.one](https://guide.sillytavern.one/)

>**遇到其他问题**: 查看 [故障排查分类](/troubleshooting/) 或加入 SillyTavern 社区讨论

---

## 📖 关于本文

- **原文**: [SillyTavern 1.17.0 升级后魔法棒按钮消失?一键修复](https://guide.sillytavern.one/troubleshooting/missing-wand-button-1170/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/troubleshooting/missing-wand-button-1170/) 为准。

---
title: "角色卡导入完整指南:从下载到第一次对话的全流程"
description: "SillyTavern 角色卡导入完整流程,含导入方法、备选问候语切换、导入失败 9 大原因排查。"
slug: import-guide
category: character-cards
canonical: https://guide.sillytavern.one/character-cards/import-guide/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/character-cards/import-guide/](https://guide.sillytavern.one/character-cards/import-guide/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

下载了角色卡却不知道怎么导入？导入了却发现头像是空的？或者点了"导入"什么反应都没有？这一篇把整个流程从头到尾梳理一遍。

## 导入前的准备

确认 3 件事：

1. SillyTavern 已经能正常打开
2. 已下载好角色卡文件（PNG 或 JSON）
3. API 已连接成功（不一定先连，但聊天时一定要有）

<div class="note">

**提示**:还没下载过角色卡的话,中文圈用 [SillyTavern 中文角色卡库](https://cards.sillytavern.one/) 比较顺手(精品向、中文卡为主、国内可访问),其他来源的优劣对比见 [角色卡是什么里的来源对比章节](/character-cards/what-is-character-card/)。第一次建议挑设定简单、第一句话清晰的卡,体验更顺。

</div>

## 方法一：通过界面按钮导入（推荐新手）

1. 打开 SillyTavern 界面
2. 点击左侧/顶部的**"角色"图标**（小人头）
3. 找到"**导入角色**"按钮（向下箭头图标）
4. 选中下载好的角色卡（.png 或 .json）
5. 等几秒，角色出现在列表里
6. 点击角色头像进入对话
7. 第一句话自动显示，开始聊

## 方法二：拖拽导入（更快）

SillyTavern 支持直接把文件拖进浏览器：

1. 打开角色列表页
2. 从文件夹把角色卡 PNG **拖到浏览器窗口**
3. 看到上传提示后松手
4. 角色出现在列表里

适合一次导入多张——选中多个文件一起拖即可。

## 方法三：从 URL 导入（适合云端版）

部分云端版本支持粘贴角色卡链接：

1. 复制角色卡的下载 URL
2. 在"导入角色"对话框找"从 URL 导入"
3. 粘贴 URL，点击导入

不是所有版本都支持，能用最方便。

## 导入成功后的常规操作

### 1. 检查头像
PNG 导入头像应该自动显示。JSON 的话头像位置可能空，需要手动上传。

### 2. 切换备选问候语
不少卡有多个开场剧情。对话框上方有"**下一个问候语**"箭头按钮，可以切换。

### 3. 阅读角色描述
第一次用一张新卡，**强烈建议看一眼角色描述**（点角色头像 → 编辑），了解：

- 角色背景
- "你"被设定为什么身份
- 有没有特殊场景设定

不然聊起来一脸懵。

### 4. 设置 Persona（你自己）
SillyTavern 里"你"也是有人设的，叫 Persona。可以设置自己的名字、简介，让 AI 更准确地称呼你。

说真的,导入失败 9 成情况都不是"卡有问题",是"文件下错了"。**先重新下载,比反复折腾效率高十倍**。

## 导入失败？9 大常见原因

| # | 问题 | 排查方式 |
|---|---|---|
| 1 | 文件不完整 | 看大小，正常 100KB~3MB |
| 2 | PNG 里没人设数据 | 有些只是张图，没塞数据 |
| 3 | 改名导致格式错 | 别随便改后缀 |
| 4 | JSON 格式被破坏 | 用文本编辑器打开检查，常见是被微信/QQ 转发后编码错乱 |
| 5 | 卡片版本太旧 | 老 v1 卡新版可能不支持 |
| 6 | 浏览器拦截上传 | 换浏览器或检查隐私扩展 |
| 7 | 云端限单文件大小 | 有的限 5MB 内 |
| 8 | 同名角色已存在 | 先删旧的 |
| 9 | 路径含特殊字符 | 文件名 emoji/中括号会出问题 |

<div class="tip">

**万能解法**：90% 的导入问题靠"**重新下载 + 重命名为纯英文 + 用 PNG 而不是 JSON**"解决。

</div>

## 导入成功但 AI 不像"那个角色"

大概率是你**没用预设**。先看 [《预设是什么》](/presets-lorebooks/what-is-preset/)。

不是角色卡的问题，大概率是：

1. **没用预设**：默认提示词太通用，AI 不会"演"
2. **模型不匹配**：有些卡为 Claude 调的，套 GPT 效果一般
3. **第一句话语境没接上**：你的回复完全脱离角色设定
4. **聊太久没总结**：上下文超长，AI 把人设忘了

这些会在专门的预设和长对话总结篇里讲。

## 导入完后的最佳实践

- **分类管理**：用酒馆自带标签给角色分类（恋爱/跑团/写作）
- **定期备份**：角色卡库越积越多，定期把整个 characters 文件夹打包
- **记录使用感受**：哪张卡配哪个预设最好，记下来
- **尊重原作者**：分享前看作者有没有规定"是否允许二改/转发"

---

## 相关阅读

- [角色卡到底是什么？](/character-cards/what-is-character-card/)
- [SillyTavern 是什么？](/getting-started/what-is-sillytavern/)

---

## 📖 关于本文

- **原文**: [角色卡导入完整指南:从下载到第一次对话的全流程](https://guide.sillytavern.one/character-cards/import-guide/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/character-cards/import-guide/) 为准。

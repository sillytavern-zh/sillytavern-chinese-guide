---
title: "酒馆名词速查表:Preset / Lorebook / Persona 一篇讲清"
description: "SillyTavern 常见英文术语速查:角色卡、预设、世界书、Persona、Token、Temperature、Top P、流式输出等核心概念一次讲清楚。覆盖新手最容易混淆的 20+ 名词,每个术语给出通俗解释、实际作用、和日常聊天的关系,边学边查的最快入门方式。"
slug: glossary
category: getting-started
canonical: https://guide.sillytavern.one/getting-started/glossary/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/getting-started/glossary/](https://guide.sillytavern.one/getting-started/glossary/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

SillyTavern 圈子里有一堆让新人头疼的英文术语。这一篇把它们一次性讲清楚，**遇到不懂的回来查就行**。

按使用频率从高到低排序。

群里看到不懂的词,回这里查就行,**别硬记**——用多了自然就熟。

## 一、核心概念

### Character Card（角色卡）
一张 PNG 图片或 JSON 文件，里面塞了 AI 的人设。详见 [《角色卡是什么》](/character-cards/what-is-character-card/)。

### Preset（预设）
一组提示词 + 参数的打包，决定 AI 的"灵魂质量"。**没预设和有预设的体验差 5 倍**。

### Lorebook / World Info（世界书）
背景设定的"数据库"。AI 聊到特定关键词时，对应设定会被自动注入提示词，让 AI 记住复杂世界观。

### Persona（你自己的人设）
SillyTavern 里"你"也是有人设的。可以设名字、外貌、性格，让 AI 更准确地称呼和理解你。

### Greeting / First Message（第一句话）
角色登场的开场白。决定了对话的初始场景。

## 二、技术名词

### API Key（密钥）
你访问 AI 模型的"通行证"。通常 `sk-` 开头的一长串。

### Endpoint / Base URL（端点）
API 服务的"地址"。酒馆里填的通常以 `/v1` 结尾，**不要写到 `/chat/completions`**。

### Token（词元）
AI 计费和计算的单位。1 token ≈ 0.5 个汉字 或 1 个英文单词。

### Context Length（上下文长度）
AI 一次能"看见"的最大文本量。常见值：
- Claude：200K（约 15 万汉字）
- Gemini：1M+（极长）
- GPT-4：128K

### Stream（流式输出）
开启后 AI 一边生成一边显示，体验更流畅。关闭后等全部生成完一次显示。

### Max Tokens（最大回复长度）
限制 AI 单次回复最多多长。设小了会截断，设大了浪费 token。

## 三、生成参数

### Temperature（温度）
控制随机性。**0.5 保守，1.0 平衡，1.5 创意**。

### Top P
另一种随机性控制。一般保持 0.9。

### Top K
候选词数量限制。Claude 和部分 Gemini 不支持，**设了会报错**。

### Frequency Penalty（频率惩罚）
降低重复。Claude **必须设 0**，否则报 500。

### Presence Penalty（存在惩罚）
鼓励引入新话题。Claude **也必须设 0**。

## 四、插件 / 扩展

### Tavern Helper / Tavern-Helper（酒馆助手）
社区里最流行的扩展底座，很多其他插件依赖它。

### Memory Enhancement（记忆增强）
让 AI 不再失忆的核心方案。把对话总结存到世界书，腾出上下文空间。

### TTS（语音合成）
把 AI 回复读出来。

### Regex Script（正则脚本）
对 AI 输入输出做自动处理。进阶玩法。

## 五、常见错误码

| 码 | 含义 | 怎么办 |
|---|---|---|
| 401 | 没授权 / Key 错 | 重新填 Key |
| 403 | 被禁 | 看是 IP 被封还是账户被封 |
| 404 | 模型不存在 | 检查模型名 |
| 429 | 限流 | 等一会，或换 Key |
| 500 | 上游错 | 看 [《Valid 但 500 排查》](/troubleshooting/valid-but-500/) |
| 502 | 渠道炸了 | 换渠道或等修复 |

## 六、常被搞混的词

- **Preset ≠ Persona**：预设是 AI 怎么说话，Persona 是你是谁
- **Lorebook ≠ Description**：世界书是按关键词动态注入，Description 是角色卡里固定塞进去的
- **API Key ≠ 模型名**：Key 是你的通行证，模型名是你点的菜

---

## 相关阅读

- [SillyTavern 是什么](/getting-started/what-is-sillytavern/)
- [预设是什么](/presets-lorebooks/what-is-preset/)

---

## 📖 关于本文

- **原文**: [酒馆名词速查表:Preset / Lorebook / Persona 一篇讲清](https://guide.sillytavern.one/getting-started/glossary/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/getting-started/glossary/) 为准。

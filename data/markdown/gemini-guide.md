---
title: "Gemini 全家桶解析:Flash 和 Pro 的真实差异"
description: "Gemini 系列完整选型指南。Flash 性价比之王、Pro 中端主力、Ultra 为何不推荐、空回复反截断完整解决方案、100 万 token 上下文的妙用。覆盖参数避雷、Safety Settings 完整禁用、长上下文跑团 / 长篇小说写作技巧、跟 Claude / GPT 的真实差异。"
slug: gemini-guide
category: ai-models
canonical: https://guide.sillytavern.one/ai-models/gemini-guide/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/ai-models/gemini-guide/](https://guide.sillytavern.one/ai-models/gemini-guide/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

Google 的 Gemini 在最近这两年突飞猛进。从最初被吐槽"不如 GPT-3.5"到现在成为很多重度玩家的主力——尤其是**写长篇的**。

但 Gemini 也是脾气最古怪的——你以为它跑得好好的,它突然给你来一个空白回复。

这一篇讲清楚 Gemini 全家桶的差异、什么时候用、怎么用对。**具体版本号每隔几个月会更新,本文不写死任何版本号——以你用的当时最新版为准**。

## 产品分档(长期稳定)

Gemini 的产品分档比较稳定:

- **Gemini Flash 模型**(及更轻量的 Flash-Lite):轻量、快、便宜
- **Gemini Pro 模型**:平衡档(对应 Claude Sonnet 那个层级)
- **Gemini Ultra / Advanced 模型**(部分版本叫这个):旗舰

版本号会细分多代——但**直接用最新一代**。Google 的迭代速度很快,新版几乎全方位优于旧版。

## Gemini 最强的特点:长上下文

Gemini 系列从早期开始就以"上下文长"著称。**当前主流的 Pro 和 Flash 都已经达到百万 token 级别**(约 75 万中文字)。

这意味着:**够你聊几个月不用做总结**。

这是 Gemini 在长篇连载场景下被推崇的根本原因——你不必频繁停下来做记忆管理,可以一直往下写。

## Gemini Flash 模型:性价比之王

如果你刚接触 AI 角色扮演,**Gemini Flash 模型** 是值得第一个尝试的:

- **极便宜**(便宜到几乎是免费的)
- **速度极快**(回复几乎瞬时)
- 文笔能用(不算精致但不假)
- 上下文长

**什么场景用 Flash**:

- 新手入门,先跑通流程
- 日常聊天,不太追求文笔
- 想试不同的角色卡,但不舍得花 Claude 的钱
- 做总结、做翻译(性价比无敌)

**Flash 的弱点**:

- 复杂心理刻画不如 Claude Sonnet
- 偶尔会犯逻辑错误
- 对复杂世界书的处理有时不到位

某些版本还有更轻量的 Flash-Lite,价格更低,速度更快——适合做大批量自动化任务。

## Gemini Pro 模型:中端主力

**Gemini Pro 模型** 是当前 **Claude Sonnet 模型** 最大的竞争者。

- 文笔明显比 Flash 好
- 上下文长度和 Sonnet 同档(都是百万级)
- 价格友好(通常是 Sonnet 的 1/2 - 2/3)

**什么场景用 Pro**:

- 你写长篇连载,需要保留大量历史对话
- 你的角色卡和世界书加起来 30K+ 字
- 你想用 Claude 但预算紧

**Pro 的弱点**(也是 Gemini 全系的问题):

- 偶尔空回(后面专门讲)
- 流式输出处理不稳定
- 对反审查相对严

## Gemini Ultra/Advanced 模型:为什么不一定推荐

Gemini 旗舰版价格逼近 Claude Opus,但综合表现:

- 长上下文还是强(继承全家桶优势)
- 写作质量比 Pro 提升不明显(差距小)
- 多模态(理解图片、3D 等)是真亮点

**如果你只做角色扮演**:Pro 已经足够,旗舰版性价比反而不如 Pro。
**如果你做多模态**(自动配图、图片识别等):旗舰版才能体现差距。

## Gemini 的脾气:你必须知道的问题

### 1. 空回复

最让人崩溃的现象:

- 你发一句话
- AI 回复了个空白
- 你重发,还是空白

**原因复杂**,包括:

- 内容触发审查(Gemini 内容审核相对严)
- 流式输出代理断裂
- 模型自己判定停了

**解决方案**:

- 关闭流式输出(关掉 Stream)
- 重新生成一次(80% 概率好转)
- 检查内容是否敏感
- 备用模型顶上

### 2. 反截断必须做

Gemini 比 Claude 更容易"中途停"。

**预设里必须有反截断指令**,大致内容:
> 不要中途停止回复。完整地表达你的想法,即使内容很长。
> 不要以问号、删节号或开放式结尾结束。

### 3. 关闭 Stream 是金科玉律

**几乎所有 Gemini 用户都开非流式**。空回复 / 截断的全套排查见 [《AI 回复空白 / 截断》](/troubleshooting/empty-truncated/)。流式带来的体验提升,远不如它带来的稳定性损失。

## Penalty 参数怎么设

跟 Claude 不同,**Gemini 支持 Frequency / Presence Penalty**。

- Frequency Penalty: 0.1-0.2(防重复)
- Presence Penalty: 0.1-0.25(鼓励新内容)
- Temperature: 1.0-1.2
- Top P: 0.9
- Top K: 40-50(Gemini 支持,Claude 不支持)

## 国内怎么用 Gemini

跟 Claude 一样:

- 官方需要 Google 账号、海外 IP、海外信用卡
- 95% 中文玩家走中转

中转价格比 Claude 便宜很多,**这也是 Gemini 在国内特别流行的原因之一**。

**长上下文场景特别提醒**:Gemini 的上下文虽然长,但按量计费下,长上下文 token 成本会快速堆高。**如果你经常使用 50 万+ token 的对话,强烈建议选按次计费的渠道**,详见 [按次 vs 按量计费](/api-config/pricing-models/)。

## 老版本还能用吗?

可以。Gemini 老版本(比如 Pro 系列的上一代)通常:

- 价格更便宜
- 中转商支持更广
- 预设和反截断方案适配更成熟

**实战经验**:除非新版有重大功能突破,老版本通常更稳。

## 选型方法论

- **日常使用、长篇连载**:**Gemini Pro 模型**(主力)
- **极致文笔关键剧情**:切到 Claude Sonnet/Opus
- **总结/翻译/批处理**:**Gemini Flash 模型** / Flash-Lite
- **主渠道挂了的备份**:多备一个中转商

**新人推荐**:Flash 起步,Pro 升级。

## 相关阅读

- [Claude 全系深度指南](/ai-models/claude-guide/)
- [2026 主流 AI 模型横评](/ai-models/comparison-2026/)
- [按次 vs 按量计费完整对比](/api-config/pricing-models/)
- [AI 回复空白 / 截断完整排查](/troubleshooting/empty-truncated/)

---

## 📖 关于本文

- **原文**: [Gemini 全家桶解析:Flash 和 Pro 的真实差异](https://guide.sillytavern.one/ai-models/gemini-guide/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/ai-models/gemini-guide/) 为准。

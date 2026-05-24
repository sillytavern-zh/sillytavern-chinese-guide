---
title: "Claude 全系深度指南:Sonnet / Opus / Haiku 怎么选"
description: "Claude 在中文角色扮演中为什么是顶端选择?Sonnet、Opus、Haiku 三档对比、参数避雷、反审查表现、国内中转方案全解。覆盖 Sonnet 性价比平衡、Opus 顶级写作、Haiku 速度优先的场景选择,带 prompt 优化技巧、反审查 jailbreak 现状、国内中转 + 直连方案完整对比。"
slug: claude-guide
category: ai-models
canonical: https://guide.sillytavern.one/ai-models/claude-guide/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/ai-models/claude-guide/](https://guide.sillytavern.one/ai-models/claude-guide/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

中文圈玩 AI 角色扮演,**Claude 系列长期是社区公认的文笔天花板**。

理由不是"它最强",而是它最适合中文创作:文笔自然、不假大空、能写长篇、对复杂角色心理刻画细腻。

但 Claude 也是新手最容易踩坑的——你不懂它的"脾气",参数填错直接给你 500/422 报错。

这一篇把 Claude 系列讲透。注意:**具体的版本号会随时迭代**(每隔几个月就有新版),本文不写死任何具体版本号——以你用的中转商或官方当前的最新版为准。

## Anthropic 的产品分档(长期不变)

Claude 一直保持三档结构(过去几年都没变过,未来 1-2 年也不太可能变):

- **Claude Haiku 模型**:轻量档,速度快,价格便宜
- **Claude Sonnet 模型**:平衡档,大多数玩家的主力
- **Claude Opus 模型**:旗舰档,最强,贵,但偶尔出乎意料的好

你点开任何一个中转商的模型列表,基本能看到这三档的当前最新版。**直接选最新版的 Sonnet 起步,90% 不会错**。

## Claude Sonnet 模型:最推荐给新手

如果你刚开始,直接用 **Claude Sonnet 模型**。

**理由**:

- 文笔够好(应付 90% 角色扮演场景)
- 价格中等(Opus 的 1/5 左右,Haiku 的 3 倍左右)
- 反审查相对宽松(比 OpenAI 好很多)
- 上下文很长(当前主流已达数十万到百万 token 级)

**Sonnet 的强项是细腻**。同一段剧情让 Sonnet 写,角色情绪的转变、动作的细节、心理的层次,都比其他同价位模型出色。

**Sonnet 的弱点**:对 Prompt 工程敏感。同样的角色卡和预设,在 Sonnet 上能跑出 90 分,换到别的模型可能只有 70 分——**但前提是你得用对预设**。

## Claude Opus 模型:重度玩家的选项

**Claude Opus 模型** 是 Claude 系列的旗舰。文笔比 Sonnet 再细一档——尤其在:

- 写长篇连载(单次输出几千字毫无压力)
- 复杂角色心理(双重人格、矛盾情感这种)
- 跨章节剧情一致性

**但 Opus 贵**,通常是 Sonnet 的 3-5 倍价。日常聊天没必要上。

**什么时候用 Opus**:

- 你在写一个长篇小说的关键章节
- 你想要最高质量的角色扮演体验,不在乎成本
- Sonnet 写出来的你觉得"还差一口气"

**如果你是新人,别一上来就 Opus**。先用 Sonnet 跑顺,熟练了再决定要不要升级。

## Claude Haiku 模型:不推荐用于角色扮演

便宜是真便宜,大约是 Sonnet 的 1/3 价格。但是:

- 文笔明显粗糙
- 复杂剧情容易跑偏

**Haiku 适合**:批量处理、做总结、做翻译、做数据提取。

**Haiku 不适合**:你坐下来跟一个虚拟角色谈感情。

## Claude 的"地雷":这些参数一定要设对

这是 Claude 用户**最常翻车**的地方。

### Frequency Penalty 必须 = 0

不是"调小",是**设 0**。Claude API 完全不支持这个参数,你设 0.1 它都给你 500/422。

### Presence Penalty 必须 = 0

同上。

### Repetition Penalty 必须 = 0 或留空

同上。**这是社区里 500 错误最高频的来源之一**——很多预设默认 `repetition_penalty=1.05`,在 OpenAI 上没事,套到 Claude 直接崩。

### Top K 别填

Claude 也不支持 Top K。让酒馆默认就行,不要手动设。

### Temperature 1.0 起步

Claude 的温度感比 OpenAI 更敏感。

- 0.5-0.7:回答会偏保守、机械
- 1.0:平衡(推荐)
- 1.2-1.5:更有创意,但偶尔脱戏
- 超过 1.5:基本失控

### Top P 0.9 经典值

不要乱改。

## Claude 的反审查表现

这是大家最关心的。

实话说:**Claude 的反审查不是"无限"**。它有内容边界,涉及极端内容时会拒绝(回复 "I cannot")。

但相比 OpenAI:

- Claude 容忍度高得多
- 通过合理的预设,**绝大多数成人向角色扮演场景都能跑通**
- 不会无端弹"作为一个 AI..."的废话

**什么情况下 Claude 也会拒绝**:

- 涉及未成年
- 极端暴力的细节描写
- 真实人物的诽谤

这些是底线,任何商用 AI 都拒。

## 国内怎么用 Claude

### 直接用 Anthropic 官方

- 注册需要海外身份
- 信用卡要海外卡
- 需要梯子
- 充值要美金

**95% 中文玩家走中转**:

- 各种中转商把 Claude 转卖给你
- 价格通常比官方贵 10-30%
- 不需要梯子(中转商有海外服务器)
- 用人民币付款

### 挑中转商

- 别贪便宜(过低价格 = 转卖共享 Key,随时崩)
- 看运营时长(超过 1 年的相对靠谱)
- 看群活跃度
- 关注计费方式:重度长上下文用户考虑按次计费的渠道,详见 [按次 vs 按量计费完整对比](/api-config/pricing-models/)

## 老版本还能用吗?

看情况。

官方旗舰版迭代很快——每隔 3-6 个月就有新版。但老版本不会立即下线,通常还能用一段时间。

**实战经验**:

- 老版本通常便宜(中转商清库存)
- 新版本质量略好但价格高
- 老版 Sonnet 和新版 Sonnet 的差距,**不像营销宣传里那么夸张**

**新人不必追逐最新**:用一个稳定运行 6 个月以上的版本反而更稳。等中转商和预设都适配了再升级。

## 选型方法论

不绑死版本,只看类别:

- 日常 90% 用 **Claude Sonnet 模型**(任何当前最新版)
- 长篇关键章节切到 **Claude Opus 模型**
- 做总结、翻译、批处理切 **Claude Haiku 模型**
- 配 1 个备用渠道防主渠道炸

**新人参考**:先 Claude Sonnet 模型,熟练后再说。

## 相关阅读

- [按次计费 vs 按量计费完整对比](/api-config/pricing-models/)
- [Gemini 全家桶解析](/ai-models/gemini-guide/)
- [2026 主流 AI 模型横评](/ai-models/comparison-2026/)
- [自定义 API 端点配置](/api-config/custom-api-setup/)
- [Temperature / Top P / Top K 参数详解](/presets-lorebooks/temperature-topp/)

---

## 📖 关于本文

- **原文**: [Claude 全系深度指南:Sonnet / Opus / Haiku 怎么选](https://guide.sillytavern.one/ai-models/claude-guide/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/ai-models/claude-guide/) 为准。

---
title: "世界书入门:让 AI 记住你的整个世界"
description: "SillyTavern 世界书 (Lorebook) 完整入门。讲解条目、关键词、激活策略、插入位置 5 个核心概念,从零创建第一个能用的世界书。覆盖正则关键词、连锁触发、深度策略、Token 预算控制、跟主提示词的优先级关系,让 AI 跨百万字记住整个世界设定。"
slug: lorebook-basics
category: presets-lorebooks
canonical: https://guide.sillytavern.one/presets-lorebooks/lorebook-basics/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/presets-lorebooks/lorebook-basics/](https://guide.sillytavern.one/presets-lorebooks/lorebook-basics/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

角色卡能让 AI 变成一个人，**世界书能让 AI 知道整个世界**。

这一篇带你从零理解世界书，做出第一个能用的世界书。

## 世界书是什么

> 世界书（Lorebook / World Info）是一套**按关键词触发的背景知识库**。

举个例子：

- 角色卡只能塞固定字数的人设
- 但如果你的故事涉及 50 个 NPC、20 个地点、10 项魔法系统呢？
- 全塞进角色卡 → 上下文爆炸，关键信息被挤掉
- **世界书的解决方案**：当对话提到"魔法塔"时，自动注入魔法塔的设定；不提就不占空间

## 5 个核心概念

### 1. 条目 (Entry)
世界书里的最小单位。一个条目 = 一段背景知识。

### 2. 关键词 (Key)
触发条目的"暗号"。AI 看到关键词就调出对应条目。

### 3. 激活策略 (Strategy)

| 策略 | 说明 | 适用 |
|---|---|---|
| 蓝灯 (Constant) | 永远生效 | 全局世界观、大总结 |
| 绿灯 (Normal) | 关键词出现在最近 N 条消息时激活 | 角色信息、地点描述 |
| 黄灯 (Selective) | 关键词出现在整个聊天历史时激活 | 罕见但重要的事件 |
| 红灯 | 禁用 | 暂时不用的条目 |

### 4. 插入位置 (Position)
条目在最终提示里被放在哪里。常用 `@D` 表示"在系统消息处"。

### 5. 扫描深度 (Scan Depth)
查多少条最近消息找关键词。一般 3-5。设太大浪费 token，太小可能错过。

## 创建第一个世界书

假设你想做"修仙世界"的世界观。

### Step 1：新建
顶部「世界书」图标 → 「新建」→ 起名"修仙世界"。

### Step 2：全局设定（蓝灯）

- **标题**：世界总观
- **内容**：这是一个修真大世界，凡人通过修炼可以从练气、筑基一直晋升到仙人...
- **关键词**：（留空）
- **策略**：蓝灯 (Constant)
- **位置**：@D
- **优先级**：9999

蓝灯条目永远生效，作为整个世界的"宪法"。

### Step 3：地点（绿灯）

- **标题**：青云宗
- **内容**：青云宗位于大陆中央，十大正派之首，掌门玄真子...
- **关键词**：青云宗, 玄真子
- **策略**：绿灯
- **扫描深度**：5

只在对话提到"青云宗"或"玄真子"时才激活。

### Step 4：角色背景（绿灯）
为重要 NPC 单独建条目，关键词覆盖角色的多种叫法（"林浅雪 / 大师姐 / 雪姐"一起放）。

### Step 5：测试
回到对话，提到关键词，看 AI 是否能正确引用设定。

## 调优技巧

### 用蓝灯沉淀核心设定
最重要的 1-3 条用蓝灯。

### 用绿灯控制按需注入
能用绿灯就别用蓝灯，**省 token 就是省钱**。

### 关键词覆盖多种叫法
"林浅雪 / 大师姐 / 雪姐 / 寒月剑主" 一起放，确保不漏触发。

### 优先级排序
多个条目同时触发时，优先级高的先注入。

### 定期审查长度
一条建议 200-500 字，过长拆成多条。

## 常见错误

| 错误 | 解决 |
|---|---|
| 关键词写错或太罕见 | 多准备几个同义词 |
| 全用蓝灯导致上下文爆炸 | 大部分应该用绿灯 |
| 条目太长 | 拆分提炼 |
| 没启用世界书 | 在右上角勾选启用 |
| 关键词包含标点 | 改成纯文本 |

## 用世界书 + 总结组合解决长对话失忆

世界书的另一个最常用场景是**配合总结使用**——把超长对话的关键剧情存进世界书。详见 [《长对话失忆终极解决方案》](/advanced/long-chat-summary/)。

## 一个新手最大的误区

世界书是新手最容易"过度设计"的地方。**先做 5 条用半个月,再考虑要不要扩**。一上来写 50 条,十有八九是浪费。

> "世界书写得越多越好"

**完全相反**。一个 100 条精炼的世界书 ≠ 一个 500 条冗余的世界书。

**少而准，胜过多而乱**。

---

## 相关阅读

- [预设是什么](/presets-lorebooks/what-is-preset/)
- [长对话总结技巧](/advanced/long-chat-summary/)

---

## 📖 关于本文

- **原文**: [世界书入门:让 AI 记住你的整个世界](https://guide.sillytavern.one/presets-lorebooks/lorebook-basics/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/presets-lorebooks/lorebook-basics/) 为准。

---
title: "群聊模式入门:让多个 AI 角色同台演出"
description: "SillyTavern 群聊 (Group Chat) 完整入门。创建群聊、配置发言策略、多角色互动技巧、常见问题与让群聊活起来的秘诀。"
slug: group-chat
category: advanced
canonical: https://guide.sillytavern.one/advanced/group-chat/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/advanced/group-chat/](https://guide.sillytavern.one/advanced/group-chat/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

单角色聊久了无聊？**让多个角色同台演出**才是真精彩。

这一篇带你玩转 SillyTavern 的群聊功能。

## 群聊是什么

> 群聊（Group Chat）让你**同时和多个 AI 角色对话**。

适合场景：

- 三人小队冒险
- 朋友圈聚会
- 跑团多 NPC 互动
- 多角度剧情（主角 + 配角 + 反派同台）

群聊上手不难,**但要让它"活起来"是另一回事**。耐心比技巧重要。

## 创建群聊

### Step 1：新建群组
顶部「角色」图标 → 找「Create New Chat Group」（或类似按钮）。

### Step 2：命名 + 选成员

选成员前最好有几张状态正常的[角色卡](/character-cards/what-is-character-card/),没有的先去导入。

- 给群组起个名字（比如"修仙小队"）
- 从已有角色卡里勾选要加入的（**2-5 个最佳**，太多会乱）

### Step 3：配置发言策略

| 策略 | 说明 |
|---|---|
| 自然 (Natural) | AI 自己判断该谁说 |
| 列表 (List) | 按列表顺序轮流 |
| 手动 (Manual) | 你决定让谁说 |

新手推荐**手动模式**，你能控制每一句谁来说。

## 群聊里的角色互动

### 让角色之间对话（不通过你）
你输入旁白：

> 林浅雪转头看向小师弟："你也觉得师叔说得不对？"

然后**让小师弟先说**，再让林浅雪回应。AI 之间会接话。

### 旁白模式
有些场景**你不想说话，只想看角色互动**：

- 切到"旁白模式"
- 你描述场景："他俩在凉亭里下棋，棋盘上的局势越来越紧"
- 让两个角色自己接戏

### 让某个角色"暂时离场"
不想他参与某段剧情：

- 在他名字旁的设置里"暂时禁用"
- 等剧情需要他时再启用

## 多角色互动技巧

### 1. 设计角色冲突
没有冲突的群聊**很无聊**。设计：

- 师姐 vs 师妹：暗中较劲
- 主角 vs 反派：立场对立
- 文官 vs 武将：理念差异

### 2. 用旁白推动剧情
群聊容易陷入"互相寒暄"：

- 适时插入旁白触发事件
- "突然敲门声响起"
- "她注意到桌上的信"

### 3. 给每个角色独立的语气

- A 用"欸""哈哈"
- B 用"在下""见过"
- C 用"...嗯""略"

让你能不看名字就分清楚谁在说。

### 4. 分场景而不是全员一直在场
现实里不可能 5 个人时刻在场。**写场景切换**：

- "一个时辰后，只剩林浅雪和你在禅房"
- 让某些角色"离场"，让 1-2 个角色独占当前剧情

## 群聊常见问题

### 问题 1：角色互相重复
**原因**：上下文紧张，AI 抄前面的说法
**解决**：总结 + 减少同时上场角色 + 加强反重复指令

### 问题 2：角色说话方式串了
**原因**：AI 没区分清楚谁是谁
**解决**：

- 检查每个角色卡的"说话风格"
- 在系统提示里强调"角色之间风格不能混"
- 用更强的预设

### 问题 3：总是一个角色独占
**原因**：你给那个角色发了太多专属内容
**解决**：切手动模式，主动给沉默的角色发言机会

### 问题 4：剧情卡住不推进
**原因**：AI 怕推进得太快
**解决**：你来当"推动者"，用旁白制造事件

## 一个让群聊"活起来"的秘诀

**写一个共同事件，让所有人卷入**：

- "突然外面传来惊呼"
- "桌上的信散落一地"
- "门外有马蹄声急促接近"

你不直接对某个人说话，而是**抛一个事件**。所有角色都会自然反应，这才像真群聊。

---

## 相关阅读

- [角色卡是什么](/character-cards/what-is-character-card/)
- [世界书入门](/presets-lorebooks/lorebook-basics/)

---

## 📖 关于本文

- **原文**: [群聊模式入门:让多个 AI 角色同台演出](https://guide.sillytavern.one/advanced/group-chat/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/advanced/group-chat/) 为准。

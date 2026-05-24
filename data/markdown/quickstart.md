---
title: "30 分钟极速上手:从零到第一次 AI 对话"
description: "SillyTavern 新手 30 分钟极速上手。5 步走完:选部署方式、获取 API、配置连接、导角色卡和预设、第一次对话。失败率 70% 源于模型名错,每一步附精准排查跳转。包含 HowTo 结构化步骤、错误现象 → 跳转 ID 的完整诊断地图,小白也能不卡壳通到第一次 AI 对话。"
slug: quickstart
category: getting-started
canonical: https://guide.sillytavern.one/getting-started/quickstart/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/getting-started/quickstart/](https://guide.sillytavern.one/getting-started/quickstart/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

# 30 分钟极速上手:从零到第一次 AI 对话

> **一句话答**:5 步搞定 —— 选部署方式 → 拿 API → 配端点 → 导角色卡 → 开始对话。第一次失败?**70% 是模型名写错**、15% 是端点少了 `/v1`、10% 是 Key 余额为 0,剩下 5% 各种小事。
>
> **关键事实**:
>
> - 平均耗时 30 分钟(云端新手)/ 60-90 分钟(本地部署)
> - 不会代码也能跑通,关键是**别跳过任何一步**
> - 每一步都有明确的失败跳转,卡住别硬耗
> - 学会后 80% 的日常使用都不用再查教程

---

想一次跑通酒馆,但群里的教程动辄上万字,越读越晕。

说实话,30 分钟确实够。**前提是:每一步别耗超过 5 分钟**。

卡住了立刻按错误去查对应文章,不要在同一个屏幕上瞪 10 分钟。这是酒馆社群里失败最常见的原因——**在同一个坑里死磕**。

这篇按分钟拆,每一步都有"如果卡住去哪"的跳转。

## 流程总览(先花 2 分钟看)

| 步骤 | 时间 | 做什么 | 最容易失败 |
|---|---|---|---|
| Step 1 | 0-5 min | 决定用云端还是本地 | 选错路径浪费 1 小时 |
| Step 2 | 5-10 min | 准备 AI API(endpoint/key/模型名) | 模型名拼错、少 /v1 |
| Step 3 | 10-15 min | 在酒馆里配 API | 连上了但发消息 500 |
| Step 4 | 15-20 min | 导入第一张角色卡 | 格式 / NSFW 模型拒绝 |
| Step 5 | 20-25 min | 加一个预设 | 导入后没激活 |
| Step 6 | 25-30 min | 第一次对话 + 调试 | AI 空回或复读 |

**最重要的原则**:**云端新手 ≠ 本地新手**。两条路的学习曲线不一样,先选对再上路。

---

## Step 1(0-5 min):决定云端 or 本地

这 5 分钟决定的不是"今天跑多久",而是**接下来 1 周的体验**。

### 3 问决策树
问 1:你懂点命令行操作吗?

不懂 → 直接去云端,不要犹豫
懂一点 → 问 2
问 2:你希望数据完全在自己电脑?

完全在本地 → 选本地
不介意在服务商手里 → 问 3
问 3:你每天会用酒馆超过 1 小时吗?

很少 → 云端
高频 → 两条路都行,云端省心
**90% 新手结论**:**选云端**。

### 推荐云端服务

**云端版部署**:第三方搭好的 SillyTavern 网页版,注册登录直接用,中文圈和海外都有多家在运营。

- 优势:注册登录就能用 / 跨设备同步 / 内置 API 免费额度 / 手机浏览器完美
- 劣势:数据在服务商那里(非常介意隐私的人跳本地)

### 本地部署条件

**同时满足下面 3 条**才值得走本地:

1. 你会基础命令行(能执行 `npm install` 这种)
2. 你的电脑长期开机(不是手机,不是合盖即关的笔记本)
3. 你愿意自己解决端口冲突、防火墙、跨设备同步等问题

任何一条不满足,**立刻换云端,不要浪费时间**。

详细:[云端 vs 本地完全对比 →](/getting-started/cloud-vs-local/)

### 时间节点

Step 1 应该在 **0-5 分钟**搞定。如果你用了 10 分钟还在纠结,**先选云端**,以后想改再说。

---

## Step 2(5-10 min):准备 AI API

这一步本质是搞清楚 3 件东西:

1. **API Endpoint**(AI 服务器地址,通常以 `/v1` 结尾)
2. **API Key**(你的身份凭证,通常以 `sk-` 开头)
3. **模型完整名称 / slug**(AI 型号代号,具体格式取决于服务商,以服务商当前文档为准)

这 3 样东西是 90% 失败的源头。**每一个都要对**。

### 3 种 API 来源

#### 方案 A:站内免费模型(最简单,新手首选)

很多在线版部署服务给注册用户内置了一些免费额度的模型,登录后直接能用,完全不用自己接 API。

优点:0 配置、账号即 API、免费额度够日常轻量聊天。
适合:第一次体验、不想花钱、测试酒馆值不值得深入。

#### 方案 B:官方 API(最稳定但贵)

去 OpenAI / Anthropic / Google Cloud 官网注册账号,绑卡,申请 API Key。

- 优点:最稳定、最新模型最快出现
- 劣势:国内访问需代理、绑卡审核可能卡住、按 token 计费

适合:有外币卡、海外用户,或重度使用 + 不差钱。

详细:[API Key 完整指南 →](/api-config/api-key-guide/)

#### 方案 C:中转商(国内最实用)

国内第三方聚合平台,一个 Key 能用所有主流模型,通常按量或按包月付。

- 优点:国内直连稳定、一 Key 通用、比官方便宜
- 劣势:服务商质量参差,需要挑

### 拿到 3 样东西后怎么记

建议你开个记事本,写下:
endpoint: https://xxx.com/v1
key: sk-xxx…xxx
model: 你的服务商文档里列出的完整 slug

**关键细节**:
- endpoint 必须 `/v1` 结尾,**不是** `/v1/`,不是 `/v1/chat/completions`
- key **整串复制,不要有多余空格或换行**
- 模型名**完全抄官方或中转商文档**,不要自己脑补

### 时间节点

5-10 分钟。卡住 8 分钟以上?**换 Plan A 站内免费模型,先跑通再说**。

---

## Step 3(10-15 min):在酒馆里配 API

酒馆界面左上角有一个**插头图标 🔌**,点它。

### 9 步精确配置

1. **API**:下拉选 **"Chat Completion"**
2. **Chat Completion Source**:选 **"Custom (OpenAI-compatible)"**
3. **Custom Endpoint (Base URL)**:填 Step 2 记下的 endpoint(以 `/v1` 结尾)
4. **Custom API Key**:填 key(不要带 `Bearer ` 前缀)
5. 点 **"Connect"**,看右上角状态
6. **绿色 valid**:✅ 连上了,继续下一步
7. **红色 invalid**:❌ endpoint 或 key 有一个错了,**回 Step 2 重查**
8. 连上后,在 **"Available Models"** 下拉里找你的模型 slug
9. 找不到?手工在 **"Custom Model"** 输入框里填模型完整名

**第 9 步是 90% 的人栽在这里**——模型名多一个空格、中英文标点混用、版本号记错、复制时截断,都会导致后面 500。

### 保存配置(强烈建议)

- 右上角 **"Save Preset"**(⋮ 菜单里)→ 起个名,比如 `gpt4o-试用`
- 以后切换模型只需要换 preset,不用重填

### ⚠️ 如果这一步不顺

| 症状 | 跳转到 |
|---|---|
| 连接测试 invalid | 检查 endpoint 和 key 是否 100% 准确 |
| 连接 valid,发消息却 500 | [Valid 但 500 完整排查](/troubleshooting/valid-but-500/) |
| 各种奇怪错误码 | [错误码速查表](/troubleshooting/error-codes/) |
| AI 回复空白或被截断 | [空回复排查](/troubleshooting/empty-truncated/) |

详细 9 步:[自定义 API 端点完整配置](/api-config/custom-api-setup/)

### 时间节点

10-15 分钟。配不上别死磕,直接用上面跳转。

---

## Step 4(15-20 min):导入第一张角色卡

酒馆没有角色卡 = 没有演员。必须导一张。

### 去哪下载

角色卡来源比较多。中文圈常用 [SillyTavern 中文角色卡库](https://cards.sillytavern.one/)(精品向、中文卡为主、国内访问快),海外最大的是 [chub.ai](https://chub.ai)(百万级但鱼龙混杂、以英文为主),完整对比见 [角色卡是什么](/character-cards/what-is-character-card/)

推荐新手先试这几类(新手友好型):
- 热门常驻榜前 10 的任意一张(群里和社区口碑好,不容易出问题)
- 带 `friendly` / `original` tag 的卡
- **避免 NSFW 卡**(如果你用 Claude 官方 API,内容会被拒绝,新手容易误以为"酒馆坏了")

### 5 步导入

1. 在 cards 站找到一张卡,点 **"导入到聊天室"** 或下载 PNG
2. 回到酒馆,点**左侧角色栏**(人物图标)
3. 点 **"Import"**(上传图标)
4. 拖入或选择刚才下载的 PNG
5. 导入成功后**点击卡片头像**激活,它会变成当前角色

### ⚠️ 常见错误

- **Invalid character card** → 文件损坏或格式不对,换一张
- **File size too large** → 酒馆默认 2MB 限制,压缩 PNG 或换一张
- **导入后聊天栏空白** → 没点击激活,回左边栏再点

详细:[角色卡导入完整指南](/character-cards/import-guide/)

### 时间节点

15-20 分钟。这步通常最快,1-2 分钟能搞定。

---

## Step 5(20-25 min):加一个预设

很多人这一步想省,直接跳到 Step 6。**结果是 AI 回复又干又呆,像客服**。

预设决定 AI 的**文风、纪律和输出格式**。没预设 = 裸调用 AI,效果会差一整个档次。

### 预设从哪来

- 各家在线版部署服务有时附带预设分享区
- 角色卡作者的附带分享(不少作者会推荐专配预设)
- Discord / QQ 群的分享

### 3 步导入

1. 酒馆左上角 **🎚 图标**(Sampling 面板)
2. 右侧 **⋮ → Import Preset**
3. 选下载的 JSON 文件,**导入后必须从下拉里选中这个预设**才生效

### 怎么判断预设好不好

- 看作者说明是给哪个模型优化的(Claude 预设用在 GPT 上可能不灵)
- 发第一条消息,看 AI 回复的:
  - 长度(太短 = 预设可能没激活)
  - 文风(如果和角色卡设定不符,换预设)
  - 是否会"自我报告"(比如"作为 AI 助手..."这种 = 预设没压住)

### ⚠️ 常见错误

- **导入后忘了激活**:重新回 Sampling 面板,预设下拉必须显示你刚导的名字
- **预设和模型不匹配**:Claude 预设在 Gemini 上可能效果很怪
- **参数冲突**:Claude 禁止 `repetition_penalty` 非默认值,用 Claude 时必须保持默认,否则 500

详细:[预设是什么,怎么选](/presets-lorebooks/what-is-preset/) · [参数详解](/presets-lorebooks/temperature-topp/)

### 时间节点

20-25 分钟。

---

## Step 6(25-30 min):第一次对话 + 调试

万事俱备。在角色卡当前激活的状态下,发第一条消息试试。

### 正常流程

1. 底部对话框输入第一句(比如"hello")
2. 按 Enter 或点发送
3. 等 3-15 秒(视模型和网络)
4. AI 回复出现

如果一切正常,**恭喜,你完成了**。

### 第一次对话最常见的 3 种故障

#### 🔴 故障 1:500 Internal Server Error

- **概率最高:模型名错**(有中文空格 / 老版本号 / 手写 typo)
- 其次:API 余额为 0
- 再次:端点少了 `/v1`

详细排查:[Valid 但 500 完整排查](/troubleshooting/valid-but-500/)

#### 🟡 故障 2:AI 回复空白或很短

- 原因:流式输出被安全审核截断 / 模型空回 / Temperature 太低
- 快速解:Sampling 面板里关掉 Stream → 重发一次,如果仍然空回,换模型

详细:[AI 空回复完整排查](/troubleshooting/empty-truncated/)

#### 🟠 故障 3:AI 复读机(总是重复最后一句)

- 原因:Temperature 太低 / Repetition Penalty 冲突 / 卡片本身有问题
- 快速解:Temperature 调到 0.85,Presence Penalty 调 0,换预设

### 时间节点

25-30 分钟。跑通了就可以庆祝。

---

## 跑通之后的下一步(第 31 分钟+)

恭喜你已经过了 90% 新手的门槛。接下来推荐的学习路径:

### 第一天剩余时间

- 试 3-5 张不同角色卡,感受差异
- 切换不同模型,对比文风
- 看看酒馆左侧栏的其他功能按钮(扩展 / 世界书 / 群聊)

### 第一周

- 选 1 张你最喜欢的卡,长期用
- 学[世界书入门](/presets-lorebooks/lorebook-basics/)
- 理解参数:[Temperature / Top P 完全指南](/presets-lorebooks/temperature-topp/)

### 第一个月

- 理解模型差异:[主流 AI 模型横评](/ai-models/comparison-2026/)
- 玩[多角色群聊](/advanced/group-chat/)
- 处理[长对话失忆](/advanced/long-chat-summary/)

### 第三个月

- 开始自己写角色卡:[角色卡制作指南](/character-cards/manual-creation/)
- 折腾插件:[必装扩展推荐](/extensions/top-10/)
- 深度调参、尝试不同预设

---

## 失败应急树(症状 → 跳转)

| 症状 | 跳转 |
|---|---|
| Connect 按钮点了 invalid | 检查 endpoint 少 `/v1` 或 key 多余空格 |
| Connect valid 但发消息 500 | [Valid 但 500](/troubleshooting/valid-but-500/) |
| 503 Too Many Requests | Key 频率限制,等一分钟或换中转商 |
| 401 Unauthorized | Key 过期或余额为 0 |
| 角色卡导入失败 | [导入指南](/character-cards/import-guide/) |
| 预设导入后没效果 | 检查是否在 Sampling 里选中 |
| AI 空回复 | [空回复排查](/troubleshooting/empty-truncated/) |
| AI 复读机 | 调 Temperature 到 0.85 |
| AI 回复像客服 | 你没加预设,回 Step 5 |
| 其他错误码 | [错误码速查表](/troubleshooting/error-codes/) |
| 完全不知道哪里坏 | [故障诊断器](/diagnostic/) |

---

## 常见问题 FAQ

**Q: 30 分钟真的够吗?**
云端版配合站内免费模型,纯操作确实 30 分钟够。选本地或复杂中转商,第一次通常 60-90 分钟。

**Q: 我卡在 Step 3 连不上,怎么办?**
先检查 endpoint 是否 `/v1` 结尾,key 是否整串无空格。仍然 invalid,看 [Valid 但 500](/troubleshooting/valid-but-500/)。

**Q: 一定要加预设吗?**
严格说不是"必须",但没预设的酒馆体验会差一大截。3 分钟导一个预设能让体验翻倍。

**Q: 免费模型够用吗?**
日常轻量聊天够。但每天用 1 小时+,建议弄个便宜的中转商 Key,避免免费额度用完尴尬。

**Q: 可以跳过角色卡直接聊吗?**
可以,但酒馆的核心玩法就是角色扮演,不用卡片等于放弃 80% 功能。

**Q: 手机能用吗?**
云端版手机完美。本地在手机上不推荐折腾。详细:[手机使用完整指南](/getting-started/mobile-guide/)

**Q: 第一次跑完后下次怎么打开?**
云端:登录 → 继续聊天。本地:启动 server → 浏览器打开 `localhost:8000`。

**Q: 学完这篇还推荐看什么?**
按学习顺序:[角色卡是什么](/character-cards/what-is-character-card/) → [预设是什么](/presets-lorebooks/what-is-preset/) → [AI 模型横评](/ai-models/comparison-2026/)。

---

**下一步推荐**:

- 卡了某一步? → [完整故障诊断器](/diagnostic/)
- 想深入 API? → [自定义 API 端点完整配置](/api-config/custom-api-setup/)
- 想选一个适合自己的模型? → [主流 AI 模型横评](/ai-models/comparison-2026/)
- 想学更多玩法? → [群聊模式入门](/advanced/group-chat/)
- 完全新手没跑通? → [SillyTavern 是什么](/getting-started/what-is-sillytavern/) 先补认知

---

## 📖 关于本文

- **原文**: [30 分钟极速上手:从零到第一次 AI 对话](https://guide.sillytavern.one/getting-started/quickstart/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/getting-started/quickstart/) 为准。

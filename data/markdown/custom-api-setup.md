---
title: "自定义 API 端点完整配置教程:9 步打通任意 OpenAI 兼容 API"
description: "SillyTavern 自定义 API 端点完整 9 步配置教程。覆盖 Claude / GPT / Gemini / DeepSeek / Ollama 本地模型。90% 失败在端点格式或模型名,每一步附精准排查。含多 API 管理、Key 安全、完整错误码对照表。"
slug: custom-api-setup
category: api-config
canonical: https://guide.sillytavern.one/api-config/custom-api-setup/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/api-config/custom-api-setup/](https://guide.sillytavern.one/api-config/custom-api-setup/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

# 自定义 API 端点完整配置教程:9 步打通任意 OpenAI 兼容 API

> **一句话答**:9 步配通所有 OpenAI 兼容 API。成败在 2 个地方:Endpoint 是否 `/v1` 结尾、模型名是否 100% 准确(一个空格或中文标点就 500)。
>
> **关键事实**:
>
> - 所有主流中转商、官方 OpenAI、本地 Ollama/LM Studio 都走这个流程
> - 90% 以上失败是第 3 步(端点)或第 6 步(模型名)拼错
> - 配好后保存为 Preset,以后切 API 只需 2 秒
> - 重度玩家通常有 3-5 个 Preset 来回切

---

API 配置是整个酒馆里技术感最强的一步。

但说实话,这东西没有想象中复杂。真正难的不是"要填什么",而是**每个字段的格式细节**——一个空格、一个中文标点、一个 `/` 写错,整个就跑不通。

我见过最典型的失败:
- endpoint 写成 `https://api.xxx.com/v1/`(末尾多一个 `/`)
- key 复制时带了一个换行符
- 模型名抄成 `claude-sonnet- {版本}`(多一个空格)

前两个酒馆会提示 invalid,第三个最坑:**连接 valid,但发消息立刻 500**。

这篇把 9 步每一个都讲透,每个字段背后的真实规则都解释给你。

## 开始前:3 样东西必须齐全

打开酒馆之前,你需要先拿到 3 样东西。**缺一样都配不上**。

### 1. Endpoint(端点地址)

这是 AI 服务器的基准 URL。格式通常是:

```
https://api.xxx.com/v1
```

**规则**:
- 必须以 `https://` 开头(本地测试可以 `http://`)
- 必须以 `/v1` 结尾
- `/v1` 后面**不要**加斜杠
- `/v1` 后面**不要**接 `/chat/completions`

### 2. API Key

身份凭证,通常以 `sk-` 开头,后面一长串随机字符。

**规则**:
- 整串无空格
- 整串无换行
- 前面**不要**加 `Bearer `(酒馆自己会加)
- 复制时用"复制按钮"别手打

### 3. 模型完整名称(slug)

AI 型号的代号。每家格式都不同。

**示例**:
- OpenAI: GPT 旗舰款 / GPT 平价款 / GPT 推理模型
- Anthropic: Claude Sonnet 模型 / Claude Haiku 模型(具体版本号见服务商)
- Google: Gemini Pro 模型 / Gemini Flash 模型
- DeepSeek: DeepSeek 旗舰对话 / DeepSeek 推理模型

**规则**:
- 完全按官方或中转商文档抄
- 不要有中文标点
- 不要有空格(除非官方模型名本身有)
- 大小写严格区分
- 新版本号经常变,用前查一次最新

详细:[API Key 完整指南](/api-config/api-key-guide/)

---

## Step 1:选 Chat Completion 模式

酒馆界面左上角有个**插头图标** 🔌,点它。

在弹出的面板里:
- **API** 下拉菜单 → 选 **"Chat Completion"**

酒馆支持几种连接模式,对新手来说 Chat Completion 是**唯一应该选的**。其他选项(TextGen、KoboldAI、NovelAI)都是为特殊场景设计的。

---

## Step 2:Source 选 "Custom (OpenAI-compatible)"

Chat Completion 下面会出现 **"Chat Completion Source"**。

下拉选择 **"Custom (OpenAI-compatible)"**。

这是最通用的选项,支持所有遵守 OpenAI 协议的 API —— 也就是 95% 的主流服务。

其他选项(如 "OpenAI" / "Anthropic Claude" / "MistralAI")是给官方直连用的,灵活性差。**推荐新手统一用 Custom**,以后换中转商、换模型都只需要改一个地方。

---

## Step 3:填 Endpoint(最容易错的一步)

**Custom Endpoint (Base URL)** 字段,填你记下的 endpoint。

### 正确示例

```
https://api.openai.com/v1
https://api.anthropic.com/v1
https://api.deepseek.com/v1
https://openrouter.ai/api/v1
```

### 错误示例(全部会 invalid 或 500)

```
❌ https://api.openai.com          少了 /v1
❌ https://api.openai.com/v1/      末尾多一个 /
❌ https://api.openai.com/v1/chat/completions  写了完整路径
❌ api.openai.com/v1               少了 https://
❌ https://api.openai.com/V1       大小写错
```

### ⚠️ 一个最坑的细节

有些中转商的文档会给你这种 URL:

```
https://xxx.com/v1/chat/completions
```

**这是 API 调用的完整路径,不是 endpoint**。酒馆要的是"基础路径"。

正确填法:**只填到 `/v1`**:

```
https://xxx.com/v1
```

这一个坑让新手 100% 撞上至少一次。

---

## Step 4:填 API Key

**Custom API Key** 字段,填你的 key。

### 规则

- 整串无空格(复制后在 key 首尾看一眼)
- 不要加 `Bearer ` 前缀(酒馆自己会加)
- 复制时用文本编辑器的"复制",不要用图片识别或截屏文字提取

### 验证 key 正确的快速方法

打开终端跑:

```bash
curl -H "Authorization: Bearer your-key-here" \
  https://your-endpoint.com/v1/models
```

返回 JSON 就是对的。返回 `{"error":"..."}` 说明 key 有问题。

---

## Step 5:点 Connect 测连接

点 **"Connect"** 按钮。

右上角状态:

| 状态 | 含义 | 下一步 |
|---|---|---|
| 🟢 **Valid** | endpoint + key 都对 | 继续 Step 6 |
| 🔴 **Invalid** | endpoint 或 key 至少一个错 | 回 Step 3-4 重查 |
| ⏳ **Connecting...** 卡 10 秒 | 网络问题或 endpoint 不响应 | 换个网络试试 |

### ⚠️ 重要认知

**Valid 只证明 endpoint 和 key 能通,不证明模型可用**。

发消息还可能 500(最常见的情况)。详细见下一步。

如果这里卡住:[连接失败排查决策树](/troubleshooting/connection-failed/)(如已发布)

---

## Step 6:选择模型

Connect Valid 后,**"Available Models"** 下拉会列出可用模型。

### 情况 A:下拉里能看到你要的模型

直接选,搞定。

### 情况 B:下拉为空或没有你要的

大部分中转商不返回模型列表(`/v1/models` 接口是空的或只返回少数)。

这时在下面的 **"Custom Model ID"** 输入框**手动填**模型完整名。

### ⚠️ 这里是 90% 失败的源头

模型名错误有 4 种典型:

1. **中文标点混入**:用户从中文文档复制,带了中文空格或逗号
2. **版本号过期**:某个旧版日期串(比如几个月前的 Opus)已经被服务商替换成新版,但你还在用旧的
3. **大小写错**:`Claude-Sonnet-{版本}`(错)vs `claude-sonnet-{版本}`(对)
4. **复制截断**:长名字没选全

### 验证模型名的快速方法

```bash
curl -H "Authorization: Bearer your-key" \
  -H "Content-Type: application/json" \
  -d '{"model":"要测的模型名","messages":[{"role":"user","content":"hi"}]}' \
  https://your-endpoint.com/v1/chat/completions
```

返回里有 `"choices"` 字段就是对的,返回 `"error"` 说明模型名错。

详细:[主流模型 slug 参考](/ai-models/comparison-2026/)

---

## Step 7:调整参数(按模型适配)

Sampling 面板(🎚 图标)有一堆参数。新手建议**先不要动**,用默认值。

但有几个**必须按模型适配**的参数:

### Claude 系列(必改)

- **Repetition Penalty**:必须保持默认值(通常 1.0),否则 Claude 官方 API 会 400
- **Presence Penalty**:必须 `0`
- **Frequency Penalty**:必须 `0`

这 3 个参数 Claude 完全不支持。用 Claude 时只要设非默认值,**立刻 400 错误**。

### OpenAI GPT 系列

- 默认值通常就行
- Temperature:0.8-1.0 适合角色扮演
- Top P:0.95 是通用安全值

### Gemini 系列

- 空回复问题常见,**关掉 Stream**(流式输出)能减少概率
- Temperature 0.7-0.9 偏好

### 通用默认(新手直接照抄)

- **Temperature**: 0.85
- **Top P**: 0.95
- **Max Tokens**: 1024
- **Stream**: 开(除了 Gemini)

详细:[Temperature / Top P 参数详解](/presets-lorebooks/temperature-topp/)

---

## Step 8:保存为 Preset(强烈推荐)

辛苦配到这里,不保存就浪费了。

### 3 步保存

1. 右上角 **⋮** 菜单
2. **"Save Preset"**
3. 起名,推荐命名规范:`模型-来源-用途`
   - `claude-sonnet-中转`
   - `gpt4o-官方`
   - `gemini-免费-日常`

### 为什么必须保存

- 重度玩家通常有 3-5 个 API 来回切
- 没 preset = 每次切都要重填所有字段
- 有 preset = 下拉选一下 2 秒切换

### Preset 管理技巧

- **命名规范**:`模型-来源-用途`
- **定期清理**:过期中转商的 preset 删掉
- **备份**:Settings → Export 导出整个配置备份

---

## Step 9:第一次对话验证

回到聊天界面,发一句 "hello" 验证。

### 成功情况

3-15 秒内看到 AI 回复。保存 preset,下次开就用这个。

### 失败情况(按概率排)

| 症状 | 概率 | 跳转 |
|---|---|---|
| 500 Internal Server Error | 70% | [Valid 但 500 完整排查](/troubleshooting/valid-but-500/) |
| AI 回复空白 | 15% | [空回复排查](/troubleshooting/empty-truncated/) |
| AI 回复被截断 | 10% | 同上 |
| 其他奇怪错误码 | 5% | [错误码速查表](/troubleshooting/error-codes/) |

如果完全不知道哪里错:[故障诊断器](/diagnostic/)

---

## 多 API 并存的最佳实践

重度玩家会同时配多个 API。比如:

- **主力**:Claude Sonnet(中转)
- **备用**:GPT-4o-mini(便宜)
- **免费**:Gemini Flash
- **本地**:Ollama(离线)

### 管理方法

1. 每个 API 存一个 **Connection Preset**(端点+key)
2. 每个 API + 场景组合存一个 **Generation Preset**(参数组)
3. 切换 API 时下拉换 Connection Preset,对应的 key 和端点自动切换
4. Sampling 参数和模型分开,可以独立换

### 为什么要这样

- 一家中转商挂了 30 秒内切到备用,不中断对话
- 不同场景用不同模型:日常用便宜的,重要对话用 Claude
- 测试时能快速对比同一张卡在不同模型下的表现

---

## 流式 vs 非流式(Stream)

**Stream On**(默认):AI 边生成边传回来,逐字显示。
**Stream Off**:等 AI 全部生成完,一次性显示。

### 何时关

- **Gemini 空回复**:关了能解决 80% 的情况
- **内容审核被中途截断**:关了,审核完成才返回
- **网络不稳**:流式容易断,非流式更稳

### 何时开

- **大部分场景**:开着体验好
- **模型思考慢**:流式用户感知更快(虽然总耗时一样)

---

## 自定义 Header(高级)

有些中转商要求带特殊 header,比如:

- `HTTP-Referer`:OpenRouter 要求
- `X-Title`:应用名
- `X-Custom-Auth`:二次验证

酒馆的 **Custom Headers** 字段支持 JSON 格式:

```json
{
  "HTTP-Referer": "https://yourapp.com",
  "X-Title": "SillyTavern"
}
```

99% 用户不需要这个。

---

## 反向代理(可选,高级)

如果你需要:
- 给酒馆加统一的访问日志
- 给多个用户共享一个 key
- 对请求做自定义改造

可以考虑反向代理。常见方案:

- **one-api**:开源聚合网关,支持多渠道
- **new-api**:one-api 的加强版
- **自己写**:20 行 Node.js 脚本就能搞定

设置后 endpoint 填你的代理地址,对酒馆完全透明。

---

## 常见错误对照表(完整版)

| 状态码 | 含义 | 根因 | 解决 |
|---|---|---|---|
| 400 | Bad Request | 参数格式错(Claude + repetition_penalty) | 检查 Sampling 参数 |
| 401 | Unauthorized | Key 无效或过期 | 换 key |
| 402 | Payment Required | 余额不足 | 充值 |
| 403 | Forbidden | Key 对该模型无权限 | 换 key 或换模型 |
| 404 | Not Found | endpoint 路径错 | 确认 `/v1` 没加多余斜杠 |
| 429 | Too Many Requests | 频率超限 | 等 1 分钟或换中转商 |
| 500 | Internal Server Error | 模型名错 or 上游故障 | [详细排查](/troubleshooting/valid-but-500/) |
| 502 | Bad Gateway | 中转商挂了 | 等或换中转商 |
| 503 | Service Unavailable | 模型暂时不可用 | 换模型或等 |
| 504 | Gateway Timeout | 模型思考超时 | 缩短 prompt 或换模型 |

详细:[错误码速查表](/troubleshooting/error-codes/)

---

## Key 安全防护

API Key 泄露 = 有人用你的钱。

### 3 条基本防护

1. **不要把 key 截图发群**(经典失误,每个月都有人出事)
2. **不要把 key 提交到 GitHub**(会被爬虫扫到,10 分钟内被盗)
3. **定期旋转**:每 3 个月换一次 key

### 怀疑泄露立刻做

1. 去对应平台**立刻注销当前 key**(不是"删除",是"revoke")
2. 生成新 key
3. 酒馆里所有 preset 全部换新 key
4. 查账单,看有没有异常支出

---

## FAQ

**Q: Connect Valid 为什么发消息还是 500?**
99% 模型名错。回 Step 6 检查,特别注意中文标点和大小写。详细:[Valid 但 500](/troubleshooting/valid-but-500/)

**Q: 端点该填 `/v1` 还是 `/v1/`?**
只填 `/v1`,末尾不要加 `/`。

**Q: 为什么某中转商的文档让我填 `/v1/chat/completions`?**
那是 API 调用的完整路径,不是 endpoint。酒馆只要 base,填到 `/v1` 就好。

**Q: 一个 key 能用多家的吗?**
官方 key 只能用自家(OpenAI key 不能调 Claude)。中转商 key 通常能用所有接入的模型。

**Q: 免费额度用完了怎么办?**
换中转商或买小额 key。详细:[API Key 完整指南](/api-config/api-key-guide/)

**Q: 支持本地模型吗?**
支持。Ollama 启动后,endpoint 填 `http://127.0.0.1:11434/v1`,key 随便填(本地不校验)。模型名填你在 Ollama 里的模型名(如 `llama3.1:8b`)。

**Q: 一次切多个 API 有没有更好的方法?**
见上面 [多 API 并存的最佳实践](#多-api-并存的最佳实践)。

**Q: Custom Headers 什么时候需要填?**
99% 用户不需要。只有 OpenRouter 等特殊中转商文档明确要求时才填。

**Q: 切换 preset 后对话会断吗?**
不会。切 preset 只影响下一条发送的 API 调用,之前的对话完整保留。

---

**下一步推荐**:

- 配好了但发消息 500? → [Valid 但 500 完整排查](/troubleshooting/valid-but-500/)
- 想选对模型? → [主流 AI 模型横评](/ai-models/comparison-2026/)
- 还在选 Key 来源? → [API Key 完整指南](/api-config/api-key-guide/)
- 按量 vs 按次谁划算? → [计费模式完整对比](/api-config/pricing-models/)
- 完全新手没跑通? → [30 分钟极速上手](/getting-started/quickstart/)
- 出各种错? → [错误码速查表](/troubleshooting/error-codes/)

---

## 📖 关于本文

- **原文**: [自定义 API 端点完整配置教程:9 步打通任意 OpenAI 兼容 API](https://guide.sillytavern.one/api-config/custom-api-setup/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/api-config/custom-api-setup/) 为准。

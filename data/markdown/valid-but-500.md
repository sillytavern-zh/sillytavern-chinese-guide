---
title: "SillyTavern Valid 但 500 完整排查指南:6 层决策树定位 90% 错误"
description: "API 连接 valid 但发消息 500?70% 模型名错、10% 端点缺 /v1、10% Key 余额 0、5% 参数兼容、3% 上游、2% 网络。6 层结构化排查,带 curl 验证 + Claude/o1/Gemini 各家特殊坑。覆盖 prompt-eval、token 限制、stop 参数兼容性、安全策略阻断等隐性原因,排查地图直击根本原因。"
slug: valid-but-500
category: troubleshooting
canonical: https://guide.sillytavern.one/troubleshooting/valid-but-500/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/troubleshooting/valid-but-500/](https://guide.sillytavern.one/troubleshooting/valid-but-500/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

你把 Key 填进去,点连接,绿色 Valid,心里刚松一口气,**结果第一句话直接 500**。

这是社群里出现频率最高的崩溃瞬间之一:

> "我点'连接'显示绿色 valid,结果发消息就报 500 / Internal Server Error,怎么回事?"

**真相**:valid 只能证明"密钥能登录",**不代表"模型能用"**。就好像门禁卡能开大门,但不一定能开你想去的那间会议室。

这一篇按出错概率从高到低,给你一份 **6 层结构化排查清单**。按顺序检查,90% 以上的问题都能在前 3 层解决。

## 排查第 1 层:模型名(70% 案例)

最常见的原因,没有之一。

### 5 种最隐蔽的 typo 类型

**1. 中文标点污染(最隐蔽)**

从微信 / QQ 群复制时,英文标点可能被替换成中文标点:

肉眼看几乎一样,但其中的 `-` 可能是 `−`(U+2212 减号)而不是真正的 `-`(U+002D 连字符)。这种污染**完全看不出来**。

**判定法**:把模型名贴进文本编辑器,按 Ctrl+F 搜——如果搜不到自己刚粘进去的东西,八成有隐藏字符。最稳的做法是**直接手敲**,不复制。

**2. 大小写错乱**

- ✅ `claude-sonnet-{版本}`(全小写、横杠分隔)
- ❌ `Claude-Sonnet-{版本}` / `CLAUDE-SONNET-{版本}`

OpenAI / Anthropic 模型名**严格区分大小写**。中转商一般不区分,但少数严格。

**3. 空格混入**

复制时手抖加了空格:

- ❌ ` claude-sonnet-{完整版本号}` (前导空格)
- ❌ `claude-sonnet -{完整版本号}` (中间空格)

中转商有的会 trim 有的不会。**手工 backspace 删一遍前后字符最稳**。

**4. 版本号过期**

3 个月前能用的某个 Opus 版本号,现在可能已下线。模型版本号每月都在迭代。

**判定法**:去服务商的"模型列表"页对照,**用他们当前列出的 slug**。

**5. 复制截断**

长模型名复制时光标没选到尾:

- 完整: `claude-sonnet-{完整日期版本号}`
- 截断: `claude-sonnet-{前半段}`

(后 4 位丢了,看起来还像那么回事)

### 主流模型 slug 参考

⚠️ 下表只是示例,**真实 slug 以你的服务商当前文档为准**,会变。

| 厂商 | 常用 slug 示例 |
|---|---|
| Anthropic | Claude Sonnet / Opus / Haiku 三档,具体版本号见服务商文档 |
| OpenAI | GPT 旗舰款 / GPT 平价款 / GPT 推理模型(o 系),具体名称见服务商文档 |
| Google | Gemini Pro / Gemini Flash,具体版本号见服务商文档 |
| DeepSeek | DeepSeek 旗舰对话 / DeepSeek 推理模型,具体版本号见服务商文档 |
| 中转商 | 通常加前缀,如 `oneapi/claude-sonnet-{版本}` |

### 命令行精确验证

复制完 Key + endpoint + model 后,跑这条 curl:
bash
curl -s -H "Authorization: Bearer YOUR_KEY" \
-H "Content-Type: application/json" \
-d '{"model":"你的模型名","messages":[{"role":"user","content":"hi"}]}' \
YOUR_ENDPOINT/chat/completions

返回 `"choices"` 字段 = 模型名对了
返回 `"error"` 含 `model not found` / `no such model` / `invalid model` = **就是模型名错**
返回其他错误 = 跳第 2-6 层

### "我抄的明明是对的,为什么还 404?"

3 种可能:

1. **服务商隐藏了某些模型**:免费层不含 Opus、限地区、限套餐
2. **中转商没接入这个模型**:换中转商或换模型
3. **临时下架**:服务商可能突然把某个版本下线,旧用户也会受影响

详细 9 步 API 配置见 [自定义 API 端点完整配置](/api-config/custom-api-setup/)。

## 排查第 2 层:端点(10% 案例)

### 端点格式速查

| 错误形式 | 正确形式 | 备注 |
|---|---|---|
| `https://api.x.com` | `https://api.x.com/v1` | 少了 `/v1` |
| `https://api.x.com/v1/` | `https://api.x.com/v1` | 末尾不要斜杠 |
| `https://api.x.com/v1/chat/completions` | `https://api.x.com/v1` | 不要写完整路径 |
| `http://api.x.com/v1` | `https://api.x.com/v1` | 缺 `s` |
| `https://api.x.com/V1` | `https://api.x.com/v1` | 必须小写 |

### 不同中转商的额外坑

- **OpenRouter**:endpoint 是 `https://openrouter.ai/api/v1`,不是 `https://api.openrouter.ai/v1`——api 在前还是后差很多人没注意
- **Azure OpenAI**:不是 OpenAI 完全兼容,endpoint 格式不一样
- **Cloudflare AI Gateway**:endpoint 含 account_id,容易抄错

### 端点验证 curl
bash
curl -s YOUR_ENDPOINT/models -H "Authorization: Bearer YOUR_KEY" | head -c 200

返回 JSON 模型列表 = 端点对
返回 HTML 或 404 = 端点错

### "连接 valid 但端点错"为什么会发生

很多平台的 valid 检测只查 `/v1/models`,而**这个接口对部分中转商即使端点错也会"路由到对的地方"**。但发消息走 `/v1/chat/completions`,这个接口对端点的严格度更高,就 404 转 500 了。

所以 valid 不代表端点 100% 对,这是设计陷阱。

## 排查第 3 层:Key 状态(10% 案例,新手最难发现)

### "Valid 但余额 0" 的底层原理

绝大多数 API 平台的 valid 检测路径是这样的:
GET /v1/models → 返回 200 + 模型列表 → Valid

**但 `/v1/models` 不查余额**。所以余额 0 也能 valid。

只有真正发消息(`/v1/chat/completions`),才会触发"扣费 → 余额不够 → 500 / 402"。这是 500 第二大元凶,新手 99% 不会想到。

### 各家平台余额查询页

| 平台 | 余额查询入口 |
|---|---|
| OpenAI | platform.openai.com → Billing → Usage |
| Anthropic | console.anthropic.com → Plans & Billing |
| Google AI | aistudio.google.com → 配额(免费 tier 看请求数) |
| DeepSeek | platform.deepseek.com → 余额 |
| 中转商 | 各家不同,看自己的 dashboard |

**建议每周扫一眼**。

### 6 种 Key 异常迹象

| 现象 | 真正原因 |
|---|---|
| 5 分钟前能用,现在突然 500 | 余额耗尽 / 临时风控 |
| 一会儿能用一会儿 500,稳定不下来 | 共享 Key 池被打挂(中转商) |
| 第一条 200,第二条起 500 | 频率限制(本应 429,被中转商转成 500) |
| 切其他模型也 500 | Key 整体被禁,不是单模型问题 |
| 白天能用晚上不能 | 中转商分时段限速 / 套餐时段限制 |
| Key 创建当天 200,第二天 500 | 试用 Key 自动失效 / 平台风控撤销 |

### 多 Key 串了(隐蔽错误)

如果你同时用多个平台,把 A 平台的 Key 复制到 B 平台的 endpoint:
endpoint: https://api.anthropic.com/v1 ← Anthropic
key: sk-proj-OpenAI字串 ← OpenAI 的 Key

平台会 reject,但**部分中转商会转发到对应原厂,返回 500 而不是 401**。这种 500 看起来跟"模型问题"一模一样,极难发现。

**防止方法**:每个 Key 单独存为一个 Connection Preset,切换时下拉一选,不动手填字段。

### Key 安全 3 条铁律

1. **不发任何聊天群**——99% 的 Key 泄露发生在群里
2. **不 commit 到 GitHub**——爬虫 10 分钟内会扫到
3. **每 3 个月旋转一次**——降低长期泄露风险

完整 Key 指南 → [API Key 怎么填、怎么验证、怎么排查问题](/api-config/api-key-guide/)

## 排查第 4 层:参数兼容性(5% 案例)

某些参数对某些模型来说是"**毒**"——填了就 500。

### Claude 的 3 条死铁律

| 参数 | Claude 是否支持 | 错填后果 |
|---|---|---|
| `frequency_penalty` | ❌ 不支持 | 422 / 500 |
| `presence_penalty` | ❌ 不支持 | 422 / 500 |
| `repetition_penalty` | ❌ 不支持 | 422 / 500 |
| `top_k` | ✅ 支持(0-100) | 0 = 默认 |

**必须设置**:用 Claude 时,在 Sampling 面板把上面 3 个 Penalty 全部归 0。

部分酒馆预设默认 `frequency_penalty = 0.1`——**这个 0.1 在 Claude 上就会 500**。

### OpenAI o1 / o3 系列的特殊限制

如果你用 o1-preview / o1-mini / o3-mini 这种 "reasoning model":

- ❌ 不支持 `stream`(**必须关 Stream**)
- ❌ 不支持 system prompt(角色卡 description 会被忽略)
- ❌ 不支持 `temperature`(必须默认 1)
- ❌ 不支持 `top_p`

**酒馆默认开 Stream,所以新手用 o1 直接 500**。这是非常常见的"我换了最新模型反而不能用了"现象。

### Gemini 部分中转商不支持 Top K

OpenAI 系不支持 Top K,但 Gemini 原生支持。如果中转商把 Gemini 包成 OpenAI 兼容,Top K 字段会被转发,部分实现报 500。

**保险做法**:用 Gemini 时,Top K 留空或 0。

### Stream 被中转 / 反代截断

中转商如果用了不稳定的反代或 CDN,**SSE 流可能在中途被关闭**,酒馆看到的就是 500 或空回复。

**判定法**:关掉 Stream → 重发 → 如果稳定了,就是流式问题。

详细参数指南 → [Temperature / Top P / Top K 参数详解](/presets-lorebooks/temperature-topp/)

### Max Tokens / 上下文超长

- Max Tokens 超过模型限制(比如设 8000,模型只支持 4096)→ 500
- 上下文 + Max Tokens 加起来超过模型上下文窗口 → 500
- 角色卡 + 世界书 + 历史对话堆到几十万 token → 中转商可能直接拒

**保险做法**:Max Tokens 设 2000-4000,够用,不冒险。

## 排查第 5 层:上游故障(3% 案例)

排到这里,前 4 层都没问题,八成是**别人的事**。

### 怎么判断不是你的问题

- ✅ 几小时前还能用,现在突然不行
- ✅ 切到同平台其他模型也 500
- ✅ 群里多人同时反馈
- ✅ 服务商状态页有故障公告
- ✅ 错误码是 502 / 503 / 504(不是 500)

### 应对策略

1. **看状态页**:服务商通常有 status.xxx.com 这种页面
2. **看社群**:中转商一般有 QQ / Discord 群,故障会被反馈
3. **切备用渠道**:这就是为什么我们一直建议 2 个以上 API 备份
4. **等 30-60 分钟**:绝大多数故障 1 小时内恢复

### 备用渠道最佳实践

不要把所有鸡蛋放在一个篮子里:

- **主力 Key**:重度使用,质量最好的中转商或官方
- **备用 Key**:不同中转商,故障时切换不到 30 秒
- **应急 Key**:免费额度模型(Gemini Flash / DeepSeek),保命用

## 排查第 6 层:本地网络(2% 案例)

最后才考虑,概率最低,但也不是 0。

| 场景 | 怎么判定 | 解决 |
|---|---|---|
| 需要梯子但没开 | 切到能上 Google 的环境就好 | 开梯子 |
| 梯子规则没覆盖该域名 | 能上别的网站,只这个 endpoint 超时 | 检查代理规则 / 切节点 |
| TLS 1.3 / SNI 被运营商干扰 | 偶尔 200 偶尔 500,无规律 | 换 DNS / 换网络 |
| 公司 / 校园网封 SSE | 短回复能成功,长回复 500 | 换网络或关 Stream |
| 浏览器扩展拦截 | 隐身模式下能用,正常窗口不能 | 禁用拦截扩展 |
| DNS 污染 | nslookup 返回奇怪 IP | 换 DNS(1.1.1.1 / 223.5.5.5) |

## 实战复盘:一个完整案例

走一遍真实排查过程,以后遇到类似场景能快速对号。

**场景**:小张刚配 Claude Sonnet 模型,Connect 显示绿色 valid,发"hello"立即报 500。

**第 1 步:验证模型名**

他抄的是服务商文档里的某个 Claude Sonnet slug。

用 curl 测试:
bash
curl -s -H "Authorization: Bearer sk-xxx" \
-d '{"model":"你的 Claude Sonnet slug","messages":[{"role":"user","content":"hi"}]}' \
https://api.xxx.com/v1/chat/completions

如果返回 `"error":"model not found"` → 模型名错
如果返回 `"error":"insufficient balance"` → 跳第 3 层
小张返回的是 `"error":"unsupported parameter: frequency_penalty"`。

**第 2 步:认知锁定 — 参数问题**

报错明确说 `frequency_penalty` 不支持。Claude 必须设 0。

小张去 Sampling 面板,发现是默认预设带了 `frequency_penalty = 0.1`。

**第 3 步:修复**

Sampling 面板 → frequency_penalty 改 0 → presence_penalty 改 0 → 保存 → 重发。

**结果**:200,AI 回复了。整个排查 3 分钟。

**关键 takeaway**:**报错原文 JSON 是金矿**。不要只看"500",看完整 error 字段,90% 直接告诉你哪一层。

## 5 条预防性配置习惯

1. **截图保存配置**:每次成功配通后,截图 endpoint + 模型名 + Sampling 参数,以后对照用
2. **第一次连接成功立即测试发消息**:别等正式用才发现 500
3. **给每个模型存独立 Connection Preset**:切换时下拉一选,不动手填字段,避免串号
4. **每周扫一遍余额**:5 秒的事,但能避免"凌晨想用突然 500"
5. **备用 Key 常驻**:免费的 Gemini Flash / DeepSeek 各注册一个,主力挂了直接顶

## 闪电排查表(截图保存)
500 排查顺序(按概率):

模型名 100% 准确?(70% 案例)
→ 中文标点 / 大小写 / 空格 / 版本号过期 / 复制截断

端点是 /v1 结尾?不带 /chat/completions?(10%)

Key 余额 > 0?Key 没过期?(10%)

参数兼容性?(5%)
→ Claude 三 Penalty 必须 0
→ o1/o3 不能 Stream

上游 / 渠道炸?(3%)
→ 服务商状态页 / 群公告 / 切备用

本地网络?(2%)
→ 梯子 / DNS / 公司网

每层卡 5 分钟无果,跳下一层。别在一层死磕。

## 全部排查后还不行?

社群求助请按这个格式(没人喜欢"我不能用 + 没截图"):
模型名:(完整 slug,粘贴不截图)
端点:(完整 URL)
错误码:(HTTP code)
错误原文 JSON:(整段复制)
最近改过什么:(实话,别隐瞒)
其他人能用吗:(是 / 否)
酒馆版本:(可选)

带这些信息,老玩家 5 分钟就能给你答案。**最关键的是"错误原文 JSON"——绝大多数 500 的真因都在原文里**。

## 其他错误码不是 500?

直接看 [常见错误码速查](/troubleshooting/error-codes/),401 / 403 / 429 / 502 各有各的修法。

## 相关阅读

- [自定义 API 端点完整配置](/api-config/custom-api-setup/)
- [API Key 怎么填、怎么验证、怎么排查问题](/api-config/api-key-guide/)
- [AI 回复空白 / 截断 / 突然停止](/troubleshooting/empty-truncated/)
- [30 分钟极速上手](/getting-started/quickstart/)

---

## 📖 关于本文

- **原文**: [SillyTavern Valid 但 500 完整排查指南:6 层决策树定位 90% 错误](https://guide.sillytavern.one/troubleshooting/valid-but-500/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/troubleshooting/valid-but-500/) 为准。

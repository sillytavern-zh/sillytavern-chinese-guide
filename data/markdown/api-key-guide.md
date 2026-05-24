---
title: "API Key 怎么填、怎么验证、怎么排查问题"
description: "SillyTavern API Key 配置完整实战。从复制 Key 到 valid 验证、余额查询、多 Key 管理、安全保存的所有坑点和解决方案。覆盖 Claude / GPT / Gemini / DeepSeek / 国内中转商各家的 Key 格式差异、有效期管理、Key 泄露后的应急处理、防止误推 GitHub 的安全实践。"
slug: api-key-guide
category: api-config
canonical: https://guide.sillytavern.one/api-config/api-key-guide/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/api-config/api-key-guide/](https://guide.sillytavern.one/api-config/api-key-guide/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

打开酒馆,设置好端点,Key 一贴...
Invalid API Key

你站在那儿盯着这行红字,心里想着"我明明刚才在后台复制的啊"。

这是新人最经典的崩溃瞬间。下面这些坑我自己踩过、群里见过无数遍。一篇说清楚。

## Key 到底是什么

API Key 就是你访问某个 AI 服务的"门禁卡"。
- 你在 OpenAI(或其他平台)注册账号 → 在控制台生成一串 Key
- 把 Key 给酒馆 → 酒馆带着这串字符去敲服务器的门
- 服务器一看"这串号是我发的、还没过期、有余额" → 让进

Key 长什么样?以 `sk-` 开头的最常见,后面跟 40-50 位字符。也有些服务商不带前缀,各种格式都有。

Key 这玩意,真不是技术问题,**是细心问题**。

## 第一次失败:复制时多/少了字符

最常见,真的。

很多 API 后台显示 Key 时只显示前几位和后几位,中间星号遮住。**手动选中复制极易少字符**。

- 一定**点平台提供的"复制"按钮**,别用鼠标拖
- 粘贴到酒馆后,**点出来看一眼长度**对不对
- 检查首尾有没有空格(粘贴时最容易混进去)

最离谱的一次:有人把 Key 粘到 Word 里"先看看",结果 Word 自动给开头加了大写,变成 `Sk-...`。`Sk` 跟 `sk` 在 API 那边是完全不同的字符串。

## 第二次失败:粘错地方了

酒馆的设置界面有好几个输入框。**Key 必须粘到「API Key」那一栏**,不是「Custom Model」、不是「Endpoint」、更不是「System Prompt」。

听起来废话?群里每周都有人。

## 第三次失败:粘了 Bearer

某些 API 文档示例代码会写:
Authorization: Bearer sk-xxxx

新手一激动,把整段都复制了,粘到酒馆里变成:
Bearer sk-xxxx

**前面的 "Bearer " 不能要**。酒馆调用 API 时会自己加,你再加一个就重复了。

## 怎么确认 Key 真的有效

点"连接"显示绿色 Valid?**不一定**。

很多平台的 valid 检查只是请求一下 `/v1/models`,看你有没有权限列模型。但这个接口和 `/v1/chat/completions`(真正聊天)用的可能是不同的权限规则。

最稳的验证方式:
1. 配好连接
2. 创建一个新角色,简单的那种
3. 发"你好"三个字
4. 看 AI 回不回话

回话了才叫真的能用。

## Key 余额到底怎么查

这是新人最容易忽略的事。

**Key 没了余额还是 valid 的**。你能看到模型列表、你能聊?不能。

每家 API 服务商的余额查询页都不一样,有自己专门的"用量"或"账单"页面。

每周扫一眼,别等 500 报错才反应过来。

## 多个 Key 怎么管

老玩家通常手里都有 3-5 个 Key:
- 主力 Key(花得最多)
- 备用 Key(主力挂了顶上)
- 测试 Key(试新模型用,不舍得花主力)

酒馆里**给每套 Key 单独存一份连接配置**。在设置面板顶部有个"Preset"下拉,可以保存当前所有 API 配置,起名 `主力Claude`、`备用Gemini`,切换只要点一下。

别想着"一个配置改改就行"。

## 安全:Key 千万不能贴出去

- 不要在群里贴
- 不要发到客服
- 不要传到 GitHub
- 不要写在博客里

Key 泄露后果:别人能用你的额度,把你账上的钱花光。见过有人 Key 泄露 12 小时被花掉 8000 美元的。

如果不小心泄露了:
1. **立刻**去后台撤销那个 Key
2. **立刻**生成新 Key
3. 检查近期账单有没有异常消费

## Key 长期保存

我用密码管理器存所有 Key,按服务商分类。每个 Key 配上:
- 服务商
- 用途备注
- 余额查询地址
- 到期日期(如果有)

不要存在浏览器密码管理器里——某天浏览器崩了你哭都来不及。

## 一句结语

API Key 这玩意吧,本身简单。复杂的是你的手不抖、眼不花、复制时不带空格、粘贴时不带 Bearer、保存时不到处发。

新人遇到「Invalid API Key」时,先别怀疑服务商,先怀疑自己。其他错误码速查见 [《常见错误码大全》](/troubleshooting/error-codes/)。

---

## 相关阅读

- [Valid 但 500 完整排查](/troubleshooting/valid-but-500/)
- [自定义 API 端点完整配置](/api-config/custom-api-setup/)

---

## 📖 关于本文

- **原文**: [API Key 怎么填、怎么验证、怎么排查问题](https://guide.sillytavern.one/api-config/api-key-guide/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/api-config/api-key-guide/) 为准。

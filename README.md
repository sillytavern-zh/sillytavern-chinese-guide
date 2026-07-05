# 📖 SillyTavern 中文教程站

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Last Sync](https://img.shields.io/badge/last%20sync-2026-07-05-blue)](https://github.com/sillytavern-zh/sillytavern-chinese-guide/commits/main)
[![Articles](https://img.shields.io/badge/articles-28-green)](#-完整目录)
[![Pillar](https://img.shields.io/badge/pillar-5-orange)](#-完整目录)

> 中文 SillyTavern 用户的权威教程、故障排查与进阶玩法

🌐 **在线版(原文):** https://guide.sillytavern.one/

> ⚠️ **本仓库是镜像归档,不是主站**。最新内容、最新示例、最新外链请访问 [guide.sillytavern.one](https://guide.sillytavern.one/)。

本仓库是 [guide.sillytavern.one](https://guide.sillytavern.one/) 的内容快照,所有文章独立维护,不隶属任何运营方,不出售任何 API 或订阅。

📊 **当前**: 28 篇精品教程 · 5 篇 Pillar 长文(3000-4500 字深度解析)

---

## 📚 完整目录

> ⭐ = Pillar 级长文(3000+字) · 🛡 = 反时效化(版本中性,长期有效)

### 🚀 新手入门
_从零到第一次 AI 对话_

- **[SillyTavern 本地部署完整教程:Windows / macOS / Linux 三平台傻瓜式指南](data/markdown/local-install.md)**
  - SillyTavern 本地部署全平台完整步骤。从装 Node.js 到跑通第一次对话,所有报错完整对照表,30-90 分钟跑通。覆盖 Windows / macOS / Linux 三大平台,...
  - 🌐 [在线阅读](https://guide.sillytavern.one/getting-started/local-install/)

- **[SillyTavern 是什么?从开源前端到 AI 角色扮演神器的完整解读](data/markdown/what-is-sillytavern.md)** ⭐🛡
  - SillyTavern(酒馆)是什么?一篇读完:生态关系、和 ChatGPT/Character.AI 的本质差别、2026 年为什么仍值得学、7 种用户画像、真实成本、新手误解、常见故障速查。...
  - 🌐 [在线阅读](https://guide.sillytavern.one/getting-started/what-is-sillytavern/)

- **[云端版 vs 本地部署:成本、稳定性、上手难度深度对比](data/markdown/cloud-vs-local.md)**
  - SillyTavern 云端版和本地部署到底哪个适合你?从成本、稳定性、易用性、隐私四个维度完整对比,附本地部署快速教程和挑选云端运营方标准。新手 90% 应该选云端,老玩家什么时候应该转本地。...
  - 🌐 [在线阅读](https://guide.sillytavern.one/getting-started/cloud-vs-local/)

- **[30 分钟极速上手:从零到第一次 AI 对话](data/markdown/quickstart.md)** ⭐🛡
  - SillyTavern 新手 30 分钟极速上手。5 步走完:选部署方式、获取 API、配置连接、导角色卡和预设、第一次对话。失败率 70% 源于模型名错,每一步附精准排查跳转。包含 HowTo...
  - 🌐 [在线阅读](https://guide.sillytavern.one/getting-started/quickstart/)

- **[手机使用 SillyTavern 完整指南:iOS / Android / iPad](data/markdown/mobile-guide.md)**
  - 手机怎么用 SillyTavern?iOS、Android、iPad 三大平台的最佳方案完整对比和操作步骤,含 Termux 本地部署。覆盖云端访问 vs 本地运行、Termux 安装步骤、iO...
  - 🌐 [在线阅读](https://guide.sillytavern.one/getting-started/mobile-guide/)

- **[酒馆名词速查表:Preset / Lorebook / Persona 一篇讲清](data/markdown/glossary.md)**
  - SillyTavern 常见英文术语速查:角色卡、预设、世界书、Persona、Token、Temperature、Top P、流式输出等核心概念一次讲清楚。覆盖新手最容易混淆的 20+ 名词,...
  - 🌐 [在线阅读](https://guide.sillytavern.one/getting-started/glossary/)


### 🎭 角色卡
_导入、自制、避坑_

- **[角色卡到底是什么?一张 PNG 背后藏着 AI 的灵魂](data/markdown/what-is-character-card.md)**
  - 角色卡是 SillyTavern 的核心。本文从原理、结构、获取方式、使用注意四个角度讲清楚一张角色卡到底是什么。覆盖 PNG 隐写原理、V2/V3 格式差异、字段含义(name/descrip...
  - 🌐 [在线阅读](https://guide.sillytavern.one/character-cards/what-is-character-card/)

- **[角色卡导入完整指南:从下载到第一次对话的全流程](data/markdown/import-guide.md)**
  - SillyTavern 角色卡导入完整流程,含导入方法、备选问候语切换、导入失败 9 大原因排查。覆盖网页拖入、URL 直接导入、本地文件上传 3 种方法,导入失败 9 大原因(文件损坏、格式错...
  - 🌐 [在线阅读](https://guide.sillytavern.one/character-cards/import-guide/)

- **[自己做一张角色卡:从概念到成品的 5 步流程](data/markdown/manual-creation.md)**
  - SillyTavern 角色卡制作完整教程,5 步走完概念设计、角色描述、第一句话、示例对话、测试导出,含好描述/坏描述对比与避坑指南。从零开始 90 分钟做出第一张能用的卡,覆盖人设深度、性格...
  - 🌐 [在线阅读](https://guide.sillytavern.one/character-cards/manual-creation/)


### 📚 预设 · 世界书
_让 AI 灵魂质量升级_

- **[预设是什么?为什么决定了 AI 的灵魂质量](data/markdown/what-is-preset.md)**
  - SillyTavern 预设(Preset)是什么?为什么用了预设的 AI 比不用的强 5 倍?本文从结构、作用、选择、调参四个角度讲清楚。覆盖系统提示词模板、上下文管理、Story Strin...
  - 🌐 [在线阅读](https://guide.sillytavern.one/presets-lorebooks/what-is-preset/)

- **[世界书入门:让 AI 记住你的整个世界](data/markdown/lorebook-basics.md)**
  - SillyTavern 世界书 (Lorebook) 完整入门。讲解条目、关键词、激活策略、插入位置 5 个核心概念,从零创建第一个能用的世界书。覆盖正则关键词、连锁触发、深度策略、Token ...
  - 🌐 [在线阅读](https://guide.sillytavern.one/presets-lorebooks/lorebook-basics/)

- **[Temperature / Top P / Top K 参数详解:决定 AI '性格'的旋钮](data/markdown/temperature-topp.md)**
  - SillyTavern 生成参数完整解析。Temperature 温度、Top P 核采样、Top K、Frequency Penalty、Presence Penalty 各自的原理与三大模型...
  - 🌐 [在线阅读](https://guide.sillytavern.one/presets-lorebooks/temperature-topp/)


### 🤖 AI 模型
_Claude / Gemini / GPT / DeepSeek 横评_

- **[2026 主流 AI 模型横评:Claude / Gemini / GPT / DeepSeek](data/markdown/comparison-2026.md)** 🛡
  - 2026 年 SillyTavern 主流 AI 模型完整横评,Claude、Gemini、GPT-4o、DeepSeek 四大模型优劣势对比,根据场景给出选型建议。覆盖中文表现、反审查能力、推...
  - 🌐 [在线阅读](https://guide.sillytavern.one/ai-models/comparison-2026/)

- **[Claude 全系深度指南:Sonnet / Opus / Haiku 怎么选](data/markdown/claude-guide.md)** 🛡
  - Claude 在中文角色扮演中为什么是顶端选择?Sonnet、Opus、Haiku 三档对比、参数避雷、反审查表现、国内中转方案全解。覆盖 Sonnet 性价比平衡、Opus 顶级写作、Haik...
  - 🌐 [在线阅读](https://guide.sillytavern.one/ai-models/claude-guide/)

- **[Gemini 全家桶解析:Flash 和 Pro 的真实差异](data/markdown/gemini-guide.md)** 🛡
  - Gemini 系列完整选型指南。Flash 性价比之王、Pro 中端主力、Ultra 为何不推荐、空回复反截断完整解决方案、100 万 token 上下文的妙用。覆盖参数避雷、Safety Se...
  - 🌐 [在线阅读](https://guide.sillytavern.one/ai-models/gemini-guide/)


### 🔌 API 配置
_从端点到密钥管理_

- **[自定义 API 端点完整配置教程:9 步打通任意 OpenAI 兼容 API](data/markdown/custom-api-setup.md)** ⭐🛡
  - SillyTavern 自定义 API 端点完整 9 步配置教程。覆盖 Claude / GPT / Gemini / DeepSeek / Ollama 本地模型。90% 失败在端点格式或模型...
  - 🌐 [在线阅读](https://guide.sillytavern.one/api-config/custom-api-setup/)

- **[API Key 怎么填、怎么验证、怎么排查问题](data/markdown/api-key-guide.md)**
  - SillyTavern API Key 配置完整实战。从复制 Key 到 valid 验证、余额查询、多 Key 管理、安全保存的所有坑点和解决方案。覆盖 Claude / GPT / Gemi...
  - 🌐 [在线阅读](https://guide.sillytavern.one/api-config/api-key-guide/)

- **[按次计费 vs 按量计费:长上下文场景如何省 40 倍](data/markdown/pricing-models.md)** 🛡
  - AI API 两种主流计费模式完整对比。短对话用按量、长上下文必选按次的真实成本案例,Agent / 长文档分析 / 多轮对话场景的最优选择策略。带具体的成本计算公式、不同 Token 数下的盈...
  - 🌐 [在线阅读](https://guide.sillytavern.one/api-config/pricing-models/)


### 🧩 扩展 · 插件
_酒馆助手 / 记忆插件 / 必装清单_

- **[SillyTavern 必装扩展 TOP 10:让酒馆体验质变](data/markdown/top-10.md)**
  - 2026 实测有效的 10 个必装扩展,按重要程度排序。酒馆助手、记忆增强、文生图、QR 助手、TTS、翻译、字体管理器等。每个扩展给出"必装理由 + 效果展示 + 安装步骤 + 跟其他扩展的兼...
  - 🌐 [在线阅读](https://guide.sillytavern.one/extensions/top-10/)

- **[酒馆助手 Tavern Helper:80% 高级扩展依赖的'地基'](data/markdown/tavern-helper.md)**
  - 为什么酒馆助手是必须装的第一个扩展?它的作用、安装方法、常见安装失败原因、高级用法(自定义 JS / Slash 命令 / 双向交互)完整指南。覆盖 80% 高级扩展依赖的"地基"概念、和原生功...
  - 🌐 [在线阅读](https://guide.sillytavern.one/extensions/tavern-helper/)

- **[SillyTavern 记忆插件横评:Horae / 记忆表格 / Amily2 / 全自动总结 4 家选哪个](data/markdown/memory-extensions.md)** ⭐🛡
  - 4 家主流 SillyTavern 记忆插件深度对比,5 维度横评 + 5 步决策树。Horae 时光记忆 / 记忆表格 / Amily2 / 全自动总结脚本各擅长什么、Token 消耗如何、谁...
  - 🌐 [在线阅读](https://guide.sillytavern.one/extensions/memory-extensions/)

- **[SillyTavern 文生图完整指南:三大后端 + 三种触发方式 + 国内用户特殊挑战](data/markdown/image-generation.md)** 🛡
  - SillyTavern 文生图完整指南。集成 Stable Diffusion / NovelAI / DALL-E 3 三大后端,角色头像生成、场景插图、动态画面 3 种触发方式,中国大陆用户...
  - 🌐 [在线阅读](https://guide.sillytavern.one/extensions/image-generation/)


### 🔧 故障排查
_Valid 但 500 / 空回复 / 错误码_

- **[SillyTavern 1.17.0 升级后魔法棒按钮消失?一键修复](data/markdown/missing-wand-button-1170.md)**
  - SillyTavern 1.17.0 升级后左下角魔法棒(扩展菜单)按钮不见了?这是新版默认隐藏导致。本文教你 30 秒一键恢复经典布局,附完整原因分析和 GitHub 开源扩展。
  - 🌐 [在线阅读](https://guide.sillytavern.one/troubleshooting/missing-wand-button-1170/)

- **[SillyTavern Valid 但 500 完整排查指南:6 层决策树定位 90% 错误](data/markdown/valid-but-500.md)** ⭐🛡
  - API 连接 valid 但发消息 500?70% 模型名错、10% 端点缺 /v1、10% Key 余额 0、5% 参数兼容、3% 上游、2% 网络。6 层结构化排查,带 curl 验证 + ...
  - 🌐 [在线阅读](https://guide.sillytavern.one/troubleshooting/valid-but-500/)

- **[AI 回复空白 / 截断 / 突然停止:六大原因与对策](data/markdown/empty-truncated.md)**
  - SillyTavern AI 回复异常完整排查:回复为空、中途截断、内容太短、突然失联四种现象分别对应的原因和解决方案,含万能反截断技巧。覆盖 Safety Filter、Max Tokens ...
  - 🌐 [在线阅读](https://guide.sillytavern.one/troubleshooting/empty-truncated/)

- **[常见错误码速查:401 / 403 / 404 / 429 / 500 / 502](data/markdown/error-codes.md)**
  - SillyTavern HTTP 错误码完整速查表,按出错概率排序。401 鉴权失败、429 限流、500 内部错误、ECONNRESET 等所有场景的真实原因与解决方案。每个错误码给出 3 种...
  - 🌐 [在线阅读](https://guide.sillytavern.one/troubleshooting/error-codes/)


### 🎯 进阶玩法
_长对话 / 群聊 / 高阶技巧_

- **[长对话失忆终极解决方案:三种总结技巧](data/markdown/long-chat-summary.md)**
  - SillyTavern 聊久了 AI 失忆怎么办?手动总结+隐藏、自动总结插件、记忆表格三种方案完整对比与最佳实践组合。覆盖 Vector Storage 向量化记忆、Summarize 总结脚...
  - 🌐 [在线阅读](https://guide.sillytavern.one/advanced/long-chat-summary/)

- **[群聊模式入门:让多个 AI 角色同台演出](data/markdown/group-chat.md)**
  - SillyTavern 群聊 (Group Chat) 完整入门。创建群聊、配置发言策略、多角色互动技巧、常见问题与让群聊活起来的秘诀。覆盖角色发言顺序设置、共享记忆策略、群聊专用提示词、单独 ...
  - 🌐 [在线阅读](https://guide.sillytavern.one/advanced/group-chat/)


---

## 🤝 贡献

欢迎社区贡献:
- 修错字 / 排版 / 链接失效 → 直接 PR
- 补充新坑 / 实战经验 → 先开 issue 讨论
- 加新教程 → 先开 issue 讨论选题

详见 [CONTRIBUTING.md](CONTRIBUTING.md)。

**不接受**:任何 API / 中转商推广 / 广告内容 / 商业引流。

## 📜 协议

内容采用 [**CC BY-NC-SA 4.0**](LICENSE)。允许转载、改编、再创作(注明来源),不允许商用和不署名使用。

## ✍️ 写作原则(反时效化设计)

1. **反时效化** — 写 "Claude Sonnet 模型" 而不是 "Claude Sonnet 4.5"
2. **多家平等** — 横评时按字母序或上手难度排,不刻意暗示主推
3. **客观避坑** — 实事求是说优缺点,不用 "最强 / 唯一" 等吹捧词
4. **不带广告** — 推荐工具时只链官方 / 开源仓库
5. **数字模糊化** — 写 "30000+ 角色卡" 而不是精确数字

## 🔄 更新

本仓库每周日 23:30 自动从 [在线版](https://guide.sillytavern.one/) 同步一次完整快照。

## 🙏 鸣谢

感谢 [SillyTavern 开源项目](https://github.com/SillyTavern/SillyTavern) 和所有为中文社区贡献过角色卡、预设、扩展的作者。
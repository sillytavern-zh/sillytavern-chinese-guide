---
title: "SillyTavern 文生图完整指南:三大后端 + 三种触发方式 + 国内用户特殊挑战"
description: "SillyTavern 文生图完整指南。集成 Stable Diffusion / NovelAI / DALL-E 3 三大后端,角色头像生成、场景插图、动态画面 3 种触发方式,中国大陆用户的 ComfyUI 本地方案、付费云端方案、API 中转方案对比,带提示词模板与避坑清单。"
slug: image-generation
category: extensions
canonical: https://guide.sillytavern.one/extensions/image-generation/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/extensions/image-generation/](https://guide.sillytavern.one/extensions/image-generation/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

# SillyTavern 文生图完整指南:三大后端 + 三种触发方式 + 国内用户特殊挑战

SillyTavern 内置的图像生成扩展是中文 AI 角色扮演圈最被低估的功能之一。配置好之后,你不只能让 AI 描写场景——还能让它**直接画出来**。本文从零讲清楚后端选择、3 种触发方式、提示词方法论、角色一致性技巧,以及国内用户最常踩的坑。

## 谁应该看这篇

- 已经能在 SillyTavern 跑通 AI 对话,想再上一台阶玩"图文沉浸式"
- 听说"AI 画图很复杂",但实际不知道从哪下手
- 想让 AI 在合适的时刻自动配图,而不是手动一张张画
- 国内用户,搞不清显卡门槛 / 网络问题 / 中转商风险

如果你还没跑通基础对话,先看 [30 分钟极速上手](/getting-started/quickstart/) 把基础打好,再回来。

## 核心机制:SillyTavern 不画图,它"调度"画图

理解这一点是看懂全文的钥匙。

> SillyTavern 本身是 **调度器**,不是 **绘图引擎**。
>
> `你 / AI` → `SillyTavern` → `画图后端` → 返回图像 → 显示在聊天里

后端可以是:
- 你电脑上跑的 Stable Diffusion WebUI 或 ComfyUI(本地后端)
- 云端付费 API(OpenAI / FLUX / Stability AI / NovelAI 等)
- 免费志愿者池 Stable Horde(慢但白嫖)

**这意味着两件事**:
1. SillyTavern 配置极简(填一个后端地址就完了),复杂度全在选哪种后端
2. 你的画图能力 = 后端能力,SillyTavern 不会"提升画质"

## 三大后端类型客观对比

| 维度 | 本地 SD WebUI | 本地 ComfyUI | 云端付费 API | 免费 Horde |
|------|--------------|--------------|-------------|-----------|
| 上手难度 | ⭐⭐ 简单 | ⭐⭐⭐⭐ 进阶 | ⭐ 最简单 | ⭐ 最简单 |
| 显卡要求 | 6GB+ 显存 | 6GB+ 显存 | 无 | 无 |
| 一次性成本 | 显卡费 | 显卡费 | 0 | 0 |
| 长期成本 | 电费 | 电费 | 按量计费 | 0 |
| 出图速度 | 5-30 秒 | 5-30 秒 | 10-60 秒 | 几分钟到几十分钟 |
| 模型生态 | 极丰富 | 最丰富 | 受官方限制 | 中等 |
| 内容自由度 | 完全自由 | 完全自由 | 严格限制 | 中等 |
| 隐私 | 100% 本地 | 100% 本地 | 提示词上传云端 | 提示词上传公共池 |

### 三句话决策法

- **有中端显卡(显存 ≥ 6GB)+ 想自由折腾** → 本地 ComfyUI
- **有显卡但不想学复杂工作流** → 本地 SD WebUI
- **没有显卡 + 不在乎付费** → 云端 API
- **没有显卡 + 想白嫖** → Stable Horde

## 实战 1:本地 SD WebUI 接入(8 步)

最经典、最稳定,也是国内中文社区资料最多的方案。

### 步骤 1-3:启动 SD WebUI 并打开 API

确保你已经成功跑通 SD WebUI 本身(本文不教 SD WebUI 的安装,那是单独主题)。

启动时**必须**带上 `--api` 参数:

- Windows:编辑 `webui-user.bat`,在 `set COMMANDLINE_ARGS=` 后加 `--api`
- Linux/macOS:`./webui.sh --api`

SD WebUI 默认监听 `http://127.0.0.1:7860`,启动后保持窗口开着。

### 步骤 4-6:在 SillyTavern 中接入

1. 进入 SillyTavern,点右上角扩展菜单(拼图图标)
2. 找到 "Image Generation" 扩展并展开
3. **API 类型**:选 `Stable Diffusion WebUI`
4. **服务器 URL**:填 `http://127.0.0.1:7860`
5. 点 **Connect** 按钮,显示 "Connected" 即成功

### 步骤 7-8:测试一张

聊天框输入 `/sd 一只猫坐在窗台上,水彩画风格`,等待 5-30 秒,图就出来了。

如果失败,看下方"故障排查"章节。

## 实战 2:本地 ComfyUI 接入(6 步)

更灵活、更强大,但学习曲线更陡。

ComfyUI 是节点式工作流图形化工具——把"加载模型 → 编码提示词 → 采样 → 解码 → 保存"每一步都做成节点,你拖拽连接。

### 步骤 1:启动 ComfyUI

正常启动 ComfyUI,无需任何特殊参数(API 默认开启)。默认监听 `http://127.0.0.1:8188`。

### 步骤 2-3:SillyTavern 中接入

1. 扩展面板 → Image Generation
2. **API 类型**:选 `ComfyUI`
3. **服务器 URL**:`http://127.0.0.1:8188`
4. 点 Connect

### 步骤 4-5:选择默认工作流

连接成功后,**Workflow** 下拉菜单选 `Default_Comfy_Workflow.json`。这是 SillyTavern 自带的基础文生图工作流,直接能用。

如果你想用自己的工作流:
1. 在 ComfyUI 里搭建并测试通过
2. 开启 ComfyUI 的"开发者模式"(设置里)
3. 点 **Save (API Format)** 下载 JSON
4. 回 SillyTavern,**Create New Workflow**,粘贴 JSON

### 步骤 6:测试

`/sd test`,出图即成功。

## 实战 3:云端 API 接入(5 选 1)

完全没显卡的用户的救星。

### 选项 A:OpenAI DALL-E 系列

- 优点:质量稳定,API 文档完善
- 缺点:严格内容审查,价格不低
- 配置:**API 类型** 选 `OpenAI`,填你的 OpenAI API key

### 选项 B:Black Forest Labs FLUX

- 优点:目前画质标杆之一
- 缺点:贵,需要 BFL 账号
- 配置:**API 类型** 选 `Black Forest Labs`

### 选项 C:Stability AI 官方

- 优点:模型作者亲生,API 最早
- 缺点:贵,审查较严

### 选项 D:NovelAI

- 优点:动漫风格圈内首选,提示词系统强大
- 缺点:海外服务,国内访问困难;需 NAI 订阅
- 国内用户经常配合中转使用(见后文国内挑战章节)

### 选项 E:Stable Horde(免费!)

- 优点:**完全免费**,无需信用卡
- 缺点:志愿者池排队,慢的时候要等几十分钟
- 适合:偶尔想画一张玩玩,不在乎速度
- 配置:**API 类型** 选 `Stable Horde`,可以选填 anonymous 或注册 key 提速

## 三种触发方式

配置好后端,有三种方式让图出来。

### 方式 1:魔杖菜单(图形化,最直观)

1. 聊天界面右上角,点魔杖图标
2. 选 **Image Generation**
3. 选生成模式:
   - **Character**:画当前对话的 AI 角色
   - **Self**:画用户自己(基于 Persona 描述)
   - **Scene**:画当前场景(基于最近几条消息)
   - **Raw Last Message**:基于最后一条消息生成
   - **Free Mode**:你直接输入提示词
4. 点 Generate,图自动插入聊天

### 方式 2:`/sd` 斜杠命令(最快)

直接在聊天框输入:

```
/sd 你的提示词
```

进阶用法:

```
/sd character          # 画当前角色
/sd self               # 画用户
/sd scene              # 画场景
/sd background         # 生成背景图
/sd raw=...            # 不带任何模板,纯提示词出图
```

加负面提示词:

```
/sd negative=低质量,模糊 一只可爱的猫,水彩画
```

### 方式 3:函数调用自动生成(最沉浸)

让 AI 在合适时刻自动决定要画图。

1. 扩展面板 → Image Generation → 勾选 **Interactive Mode** / 函数调用
2. 你的对话模型必须支持函数调用(Claude / GPT-4o 系列等)
3. 在聊天里说"展示一下你现在的样子"或"画一下我们现在的房间",AI 会自动触发画图

这种方式最沉浸,但**需要相对强的对话模型才能正确判断时机**,弱模型会乱触发或永远不触发。

## 提示词工程方法论(不教具体 tag,教思路)

提示词工程是单独的学科,本节只讲**通用思路**。具体的 tag 词典请去:

- [Danbooru wiki](https://danbooru.donmai.us/wiki_pages)(动漫风格)
- 各模型官方文档

### 三层结构法

一个有效的提示词通常分三层:

```
[质量层] [风格层] [内容层]

例:
  masterpiece, best quality, highly detailed,    ← 质量层(固定)
  anime style, watercolor,                       ← 风格层
  1girl, long hair, smile, sitting in cafe       ← 内容层
```

### 负面提示词

负面提示词排除"你不想要的":

```
lowres, bad anatomy, bad hands, blurry, jpeg artifacts,
worst quality, low quality, signature, watermark
```

新手把这一串当模板抄上,效果立刻提升一档。

### 不要踩的坑

1. **提示词越多≠越好**:超过 75 个 token 后权重会下降,精简比堆砌强
2. **正负相互覆盖**:同一个词同时出现在正面和负面 = 0 效果
3. **追求"超详细描述"**:模型理解力有限,过多细节反而让画面混乱
4. **照抄别人的画师串**:不同模型的风格 tag 不通用,SDXL 系画师串拿到 SD 1.5 完全无效

## 角色一致性(进阶痛点)

新手最快遇到的痛:**每次生成同一个角色都长得不一样**。三种解决方案,从简单到复杂:

### 方案 1:固定 Seed + 提示词模板(免费)

在角色信息里填详细的"外貌描述"(头发颜色、瞳色、典型服装等)作为图像生成前缀。SillyTavern 会自动加到每次生成的提示词前。

- 优点:简单
- 缺点:同一描述还是会画出不同人

### 方案 2:IP-Adapter(本地 ComfyUI 进阶)

IP-Adapter 是一个让模型"参考一张图"再生成的技术。你给它一张你定义好的角色头像,它会在新生成时尽量保持五官一致。

需要在 ComfyUI 里搭工作流(网上教程多)。

### 方案 3:Auto Illustrator 扩展(自动配图)

第三方 SillyTavern 扩展,在 AI 回复时自动在合适时刻插入插图。

仓库地址:[github.com/gamer-mitsuha/sillytavern-auto-illustrator](https://github.com/gamer-mitsuha/sillytavern-auto-illustrator)

安装方式:

1. SillyTavern → 扩展菜单 → Install Extension
2. 粘贴上面的 URL
3. 安装完成后,在扩展列表里找到 Auto Illustrator,启用并配置

## 国内用户特殊挑战(客观说明,不推荐具体商家)

国内用户配置文生图后端时,会遇到 3 个典型问题。我们客观说明,你自己评估方案。

### 挑战 1:本地显卡门槛

Stable Diffusion 系列模型对显卡的要求:

- **极简凑合**:6GB 显存,跑得动但慢、分辨率受限
- **舒适**:12GB+ 显存,流畅出图
- **专业**:24GB+ 显存,大模型 + 高分辨率 + 批量

如果你的电脑没有合适显卡,**不要硬上**——用云端 / Horde 即可。

### 挑战 2:海外 AI 服务的网络访问

OpenAI / FLUX / NovelAI 等海外服务,国内直接访问会:

- 速度极慢或频繁超时
- 部分服务地区屏蔽
- 需要科学上网

可选方案:

**方案 A:用国际信用卡或 PayPal 直接订阅**

最稳,价格最透明,数据隐私最高。但需要工具能稳定访问。

**方案 B:使用国内 NAI / SD 中转服务**

市面上存在多家中转,**选择时务必评估**:

- 服务商透明度(是否有备案、客服、合规声明)
- 价格合理性(每次生成 0.01-0.05 元为常见区间,异常便宜要警惕)
- 隐私政策(是否会保存你的提示词或生成结果)
- 跑路风险(预付金额建议先试水,不要一次充很多)
- 用户评价(在公开社区搜真实用户反馈)

**本站不推荐任何具体中转商**,因为这个市场频繁洗牌,推荐 = 给用户挖坑。

**方案 C:Stable Horde 免费**

慢但完全免费,适合偶尔玩。

### 挑战 3:NSFW 内容的合规边界

如果你打算生成包含成人内容的图像:

- **本地后端**:技术上完全自由,但**请务必遵守当地法律**,不分发不传播
- **云端官方 API**:OpenAI / Stability AI / FLUX 全部明确禁止 NSFW
- **国内中转**:某些中转不限制但属于灰色地带,**自负风险**

我们站点定位为**纯公益教程**,不提供任何 NSFW 内容引导,不发布具体 NSFW 提示词或画师 tag。如果你需要这方面的资源,请自行去对应社区寻找。

## 5 个最常见的误区

### 误区 1:"装上 SillyTavern 就能画图了"

错。SillyTavern 是调度器,**必须**配一个后端才能画。

### 误区 2:"AI 画图就是输入几个字让它画"

错。出好图 = 提示词工程 + 负面提示词 + 模型选择 + 参数调整,有学习曲线。

### 误区 3:"贵的云端 API 一定比本地好"

不一定。本地 SDXL + 一个好的 finetune 模型,在动漫风格上可能比 DALL-E 还好。云端的优势主要是**省心** + **不用显卡**,不是绝对画质。

### 误区 4:"中转商是国内用户唯一选择"

错。除了中转,还有:

- 直接订阅(用国际支付方式)
- Stable Horde 免费
- 自己装本地 ComfyUI

### 误区 5:"装了文生图就能让所有 AI 自动配图"

不一定。**自动函数调用要求 AI 模型本身支持 function calling**(GPT-4o / Claude 系列等),弱模型只能用斜杠命令或魔杖菜单手动触发。

## 常见问题速查

### Q1:SD WebUI 显示连接失败?

检查:

- 是否带 `--api` 启动?
- 端口是否 7860?
- 试试 `http://localhost:7860` 替换 `127.0.0.1:7860`
- 防火墙是否拦截

### Q2:ComfyUI 工作流报"missing node"?

工作流里有缺失的节点。多数情况下需要在 ComfyUI 里装对应自定义节点。如果是基础工作流,先用 `Default_Comfy_Workflow.json` 测试。

### Q3:生成的图和描述不符?

- 提示词不够具体(用三层结构)
- CFG Scale 设太高或太低(常用 7-10)
- 步数不够(常用 25-40)
- 模型选择不对(动漫题材选动漫模型,写实选写实模型)
- 加详细的负面提示词

### Q4:角色每次画都不一样?

正常的,见前面"角色一致性"章节。三种方案选一个用。

### Q5:云端 API 报"content policy violation"?

提示词触发了官方内容审查。改用更中性的描述,或换支持 NSFW 的本地后端。

### Q6:Stable Horde 排队太久?

正常的,这是免费志愿者池。考虑:

- 上 Horde 网站充点 kudos 提速(其实也是免费可获取的)
- 改用本地或付费云端

### Q7:画图速度慢怎么办?

本地:

- 升级显卡
- 降低分辨率(从 1024×1024 降到 768×768 立刻快一倍)
- 减少步数(40 → 25)
- 用 Turbo / LCM 系列快速模型

云端:网络问题为主,改时段或换节点。

### Q8:可以让 AI 在对话过程中自动配图吗?

可以。两种方案:

1. SillyTavern 内置的 Interactive Mode(扩展面板里勾选)
2. 装 Auto Illustrator 扩展

效果取决于你的对话模型够不够聪明。

## 接下来去哪

- 没装过 SillyTavern → [30 分钟极速上手](/getting-started/quickstart/)
- 想了解扩展生态 → [必装扩展 TOP 10](/extensions/top-10/)
- AI 经常报错 → [Valid 但 500 完整排查](/troubleshooting/valid-but-500/)
- AI 总是失忆 → [记忆插件 4 家横评](/extensions/memory-extensions/)
- 想玩长篇剧情 → [长对话失忆终极方案](/advanced/long-chat-summary/)

---

## 📖 关于本文

- **原文**: [SillyTavern 文生图完整指南:三大后端 + 三种触发方式 + 国内用户特殊挑战](https://guide.sillytavern.one/extensions/image-generation/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/extensions/image-generation/) 为准。

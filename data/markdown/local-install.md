---
title: "SillyTavern 本地部署完整教程:Windows / macOS / Linux 三平台傻瓜式指南"
description: "SillyTavern 本地部署全平台完整步骤。从装 Node.js 到跑通第一次对话,所有报错完整对照表,30-90 分钟跑通。"
slug: local-install
category: getting-started
canonical: https://guide.sillytavern.one/getting-started/local-install/
license: CC BY-NC-SA 4.0
source: SillyTavern 中文教程站
---

> 📚 **本文原始版本及最新更新**: [https://guide.sillytavern.one/getting-started/local-install/](https://guide.sillytavern.one/getting-started/local-install/)
> 📜 协议: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

> **一句话答**:跑通本地部署 = 装 Node.js 20+ → git clone → npm install → node server.js → 浏览器打开 localhost:8000。三个平台原理一致,差异只在装 Node 这一步上。

> **关键事实**
> - 第一次跑通通常 30-90 分钟,大头是 npm install 拉依赖
> - 95% 的失败是 Node 版本太老,或国内网络拉不到 npm 包
> - 跟着步骤一步一步来,几乎不会卡住
> - 后续更新只要 git pull 加 npm install 一次

本地部署没有想象中难。难的是中间报错时不知道是网络问题、版本问题还是权限问题。

这一篇按 Windows / macOS / Linux 三个平台分别讲一遍,所有可能的报错列在末尾对照表里,卡住直接 Ctrl+F 搜错误文字。

## 谁应该选本地部署

不要看别人说"本地数据私有所以好",自己要不要折腾看 3 个问题:

**问 1**:你能基本看懂命令行报错吗?(`npm install` 报红字时不会立刻关电脑)

**问 2**:你的电脑能长期开着吗?(笔记本合盖即关 / 手机不算)

**问 3**:你愿意自己解决端口冲突、防火墙、跨设备同步问题吗?

**任何一个问题答"不"——直接走云端版**,不要硬上本地。

如果三个都"是",继续看。

## 准备工作(三平台共通)

无论哪个系统,你都需要:

1. **能稳定访问 GitHub 的网络**(国内通常需要梯子,或用国内镜像)
2. **Node.js 20.x LTS 或更新**(18.x 也能跑但不推荐)
3. **Git 命令行工具**
4. **一个固定目录放代码**:Windows 推荐 `D:\SillyTavern`,macOS / Linux 推荐 `~/SillyTavern`
5. **30 分钟空闲时间**(不要在赶时间时装)

---

## Windows 完整步骤

### 1.1 装 Node.js

访问 https://[nodejs.org](https://nodejs.org) → 下载 **LTS 版本**(标着 Recommended)→ 双击 .msi 安装包 → **一路 Next 默认就行**(不需要改任何选项)→ 完成。

打开 PowerShell(开始菜单搜 powershell)→ 跑:

```
node --version
npm --version
```

显示版本号(比如 `v20.18.0` 和 `10.x.x`) = 装好了。

> **国内拉不到 [nodejs.org](https://nodejs.org)**?用淘宝镜像 https://npmmirror.com/mirrors/node/ 找最新 LTS 版手动下载 .msi。

### 1.2 装 Git

访问 https://git-scm.com/download/win → 下载 → 一路 Next → 安装完打开 PowerShell:

```
git --version
```

显示版本号 = OK。

### 1.3 拉酒馆代码

PowerShell 里跑:

```
cd D:\
git clone https://github.com/SillyTavern/SillyTavern.git
cd SillyTavern
```

> **git clone 拉不动 / 超时**?
> - 开梯子重试
> - 或下载 zip:打开 https://github.com/SillyTavern/SillyTavern/archive/refs/heads/release.zip → 解压到 `D:\SillyTavern`

### 1.4 装依赖

```
npm install --no-audit --no-fund
```

第一次大约 5-15 分钟,慢点正常。

> **国内 npm 慢**?换淘宝源后再装:
>
> ```
> npm config set registry https://registry.npmmirror.com
> npm install --no-audit --no-fund
> ```

### 1.5 启动

```
node server.js
```

看到 `SillyTavern is listening on http://0.0.0.0:8000` 这行 = 成功。**保持这个 PowerShell 窗口开着**(关了酒馆就停了)。

### 1.6 浏览器访问

浏览器打开:**`http://localhost:8000`**

看到酒馆界面 = 跑通了。

---

## macOS 完整步骤

### 2.1 装 Homebrew(如果没装)

打开 Terminal,跑:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

按提示输密码,等几分钟。

### 2.2 装 Node 和 Git

```
brew install node@20 git
brew link node@20 --force
node --version
```

### 2.3 拉代码 + 装依赖 + 启动

```
cd ~
git clone https://github.com/SillyTavern/SillyTavern.git
cd SillyTavern
npm install --no-audit --no-fund
node server.js
```

浏览器开 **`http://localhost:8000`**。

> **macOS 11 以下**:Homebrew 新版可能不支持太老的 macOS。可以直接从 https://[nodejs.org](https://nodejs.org) 下载 .pkg 安装包。

---

## Linux(Ubuntu / Debian)完整步骤

### 3.1 装基础工具

```
sudo apt update
sudo apt install -y curl git build-essential
```

### 3.2 装 Node 20

```
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
node --version
```

### 3.3 拉代码 + 启动

```
cd ~
git clone https://github.com/SillyTavern/SillyTavern.git
cd SillyTavern
npm install --no-audit --no-fund
node server.js
```

浏览器开 **`http://localhost:8000`**。

> **CentOS / RHEL / Fedora**:用 `dnf` 替代 `apt`,Node 安装脚本是 `https://rpm.nodesource.com/setup_20.x`。
>
> **Arch / Manjaro**:`sudo pacman -S nodejs npm git base-devel`。

---

## 启动后第一次配置

浏览器开 `http://localhost:8000` 看到酒馆界面就跑通了。

接下来按 [30 分钟极速上手](/getting-started/quickstart/) 一步步配 API、导卡、配预设。本地部署和云端版从这一步开始用法完全一样。

---

## 常见报错完整对照表

按报错文字 Ctrl+F 找。

### 启动报错

| 报错关键字 | 原因 | 解决 |
|---|---|---|
| `EADDRINUSE` 或 `address already in use` | 8000 端口被占 | 改端口启动:`node server.js --port 8001`,或编辑 `config.yaml` 改 `port: 8001` |
| `Cannot find module 'xxx'` | 依赖没装全 | `rm -rf node_modules && npm install`(Windows 用 `Remove-Item -Recurse node_modules`) |
| `SyntaxError: Unexpected token` | Node 版本太老 | 升级到 20.x LTS |
| `Whitelist mode rejected` 但你就在本机访问 | 浏览器代理把请求改了源 IP | 关掉浏览器代理 / 改用 127.0.0.1 |

### npm install 报错

| 报错关键字 | 原因 | 解决 |
|---|---|---|
| `network timeout` / `ETIMEDOUT` | 拉 npm 包超时 | 换淘宝源:`npm config set registry https://registry.npmmirror.com` |
| `EACCES: permission denied` | 权限问题(Linux/Mac) | `sudo chown -R $USER ~/SillyTavern`,**不要**用 sudo 跑 npm install |
| `gyp ERR! find Python` | 缺 Python(某些 native 依赖需要) | Linux/Mac:`sudo apt install python3-dev` 或 `brew install python`;Windows:装 Visual Studio Build Tools |
| `node-gyp rebuild` 报错 | C++ 编译工具缺失 | Windows:装 Visual Studio Installer 选 "Desktop development with C++";Linux: `sudo apt install build-essential` |
| 磁盘空间不足 | `node_modules` 占 ~500MB | `df -h`(Linux/Mac)/ 资源管理器看看(Windows),清空间 |

### git clone 报错

| 报错关键字 | 原因 | 解决 |
|---|---|---|
| `RPC failed; curl 28 ...` | 超时,通常梯子问题 | 重试 / 换梯子节点 / 或下载 zip 解压 |
| `unable to resolve host` | DNS 问题 | 换 DNS(8.8.8.8 / 1.1.1.1),`nslookup github.com` 验证 |
| `SSL certificate problem` | 证书问题(公司/校园网常见) | **临时**:`git config --global http.sslVerify false`(用完记得开回来) |

### 浏览器打开报错

| 现象 | 原因 | 解决 |
|---|---|---|
| 浏览器显示"无法访问此站点" | 终端没有 listening 那行 | 看终端有没有报错 |
| 弹窗 Windows 防火墙 | 第一次启动 Node 触发 | 点"允许访问" |
| 页面打开但白屏 | 浏览器版本太老 | 换 Chrome / Edge 最新版 |
| 其他设备连不上 | 默认只监听 localhost | 改 `config.yaml` 里 `listen: true`,然后用电脑局域网 IP 访问(如 `192.168.1.100:8000`) |

---

## 日常更新

```bash
cd ~/SillyTavern    # 或 D:\SillyTavern
git pull
npm install --no-audit --no-fund
node server.js
```

---

## 跨设备访问(手机/平板访问电脑上的酒馆)

1. 电脑和手机在**同一个 WiFi** 下
2. 编辑酒馆目录下的 `config.yaml`,找到 `listen` 设为 `true`
3. 重启酒馆
4. 手机浏览器输入 `http://电脑内网IP:8000`(比如 `http://192.168.1.100:8000`)

> **找不到电脑 IP**?Windows 跑 `ipconfig`,macOS/Linux 跑 `ifconfig` 或 `ip addr`,找 `192.168.x.x` 的那行。

---

## 卸载

1. 停掉酒馆(终端 Ctrl+C)
2. 删掉整个 `SillyTavern` 文件夹
3. Node.js 如果不用了可以卸(Windows 控制面板 / macOS `brew uninstall node` / Linux `sudo apt remove nodejs`)

---

## 相关阅读

- [云端版 vs 本地部署完整对比](/getting-started/cloud-vs-local/)
- [30 分钟极速上手](/getting-started/quickstart/)
- [自定义 API 端点配置](/api-config/custom-api-setup/)

---

## 📖 关于本文

- **原文**: [SillyTavern 本地部署完整教程:Windows / macOS / Linux 三平台傻瓜式指南](https://guide.sillytavern.one/getting-started/local-install/)
- **教程站首页**: [SillyTavern 中文教程站](https://guide.sillytavern.one/)
- **GitHub 镜像**: [sillytavern-zh/sillytavern-chinese-guide](https://github.com/sillytavern-zh/sillytavern-chinese-guide)
- **协议**: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 允许转载/改编/再创作(需注明来源),不允许商用

> 转载请保留本段。最新内容请以 [在线版](https://guide.sillytavern.one/getting-started/local-install/) 为准。

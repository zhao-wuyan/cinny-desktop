# Cinny desktop

中文 | [English](./README.md)

<a href="https://github.com/cinnyapp/cinny-desktop/releases">
  <img alt="GitHub release downloads" src="https://img.shields.io/github/downloads/cinnyapp/cinny-desktop/total?style=social"></a>

Cinny 是一款注重简洁、优雅和安全界面的 Matrix 客户端。桌面应用基于 Tauri 构建。

## Fork 特性

本 fork 在原版 Cinny 基础上新增以下特性：

| 特性 | 说明 |
|------|------|
| **Markdown 表格渲染** | 支持在消息中渲染 MD 表格，便于查看结构化数据 |
| **i18n 多语言** | 内置完整的中文等多语言翻译，提升本地化体验 |
| **多账户切换** (`feature/mulact`) | 支持在同一客户端内管理多个 Matrix 账户，快速切换登录 |

> 子模块指向 [cinny-i18n](https://github.com/zhao-wuyan/cinny-i18n)，包含最新的国际化翻译。

## 下载

macOS、Windows 和 Linux 的安装包可从 [GitHub Releases](https://github.com/cinnyapp/cinny-desktop/releases) 下载。发布版本使用 [Ed25519](https://ed25519.cr.yp.to/) 公钥签名。

操作系统 | 下载
---|---
Windows | <a href='https://github.com/cinnyapp/cinny-desktop/releases/latest/download/Cinny_desktop-x86_64.msi'>Windows 版下载</a>
macOS | <a href='https://github.com/cinnyapp/cinny-desktop/releases/latest/download/Cinny_desktop-universal.dmg'>macOS 版下载</a>
Linux | <a href='https://github.com/cinnyapp/cinny-desktop/releases/latest/download/Cinny_desktop-x86_64.AppImage'>Linux 版下载</a> · <a href='https://flathub.org/apps/details/in.cinny.Cinny'>Flatpak</a>

公钥内容：
> RWSFOsZ6hsZQsf9PVx4oZeh/kx44Fb2PR2djy4UtXGqnouNHQtzc5JUY

验证发布文件，需要下载 [minisign](https://jedisct1.github.io/minisign/) 工具并先 [解码](https://www.base64decode.org/) *.sig* 文件：
>  minisign -Vm ***RELEASE_FILE.msi.zip*** -P RWSFOsZ6hsZQsf9PVx4oZeh/kx44Fb2PR2djy4UtXGqnouNHQtzc5JUY -x ***SINGATURE.msi.zip.sig***

## 本地开发

首先，按照 [Tauri 文档](https://tauri.app/v1/guides/getting-started/prerequisites) 配置 Rust、NodeJS 和构建工具。

然后运行以下命令设置本地开发环境：
* `git clone --recursive https://github.com/zhao-wuyan/cinny-desktop.git`
* `cd cinny-desktop/cinny`
* `npm ci`
* `cd ..`
* `npm ci`

本地构建应用：
* `npm run tauri build`

启动本地开发服务器：
* `npm run tauri dev`

## 子模块管理

本项目使用 `cinny` 作为 git 子模块，指向 [cinny-i18n](https://github.com/zhao-wuyan/cinny-i18n)。

> **注意**：子模块 **不会** 自动更新。它们固定在特定提交。需要时必须手动更新。

### 更新子模块到最新版本

**方法 1：快速更新（推荐）**
```bash
# 拉取远程最新提交
git submodule update --remote cinny
git add cinny
git commit -m "chore: update cinny submodule"
```

**方法 2：合并/变基模式（适用于有本地修改）**
```bash
# 合并模式
git submodule update --remote --merge cinny

# 变基模式
git submodule update --remote --rebase cinny
```

**方法 3：手动更新**
```bash
cd cinny
git checkout main
git pull origin main
cd ..
git add cinny
git commit -m "chore: update cinny submodule"
```

**一行命令（完整流程）：**
```bash
git submodule update --remote --merge cinny && git add cinny && git commit -m "chore: update cinny submodule"
```

### 初始化子模块

**新克隆时使用 `--recursive`：**
```bash
git clone --recursive https://github.com/zhao-wuyan/cinny-desktop.git
```

**已克隆但无子模块：**
```bash
git submodule update --init cinny
```

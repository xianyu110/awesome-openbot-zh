# OpenBot 小白中文教程

> **nightly-labs/openbot** 本地优先「持久 AI 队友」桌面工作区 · 社区非官方中文入门  
> 上游：[`nightly-labs/openbot`](https://github.com/nightly-labs/openbot) · 官网：[openbot.run](https://openbot.run/)  
> 教程校对：2026-10-27（Asia/Shanghai）· 对照上游 **v0.51.1**

[![GitHub stars](https://img.shields.io/github/stars/xianyu110/awesome-openbot-zh?style=social)](https://github.com/xianyu110/awesome-openbot-zh)
[![Upstream](https://img.shields.io/badge/upstream-nightly--labs%2Fopenbot-blue)](https://github.com/nightly-labs/openbot)
[![License](https://img.shields.io/badge/license-MIT%20(tutorial)-green.svg)](LICENSE)
[![Pages](https://img.shields.io/badge/GitHub%20Pages-online-brightgreen)](https://xianyu110.github.io/awesome-openbot-zh/)

---

## 先分清：这不是 Intel OpenBot

| 名称 | 是什么 | 链接 |
|------|--------|------|
| **本教程的 OpenBot** | nightly-labs 的 **桌面 AI 队友工作区**（Electron），对接 Codex / Claude / Grok / OpenCode / Gemini / Cursor CLI / Cline 等 | https://github.com/nightly-labs/openbot |
| Intel **OpenBot**（机器人） | 面向安卓手机的开源机器人平台，和本文无关 | （请勿混淆） |

下文「OpenBot」一律指 **nightly-labs/openbot**。

---

## 这是什么？

OpenBot 是 **local-first** 的桌面工作区：每个 Agent 有独立工作区与对话，支持本地队列、文件传输、内嵌浏览器、Agent 之间互发消息。它能对接：

- 本地 [Codex App Server](https://learn.chatgpt.com/docs/app-server)、[Claude Code](https://code.claude.com/docs/en/overview)
- [Grok CLI](https://docs.x.ai/build/overview)、OpenCode、Gemini、[Cursor CLI](https://cursor.com/cli)、[Cline CLI](https://cline.bot/cli)（经 ACP）
- **自定义 OpenAI 兼容端点**，以及本机 **Ollama / LM Studio** 等本地模型服务的探测

> [!WARNING]
> 上游明确：当前为开发预览。Agent 以 `danger-full-access` + `approvalPolicy: never` 运行——首次同意后，可读写文件、跑命令、上网、控制内嵌浏览器，**无逐步确认**。只跑你信任的任务，做好备份，先读上游 [Security](https://github.com/nightly-labs/openbot#security)。

本仓库只提供**中文小白教程**（MIT），**不二次分发**官方安装包 / 二进制。

---

## 官方链接

| 资源 | 链接 |
|------|------|
| 官网 | https://openbot.run/ |
| 源码 | https://github.com/nightly-labs/openbot |
| Releases | https://github.com/nightly-labs/openbot/releases |
| 排障 | https://github.com/nightly-labs/openbot/blob/main/docs/TROUBLESHOOTING.md |
| 隐私 | https://github.com/nightly-labs/openbot/blob/main/PRIVACY.md |
| 协议全文 | [PolyForm Noncommercial 1.0.0](https://github.com/nightly-labs/openbot/blob/main/LICENSE) |

---

## 许可证（务必读）

| 内容 | 协议 |
|------|------|
| **本教程文案** | [MIT](LICENSE) |
| **OpenBot 上游软件** | **PolyForm Noncommercial License 1.0.0**（非商业用途下可使用 / 修改 / 分发代码；**商业使用需另向版权方授权**） |

合规要点（教程侧）：

1. **可以**写教程、截图说明安装步骤。  
2. **不要**在本仓库或镜像站**再分发**官方 `.dmg` / `.exe` / `.AppImage` 等二进制。请用户始终从 [GitHub Releases](https://github.com/nightly-labs/openbot/releases) 下载。  
3. 商业场景请联系上游：`licenses@openbot.run`（见官方 README）。  
4. ≤0.1.11 曾 Apache-2.0；当前主线以 PolyForm Noncommercial 为准。

---

## 环境要求（摘要）

- **macOS 13+**（Apple Silicon 或 Intel）
- **Windows 10+**（x64）
- **Linux**：x64 / arm64 **AppImage**
- 至少准备好一种 Agent 运行时（应用内可 Download，或本机已装 CLI）
- OpenBot 是 local-first，**不是**完全离线：各供应商仍会连各自云端

---

## 安装：macOS

1. 打开 [Releases](https://github.com/nightly-labs/openbot/releases/latest)，下载例如：  
   - Apple Silicon：`OpenBot-0.51.1-arm64.dmg`  
   - Intel：`OpenBot-0.51.1-x64.dmg`  
   （版本号以页面最新为准）
2. 打开 DMG，把 **OpenBot** 拖到「应用程序」。
3. 首次启动时仔细阅读并确认 **danger-full-access** 同意提示。

---

## 安装：Windows

1. 下载例如：`OpenBot-0.51.1-x64.exe`。  
2. 运行安装程序，打开 OpenBot。  
3. Windows 发行包由 `SYNTHETIFY LABS …` 签名；新版本仍可能触发 SmartScreen——请核对 Release 校验和 / attestation 后再运行。

---

## 安装：Linux（AppImage）

```bash
# 下载对应架构后：
chmod +x OpenBot-*-x86_64.AppImage   # 或 arm64
./OpenBot-*-x86_64.AppImage
```

常见系统注意（摘自官方）：

- 需要 **fuse3**（`fusermount3`），不是 libfuse2。  
- **Ubuntu 23.10+ / Debian 13**：AppArmor 限制用户命名空间时，需安装官方 AppArmor 配置后 `systemctl reload apparmor`。  
- **不要**用 `--no-sandbox` 启动（官方明确不支持）。

无界面服务器（Ubuntu 24.04/26.04 + systemd）可选：

```bash
curl -fsSL https://raw.githubusercontent.com/nightly-labs/openbot/main/scripts/install-server.sh | sudo bash
sudo openbot login
```

Docker / Nix 见上游 README，本教程不展开。

---

## Agent 运行时（第一次必做）

应用内可在引导 / Settings / 模型选择里点 **Download** 让 OpenBot 管理 CLI。也可自己装：

**Codex（macOS 示例）：**

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
codex login
```

**Claude：**

```bash
curl -fsSL https://claude.ai/install.sh | bash
claude auth login
```

Windows：自行安装原生 CLI，确保 PowerShell 里能跑 `codex` / `claude` / `grok` 等；Claude Code 还需要 **Git for Windows**。装好后**完全退出再打开** OpenBot。

本地模型：可在设置里接 **OpenAI 兼容端点**，并优先探测本机 **Ollama / LM Studio**（官方能力）。国内读者请优先本地或合规国内端，见下文「合规」。

排障入口：[docs/TROUBLESHOOTING.md](https://github.com/nightly-labs/openbot/blob/main/docs/TROUBLESHOOTING.md)。

---

## 第一次演示任务（约 15 分钟）

1. 安装并打开 OpenBot，完成首次安全同意。  
2. 在 Providers 里选一个你已有账号的供应商（或本机 Ollama），完成 Connect / Sign in。  
3. 新建一个 Agent，工作区指向一个**玩具 git 仓库**（不要直接指向重要生产目录）。  
4. 发一句只读任务，例如：  
   `请只读当前工作区 README，用中文列 5 条要点，不要修改任何文件。`  
5. 确认对话与队列行为正常后，再尝试更复杂的改代码任务。  
6. （可选）试一下 Agent 之间发消息 / 共享频道——先用无敏感数据。

终端风格示意：

```text
OpenBot · provider: Ollama (local) · agent: demo-reader
▶ workspace: ~/OpenBot/Agents/demo-reader
▶ user: "只读 README，中文 5 条要点，不要改文件"
✓ reply ready · review Changes before any write-heavy task
```

---

## 常见报错与处理

| 现象 | 处理 |
|------|------|
| 提示需要 agent CLI | 按官方装 Codex/Claude 等，或应用内 Download；非标准路径用 `OPENBOT_*_PATH` |
| Linux AppImage 立刻退出 | 装 AppArmor profile + reload；勿用 `--no-sandbox` |
| `fusermount` 找不到 | 安装 `fuse3` |
| SmartScreen / Gatekeeper | 核对 Release 校验和后再运行 |
| GPU 导致卡顿/崩溃（Linux） | 见上游：可 `OPENBOT_DISABLE_GPU=1`；或删掉 `gpu-crash.json` 后再试 |
| Gemini 登录失败 | 需本机桌面浏览器 + `xdg-utils`；回调走 `127.0.0.1`，无桌面服务器无法完成 |

数据目录等见上游「Local data and network boundaries」（如 `~/OpenBot/Agents/...`）。

---

## 模型 / API 合规说明（国内读者）

- OpenBot **本身**主要是工作区壳；真正对话走各 CLI / 你配置的兼容端。  
- 本教程**不硬推**未备案境外模型中转。优先：  
  - **Ollama / LM Studio** 等本地端  
  - DeepSeek 等国内可用服务（以你账号与法规为准）  
  - 若必须用聚合 OpenAI 兼容口，可自行评估 [TryAllAPI](https://tryallapi.com/register?aff=5A6A)（轻提示，非必须）  
- 周边选购（可选）：[https://wzyp.cn/shop/maynorai](https://wzyp.cn/shop/maynorai)  
- **不要**把本仓当成安装包镜像站。

---

## 维护

- 作者：Maynor（[@xianyu110](https://github.com/xianyu110) / Maynor996）  
- 产品问题优先查 [上游 Issues](https://github.com/nightly-labs/openbot/issues)  
- 在线页：https://xianyu110.github.io/awesome-openbot-zh/  
- 与 nightly-labs / Synthetify Labs **无官方隶属关系**

# agent-lx-music-skills 🎶

> **AI 智能代理专属的音乐播放控制与超能力技能库**

`agent-lx-music-skills` 是一个专门为 `agent-lx-music` (alx) CLI 工具定制的 AI Agent Skills (智能技能) 仓库。它能够让如 Claude Code、Gemini CLI、Codex 等 AI 代理无缝加载，使其立即掌握搜歌、放歌、播放队列管理、高并发下载以及歌单维护的硬核超能力！

通过将技能与原包体解耦，用户与代理无需完整克隆庞大的主工程仓库，即可直接独立拉取本仓库的技能开始智能听歌旅程。

---

## 🚀 包含的技能模块 (Included Skills)

| 技能名称 (Skill Name) | 核心职责 (Core Responsibilities) |
| :--- | :--- |
| **[agent-lx-music](./agent-lx-music/SKILL.md)** | `alx` 播放器控制的基础核心技能，涵盖全部 v0.2.1 的 CLI 命令语法（播放、状态、队列等） |
| **[music-discovery](./music-discovery/SKILL.md)** | 智能音乐探索技能，支持网易云等排行榜（ board ）与个性化推荐（ discover ）的智能拉取与一键激活播放 |
| **[audio-analysis](./audio-analysis/SKILL.md)** | 音频分析与歌词、封面获取管理技能（ lyric 与 pic 命令的智能调度） |
| **[listening-companion](./listening-companion/SKILL.md)** | AI 智能音乐伴听与状态智能巡检守护技能 |

---

## 🛠️ 安装与使用指南

### 方法 1: 使用 CLI 下载脚本
你可以使用内置的便捷脚本直接克隆本仓库技能至你的代理配置目录中：
```bash
# 克隆或下载技能到本地的 agents 技能集路径下
git clone https://github.com/Xuepoo/agent-lx-music-skills.git ~/.gemini/antigravity-cli/skills/
```

### 方法 2: 独立拉取
如果只想拉取特定的技能文件，可配合 `curl` 直接拉取其中的 `SKILL.md` 描述：
```bash
curl -o SKILL.md https://raw.githubusercontent.com/Xuepoo/agent-lx-music-skills/main/agent-lx-music/SKILL.md
```

---

## 🌐 语言支持 (Languages)
* [中文说明 (README.md)](./README.md)
* [English Guide (README.en.md)](./README.en.md)

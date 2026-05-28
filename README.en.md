# agent-lx-music-skills 🎶

> **Dedicated AI Agent Skills Repository for agent-lx-music (alx)**

`agent-lx-music-skills` is a specialized, lightweight repository hosting modular AI Agent Skills tailored for `agent-lx-music` (alx). It empowers AI coding agents (such as Claude Code, Gemini CLI, Codex, etc.) to immediately gain capabilities like cross-platform search, queue operations, concurrent downloads, leaderboard exploration, and playlist manipulations without cloning the entire player source tree.

---

## 🚀 Included Skills

| Skill Folder | Core Responsibilities |
| :--- | :--- |
| **[agent-lx-music](./agent-lx-music/SKILL.md)** | Core controller skill covering basic CLI operations (play, pause, volume, status, repeat, shuffle) tailored for v0.2.1 |
| **[music-discovery](./music-discovery/SKILL.md)** | Discovery helper automating leaderboard browsing (`alx board`) and recommended playlists (`alx discover`) |
| **[audio-analysis](./audio-analysis/SKILL.md)** | Metadata extraction automating cover art downloads and lyric fetching |
| **[listening-companion](./listening-companion/SKILL.md)** | Smart daemon monitor tracking player history and playback logs |

---

## 🛠️ Installation & Usage

### Method 1: Using Vercel Open Agent Skills (npx skills) (Highly Recommended)

This repository is fully compatible with Vercel's `vercel-labs/skills` framework. AI agents or developers can dynamically install and register individual music skills via simple commands without manual clones!

* **Add Core Controller Skill**:
  ```bash
  npx skills add https://github.com/Xuepoo/agent-lx-music-skills/tree/main/agent-lx-music
  ```
* **Add Music Discovery & Leaderboards Skill**:
  ```bash
  npx skills add https://github.com/Xuepoo/agent-lx-music-skills/tree/main/music-discovery
  ```
* **Add Lyrics & Covers Audio Analysis Skill**:
  ```bash
  npx skills add https://github.com/Xuepoo/agent-lx-music-skills/tree/main/audio-analysis
  ```
* **Add Smart Listening Companion Skill**:
  ```bash
  npx skills add https://github.com/Xuepoo/agent-lx-music-skills/tree/main/listening-companion
  ```

#### 💡 Management Commands
* **List Installed Skills**: `npx skills list`
* **Update All Skills**: `npx skills update`
* **Remove a Skill**: `npx skills remove <skill-name>`

### Method 2: Full Git Clone
You can clone the entire repository directly into your Agent's config skills path:
```bash
git clone https://github.com/Xuepoo/agent-lx-music-skills.git ~/.gemini/antigravity-cli/skills/
```

### Method 3: Single Skill Retrieval (Curl)
To retrieve a single skill dynamically, fetch the raw markdown file using `curl`:
```bash
curl -o SKILL.md https://raw.githubusercontent.com/Xuepoo/agent-lx-music-skills/main/agent-lx-music/SKILL.md
```

---

## 🌐 Internationalization
* [Chinese Guide (README.md)](./README.md)
* [English Guide (README.en.md)](./README.en.md)

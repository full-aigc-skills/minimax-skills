<div align="center">

# minimax-skills

**MiniMax AIGC skills — text, image, video, speech, music generation**

[![GitHub](https://img.shields.io/badge/github-full--aigc--skills%2Fminimax-skills-green.svg)](https://github.com/full-aigc-skills/minimax-skills)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Compatible-purple.svg)](https://agentskills.io)

English | [简体中文](./README.zh-CN.md)

[Introduction](#-introduction) · [Install](#-install) · [Skills](#-skills) · [Supported Agents](#-supported-agents) · [Ecosystem](#-ecosystem)

</div>

---

## 📖 Introduction

**minimax-skills** is a curated collection of Agent Skills for AI coding agents, part of the [Full AIGC Skills](https://github.com/full-aigc-skills) ecosystem.

This package includes **3 skills**. Each skill is a self-contained `SKILL.md` file that AI agents load on-demand.

## 📦 Install

```bash
npx skills add full-aigc-skills/minimax-skills
```

Or install specific skills: `npx skills add full-aigc-skills/minimax-skills --skill <skill-name>`

## 🎯 Skills (3)

| Skill | Description |
|-------|-------------|
| `minimax-multimodal-toolkit` |  Use mmx to generate text, images, video, speech, and music via the MiniMax AI platform. Use when th |
| `minimax-music-gen` |  Use when user wants to generate music, songs, or audio tracks. Triggers on any request involving mu |
| `minimax-music-playlist` |  Generate personalized music playlists by analyzing the user's music taste and generation feedback h |

## 🤖 Supported Agents

Works with [Claude Code](https://code.claude.com), [Codex](https://developers.openai.com/codex), [Cursor](https://cursor.com), [OpenCode](https://opencode.ai), [Gemini CLI](https://geminicli.com), [GitHub Copilot](https://github.com/features/copilot), [Windsurf](https://codeium.com/windsurf), and [70+ others](https://agentskills.io/clients).

### Claude Code Installation

**Option 1: npx skills CLI (Recommended)**

```bash
npx skills add full-aigc-skills/minimax-skills
```

**Option 2: Manual Installation**

```bash
git clone https://github.com/full-aigc-skills/minimax-skills.git
cp -r minimax-skills/skills/* .claude/skills/
```

For more details, see the [Claude Code Skills Guide](https://code.claude.com/docs/en/skills) and [Agent Skills Spec](https://agentskills.io/).

## 🌐 Ecosystem

| Resource | Link |
|----------|------|
| **Full AIGC Skills** | [github.com/full-aigc-skills](https://github.com/full-aigc-skills) |
| **Agent Skills Spec** | [agentskills.io](https://agentskills.io) |
| **Skills CLI** | [github.com/vercel-labs/skills](https://github.com/vercel-labs/skills) |

## 📄 License

Apache 2.0 — see [LICENSE](LICENSE).

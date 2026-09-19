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

This package includes **12 skills**. Each skill is a self-contained skill tree that AI agents can install and load on demand.

## 📦 Install

```bash
npx skills add full-aigc-skills/minimax-skills
```

Or install specific skills: `npx skills add full-aigc-skills/minimax-skills --skill <skill-name>`

## 🎯 Skills (12)

| Skill | Description |
|-------|-------------|
| `3d-animation-short-generator` | Story-first 3D animated short production with bounded generation and assembly gates. |
| `brand-promo-video-generator` | Produce brand promotional shorts from verified brand assets and campaign goals. |
| `co-op-game-intro-generator` | Design two-player co-op game menu and intro animations with coordinated UI motion. |
| `h3-prompt-writing` | Write structured prompts for MiniMax H3 while preserving scope and safety constraints. |
| `handdrawn-live-video-generator` | Plan surreal hand-drawn animation fused with live-action spaces. |
| `minimalist-product-ad-generator` | Build minimalist product-ad shorts with beat-synced typography and camera direction. |
| `minimax-multimodal-toolkit` | Route MiniMax text, image, video, speech and music tasks through the portable toolchain. |
| `minimax-music-gen` | Generate music with explicit model, budget and artifact verification gates. |
| `minimax-music-playlist` | Create a personalized generated-music playlist from user taste and feedback. |
| `music-video-subtitle-generator` | Produce music-video plans with beat-reactive lyric typography and prompt audits. |
| `paper-collage-explainer-generator` | Create tactile paper-collage explainer plans and stop-motion clips. |
| `papercraft-stop-motion-explainer` | Create papercraft stop-motion explainers with layered staging and tactile sound design. |

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

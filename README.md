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

<!-- FULL_STACK_DOC_START -->
## Project positioning and boundaries

`minimax-skills` is the source repository for **12 independently installable Agent Skills**. The package manifest currently reports version `1.1.1`. This repository owns trigger contracts, workflows, references, examples, and quality gates; executable hooks, MCP servers, credential injection, and provider runtimes belong to consuming plugins.

| Confirmed fact | Value | Evidence |
|---|---|---|
| Package | `full-aigc-skills/minimax-skills` | `.claude-plugin/plugin.json`, repository remote |
| Installable skills | 12 | `skills/*/SKILL.md` |
| Current version | `1.1.1` | `.claude-plugin/plugin.json` |
| Specification source | OpenSpec | `openspec/config.yaml` |
| License | Apache-2.0 | `LICENSE` |

### Out of scope

- This package does not replace executable harnesses, MCP services, hooks, or provider clients.
- Copying `SKILL.md` does not prove host discovery, triggering, or successful execution.
- Skills do not silently authorize network calls, paid generation, overwrites, uploads, or publishing.
- Managed copies inside consumer plugins must be updated from immutable releases, not edited directly.

## At a glance

```text
user task -> name/description discovery -> read SKILL.md
          -> load only required references/examples/scripts
          -> execute domain workflow -> collect evidence
          -> PASS / FAIL / UNVERIFIED
```

## Verified installation and discovery

```bash
npx skills add full-aigc-skills/minimax-skills
npx skills add full-aigc-skills/minimax-skills --skill 3d-animation-short-generator
npx skills list --json
```

Use an immutable GitHub Release/tag when pinning a version; do not treat a moving `main` branch as a release. After installation, verify the skill count, names, resources, and target-agent list. Real Codex, ZCode, and Kimi plugin loading remains a separate runtime proof level.

## Package structure and loading

```text
minimax-skills/
├── .claude-plugin/plugin.json
├── skills/<name>/SKILL.md
├── skills/<name>/references/
├── skills/<name>/examples/
├── scripts/
├── openspec/
└── LICENSE
```

Cross-skill handoffs must use the skill name and install command, never a `../sibling-skill/` link: granular installations may contain only one skill.

## Quality, release, and security

```bash
python3 scripts/lint_skills.py
```

Before release, verify frontmatter, relative links, bundled resources, TRACE thresholds, manifest versions, and a clean-environment install. Published tags are immutable. A consuming plugin upgrades through a reviewed lock change containing the release tag, peeled SHA, and content digests.

Do not commit credentials, accounts, local absolute paths, or private repository names. Paid, upload, delete, overwrite, and publish operations require explicit authorization.

## Troubleshooting

| Symptom | Check | Resolution |
|---|---|---|
| Skill is not discovered | Frontmatter, agent discovery path, refresh requirement | Confirm with `skills list --json` |
| Granular install has missing references | Cross-skill relative paths | Move required resources into the skill or install the dependency by name |
| Plugin integrity check fails | Tag, peeled SHA, digest, local-skill manifest | Publish a new source release and update through the sync PR |
| Tool or credential is unavailable | `compatibility` and runtime prerequisites | Report `UNVERIFIED`; do not claim success |
| A second generator run changes files | Non-idempotent generation or manifest drift | Block release and repair generation/sorting |
<!-- FULL_STACK_DOC_END -->

## 📄 License

Apache 2.0 — see [LICENSE](LICENSE).

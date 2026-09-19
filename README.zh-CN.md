<div align="center">

# minimax-skills

**MiniMax AIGC 技能 — 文本、图像、视频、语音、音乐生成**

[![GitHub](https://img.shields.io/badge/github-full--aigc--skills%2Fminimax-skills-green.svg)](https://github.com/full-aigc-skills/minimax-skills)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-兼容-purple.svg)](https://agentskills.io)

[English](./README.md) | 简体中文

</div>

---

## 📖 简介

**minimax-skills** 是一组 AI 编码智能体技能，属于 [Full AIGC Skills](https://github.com/full-aigc-skills) 生态。包含 **12 个可独立安装的技能**。

## 📦 安装

```bash
npx skills add full-aigc-skills/minimax-skills
```

## 🎯 技能列表 (12)

| 技能 | 描述 |
|------|------|
| `3d-animation-short-generator` | 以故事为核心生成 3D 动画短片方案，并设置生成与组装门禁。 |
| `brand-promo-video-generator` | 从已验证品牌素材和传播目标制作品牌宣传短片。 |
| `co-op-game-intro-generator` | 设计双人合作游戏菜单与开场动画。 |
| `h3-prompt-writing` | 在范围和安全约束下编写结构化 MiniMax H3 提示词。 |
| `handdrawn-live-video-generator` | 规划手绘动画与实拍空间融合的视频。 |
| `minimalist-product-ad-generator` | 构建极简产品广告短片、节奏字幕与镜头语言。 |
| `minimax-multimodal-toolkit` | 路由 MiniMax 文本、图像、视频、语音和音乐任务。 |
| `minimax-music-gen` | 在模型、预算和产物验证门禁下生成音乐。 |
| `minimax-music-playlist` | 根据用户偏好和反馈创建个性化生成音乐歌单。 |
| `music-video-subtitle-generator` | 制作随节拍变化的歌词排版和音乐视频方案。 |
| `paper-collage-explainer-generator` | 创建纸张拼贴知识解释方案和定格动画片段。 |
| `papercraft-stop-motion-explainer` | 创建多层纸艺舞台与触感声音设计的定格解释视频。 |

## 🤖 支持的智能体

适用于 [Claude Code](https://code.claude.com)、[Codex](https://developers.openai.com/codex)、[Cursor](https://cursor.com)、[OpenCode](https://opencode.ai)、[Gemini CLI](https://geminicli.com)、[GitHub Copilot](https://github.com/features/copilot)、[Windsurf](https://codeium.com/windsurf) 及 [70+ 其他](https://agentskills.io/clients)。

### Claude Code 安装

**方式一：npx skills CLI（推荐）**

```bash
npx skills add full-aigc-skills/minimax-skills
```

**方式二：手动安装**

```bash
git clone https://github.com/full-aigc-skills/minimax-skills.git
cp -r minimax-skills/skills/* .claude/skills/
```

<!-- FULL_STACK_DOC_START -->
## 项目定位与边界

`minimax-skills` 是包含 **12 个可独立安装 Agent Skill** 的源代码仓库，当前清单版本为 `1.1.1`。本仓负责技能的触发说明、工作流、references、examples 与质量门禁；宿主插件的 Hook、MCP、凭据注入和运行时脚本不属于本仓职责。

| 已确认事实 | 值 | 证据 |
|---|---|---|
| 安装包 | `full-aigc-skills/minimax-skills` | `.claude-plugin/plugin.json`、仓库远端 |
| 可安装技能 | 12 | `skills/*/SKILL.md` |
| 当前版本 | `1.1.1` | `.claude-plugin/plugin.json` |
| 规格事实源 | OpenSpec | `openspec/config.yaml` |
| 许可证 | Apache-2.0 | `LICENSE` |

### 不负责

- 不替代消费插件中的可执行 Harness、MCP 服务、Hook 或供应商客户端；
- 不把 `SKILL.md` 被复制到目录视为宿主已经发现、触发或成功执行；
- 不自动授权网络调用、付费生成、文件覆盖、上传或发布；
- 不允许消费插件直接修改受 `skills.lock.json` 管理的副本。

## 一眼看懂

```text
用户任务
  │
  ▼
name / description 发现技能
  │
  ▼
读取完整 SKILL.md ──► 按需加载 references / examples / scripts
  │
  ▼
执行领域工作流 ──► 收集验证证据 ──► PASS / FAIL / UNVERIFIED
```

## 已验证的安装与发现

```bash
npx skills add full-aigc-skills/minimax-skills
npx skills add full-aigc-skills/minimax-skills --skill 3d-animation-short-generator
npx skills list --json
```

固定发布版本时使用 GitHub Release/tag，不要把移动的 `main` 当成不可变版本。安装完成后应核对技能数量、名称、资源文件和目标 Agent 列表；Codex、ZCode、Kimi 的真实插件加载仍需分别验证。

## 包结构与加载规则

```text
minimax-skills/
├── .claude-plugin/plugin.json   # 包名、版本与技能清单
├── skills/<name>/SKILL.md       # 触发条件与主工作流
├── skills/<name>/references/    # 按任务加载的领域知识
├── skills/<name>/examples/      # 请求、验收与恢复示例
├── scripts/                     # 仓库级生成和质量门禁（若存在）
├── openspec/                    # 规格与归档变更
└── LICENSE
```

跨技能协作必须使用技能名和安装命令，不得依赖 `../sibling-skill/` 相对链接，因为用户可能只安装一个技能。

## 质量、发布与安全

```bash
python3 scripts/lint_skills.py
```

发布前还必须检查 frontmatter、相对链接、资源完整性、TRACE 阈值、版本清单以及干净环境安装。正式 tag 不得移动；内容变化应发布新版本，并让消费插件通过 tag、peeled SHA 和摘要更新锁文件。

安全边界：不得提交真实密钥、账号、本机绝对路径或私有仓库地址；脚本应默认最小权限，付费、上传、删除和覆盖动作必须保留显式授权门。

## 故障排查

| 现象 | 检查 | 处理 |
|---|---|---|
| 安装后未发现技能 | frontmatter、Agent 发现目录、是否需要刷新 | 用 `skills list --json` 核对实际发现结果 |
| 只安装单个技能后引用缺失 | 是否存在跨技能相对路径 | 把必需资源移入当前技能，或按名称安装依赖技能 |
| 插件完整性检查失败 | tag、peeled SHA、摘要和本地技能清单 | 在源技能仓发布新版本，再由同步 PR 更新插件 |
| 工具或凭据缺失 | `compatibility`、运行时前置条件 | 报告 `UNVERIFIED`，不要猜测成功 |
| 自动化第二次运行仍产生差异 | 生成器非幂等或清单漂移 | 阻止发布并修复生成/排序规则 |
<!-- FULL_STACK_DOC_END -->

## 📄 License

Apache 2.0

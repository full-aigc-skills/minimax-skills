---
name: brand-promo-video-generator
description: For marketers and creators producing promotional content for brands, products, websites, apps, shops, or personal projects. Users provide logos, product images, interface screenshots, official links, or other verifiable assets and confirm duration, aspect ratio, audience, and campaign focus. The Skill organizes brand facts and asset provenance, selects a narrative direction, plans precise beats and shots, generates needed imagery, video, voiceover, or music, and completes assembly and pre-delivery review. It outputs a promotional short that highlights product capabilities, use cases, and a call to action. Best for launches, website showcases, and social promotion; not for imitating real brand marks without authorized assets, inventing product claims, or producing long-form narrative films.
compatibility: Portable — runs on any agent harness with shell access. Generation goes through the mmx CLI (Token Plan) and ffmpeg for assembly; no MiniMax Hub canvas required.
---

## Tool mapping (mmx-cli edition)

This skill is the mmx-cli adaptation of the MiniMax-H3 Hub skill of the same
name: the creative methodology is unchanged, while Hub canvas tools are replaced
by the following portable equivalents.

| Hub tool | mmx-cli / portable equivalent |
|---|---|
| `hub_generate_image` | `mmx image generate --prompt "..." --out <path>` |
| `hub_generate_video` | `mmx video generate --prompt "..." --out <path>` (Hailuo; see `mmx video generate --help` for duration/model flags) |
| `hub_generate_audio` / `hub_synthesize_speech` | `mmx speech synthesize --text "..." --out <path.mp3>` |
| `hub_generate_music` | the `minimax-music-gen` skill (MiniMax music API; mmx has no music command) |
| `hub_video_edit` | ffmpeg assembly (concat / xfade / audio mix) — deterministic, offline |
| `hub_analyse_media` | `ffprobe` + `mmx vision describe <file>` |
| `hub_image_search` | user-provided assets first; `mmx search query "..."` for public references |
| `hub_canvas_get_node` / `hub_canvas_group_recent_outputs` | the episode working directory: `assets-manifest.md`, `outputs/`, `decisions.md` ledger files |
| choice cards | numbered options presented in chat, choice recorded in `decisions.md` |

Prerequisites: `npm install -g mmx-cli` and `mmx auth login --api-key sk-xxx`
(region auto-detected; `mmx quota` shows the Token Plan balance). ffmpeg/ffprobe
must be on PATH for assembly and inspection.

# Brand Promo Video Generator

Create a polished short promo video for a brand, product, website, app, shop, or personal project. Use this Skill when the user has a logo, product images, screenshots, a website link, or just a clear idea and wants the agent to turn those materials into a clean brand reel.

This mmx-cli adaptation replaces third-party Vibe Motion / Remotion implementation details with portable orchestration: source research, asset verification, story planning, image/video generation, optional speech or music, and editing assembly. Do not initialize external projects or depend on npm validators during normal execution.

## Tool Coverage Rule

The `allowed-tools` list must cover the full production promise in this Skill: source lookup, image preparation/generation, video clip generation, optional speech/music/audio generation, final editing/assembly, media inspection, and canvas grouping. If a runtime does not provide one of the listed generation or editing tools, downgrade the deliverable explicitly to a pre-production package instead of claiming that a final promo video can be generated.

## STEP 1: Intake assets and resolve the brief

Before any story planning or generation, run a required user intake. Ask the user to upload or provide links to the elements that must be verified:

- Logo files or official logo source pages
- Font files, font names, typography guidance, or official website pages that show brand typography
- Brand colors, color system, style guide, or pages that clearly show official colors
- Product images, UI screenshots, packaging, renders, footage, or other brand imagery
- Product information: official product name, feature list, launch focus, claims, CTA, disclaimers, and target audience
- Company/product official URL or official source package

Treat user-uploaded assets as usable by default for pre-production and concept planning. Do not repeatedly ask a standalone rights/permission question during the first intake unless there is a concrete risk signal, such as a visible third-party watermark, obviously scraped marketplace imagery, contradictory user wording, legal/medical/financial compliance claims, or the user asks for commercial publication. Record the source as "user-provided" and surface rights caveats in the source summary instead of blocking the flow.

In the same opening intake, ask the user to choose:

- Target duration, normally 15-30 seconds; recommend 15 seconds when the user wants a fast launch film
- Aspect ratio; offer common choices such as 16:9, 9:16, 1:1, 4:3, 3:4, or match a supplied reference

Also identify campaign focus, distribution channel, narration language, on-screen copy language, and visible copy needs when they are not already clear. Do not proceed to creative direction until the user has supplied the usable materials or explicitly confirms which elements are unavailable.

Language rule for promo content: choose narration and on-screen copy language from the brand materials, target audience, and platform context, not mechanically from the chat language. If the brand assets and visible source copy are primarily English or global corporate English, default narration and on-screen copy to English unless the user explicitly asks for Chinese localization. If the user is Chinese but says they are testing as a new user, keep chat replies in Chinese, but plan the actual video copy in the language that best fits the brand campaign.

If a logo, product UI, person, mascot, packaging, font, color system, or other identity-bearing asset cannot be authenticated, stop and ask for an authorized original instead of generating a plausible substitute.

## STEP 2: Build the brand truth sheet

Research or inspect the strongest available sources and summarize the brand truth sheet before creative production:

1. User-provided original exports
2. Official company website, static bundle, newsroom, brand portal, media kit, press kit, or official repository
3. Company-controlled media library
4. Licensed stock or authorized partner kit

Extract:

- Exact logo variants, clear space, and usage constraints
- Official fonts or visible typographic behavior
- Primary, secondary, and dynamic brand colors
- Brand tone, principles, visual motifs, and interaction language
- Current product names, features, scenarios, metrics, slogans, CTA, and disclaimers
- Official photography, renders, UI screenshots, footage, press assets, and media kit material

Do not use logo aggregation sites, search thumbnails, fan recreations, Pinterest reposts, or AI-generated substitutes as identity-bearing sources. Procedural graphics are allowed only as non-representational motion layers: masks, gradients, color fields, grids, glows, particles, trails, typography, verified-data charts, and transition geometry.

## STEP 3: Create a provenance manifest

Record every identity-bearing asset in a compact manifest that can be delivered to the user. The manifest is a markdown table in assets-manifest.md and should include:

- Stable asset ID and role
- Local file path
- Exact source URL or user-provided source note
- Source type, such as official website, media kit, user-provided original, or licensed stock
- Verification target used for comparison
- Rights or publication note
- Authenticity status: verified, user-supplied, licensed, or blocked

The manifest does not grant publication rights by itself. If authorization is unclear, label the video as an unofficial concept and tell the user commercial publication requires permission.

## STEP 4: Choose the story spine

Present 2-3 concise creative directions when the user has not already chosen one, recommend one, and continue after confirmation. Use the product category to pick a spine:

- AI / SaaS: user intent -> thinking or planning -> capabilities -> execution -> useful output -> proof -> logo
- Physical product: hero reveal -> interaction -> feature macro -> usage context -> result -> logo
- Service / company: context -> process -> evidence -> outcome -> promise -> logo
- Image-led brand: authentic imagery -> visual motif -> benefit -> emotional payoff -> logo

Keep the story product-specific. Show actual features, interactions, scenarios, outputs, and proof instead of hiding the story behind abstract effects.

## STEP 5: Plan exact beats

Plan a frame-aware timeline before generation. Use 30fps as the planning convention unless the output pipeline requires otherwise.

For a 15-second film, target 5-8 major beats. For a 30-second film, target 8-12 major beats. Each beat should define:

- Start and end time or frame range
- Visual owner and authentic asset IDs
- Primary action
- Product or brand proof shown in the shot
- Copy and readable hold
- Color state
- Incoming and outgoing transition
- Motion intent: setup, anticipation, commitment, impact, brake, settle

A useful 15-second pattern is: brand hook, user intent or setup, product mechanism, capabilities or scenarios, output or proof, product payoff, final logo and CTA. Use 6-12 frame overlaps when outgoing motion naturally supplies the next shot.

## STEP 6: Direct the motion language

Build intensity with control:

- Let product motion, cursor paths, UI flow, light, scrolling content, object edges, or matched geometry drive transitions
- Use 2-5 deliberate color states tied to meaning
- Keep one primary action per beat; delay secondary layers slightly
- Establish 2-3 high-energy peaks and quieter braking moments
- Preserve readable silhouettes, copy, and logo clear space
- Avoid fake HUDs, arbitrary glass cards, decorative text walls, unverified metrics, and identical easing everywhere

For AI products, include at least one readable chain such as: prompt -> planning -> parallel capabilities -> generated result -> proof. For physical or service products, show cause and effect from user action to concrete outcome.

## STEP 7: Hard confirmation before generation

Before generating any video, image sequence, speech, music, or final edit, stop and show the user the completed pre-production package:

- Provenance manifest or source summary
- Brand truth sheet
- Chosen creative direction
- Exact beat / shot plan
- Visible copy, CTA, narration, and audio plan
- Known authenticity, rights, or placeholder caveats

Use a concise confirmation step before generation. If the user clearly expresses approval or intent to proceed after seeing the pre-production package — for example "confirm", "generate", "go ahead", "continue", "next", "可以", "继续", "下一步", or similar — treat it as permission to generate, unless the message also asks for changes. If the user asks to skip the process, still provide a compact source summary, brand truth sheet, and beat plan first, then proceed when they indicate approval. Offer revision choices only when the user's reply is ambiguous or requests changes.

## STEP 8: Produce Hub assets

Use mmx generation and ffmpeg editing only after the hard confirmation gate has passed. Keep each dispatch self-contained with the chosen model, aspect ratio, authentic reference paths, and original request.

Typical production flow:

1. Generate or prepare verified still frames, UI plates, product hero frames, or motion-ready story images.
2. Generate video clips from those frames or from precise text prompts, preserving the same ratio and brand assets.
3. Default audio policy for native brand reels: when the user asks for BGM, music, soundtrack, ambient sound, or says nothing beyond needing a finished promo video, prefer video-native audio from the selected video model instead of generating a separate music track. For the default MiniMax H3 route, set native audio on (`generate_audio=true`) and prompt for brand-safe instrumental music / UI sound design inside the video prompt.
4. Generate separate speech or music only when the user explicitly needs controllable narration, voiceover, dialogue, replaceable standalone BGM, exact music duration independent of the video, post-production remixing, or when the selected video model cannot generate suitable audio. Do not duplicate a soundtrack between video-native audio and separate audio generation.
5. Assemble clips, any explicitly separate audio, and final brand lockup in editing. Add subtitles only when the user explicitly asks for subtitles.

Do not redraw or approximate logos, wordmarks, product UI, packaging, mascot, person, or brand scene. Use generated material only for abstract motion, atmosphere, transition geometry, or clearly conceptual scenes that do not impersonate official product evidence.

## STEP 9: Verify before delivery

Before final response, check:

- The logo and identity-bearing assets came from verified or user-authorized sources
- Product names, feature wording, claims, metrics, slogans, and CTA match official sources or are clearly marked as concept copy
- The video duration, aspect ratio, and language match the brief
- Copy is readable and not overcrowded
- The final logo is not stretched, cropped, or rebuilt
- Motion has clear visual ownership and does not obscure the product
- The output is on the canvas and multi-asset outputs are grouped

If the output fails an authenticity check, replace the questionable asset with an official/user-authorized source or stop and ask for the asset. Never improve an imitation.

## STEP 10: Deliver

Provide:

- Final video path or canvas output
- Duration, aspect ratio, and language
- Short creative summary
- Provenance manifest or source summary
- Rights/disclaimer note when needed
- Specific suggestions for the next iteration, such as pacing, claim clarity, CTA, audio, or platform crop

## Failure recovery

- Wrong or approximate logo: remove it, locate the current official file or ask for the user's original, then regenerate or re-edit.
- Fake-looking product/UI: replace with official, user-supplied, or licensed media. Do not polish the imitation.
- Beautiful but generic: add a complete product interaction, verified claim, or real output.
- Fast but chaotic: reduce simultaneous actions, assign a visual owner, and preserve matched motion across cuts.
- Smooth but slow: shorten holds, overlap transitions, and brake only around key messages.
- Asset unavailable: ask for an authorized original; never guess.

<!-- QUALITY_BASELINE_V1 -->
## When to use（什么时候使用）

当用户需要 **在明确输入、预算和交付约束后执行生成或写入操作** 时加载本技能。先从请求中提取目标、输入、约束、交付格式和验收标准；描述摘要为：For marketers and creators producing promotional content for brands, products, websites, apps, shops, or personal projects. Users provide logos, product images, interface screenshots, official links, or other verifiable assets and confirm duration, aspect ratio, audience, and campaign focus. The Skill organizes brand facts and asset provenance, selects a narrative direction, plans precise beats and shots, generates needed imagery, video, voiceover, or music, and completes assembly and pre-delivery review. It outputs a promotional short that highlights product capabilities, use cases, and a call to action. Best for launches, website showcases, and social promotion; not for imitating real brand marks without authorized assets, inventing product claims, or producing long-form narrative films.。

## Rules

- 先读后写：先确认当前状态与真实能力，再执行会改变外部状态的动作。
- 权限最小化：只使用完成当前步骤所需的文件、工具、账户与网络范围。
- 证据优先：运行结果、资源 ID、版本、哈希或测试输出缺失时，明确标记为 `NOT_VERIFIED`。
- 幂等优先：保留请求标识与阶段状态；结果不明确时先查询，不进行盲目重试。
- 隐私安全：日志、示例、回执和错误信息不得包含 token、cookie、密钥或个人敏感数据。

## Workflow

### Step 1：澄清意图

确认本技能是否匹配目标；若只是相邻需求，交给更精确的技能。
### Step 2：执行预检

校验输入、模型/工具能力、输出路径、预算上限和审批状态；任一关键条件未知时停止在只读阶段。
### Step 3：形成计划

列出将调用的工具、会改变的对象、成功标准以及失败后的安全退出方式。
### Step 4：执行动作

按一次批准执行并记录请求标识；模糊结果先查询而不是重提；每个外部调用均保留可关联的状态或回执。
### Step 5：验证交付

验证产物存在性、格式、哈希/标识、成本状态和质量门禁，并把事实、推断和未验证项分开陈述。

## Validation checklist

- [ ] 技能触发条件与用户意图一致，没有把相邻任务误路由到本技能。
- [ ] 输入、目标对象、版本和输出位置均已明确，且没有使用猜测值替代必填值。
- [ ] 所有写入、付费、发布或不可逆动作都在用户授权范围内。
- [ ] 结果已用独立检查验证；仅有“命令成功”或“文件存在”不算完整验收。
- [ ] 输出包含实际证据、失败/跳过项、剩余风险和可执行的下一步。

## Gotchas

1. **把计划当结果**：文档或提示词不等于真实执行；必须标明实际运行层级。
2. **错误重试**：超时或响应丢失可能已经产生远端状态，先查询再决定是否重试。
3. **隐式扩大范围**：批量、全量、发布、覆盖和付费不是普通读写的自然延伸。
4. **版本漂移**：引用外部资源时记录版本、tag 或提交；不要把可变分支当发布证据。
5. **证据过期**：缓存、旧截图和历史测试不能证明当前环境；在交付前刷新关键证据。

## 不适用与边界

付费、发布、覆盖、上传或外部写入必须使用当前任务的显式授权；不自动扩大次数和预算。 如果请求需要别的技能，不复制其正文；按技能名称进行交接，并保留当前任务上下文。

## Progressive disclosure

- 需要确定输入/输出、状态和授权点时，读取 `references/workflow-contract.md`。
- 需要交付前自检时，读取 `references/validation-checklist.md`。
- 遇到超时、部分成功或恢复场景时，读取 `references/error-recovery.md`。
- 首次运行、拒绝越权和失败恢复分别参考 `examples/happy-path.md`、`examples/boundary-refusal.md`、`examples/failure-recovery.md`。

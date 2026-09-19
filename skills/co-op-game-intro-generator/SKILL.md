---
name: co-op-game-intro-generator
description: For users creating a two-player co-op game menu or opening animation. Users provide two player names, a game title, a target visual style, and optional character reference images. The Skill locks identity cues, generates an approval image from a fixed menu framework with coordinated color, buttons, icons, and typography, then uses the approved result to rebuild the character, UI-copy, and event timing instructions for the final video. It outputs a co-op game intro featuring two characters, player cards, and menu interaction motion. Best for game concepts, character-led menus, and social content; not for playable game development, complex multi-page UI, exact brand-logo replication, or generic character-free title sequences.
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

# Co-op Game Intro Generator

Use this Skill when the user wants a co-op game intro video and wants to confirm the visual direction with one image before generating the final H3 video. The workflow collects style, player names, game title, and optional character refs, then creates a framework-preserving confirmation image before generating the H3 video.

## Required References

These two templates are mandatory runtime inputs, not optional background notes:

- Use `references/h3-confirmation-image-template.md` when building the confirmation-image prompt in STEP 3 and generating the first confirmation image in STEP 4. Fill the template fields in order and do not skip framework, palette, UI, character, typography, layout, or negative-constraint fields.
- Use `references/h3-video-prompt-template.md` when refilling the final Minimax H3 video prompt in STEP 6. Fill the template from the approved confirmation image, player/game data, final UI copy, event timing, motion directions, and negative constraints.

If either template is unavailable, stop and report that the Skill package is incomplete instead of improvising a different prompt structure.

## STEP 1: Ask for visual style
Ask the user to choose a preset style or enter a custom style. This style has top priority and controls supplemental style language, palette language, background texture, character rendering, expression, outfit direction, UI colors, button/icon style, and typography texture.

## STEP 2: Collect player and game info
Collect PLAYER 1 name, PLAYER 2 name, and game title. If the user provides character images, use PLAYER 1 and PLAYER 2 refs only for identity mapping: recognizable face silhouette, hairstyle, glasses, relative facial proportions, and distinctive traits. Do not inherit photographic realism, skin texture, real-world lighting, camera quality, or the original image style; redesign the face into the selected visual style while preserving identity anchors.

## STEP 3: Build the GPT confirmation-image prompt
Load and follow `references/h3-confirmation-image-template.md` as the required prompt skeleton. Use a fixed framework + dynamic style fill + palette-linked prompt structure:

1. **Overall Style**: always preserve game main menu UI, high-quality game promo poster, deep UI-character integration, modern commercial game UI design, strong visual impact, clean composition, and avoid over-decoration. Add other style terms from the selected style.
2. **Color Palette**: always follow: xx as main color, xx as UI body color, xx as text color, xx as functional accent color, red as danger accent, palette within five colors, high-contrast color blocking, fresh modern look, and xx-style color language. All later UI/button/icon/type colors must match this palette.
3. **Composition**: preserve 16:9 landscape, full-frame background, x centered characters, UI around rather than blocking them, upper-left player card, right-side vertical menu, bottom caution tape, a few corner graffiti accents, Z reading path, enough negative space, clear hierarchy, and Continue as the visual focus.
4. **Background**: follow pure xx background, slight xx texture, large solid-color blank space, texture only as detail, avoid heavy dirt/dense scratches/too much ink splash/large paint splatter, a little black spray-paint edge detail, clean modern premium UI-first background. Derive xx and additions from the selected style.
5. **Character Style**: strictly expand according to the selected style. Use source text only as dimension guidance, not fixed style.
6. **Character A**: facial features from character image 1; expression, rendering, and outfit follow selected style; optional compatible outfit dimensions include khaki short jacket, black inner layer, black cargo pants, brown boots, adventurer outfit. Fixed action: cross-legged, hands on floor, slight backward lean, looking up.
7. **Character B**: facial features from character image 2; expression, rendering, and outfit follow selected style; optional compatible outfit dimensions include green thick jacket, burgundy padded lining, white inner shirt, black pants, thick boots. Fixed action: cross-legged, hands in front of legs, slight forward lean, looking at camera.
8. **Lighting**: preserve top main light, upper-left warm/cool fill, soft bottom ambient reflection, soft shadows, contact shadows, rim light, high-quality GI, and natural character-background integration. Choose warm/cool from style.
9. **Game UI**: preserve console game menu, unified button size, rounded rectangles, slight tilt, minimal spray/drip elements, modern clean sticker design, readability, and no over-decoration. Button body, outline, and glow colors must match the palette.
10. **Layout Rules**: preserve horizontal long buttons, unified width/height/radius, width adapted to text, single-line titles only, no wrapping, no two-line titles, centered text, consistent margins and spacing.
11. **Buttons**: adapt colors from palette and icons from selected style. Continue is the large visual-center highlighted button with hover/click state. Start New Game is above Continue. Settings remains visually consistent. Exit Game uses danger/exit cue with red accents allowed.
12. **Player Cards**: preserve upper-left x-player info cards, irregular rectangular card, outline, slight edge damage, left logo/icon, right three-level info (PLAYER label, nickname, READY), bold sans-serif, industrial sticker design. Card colors, outline, READY color, and logo style follow palette and selected style.
13. **Icon System**: derive icon style from selected style, colors from palette, and keep one-row-only, no wrapping, no stacking, at most one row per UI block, minimal quantity, unified size, never stealing focus.
14. **Typography**: preserve bold sans-serif, all caps, Anton/Impact/Burbank/Tungsten-like weight, tight tracking, heavy strokes, clear hierarchy, single-line typography, no wrapping, button width adapts to text, never two-line menu titles. Colors and texture follow palette and selected style.

## STEP 4: Generate the first confirmation image
Generate only one confirmation image from the filled `references/h3-confirmation-image-template.md`. Preserve the framework structure, while making the selected style visibly dominant.

## STEP 5: Wait for approval
Do not generate video until the user approves the image. If the user changes style, names, game title, identity, or image direction, return to the image prompt step.

## STEP 6: Refill video prompt and generate with Minimax H3
After approval, load `references/h3-video-prompt-template.md` and refill the final video prompt with confirmed style, character refs, player names, game title, UI text, event timing, motion directions, and negative constraints. Generate the final video with Minimax H3.

## STEP 7: Repair common failures
If text is unreadable, reduce on-screen text. If identities swap, strengthen names, positions, and colors. If faces drift, reuse uploaded refs and explicitly preserve identity anchors, hairstyle, and outfit anchors while keeping the face rendered in the selected visual style. If the selected style is weak, rewrite Overall Style, Color Palette, Character Style, Background, Game UI, Buttons, Icons, and Typography instead of changing layout framework.

<!-- QUALITY_BASELINE_V1 -->
## When to use（什么时候使用）

当用户需要 **为当前请求选择并执行可验证、可恢复的专业工作流** 时加载本技能。先从请求中提取目标、输入、约束、交付格式和验收标准；描述摘要为：For users creating a two-player co-op game menu or opening animation. Users provide two player names, a game title, a target visual style, and optional character reference images. The Skill locks identity cues, generates an approval image from a fixed menu framework with coordinated color, buttons, icons, and typography, then uses the approved result to rebuild the character, UI-copy, and event timing instructions for the final video. It outputs a co-op game intro featuring two characters, player cards, and menu interaction motion. Best for game concepts, character-led menus, and social content; not for playable game development, complex multi-page UI, exact brand-logo replication, or generic character-free title sequences.。

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

确认目标、输入、约束、可用工具、成功标准和失败边界；任一关键条件未知时停止在只读阶段。
### Step 3：形成计划

列出将调用的工具、会改变的对象、成功标准以及失败后的安全退出方式。
### Step 4：执行动作

按最小充分步骤执行，并在关键状态变化处记录证据；每个外部调用均保留可关联的状态或回执。
### Step 5：验证交付

输出结果、验证证据、未完成项、风险和明确的下一步，并把事实、推断和未验证项分开陈述。

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

不超出用户给定范围；写入、付费、发布和不可逆动作需要明确授权。 如果请求需要别的技能，不复制其正文；按技能名称进行交接，并保留当前任务上下文。

## Progressive disclosure

- 需要确定输入/输出、状态和授权点时，读取 `references/workflow-contract.md`。
- 需要交付前自检时，读取 `references/validation-checklist.md`。
- 遇到超时、部分成功或恢复场景时，读取 `references/error-recovery.md`。
- 首次运行、拒绝越权和失败恢复分别参考 `examples/happy-path.md`、`examples/boundary-refusal.md`、`examples/failure-recovery.md`。

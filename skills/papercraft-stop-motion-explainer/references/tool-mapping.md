# Papercraft 工具映射

本技能保留 MiniMax-H3 Hub 版本的创作方法，但执行时使用可移植的 `mmx` CLI 与 FFmpeg。

| Hub tool | mmx-cli / portable equivalent |
|---|---|
| `hub_generate_image` | `mmx image generate --prompt "..." --out <path>` |
| `hub_generate_video` | `mmx video generate --prompt "..." --out <path>`；模型与时长以实时 help 为准 |
| `hub_generate_audio` / `hub_synthesize_speech` | `mmx speech synthesize --text "..." --out <path.mp3>` |
| `hub_generate_music` | 交给 `minimax-music-gen` 技能；`mmx` 当前无音乐命令 |
| `hub_video_edit` | FFmpeg concat、xfade、audio mix；离线且确定性 |
| `hub_analyse_media` | `ffprobe` 加 `mmx vision describe <file>` |
| `hub_image_search` | 优先用户资产；必要时 `mmx search query "..."` 查公开参考 |
| `hub_canvas_get_node` / `hub_canvas_group_recent_outputs` | 工作目录中的 `assets-manifest.md`、`outputs/`、`decisions.md` |
| choice cards | 对话中的编号选项，决定写入 `decisions.md` |

## 前置条件

1. `mmx-cli` 已由用户按官方方式安装，且实际命令与实时 `--help` 一致。
2. 用户已通过受支持的本地认证流程登录；不得在技能输出中展示 API key。
3. FFmpeg/ffprobe 已在 PATH 中，且在执行组装前记录实际版本。
4. 付费生成前展示模型、次数、预计成本/额度影响和输出位置，等待显式批准。

## 失败处理

- 找不到命令：停止并报告缺失前置条件，不静默安装。
- 模型或参数不可用：读取实时 help/能力快照，给出可选方案，不猜测参数。
- 提交后超时：按请求标识查询；结果模糊时不得自动重提。

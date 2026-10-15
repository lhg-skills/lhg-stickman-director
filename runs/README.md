# runs/ —— 每次运行的档案

每支片一个目录：`runs/YYYY-MM-DD-<slug>/`。交接 Agent 打开目录、读 `log.md` 最后一条，
就知道停在哪一步、下一步做什么。

```
runs/2026-10-20-ai-agent-101/
├── brief.md          # Setup gate 四要素 + 原始素材
├── proposal.md       # Phase A 导演提案（最终批准版）
├── prompts-muse.md   # Phase B Muse 版
├── prompts-flow.md   # Phase B Flow 版（仅补镜时用）
├── tts.md            # 分段旁白 + TTS 参数 + 实测时长
├── assembly.md       # 拼接指南（镜头顺序、转场、字幕、BGM）
└── log.md            # 时间线：决策、生成记录、credits、验收、复盘
```

## log.md 格式

```
## 2026-10-20 14:30 · Phase A 批准
- 结论：批准（改了第 3 镜旁白）
- 下一步：Phase B

## 2026-10-20 16:05 · Flow 补镜
- 镜头：#2、#5（Fast）
- credits：预估 40 / 实际 38 / 本月累计 120 / 1000
```

- 大体积素材（视频、音频、图片）**不入 Git**，只在 log 里记文件名与存放位置。
- 目录一旦交付成片即只读；返工新开 `-v2` 目录。

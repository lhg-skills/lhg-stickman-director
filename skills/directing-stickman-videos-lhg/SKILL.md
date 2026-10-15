---
name: directing-stickman-videos-lhg
description: "火柴人视频导演（lhg 版）：完整实现 METHOD.md 方法规格（Setup gate → Phase A 导演提案 → 批准 → Phase B 提示词包 → 生成 → 拼接），中文旁白优先，执行层为 Muse 直出 + Gemini PRO Flow 双链路。当用户说'把文案做成火柴人视频'时使用。"
---

# 火柴人视频导演（lhg 版）

## 方法

完整实现仓库根目录 `METHOD.md`。执行顺序严格按其第 1–7 节推进，
不得跳过 Setup gate 与确认门。上游原版文件（`../directing-stickman-videos/`）
仅作风格配方与样例参考，不直接执行。

## 执行层（相对上游的替换）

上游执行层 = Gemini Omni Flash via Google Flow 单链路。
本版双执行层，按路由规则选用：

### A. Muse 直出层（默认先行）

- **分镜预览图**：Muse Image，按分镜表每镜出一张预览图（画幅与成片一致），
  用于确认风格配方与构图，不烧 Flow credits。
- **草稿视频**：Muse Video，每镜一条约 10 秒（60 秒成片 = 6 条，正好一轮上限）。
  prompt 用英文画面描述（人物 DNA 锚点逐字 + 环境 + 三节拍动作 + 负约束），
  音乐只描述情绪（如 quiet piano, upbeat electronic），不指定音频文件。
  需要视觉延续时用 snapshot 引用上一镜。
- **中文配音**：Muse TTS，按分镜切分旁白文本逐段生成；
  同一视频同一音色/语速/语气参数（声音连续锁的中文实现）。
- **用途**：验证分镜、节奏、风格；简单风格可直接成片。

### B. Flow 质量层（Gemini PRO）

- **对象**：Muse 草稿中"必须高质量"的镜头（人物特写、复杂运镜、关键转场），
  默认不整片重做。
- **prompt**：沿用上游 Phase B 结构（英文画面 + 中文台词 audio-only，
  格式见 METHOD.md §5）。
- **预算纪律**：每月 1000 credits 内；Fast 档先过，Quality 档定稿；
  每天 50 免费分优先用于验证性生成。

### 路由规则

1. Phase B 输出"双版提示词"：Muse 版 + Flow 版（同一分镜，两套提交格式），
   另附 TTS 分段文本与拼接指南。
2. 先跑 Muse 全片草稿（图片预览 → 6 条视频）→ 用户看片确认。
3. 标记需 Flow 重做的镜头（用户指定，或 Muse 版明显不达标）；无标记则不进 Flow。
4. 配音（Muse TTS）→ FFmpeg/剪映合成：画面 + 配音 + 字幕（旁白烧入）+ BGM。
5. 验收按 METHOD.md §7 清单；技术通过≠审美验收。

## 工作流

1. **Setup gate**：收齐素材/画幅/时长/画风。默认 9:16、60 秒、Style 1，
   仍需用户一次确认，不静默默认。
2. **Phase A**：中文导演提案 —— 中文旁白（45–55 字/10 秒）+ 英文对照版；
   五阶段心跳引擎；N 行分镜表（含三节拍、衔接命名、BGM/SFX）。
3. **确认门**：批准 / 改镜 / 改全局（三选一）。
4. **Phase B**：双版提示词包 + TTS 文本 + 拼接指南。
5. **执行**：Muse 草稿 → 看片确认 → Flow 补镜（按需）→ 合成。
6. **验收**：METHOD.md §7。

## 人机分工

- Muse：提案、提示词、生成、合成全包；每个 Flow 补镜先报预算（credits 估算），
  用户确认后再烧。
- lhg：Phase A 拍板；看草稿片拍板；Flow 补镜清单与预算拍板。
- 不可逆操作（无）、付费操作（Flow credits 消耗）必须先报预算后执行；
  不自动购买 credits。

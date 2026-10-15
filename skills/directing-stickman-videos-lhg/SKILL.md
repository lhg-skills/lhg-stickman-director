---
name: directing-stickman-videos-lhg
description: "lhg 适配版火柴人视频导演：在上游 directing-stickman-videos 基础上，中文旁白优先、豆包/Flow 双生成链路、默认 9:16，服务 AI 工具概念讲解（中文）与出海英文版。"
---

# Directing Stickman Videos（lhg 适配版）

## 上游与覆盖方式

本 skill 改编自 kaomei（疯狂的烤妹儿 / @CrazyKaomei）的开源项目
`stickman-video-director`（https://github.com/kaomei/stickman-video-director，MIT License）。
执行前先完整读取 `../directing-stickman-videos/SKILL.md` 及其 `references/`，
以下条款覆盖上游同名条款；未被覆盖的条款（分镜方法论、风格锁定配方、
先提案后生成、连续性锁等）全部沿用上游。

## 覆盖规则

### 1. 旁白语言（覆盖上游 English VO 条款）

- Phase A 导演提案：**中文旁白正文 + 英文对照版**并列呈现。
- 中文旁白按每 10 秒约 45–55 字控制节奏（对应上游英文 20–25 词/10 秒）。
- 出海版：英文旁白沿用上游规范（20–25 词/10 秒）。
- 生成提示词中的 dialogue：国内版填中文台词（audio-only 中文配音，
  画面严格无字）；出海版填英文台词，沿用上游 audio-only 规则。
- 中文配音走外部 TTS（豆包 TTS / 剪映配音），提示词中的 voice block 改为
  "后期中文配音备注"：锁定同一视频同一音色、语速、语气，不逐段更换。

### 2. 生成端双链路（覆盖上游单一 Gemini Omni Flash 目标）

- **国内链路（默认）**：豆包 Seedance 文生视频。提交时按"分镜描述 +
  人物锁定 + 中文台词"三段式填入；先用 Mini/Fast 档出草稿验证方向，
  定稿再切满血版。BGM 与字幕一律后期加，提示词中只保留备注。
- **出海链路**：Google Flow（Omni Flash / Veo），直接沿用上游 Phase B
  提示词包原文提交。
- Phase B 输出时，同时给出两版提交说明；用户只选一条链路时只给对应版。

### 3. 默认规格

- 画幅默认 `9:16`（视频号/抖音/小红书）；`16:9` 仅用于 B 站横屏与出海 YouTube。
- 时长默认 60 秒（6 段，每段约 10 秒）；按 10 秒倍数调整。
- 画风默认 Style 1（黑白极简，信息密度最高）；按选题可换。
- Setup gate 保留：画幅、画风、时长仍需用户一次确认，不静默默认。

### 4. 选题模板：AI 工具概念讲解

在上游 5 阶段弧线基础上，AI 工具概念讲解类选题使用专用映射：

痛点钩子 → 反常识纠偏 → 原理可视化 → 操作演示映射 → 结论 + 行动召唤

要求：把"讲清一个概念"翻译成火柴人动作隐喻（每 2–3 秒一次视觉变化，
沿用上游规则）；不虚构产品功能、数据与效果。

### 5. 成片规范

- 生成画面默认不带任何文字、数字、字幕；花字与字幕后期在剪映统一加
  （样式对齐「刘洪光实名上网」账号 VI）。
- 国内版 BGM 用剪映曲库；出海版沿用上游 BGM 连续性锁。
- 拼接：按上游 stitching guide 检查每处接点，实际看片验收，不假设转场生效。

### 6. 分工

- Muse 代跑本 skill：文案 → Phase A 提案 → lhg 审核拍板 → Phase B 提示词包 →
  按选定链路生成 → 剪映成片。lhg 只在 Phase A 做拍板。

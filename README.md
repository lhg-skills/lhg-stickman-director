# lhg-stickman-director

火柴人短视频导演 · lhg 版

## 前因后果（写给交接的 Agent）

- **起因**：2026-10-15，lhg 看到 @CrazyKaomei（疯狂的烤妹儿）的一条 X 推文，
  是她「爆款复刻」专栏第 08 期：复盘一个海外 YouTube 极简火柴人频道
  （36 条视频、19 万粉、单条近 800 万播），并开源了配套的制作 skill。
  （注：推文里没有抖音账号，"抖音"只出现在她往期文章标题里，此前已澄清。）
- **调研结论**：她的方法内核（导演提案、分镜方法论、风格锁定配方）值得吸收；
  但她的执行链路（英文旁白 + Gemini Omni Flash via Google Flow 单链路）
  不适合 lhg 的中文内容体系。
- **决策**：不延续她的方法，建本仓，**吸收方法、替换执行层**。
- **目的**：让 lhg 能用中文做火柴人短视频（主攻 AI 工具概念讲解类选题），
  执行层是他自己的生产力：Muse 额度 + Gemini PRO 的 Flow。

## 这个仓库要达到什么

一套可直接执行的中文火柴人视频工作流：

文案 → 导演提案（lhg 拍板）→ 提示词包 → 双执行层生成 → 合成成片

- v0.1（已交付，2026-10-15）：方法规格 + 可执行 skill
- v0.2（待做）：第一支正式选题试跑（AI 工具概念讲解，60 秒 9:16），沉淀风格卡

## 仓库结构（交接必读）

| 路径 | 用途 | 怎么读 |
|---|---|---|
| `METHOD.md` | 方法规格（七件套），与执行层无关 | **先读这个**，理解方法后再看 skill |
| `skills/directing-stickman-videos-lhg/SKILL.md` | 可执行 skill：完整实现 METHOD.md，中文旁白优先，Muse + Flow 双执行层 | 按里面的"工作流"节一步一步执行 |
| `skills/directing-stickman-videos/` | 上游原版文件（kaomei，MIT） | 只读参考（风格配方细节），不直接执行 |
| `ADAPTATION.md` | 决策记录：为什么这样改、预算纪律、人机分工、路线图 | 了解背景时读 |
| `LICENSE` | 上游 MIT 原文，完整保留 | — |

## 方法速览（七件套一句话版）

1. **Setup gate**：素材 / 画幅 / 时长 / 画风四要素，缺画幅画风一次问全
2. **Phase A 导演提案**：五阶段高完播心跳引擎（黄金钩子→打破常识→拉出内幕→
   真相揭秘→升华互动）+ N 行分镜表（三节拍、≥4 视觉装置、相邻衔接命名）
3. **确认门**：批准 / 改镜 / 改全局（三选一）；改全局则重出 Phase A
4. **风格锁定配方**：人物 DNA 锚点逐字重复 + 环境 + 负约束（防漂移核心）
5. **Phase B 提示词包**：12 步固定结构；画面零文字铁律（花字后期加）
6. **声音连续锁**：整片一个配音 profile，BGM 首段定调、后续延续
7. **验收清单**：条数/节拍/四锁/零文字/台词一字不差，见 METHOD.md §7

## Agent 执行方式

1. 先读 `METHOD.md`，再读 `skills/directing-stickman-videos-lhg/SKILL.md`。
2. 严格按 SKILL.md "工作流"节推进；卡在确认门必须停下来等 lhg 拍板，
   不得自行跳过。
3. 双执行层路由：Muse 出全片草稿（分镜预览图 → 6 条视频 → TTS 配音）→
   lhg 看片确认 → 标记需 Flow 重做的镜头（默认无）→ FFmpeg/剪映合成
   （画面 + 配音 + 字幕 + BGM）。
4. Flow 每个补镜先报 credits 估算，lhg 确认后再烧；不自动购买 credits；
   不可逆操作一律先确认。

## 成本与预算纪律

- Skill 本身零成本；费用只发生在视频生成环节。
- Flow（Gemini PRO）：每月 1000 credits 内；Fast 档先过、Quality 档定稿；
  每天 50 免费分优先用。
- 降级链：Muse media 不可用 → Flow 免费 → Flow Pro → 豆包 Seedance
 （约 0.44 元/秒，付费兜底）。

## 来源与致谢

本仓库改编自 kaomei（疯狂的烤妹儿 / @CrazyKaomei）的开源项目
**stickman-video-director**：https://github.com/kaomei/stickman-video-director

原项目 MIT License，`LICENSE` 文件完整保留。上游更新通过 `upstream`
remote 定期同步（注意上游含大体积演示素材，`git fetch` 易 stall，
同步时建议单文件拉取）。

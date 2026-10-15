# lhg 适配方案（lhg-stickman-director）

方向：**吸收上游的方法，替换上游的执行层**。
不做"英文旁白 + Flow 单链路"的延续，也不做薄覆盖。

## 上游来源

- 改编自 kaomei（疯狂的烤妹儿 / @CrazyKaomei）的开源项目
  `stickman-video-director`：https://github.com/kaomei/stickman-video-director
- 原项目 MIT License，LICENSE 文件完整保留；`skills/directing-stickman-videos/`
  为上游原版文件（只读参考，不直接执行）。
- 上游更新通过 `upstream` remote 定期同步（注意：上游含大体积演示素材，
  `git fetch` 易 stall，同步时建议单文件拉取）。

## 方法吸收（见 METHOD.md）

把上游 skill 拆解为与执行层无关的方法规格，完整保留：

1. Setup gate：素材/画幅/时长/画风四要素门
2. Phase A 导演提案：五阶段高完播心跳引擎（黄金钩子→打破常识→拉出内幕→
   真相揭秘→升华互动）+ N 行分镜表（三节拍、≥4 视觉装置、衔接命名）
3. 确认门：批准 / 改镜 / 改全局（三选一），改全局则重出 Phase A
4. 风格锁定配方：人物 DNA 锚点逐字重复 + 环境 + 负约束（防漂移核心）
5. Phase B 提示词包：12 步固定结构 + 画面零文字铁律
6. 声音连续锁：整片一个配音 profile，BGM 首段定调后续延续

## 执行层替换（见 skills/directing-stickman-videos-lhg/SKILL.md）

| 上游 | lhg 版 |
|---|---|
| 英文旁白优先 | 中文旁白优先（45–55 字/10 秒）+ 英文对照版 |
| Gemini Omni Flash via Flow 单链路 | Muse 直出层 + Flow 质量层双链路 |
| Flow 烧分试错 | 先 Muse 出全片草稿（6 条/轮），确认后再定点用 Flow |
| 配音走模型原生 | 中文配音走 Muse TTS，后期混音合成 |

路由规则：Muse 全片草稿 → 看片确认 → 标记需 Flow 重做的镜头（默认无）
→ TTS 配音 → FFmpeg/剪映合成（画面+配音+字幕+BGM）。

## 预算纪律

- Flow（Gemini PRO）：每月 1000 credits 内；Fast 先过、Quality 定稿；
  每天 50 免费分优先用。每个补镜先报 credits 估算，用户确认后再烧。
- Muse 层：图片/TTS/视频按需用；media 能力 rollout-gated，不可用时走降级链
  （Flow 免费 → Flow Pro → 豆包 Seedance）。

## 人机分工

- Muse：提案、提示词、生成、合成全包
- lhg：Phase A 拍板；看草稿片拍板；Flow 补镜清单与预算拍板

## 路线图

- v0.1：建仓、标注来源、方法规格定稿（METHOD.md）、双执行层 skill
- v0.2：第一支正式选题试跑（AI 工具概念讲解，60 秒 9:16），沉淀风格卡
- v0.3：出海英文版链路验证（Flow 原生英文配音）
- v0.4：按 SKILL-DISTRIBUTION.md 补齐分发件（manifest.yaml、sync-to-gitee.yml、
  THIRD-PARTY-NOTICES.md），Gitee 镜像上线

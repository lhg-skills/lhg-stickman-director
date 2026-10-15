# lhg 适配方案（lhg-stickman-director）

## 上游来源
- 改编自 kaomei（疯狂的烤妹儿 / @CrazyKaomei）的开源项目
  `stickman-video-director`：https://github.com/kaomei/stickman-video-director
- 原项目 MIT License，LICENSE 文件完整保留；本仓并入了上游完整 git 历史。
- 同步上游：`git fetch upstream && git merge upstream/main`（upstream remote 已配置）。

## 适配目标
把上游"英文旁白 + Google Flow 出片"的原链路，改成服务 lhg 内容体系的版本：
中文口播优先（视频号/抖音/B站），英文版保留（出海 X/YouTube），生成端国内走豆包、
出海走 Flow。

## 改动清单（v0.2 起逐项落地）
1. **旁白语言**：导演提案默认输出中文旁白 + 英文对照版；配音分两档——
   中文（豆包 TTS / 剪映配音）、英文（Omni Flash 原生配音）。
2. **生成端双链路**：国内 = 豆包 Seedance（约 0.44 元/秒；先用 Mini/Fast 档过草稿，
   定稿再上满血版）；出海 = Google Flow（每天 50 免费积分起步，约 2–5 条）。
3. **默认规格**：9:16 竖屏、60 秒（每 10 秒一段，共 6 段提示词），对齐视频号/抖音/小红书。
4. **选题模板**：新增"AI 工具概念讲解"专用叙事结构（痛点 → 原理 → 演示 → 结论），
   替代上游默认的通用知识结构；出海版保留英文 5 节点结构。
5. **成片规范**：剪映字幕样式、BGM、封面与「刘洪光实名上网」现有 VI 对齐；
   生成画面默认不带文字，字幕后期统一加。
6. **分工**：Muse 代跑 skill（文案 → 导演提案 → 提示词包），lhg 只审提案拍板；
   生成与剪辑环节按上述双链路执行。

## 目录规划
- `skills/directing-stickman-videos/` — 上游原版 skill（保持不动，方便同步）
- `skills/directing-stickman-videos-lhg/` — lhg 适配版 skill（v0.2 新建）
- `docs/doubao-sop.md` — 豆包出片标准操作流程（v0.3 实测后沉淀）
- `examples/` — 样片与提案实例

## 路线图
- v0.1（本提交）：建仓、标注来源、适配方案定稿
- v0.2：中文旁白优先的适配版 skill
- v0.3：豆包链路实测 + SOP 文档
- v0.4：第一支正式选题试跑（AI 工具概念讲解）

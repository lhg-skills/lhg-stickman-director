# lhg-stickman-director

火柴人短视频导演 · lhg 适配版

## 来源与致谢

本仓库改编自 kaomei（疯狂的烤妹儿 / @CrazyKaomei）的开源项目
**stickman-video-director**：https://github.com/kaomei/stickman-video-director

原项目采用 MIT License，`LICENSE` 文件完整保留。
`skills/directing-stickman-videos/` 为上游原版文件（保持不动，方便同步）；
上游更新通过 `upstream` remote 定期同步：
`git fetch upstream && git merge upstream/main`。

## 改了什么（相对上游）

- 中文旁白优先，英文对照版保留（供出海）
- 生成端双链路：国内走豆包 Seedance，出海走 Google Flow
- 默认 9:16、60 秒，对齐视频号/抖音/小红书
- 新增"AI 工具概念讲解"选题模板
- 完整适配方案见 `ADAPTATION.md`；适配版 skill 在
  `skills/directing-stickman-videos-lhg/SKILL.md`

## 使用方法

直接把选题/文案发给 Muse，Muse 按适配版 skill 执行：

文案 → 导演提案（你审核拍板）→ 提示词包 → 生成 → 剪映成片

## 成本

- Skill 本身零成本；费用只发生在视频生成环节。
- 豆包 Seedance 约 0.44 元/秒：一条 60 秒约 22–26 元（不计重试）；
  先用 Mini/Fast 档出草稿，定稿再上满血版。
- Google Flow 每天 50 免费积分（约 2–5 条），适合出海版起步。

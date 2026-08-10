# CHANGELOG

## [2.0.0] - 2026-08-10

### Docs
- 新建 `AGENTS.md`（项目架构与 AI 协作指南），合并原有的 CLAUDE.md
- 更新 `README.md`，统一格式

---

## [1.0.0] - 2026-07

### Added
- 人类基准测试初始版本：7 项认知测试合集
- 单文件 `index.html`（内联 CSS/JS）+ `share-card.html`，零依赖
- 7 项测试：反应速度、数字记忆、词汇记忆、视觉记忆、序列记忆、打字速度、瞄准训练
- 深色科技风 UI，CSS 变量统一主题色
- 移动端适配 + 微信 webview 优化

### Changed
- 战绩存储从 localStorage 迁移到 GamePlatform 云端（`gameId='human-bench'`，子测试用 `meta.testId` 区分）
- 接入 GamePlatform 登录门
- 移除顶部用户栏与天梯榜浮层
- 域名改回 Cloudflare Pages 默认域名 `human-bench.pages.dev`
- 部署至 Cloudflare Pages

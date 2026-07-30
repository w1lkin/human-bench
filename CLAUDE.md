# CLAUDE.md

## 项目概览

人类基准测试 — 多项认知能力测试的合集静态 Web 应用，受 Human Benchmark 启发。

- **文件结构**：单文件 `index.html`（内联 CSS/JS），零依赖，打开即玩
- **部署地址**：`https://human-bench.pages.dev/`
- **分享卡片**：`share-card.html`（1200×1600 Canvas 分享图 + QR 码）

## 子测试列表

| 测试名称 | 测试内容 | 衡量指标 |
|---|---|---|
| 反应速度 | 屏幕变绿时尽快点击 | 反应时间（ms） |
| 数字记忆 | 记住并复述逐渐增长的数字串 | 最大位数 |
| 词汇记忆 | 记住并复述逐渐增长的词汇列表 | 最大词汇数 |
| 视觉记忆 | 记住亮起的格子位置并复现 | 最大格子数 |
| 序列记忆 | 记住并复现随机亮起的方块顺序 | 最大序列长度 |
| 打字速度 | 尽可能快和准确地输入随机词汇 | WPM、准确率 |
| 瞄准训练 | 尽快点击随机出现的目标 | 平均反应时间 |

## 运行方式

直接浏览器打开 `index.html`，无需构建、安装或本地服务器。

## 技术架构

单文件 `index.html`，结构如下：

```
HTML
├── <head> —— meta 标签（移动端适配、og 社交分享）、内联 CSS
└── <body>
    ├── #app —— 主容器
    │   ├── #menu —— 主菜单（所有测试的入口卡片）
    │   ├── #test-container —— 测试区域（各测试共用的游戏容器）
    │   │   └── 各测试通过 innerHTML 动态注入内容
    │   └── #result —— 结果页（测试完成后展示分数和排名）
    ├── #share-overlay —— 分享卡片浮层
    └── <script> —— 内联 JavaScript
```

- 每个子测试是一个独立的对象，包含 `id`、`name`、`desc`、`emoji`、`init()`、`destroy()` 方法
- 在主菜单点击测试卡片 → 隐藏菜单 → 调用 `test.init()` → 渲染测试界面到 `#test-container`
- 测试完成后显示 `#result`，展示本次得分和历史最佳（localStorage 存储）

## 移动交互约定

- 触屏点击为主交互方式（无长按）
- `user-scalable=no` 防止双击缩放
- CSS `user-select: none` 防止微信长按选中
- `touch-action: manipulation` 消除点击 300ms 延迟

## 数据存储

- 每个测试的最高分存储在 `localStorage`，key 格式：`humanbench_{testId}`
- 每次测试完成对比并更新最高分

## 约定

- 不引入任何外部依赖（CDN、框架、字体）
- 所有 CSS 内联在 `<style>` 标签
- 所有 JS 内联在 `<script>` 标签
- 移动优先，适配 320px-428px 宽度
- 中文界面，全量中文注释
- 使用 CSS 变量统一主题色

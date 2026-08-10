# 人类基准测试

## 项目概览

纯前端认知测试合集，灵感来自 Human Benchmark：7 项小游戏测反应、记忆、打字、瞄准能力。

- **形态**：`index.html`（主游戏，内联 CSS/JS）+ `share-card.html`，零依赖
- **数据云端**：各测试成绩通过 `GamePlatform` SDK 上报云端（`gameId='human-bench'`，子测试用 `meta.testId` 区分），需登录后游玩
- **移动适配**：触屏 + 微信 webview
- **部署域名**：`https://human-bench.pages.dev/`

## 包含的测试

| 测试 | 玩法 | 衡量指标 |
|---|---|---|
| 反应速度 | 屏幕变绿时尽快点击 | 平均反应时间（ms） |
| 数字记忆 | 记住并复述逐渐变长的数字串 | 最大位数 |
| 词汇记忆 | 判断词汇是否出现过 | 正确次数 |
| 视觉记忆 | 记住并复现亮起格子的位置 | 最大格子数 |
| 序列记忆 | 记住并复现方块亮起顺序 | 最大序列长度 |
| 打字速度 | 限时内尽量快准地输入英文 | WPM |
| 瞄准训练 | 尽快点击随机出现的目标 | 平均反应时间（ms） |

## 本地运行

```sh
cd human-bench
python3 -m http.server 8000
# 浏览器访问 http://localhost:8000
```

> 分享卡片二维码依赖 `api.qrserver.com`，需 http(s) 来源加载，**不要用 `file://` 直接打开**。

## 技术架构

单文件 `index.html`，DOM 结构：

```
#app                      # 主容器
├── #menu                 # 主菜单（所有测试的入口卡片）
├── #test-container       # 测试区域（各测试共用容器，通过 innerHTML 注入）
└── #result               # 结果页（测试完成后展示分数和排名）
#share-overlay            # 分享卡片浮层
```

- 每个子测试是一个独立对象：`id` / `name` / `desc` / `emoji` / `init()` / `destroy()`
- 点击测试卡 → 隐藏菜单 → `test.init()` → 渲染到 `#test-container` → 完成后显示 `#result`
- 每次测试完成对比并更新最高分（云端存储，需登录后上报）

## 移动交互约定

- 触屏点击为主交互方式（无长按）
- `user-scalable=no` 防止双击缩放
- CSS `user-select: none` 防止微信长按选中
- `touch-action: manipulation` 消除点击 300ms 延迟

## 数据存储

- 每个测试的成绩统一上报到云端 `gameId='human-bench'`（子测试用 `meta.testId` 区分），需登录后游玩；本地不再保存任何数据

## 约定

- 不引入任何外部依赖（CDN、框架、字体）
- 所有 CSS 内联在 `<style>` 标签；所有 JS 内联在 `<script>` 标签
- 移动优先，适配 320px-428px 宽度
- 中文界面，全量中文注释
- 使用 CSS 变量统一主题色

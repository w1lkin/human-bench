# 人类基准测试（Human Bench）

纯前端单机基准测试小游戏（即将上线）。

## 单机版特性

- **纯静态**：计划为 `index.html`（内联 CSS/JS），零依赖、无构建步骤。
- **无需联网**：测试逻辑将全部在浏览器本地运行。
- **数据本地**：成绩保存在本机 `localStorage`，无账号、无后端。

## 状态

当前为占位项目（`index.html` 为「即将上线」页），功能待开发。

## 本地预览

```sh
cd human-bench
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

## 文件结构

```
human-bench/
└── index.html   # 占位 / 即将上线
```

## 部署

可部署到 Cloudflare Pages。

## 版本

当前分支：`release/1.0.0`

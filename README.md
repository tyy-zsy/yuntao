# 云铸 yuntao · 点云基元识别工作区

云铸（CloudForge）是一个面向点云的**基元识别与几何重建工作台**：对点云做 RANSAC 基元
（平面/球/圆柱/圆锥/圆环）检测、精拟合，并联动 CAD 生成与结果核验。本仓库同时包含其依赖的
**Agnes 智能体运行框架（agnes-harness）** 与点云数据集。

## 目录

- [`CloudForge/`](CloudForge/) — 云铸桌面端：Tauri 2 + Vue 3 + Three.js / Rust / C++17 / Python
- [`agnes-harness/`](agnes-harness/) — Agnes 智能体框架（Node + TypeScript，pnpm monorepo）
- [`data/`](data/) — 点云数据集（livingroom1 / office1 片段等，已随仓）
- [`deliverables/`](deliverables/) — 演示 PPT、4K 海报等交付物
- [`复现指南.md`](复现指南.md) — **环境搭建、依赖清单与复现步骤（从这里开始）**
- [`BUILD-CHECKLIST.md`](BUILD-CHECKLIST.md) — 安装/构建过程的问题清单与排错记录

## 快速开始

依赖与构建产物不入库，克隆后请按 **[复现指南.md](复现指南.md)** 安装工具链并构建。最小流程：

```bash
# 1) CloudForge 前端
cd CloudForge && npm ci && npm run dev        # http://localhost:5183

# 2) Agnes 智能体服务
cd ../agnes-harness && corepack enable
pnpm install && pnpm --filter @agnes/cli build:local
cd ../CloudForge && node ../agnes-harness/packages/cli/dist/local/agnes.mjs serve   # http://127.0.0.1:4177

# 3) 桌面端（需先补齐 C++ 第三方 ransac_sd，见复现指南第五节）
cd CloudForge && npm run tauri dev
```

## 许可说明

- 项目自有代码：Apache-2.0（Agnes / CloudForge 各 package.json 中标注）。
- 第三方组件：`CloudForge/src-tauri/cpp/third_party/`（Eigen 随仓；`ransac_sd` 因仅授权研究
  用途、未授予再分发权利而**不随仓分发**，获取方式见该目录 README）。

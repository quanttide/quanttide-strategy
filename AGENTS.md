# AGENTS.md

## 子模块

- `apps/` — 可部署应用
- `packages/toolkit` — 领域共享库/工具集
- `examples/default` — 实验室——实验性/原型项目
- `docs/` — 领域文档

## 子模块同步约定

- 子模块初始化后若报错"找不到当前版本"，检查子模块 git 目录中的 `remote.origin` 配置，缺失时手动补上再 fetch。
- `.gitmodules` 中为各子模块配置 `branch`（如 `submodule.<path>.branch main`），以便 `git submodule update --remote` 跟踪远端分支。
- 更新子模块后及时提交 gitlink 指针变更并推送远端，保持同步。

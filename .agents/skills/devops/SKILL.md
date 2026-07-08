---
name: devops
version: 1.0.0
description: "量潮DevOps命令行工具（qtcloud-devops）：管理构建/测试/发布全生命周期、规划进度、代码审计、契约状态和环境诊断。当用户需要查看构建/测试/发布状态、执行审计、发布版本、管理ROADMAP规划进度、检查组件同步状态、查看契约或诊断环境依赖时使用。"
metadata:
  requires:
    bins: ["qtcloud-devops"]
---

# 量潮DevOps（qtcloud-devops）

> **量潮DevOps实验室 — Git 子模块管理 & 发布管理**

## 概述

命令按**生命周期阶段**（build → test → release）和**跨阶段**（code / plan / contract / source）组织，另有聚合命令（status / audit）。

## 命令参考

### 生命周期：构建（build）

| 子命令 | 用途 |
|--------|------|
| `build status` | 查看构建状态 |
| `build clean` | 清理构建产物（`target/`、`dist/` 等） |
| `build audit` | 构建审计：检查编译器配置、CI 工作流、依赖声明 |

### 生命周期：测试（test）

| 子命令 | 用途 |
|--------|------|
| `test status` | 查看测试状态 |
| `test clean` | 清理本地测试产物（覆盖率报告等） |
| `test audit` | 质量审计：扫描测试覆盖率、错误变体覆盖、门禁达标情况 |

### 生命周期：发布（release）

| 子命令 | 用途 |
|--------|------|
| `release status` | 查看发布状态：版本号、标签、CHANGELOG、工作区状态 |
| `release audit` | 发布预检审计：检查版本号、配置文件、CHANGELOG、工作区、标签冲突、远程可达性 |
| `release publish` | **发布版本：** 校验 CHANGELOG → 创建 tag → 推送到远端 → 创建 GitHub Release |

### 跨阶段：代码（code）

| 子命令 | 用途 |
|--------|------|
| `code status` | 查看组件（Git 子模块）同步状态 |
| `code audit` | 审计代码质量：scope 目录、TODO/FIXME 密度、语法检查 |

### 跨阶段：规划（plan）

| 子命令 | 用途 |
|--------|------|
| `plan status` | 查看 ROADMAP.md 规划进度 |
| `plan clean` | 删除 ROADMAP 中 scope 已完成条目 |
| `plan audit` | 审计 ROADMAP 与 TODO 的关系：ROADMAP 是完整规划，TODO 是待办 |
| `plan doctor` | 修复 ROADMAP 和 TODO 的格式：标准化版本头、分类、checkbox |

### 跨阶段：契约（contract）

| 子命令 | 用途 |
|--------|------|
| `contract status` | 查看契约配置与状态 |

### 跨阶段：环境（source）

| 子命令 | 用途 |
|--------|------|
| `source status` | 检查系统外部依赖命令状态 |

### 聚合命令

| 命令 | 用途 |
|------|------|
| `status` | 聚合所有 `status`（build + test + release + contract + plan） |
| `audit` | 聚合所有 `audit`（build + test + release） |
| `help` | 按 stage 分组展示命令导览 |

## 使用场景

### 日常开发检查

```bash
# 快速查看整体状态
qtcloud-devops status

# 查看组件同步（子模块）状态
qtcloud-devops code status

# 环境诊断
qtcloud-devops source status
```

### 构建与测试

```bash
# 构建状态 → 清理 → 审计
qtcloud-devops build status
qtcloud-devops build clean
qtcloud-devops build audit

# 测试状态 → 清理 → 审计
qtcloud-devops test status
qtcloud-devops test clean
qtcloud-devops test audit
```

### 发布管理

```bash
# 发布预检审计
qtcloud-devops release audit

# 发布版本（校验 → tag → push → GitHub Release）
qtcloud-devops release publish

# 指定版本号发布（范围化版本如 cli/v0.5.0）
qtcloud-devops release publish --version cli/v0.5.0

# 预览模式（不执行任何写操作）
qtcloud-devops release publish --dry-run

# 跳过确认并推送注册表提示
qtcloud-devops release publish -y --registry crates

# 强制重新发布（删除已有 tag 和 Release 后重建）
qtcloud-devops release publish --force
```

> `release publish` 是写入操作，**默认会要求用户确认**。建议先 `--dry-run` 预览再执行。

### 规划管理

```bash
# 查看 ROADMAP 进度
qtcloud-devops plan status

# 审计规划完整性
qtcloud-devops plan audit

# 修复 ROADMAP/TODO 格式
qtcloud-devops plan doctor

# 清理已完成条目
qtcloud-devops plan clean
```

# AI Agent Runtime - 项目上下文

为 iFlow CLI AI 代理提供的项目上下文信息。

## 项目概述

**项目名称**：ai-agent-runtime

**核心愿景**：围绕大模型或已有 coding agent 的运行时环境，提供从项目搭建到项目管理的全流程支持。

**开源协议**：Apache License 2.0

**Git 仓库**：git@github.com:lihaizhong/ai-agent-runtime.git

**主要维护者**：niuma

## 核心架构

### Scaffolding（工程搭建准备）

**职责**：项目启动前的准备工作

**核心功能**：项目初始化、模板管理、环境检查、配置生成、依赖安装、目录结构创建、代码规范设置、版本控制初始化、Hooks 配置

**内部结构**：
```
scaffolding/
├── README.md
├── commands/
├── agents/
├── skills/
└── templates/
```

### Harness（工程运行治理）

**职责**：模型工作时的支持和治理

**核心功能**：工具分发、上下文压缩、跨伦状态管理、安全规则执行、经验记忆写入、长会话稳定性保障

**工具集成**：superpowers、openspec、speckit

**内部结构**：
```
harness/
├── README.md
├── commands/
├── agents/
├── skills/
└── middleware/
```

## 工作流程

```
项目启动 → [Scaffolding] 工程搭建准备 → 项目开发 → [Harness] 工程运行治理 → 项目交付
```

## 临时/共享资源

**skills/** - 临时/共享技能定义（待整理）：evals、fullstack、openexp、prompt-learning

**commands/** - 临时/共享命令定义（待整理）：openexp.md

## 核心技能

### prompt-learning（提示词工程学习助手）

**位置**：`skills/prompt-learning/`

**功能**：学习和实践提示词工程，提供教程、练习题和质量评估

**核心原则**：清晰明确、提供上下文、指定输出格式、提供示例、分解复杂任务

### fullstack（全栈开发工作流）

**位置**：`skills/fullstack/`

**功能**：协调多个 subagent 完成复杂全栈开发任务（API 设计、架构设计、多组件集成）

**核心原则**：Spec-Driven、Workspace Isolation、No Over-Engineering

**关键命令**：`/opsx:propose`、`/opsx:apply`、`/opsx:archive`

### openexp（经验管理技能）

**位置**：`skills/openexp/`

**功能**：从对话中学习积累经验，并在未来交互中应用（Obsidian Markdown 格式）

**数据存储**：`~/Exp Vault`

**相关命令**：`/openexp`

## 项目目录结构

```
ai-agent-runtime/
├── AGENTS.md
├── README.md
├── LICENSE
├── commands/
├── scaffolding/
├── harness/
└── skills/
```

## 开发约定

- **技能命名**：kebab-case（如 `prompt-learning`）
- **命令命名**：斜杠前缀（如 `/openexp`）
- **目录命名**：小写字母和连字符
- **文档格式**：Markdown，每个技能包含 `SKILL.md`

## 环境依赖

**必需工具**：Python 3.9+、Obsidian 桌面应用（1.12+）

**可选工具**：uv、storks-obsidian-mcp

---

**更新日期**：2026-03-14
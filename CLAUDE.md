# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

AI Agent Runtime 是为大模型和 coding agent 提供的运行时环境，包含两大核心模块：
- **Scaffolding** (`scaffolding/`): 工程搭建准备，负责项目初始化、环境配置
- **Harness** (`harness/`): 工程运行治理，负责工具分发、上下文管理、安全执行

## 核心架构

```
ai-agent-runtime/
├── agents/          # 专业智能体定义（api-designer, tester, spec-writer 等）
├── skills/          # 技能定义
│   ├── fullstack/   # TDD 驱动的全栈开发工作流
│   ├── openexp/     # 经验管理技能（Obsidian 存储）
│   └── prompt-learning/  # 提示词工程学习
├── commands/        # 命令定义（openexp.md）
├── scaffolding/     # 工程搭建模块（规划中）
└── harness/         # 工程运行治理模块（规划中）
```

**注意**: `scaffolding/` 和 `harness/` 目录目前处于规划阶段。

## 技能使用指南

### fullstack 技能

**适用场景**: 复杂任务（API 设计 5+ 端点、多模块架构、前后端集成）

**不适用**: 简单任务（< 200 行代码、单文件修改、快速原型）

**核心原则**:
- Spec-Driven: 必须先运行 `/opsx:propose` 创建变更提案
- TDD 循环: Red（测试先行）→ Green（最小实现）→ Refactor（优化）
- Workspace Isolation: 每个变更在独立上下文中执行
- No Over-Engineering: 只实现明确要求的功能

### openexp 技能

**数据存储**: `~/Exp Vault`

**脚本路径**: 使用动态查找
```bash
OPENEXP_SCRIPTS=$(find . -path "*/skills/openexp/scripts/obsidian-cli.sh" -type f 2>/dev/null | head -1 | xargs dirname 2>/dev/null)
```

**常用操作**:
```bash
# 搜索经验
$OPENEXP_SCRIPTS/obsidian-cli.sh search <query>

# 创建经验
$OPENEXP_SCRIPTS/obsidian-cli.sh create <path> '<content>'

# 维护经验库（建议每周）
python3 $OPENEXP_SCRIPTS/maintain-experience-vault.py
```

**经验类型**: `preference`（偏好）、`workflow`（工作流）、`solution`（解决方案）、`knowledge`（知识）、`experience`（完整经验）、`convention`（约定）

**文件命名格式**: `exp_<type>_<YYYYMMDD_HHMMSS>_<seq>.md`

## 开发约定

- **技能命名**: kebab-case（如 `prompt-learning`）
- **命令命名**: 斜杠前缀（如 `/openexp`）
- **目录命名**: 小写字母和连字符
- **文档格式**: Markdown，每个技能包含 `SKILL.md`

## 环境依赖

**必需**:
- Python 3.9+
- Obsidian 桌面应用（1.12+）
- Obsidian CLI（从 Obsidian 设置中安装）

**可选**: uv
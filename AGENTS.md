# AI Agent Skills 项目

为 iFlow CLI 设计的 AI 代理技能集合，用于定义、管理和扩展 AI 代理的能力。

## 项目概述

本项目通过 Markdown 格式的 `SKILL.md` 文件定义技能，包含元数据、功能描述、使用方法和最佳实践。

**开源协议**：Apache License 2.0

## 核心技能

### 1. prompt-learning（提示词工程学习助手）
- **位置**：`skills/SKILL.md`
- **功能**：学习和实践提示词工程，提供教程、练习题和质量评估
- **触发关键词**：学习提示词工程、零样本、少样本、思维链、CoT 等

### 2. fullstack（全栈开发工作流）
- **位置**：`skills/fullstack/SKILL.md`
- **功能**：协调多个 subagent 完成复杂全栈开发任务
- **适用场景**：API 设计（5+ 端点）、复杂架构设计、多组件集成
- **核心原则**：Spec-Driven、Workspace Isolation、No Over-Engineering
- **关键命令**：`/opsx:propose`、`/opsx:apply`、`/opsx:archive`

### 3. openexp（经验管理技能）
- **位置**：`skills/openexp/SKILL.md`
- **功能**：从对话中学习积累经验，应用于未来交互
- **数据存储**：`~/Exp Vault`（Obsidian Markdown 格式）
- **相关命令**：`/openexp`

## 自定义命令

### /openexp
- **位置**：`commands` 文件
- **功能**：经验管理，使用自然语言描述需求
- **示例**：
  - 添加经验：`/openexp 我喜欢用 pnpm`
  - 搜索经验：`/openexp 搜索 CORS 相关的经验`
  - 应用经验：`/openexp 遇到了 CORS 问题，有什么经验吗？`

## 开发约定

### 技能命名
- 使用 kebab-case（如 `prompt-learning`、`fullstack`）
- 简洁且具有描述性

### 文件结构
- 每个技能必须包含 `SKILL.md`
- 复杂技能在 `reference/` 目录提供详细文档
- 使用 Markdown 格式，保持清晰层级

### 版本管理
- 使用语义化版本
- 在 `metadata.version` 中维护版本号
- 在文档底部记录版本历史

## 环境依赖

**必需工具**：
- Python 3.9+（运行维护脚本）
- Obsidian 桌面应用（1.12+，openexp 技能）

**可选工具**：
- uv（Python 包管理器）
- storks-obsidian-mcp（Obsidian MCP 服务器）

## 项目元数据

- **项目名称**：ai-agent-skills
- **开源协议**：Apache License 2.0
- **兼容性**：iFlow CLI
- **主要维护者**：niuma
- **Git 仓库**：git@github.com:lihaizhong/ai-agent-skills.git
# AI Agent Skills

为 iFlow CLI 设计的 AI 代理技能集合，用于定义、管理和扩展 AI 代理的能力。

## 项目简介

本项目是一个技能配置和文档项目，专注于定义和组织 AI 代理的技能配置和工作流程。每个技能都通过 Markdown 格式的 `SKILL.md` 文件进行定义，包含技能的元数据、功能描述、使用方法和最佳实践。

**开源协议**：Apache License 2.0

## 核心技能

### prompt-learning（提示词工程学习助手）
帮助用户学习和实践提示词工程和上下文工程，提供结构化的教程、练习题和提示词质量评估。

**使用场景**：
- 想要系统学习提示词工程的基础概念
- 需要分析和改进现有的提示词
- 希望通过练习题提升提示词编写能力
- 评估提示词质量并获取优化建议

### fullstack（全栈开发工作流）
协调多个专业 subagent 协作完成复杂全栈开发任务，包括 API 设计、架构设计和多组件集成。

**使用场景**：
- 设计包含多个端点的 API（如认证系统、电商系统）
- 构建复杂的前后端应用（如博客平台、实时聊天）
- 需要微服务架构、数据可视化 dashboard 等多模块系统

**核心原则**：
- Spec-Driven：所有代码变更必须先有规格定义
- Workspace Isolation：每个变更在独立上下文中执行
- No Over-Engineering：只实现明确要求的功能

### openexp（经验管理技能）
从对话中学习、积累经验，并在未来交互中应用这些经验以提供更智能的响应。使用 Obsidian Markdown 格式存储。

**使用场景**：
- 记录用户偏好和工作模式
- 存储和检索解决方案和最佳实践
- 应用历史经验优化响应
- 通过反馈不断改进经验质量

## 快速开始

### 环境准备

**必需工具**：
- Python 3.9+
- Obsidian 桌面应用（1.12+）

**可选工具**：
- uv（Python 包管理器）
- storks-obsidian-mcp（Obsidian MCP 服务器）

### 安装配置

1. 克隆项目：
```bash
git clone git@github.com:lihaizhong/ai-agent-skills.git
cd ai-agent-skills
```

2. 配置 Obsidian Vault（用于 openexp 技能）：
```bash
mkdir -p ~/Exp\ Vault
```

3. （可选）配置 Obsidian MCP 服务器：
在 MCP 客户端配置文件中添加 storks-obsidian-mcp 配置

### 使用示例

#### 提示词工程学习

```
用户：我想学习提示词工程的基础知识
AI：提供结构化的教程内容，包含定义、重要性、核心原则和实际示例
```

#### 全栈开发工作流

```
用户：帮我设计一个电商系统的 API
AI：
1. 执行 /opsx:propose 创建变更提案
2. 协调 api-designer 设计 API 结构
3. 使用 frontend-developer 和 backend-developer 实现前后端
4. 通过 frontend-tester 验证功能
5. 执行 /opsx:archive 归档变更
```

#### 经验管理

```
用户：/openexp 我喜欢用 pnpm 而不是 npm
AI：自动创建用户偏好记录

用户：/openexp 遇到了 CORS 问题，有什么经验吗？
AI：搜索相关经验并提供建议
```

## 目录结构

```
ai-agent-skills/
├── AGENTS.md              # 项目上下文文件（开发参考）
├── README.md              # 项目说明（本文件）
├── LICENSE                # Apache 2.0 开源协议
├── commands               # 自定义命令定义
│   └── /openexp          # 经验管理命令
└── skills/                # 技能定义目录
    ├── SKILL.md          # 提示词工程学习助手
    ├── evals/            # 技能评估测试
    │   └── evals.json
    ├── fullstack/        # 全栈开发工作流
    │   ├── SKILL.md
    │   └── reference/    # 参考文档
    └── openexp/          # 经验管理技能
        ├── SKILL.md
        ├── Conventions/  # 约定规范
        ├── reference/    # 参考文档
        ├── scripts/      # 维护脚本
        └── templates/    # Obsidian 模板
```

## 贡献指南

欢迎贡献新的技能和改进现有技能！

### 添加新技能

1. 在 `skills/` 目录下创建新的子目录
2. 创建 `SKILL.md` 文件，包含以下内容：
```yaml
---
name: skill-name
description: 技能描述
license: MIT
compatibility: iFlow CLI
metadata:
  author: 作者名
  version: "1.0"
  tags:
    - tag1
    - tag2
---
```
3. 在 `skills/evals/evals.json` 中添加评估测试用例
4. 如有需要，创建 `reference/` 目录存放参考文档

### 添加新命令

在 `commands` 目录下创建新文件，定义命令的元数据和使用方法。

### 开发约定

- 使用 kebab-case 命名技能
- 保持文档清晰简洁
- 遵循语义化版本管理
- 在文档底部记录版本历史

## 维护脚本

### maintain-experience-vault.py

**位置**：`skills/openexp/scripts/`

**功能**：维护经验库，自动计算影响力和更新索引地图

**运行频率**：建议每周运行一次

```bash
python3 skills/openexp/scripts/maintain-experience-vault.py
```

### obsidian-cli.sh

**位置**：`skills/openexp/scripts/`

**功能**：Obsidian CLI 封装脚本，提供便捷的 vault 操作接口

## 常见问题

### Q: 如何选择合适的技能？

**A**: 根据任务复杂度选择：
- 简单任务（代码审查、小功能）：直接使用对应的 subagent
- 提示词学习：使用 prompt-learning
- 复杂全栈开发：使用 fullstack
- 经验管理：使用 openexp

### Q: openexp 技能需要什么配置？

**A**: 需要配置 Obsidian：
- 安装 Obsidian 桌面应用（1.12+）
- 创建 `~/Exp Vault` 目录
- 可选：配置 storks-obsidian-mcp 服务器

### Q: fullstack 技能适合什么场景？

**A**: 适合复杂任务：
- API 设计（5+ 端点）
- 复杂架构设计
- 多组件集成
- 不适合：简单代码审查、单个 bug 修复

### Q: 如何维护经验库？

**A**: 定期运行维护脚本：
```bash
python3 skills/openexp/scripts/maintain-experience-vault.py
```
建议每周运行一次，自动更新影响力和索引地图。

## 相关资源

- [AGENTS.md](AGENTS.md) - 详细的项目上下文和开发参考
- [iFlow CLI 文档](https://iflow.cli/)
- [Obsidian 文档](https://help.obsidian.md/)
- [Prompt Engineering 指南](https://www.promptingguide.ai/)

## 项目信息

- **兼容性**：iFlow CLI
- **开源协议**：Apache License 2.0
- **主要维护者**：niuma
- **Git 仓库**：git@github.com:lihaizhong/ai-agent-skills.git

## 许可证

本项目采用 Apache License 2.0 开源协议。详见 [LICENSE](LICENSE) 文件。
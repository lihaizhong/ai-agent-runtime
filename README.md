# AI Agent Runtime

围绕大模型或已有 coding agent 的运行时环境，提供从项目搭建到项目管理的全流程支持。

## 项目简介

本项目旨在打造一套完整的 AI 工程运行时环境，支持大模型和各种 coding agent 的有效协作。通过提供工程搭建（Scaffolding）和工程运行治理（Harness）两大核心能力，确保 AI 驱动的项目能够高效、稳定地开发和运行。

**核心愿景**：为 AI 工程化提供标准化的运行时环境，降低 AI 开发门槛，提升开发效率和质量。

**开源协议**：Apache License 2.0

## 核心架构

AI Agent Runtime 由以下核心模块组成：

- **Scaffolding**：工程搭建的准备工作，负责项目初始化、环境配置、依赖管理等。内部包含专属的 commands、agents、skills 等组件
- **Harness**：工程运行时的治理工作，负责工具分发、上下文管理、安全执行等。内部包含专属的 commands、agents、skills 等组件

每个核心模块都是独立的运行时环境，拥有自己的工具集、智能体和技能系统，协同工作以提供完整的 AI 工程化支持。

## 核心技能

### fullstack（全栈开发工作流）v3.0

协调多个专业 subagent 协作完成复杂全栈开发任务，遵循 TDD 实践。

**使用场景**：
- 设计包含多个端点的 API（如认证系统、电商系统）
- 构建复杂的前后端应用（如博客平台、实时聊天）
- 需要微服务架构、数据可视化 dashboard 等多模块系统

**核心原则**：
- **TDD 循环**：Red（测试先行）→ Green（最小实现）→ Refactor（优化）
- **Spec-Driven**：所有代码变更必须先有规格定义
- **Workspace Isolation**：每个变更在独立上下文中执行
- **No Over-Engineering**：只实现明确要求的功能

### openexp（经验管理技能）v2.8

从对话中学习、积累经验，并在未来交互中应用这些经验以提供更智能的响应。使用 Obsidian Markdown 格式存储。

**使用场景**：
- 记录用户偏好和工作模式
- 存储和检索解决方案和最佳实践
- 应用历史经验优化响应
- 通过反馈不断改进经验质量

### prompt-learning（提示词工程学习助手）v2.6

帮助用户学习和实践提示词工程和上下文工程，提供结构化的教程、动态生成的练习题和提示词质量评估。

**使用场景**：
- 想要系统学习提示词工程的基础概念
- 需要分析和改进现有的提示词
- 希望通过练习题提升提示词编写能力
- 评估提示词质量并获取优化建议

## 目录结构

```
ai-agent-runtime/
├── README.md              # 项目说明（本文件）
├── CLAUDE.md              # Claude Code 指导文件
├── LICENSE                # Apache 2.0 开源协议
├── commands/              # 命令定义
│   └── openexp.md         # 经验管理命令
├── agents/                # 智能体定义
│   ├── api-designer.md    # API 设计
│   ├── backend-developer.md
│   ├── frontend-developer.md
│   ├── fullstack-developer.md
│   ├── spec-writer.md     # 规格编写（TDD Red 阶段）
│   ├── tester.md          # 测试实现（TDD Red 阶段）
│   ├── ui-designer.md
│   ├── code-explainer.md
│   └── librarian.md       # 文档管理
├── skills/                # 技能定义
│   ├── fullstack/         # TDD 驱动的全栈开发工作流
│   ├── openexp/           # 经验管理技能（Obsidian 存储）
│   └── prompt-learning/   # 提示词工程学习
├── scaffolding/           # 工程搭建模块（规划中）
└── harness/               # 工程运行治理模块（规划中）
```

**注意**：`scaffolding/` 和 `harness/` 目录目前处于规划阶段，核心功能在 `skills/` 和 `agents/` 中实现。

## 工程生命周期管理

Scaffolding 和 Harness 共同构成了完整的 AI 工程生命周期管理体系：

### Scaffolding（工程搭建准备）
- **职责**：项目启动前的准备工作
- **内容**：项目初始化、模板管理、环境检查、配置生成、依赖安装
- **时机**：一次性初始化，项目启动时执行
- **输出**：完整的项目结构、配置文件、开发环境

### Harness（工程运行治理）
- **职责**：模型工作时的支持和治理
- **内容**：工具分发、上下文压缩、跨伦状态管理、安全规则执行、经验记忆写入、长会话稳定性保障
- **时机**：持续运行，项目开发过程中执行
- **输出**：稳定的运行环境、智能的工具调度、完整的经验积累

### 工作流程

```
项目启动
    ↓
[Scaffolding] 工程搭建准备
    - 初始化项目结构
    - 配置开发环境
    - 安装依赖工具
    ↓
项目开发
    ↓
[Harness] 工程运行治理
    - 分发和管理工具
    - 优化上下文
    - 执行安全规则
    - 记录经验
    ↓
项目交付
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
- 安装 Obsidian CLI（从 Obsidian 设置中安装）

### Q: fullstack 技能适合什么场景？

**A**: 适合复杂任务：
- API 设计（5+ 端点）
- 复杂架构设计
- 多组件集成
- 复杂 Bug 修复（> 50 行或多文件修改）

**不适合**：简单代码审查、简单 Bug 修复（< 50 行）、小型功能开发（< 200 行）

**TDD 工作流**：复杂任务需遵循 Red → Green → Refactor 循环，测试先行。

### Q: 如何维护经验库？

**A**: 定期运行维护脚本：
```bash
# 动态查找脚本路径
OPENEXP_SCRIPTS=$(find . -path "*/skills/openexp/scripts/obsidian-cli.sh" -type f 2>/dev/null | head -1 | xargs dirname 2>/dev/null)

# 运行维护脚本
python3 $OPENEXP_SCRIPTS/maintain-experience-vault.py
```
建议每周运行一次，自动更新影响力和索引地图。

## 相关资源

- [CLAUDE.md](CLAUDE.md) - Claude Code 指导文件
- [iFlow CLI 文档](https://iflow.cli/)
- [Obsidian 文档](https://help.obsidian.md/)
- [Prompt Engineering 指南](https://www.promptingguide.ai/)

## 项目信息

- **兼容性**：iFlow CLI
- **开源协议**：Apache License 2.0
- **主要维护者**：niuma
- **Git 仓库**：git@github.com:lihaizhong/ai-agent-runtime.git

## 许可证

本项目采用 Apache License 2.0 开源协议。详见 [LICENSE](LICENSE) 文件。
# AGENTS.md - AI Agent Runtime Development Guide

This file provides guidelines and conventions for agents operating in the ai-agent-runtime repository.

---

## Project Overview

AI Agent Runtime is a comprehensive AI engineering runtime environment for iFlow CLI. It provides:
- **Agents**: Specialized AI agents (backend-developer, frontend-developer, etc.)
- **Skills**: Coordinated workflows (fullstack TDD, prompt-learning, openexp)
- **Commands**: CLI command definitions
- **Harness/Scaffolding**: Runtime governance and project setup (planned)

**Compatibility**: iFlow CLI
**License**: Apache 2.0

---

## Build/Lint/Test Commands

This project uses markdown-based specifications rather than compiled code. Testing is performed through evals.

### Evaluation Testing

```bash
# Run skill evaluations (located in skills/*/evals/evals.json)
# The evals use assertion-based testing with types:
# - contains: exact string match
# - contains_any: matches any of the provided values

# Example eval structure:
{
  "id": 1,
  "name": "Test name",
  "prompt": "User input",
  "expected_output": "Expected response",
  "assertions": [
    {"type": "contains", "value": "exact text"},
    {"type": "contains_any", "value": ["option1", "option2"]}
  ]
}
```

### Manual Testing

1. **Agent testing**: Load agent definition and verify YAML frontmatter
2. **Skill testing**: Verify SKILL.md structure and metadata
3. **Command testing**: Verify command metadata format

---

## Code Style Guidelines

### File Naming

- **Use kebab-case** for all file and directory names
- Agents: `backend-developer.md`, `frontend-developer.md`
- Skills: `fullstack/`, `prompt-learning/`, `openexp/`
- Commands: `openexp.md`

### Directory Structure

```
ai-agent-runtime/
├── agents/              # Agent definitions (markdown)
│   ├── backend-developer.md
│   └── frontend-developer.md
├── skills/             # Skill definitions
│   ├── fullstack/SKILL.md
│   └── prompt-learning/SKILL.md
├── commands/           # Command definitions
│   └── openexp.md
├── harness/            # Runtime governance (planned)
└── scaffolding/       # Project setup (planned)
```

### YAML Frontmatter Conventions

#### Agent Frontmatter

```yaml
---
name: agent-name              # kebab-case
description: "Use this agent when..."  # quoted string
tools: Read, Write, Edit, Bash, Glob, Grep  # comma-separated
model: MiniMax-M2.5
---
```

#### Skill Frontmatter

```yaml
---
name: skill-name              # kebab-case
description: |
  Multi-line description with | # Use | for multiline
license: MIT                   # or Apache 2.0
compatibility: iFlow CLI
metadata:
  author: author-name
  version: "1.0"               # quoted string
  tags:                        # lowercase, hyphenated
    - tag1
    - tag2
  performance:                 # optional
    avg_time_complex: "540s"
---
```

#### Command Frontmatter

```yaml
---
name: /command-name            # leading slash
id: command-id                  # lowercase
category: CategoryName         # PascalCase
description: Command description
---
```

### Markdown Formatting

1. **Headers**: Use ATX-style headers (`#`, `##`, `###`)
2. **Lists**: Use `-` for unordered lists, `1.` for ordered
3. **Tables**: Use pipe syntax with header row separator
4. **Code blocks**: Specify language for syntax highlighting
5. **Links**: Use relative paths for internal links

### Version Management

1. **Semantic versioning**: `major.minor.patch` (e.g., `3.0.0`)
2. **Version history**: Add at the bottom of SKILL.md files
3. **Last updated**: Include in metadata

```markdown
## Version History

| Version | Date | Changes |
|---------|------|---------|
| 3.0 | 2026-03-19 | Added TDD workflow |
```

---

## Error Handling

### Input Validation

- Validate YAML frontmatter on load
- Check required fields: `name`, `description`, `tools` (for agents)
- Ensure `version` is quoted string

### Graceful Degradation

- Missing optional fields should not cause failures
- Invalid formats should log warnings, not errors
- Provide helpful error messages with suggestions

---

## Tool Usage

### Available Tools

Agents have access to these tools:
- **Read**: Read files
- **Write**: Write new files
- **Edit**: Modify existing files
- **Bash**: Execute shell commands
- **Glob**: Pattern-based file search
- **Grep**: Content search
- **WebFetch**: Fetch web content
- **WebSearch**: Search the web
- **CodeSearch**: Search code examples

### Best Practices

1. **Read before edit**: Always read a file before modifying it
2. **Backup**: Don't modify files without reading them first
3. **Atomic writes**: Write complete files, not partial content
4. **Glob first**: Use glob to find files before grep

---

## Communication Patterns

### Agent Communication Protocol

```json
{
  "requesting_agent": "agent-name",
  "request_type": "action_type",
  "payload": {
    "query": "description of needs"
  }
}
```

### Status Updates

```json
{
  "agent": "agent-name",
  "status": "status_value",
  "phase": "current_phase",
  "completed": ["item1", "item2"],
  "pending": ["item3"]
}
```

---

## Content Guidelines

### Descriptions

- Be specific about when to use an agent/skill/command
- Include both "use when" and "don't use when" guidance
- Example: "**适合**: Complex APIs (5+ endpoints)... **不适合**: Simple bugs (< 50 lines)"

### TDD Workflow

For complex tasks, follow the TDD cycle:
1. **Red**: Write failing tests first (spec-writer → tester)
2. **Green**: Implement minimum code to pass (developer)
3. **Refactor**: Optimize while keeping tests green

### OpenSpec Structure

```
openspec/changes/<change-name>/
├── proposal.md      # What and why
├── specs/           # Requirements (spec.md, test.md)
├── design.md        # How to implement
└── tasks.md         # Task checklist
```

---

## Spell Checking

VSCode settings include custom words in `.vscode/settings.json`. Add new technical terms to `cSpell.words` when used frequently.

Current custom words: backlink, frontmatter, HATEOAS, mcps, openspec, WCAG, websearch, etc.

---

## Version History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-03-21 | opencode | Initial AGENTS.md creation |

---

## References

- [README.md](README.md) - Project overview
- [skills/fullstack/SKILL.md](skills/fullstack/SKILL.md) - TDD workflow
- [skills/prompt-learning/SKILL.md](skills/prompt-learning/SKILL.md) - Learning system
- [commands/openexp.md](commands/openexp.md) - Experience management

# Session Config Reference

Reference repository demonstrating every Claude Code configuration surface.
Click **"Use this template"** to create your own config repo.

## What's Inside

```
session-config-reference/
├── README.md                          # This file
├── CLAUDE.md                          # Project-level session instructions
├── .claude/
│   ├── settings.json                  # Permissions and hooks
│   ├── rules/
│   │   └── security.md                # Global rule (no path filter)
│   ├── skills/
│   │   └── review/SKILL.md            # /review skill — code review
│   └── agents/
│       └── code-reviewer.md           # Read-only reviewer subagent
└── .mcp.json                          # MCP server (memory, zero-config)
```

## Configuration Surfaces

### CLAUDE.md — Session Instructions

`CLAUDE.md` is loaded into every Claude Code session. Use it to describe
project conventions, common commands, and any context Claude should know.

**Location**: project root or `.claude/CLAUDE.md`

### .claude/settings.json — Permissions and Hooks

Controls what Claude can and cannot do:

- **allow**: Tools and commands permitted without asking
- **deny**: Tools and commands that are always blocked
- **hooks**: Shell commands that run on lifecycle events (e.g., after a file
  is edited)

This example allows read-only tools and linters, denies force-push and
destructive commands, and includes a PostToolUse hook that fires after file
modifications.

### .claude/rules/ — Rules

Markdown files in `.claude/rules/` are loaded as additional instructions.
Rules can optionally include a `paths` frontmatter field with glob patterns
to scope them to specific files.

This example has a single global rule (`security.md`) with no path filter,
so it applies to all files.

### .claude/skills/ — Skills

Skills are invokable via `/skill-name` in the Claude Code CLI. Each skill
lives in its own directory with a `SKILL.md` file containing YAML frontmatter
and markdown instructions.

This example defines `/review`, which runs `git diff`, reads changed files,
and reports bugs, security issues, and style violations grouped by severity.

### .claude/agents/ — Subagents

Agents are specialized Claude instances with scoped tools and a custom system
prompt. Claude delegates to them automatically based on the `description`
field, or you can invoke them via the Task tool.

This example defines `code-reviewer`, a read-only agent that can only use
`Read`, `Glob`, and `Grep` — it cannot modify files.

### .mcp.json — MCP Servers

Declares Model Context Protocol servers that provide additional tools and
resources. The `.mcp.json` file at the project root is checked into version
control so all collaborators share the same server configuration.

This example configures the `memory` server
(`@modelcontextprotocol/server-memory`), which provides a persistent knowledge
graph — no API keys or infrastructure required.

## How to Use This Template

1. Click **"Use this template"** > **"Create a new repository"**
2. Edit the files to match your project's needs:
   - Update `CLAUDE.md` with your project context and commands
   - Adjust `settings.json` permissions for your workflow
   - Add rules for your coding standards
   - Create skills for your common tasks
   - Define agents for specialized workflows
3. Commit and push — Claude Code will pick up the config automatically

## Adding Your Own

### Adding a New Skill

```bash
mkdir -p .claude/skills/my-skill
```

Create `.claude/skills/my-skill/SKILL.md`:

```yaml
---
name: my-skill
description: Brief description of what this skill does
---

# My Skill

Instructions for Claude when this skill is invoked.
```

### Adding a New Rule

Create `.claude/rules/my-rule.md`:

```yaml
---
paths:
  - "**/*.ext"
---

# My Rule

Standards that apply to `.ext` files.
```

### Adding a New Agent

Create `.claude/agents/my-agent.md`:

```yaml
---
name: my-agent
description: What this agent does
tools: Read, Glob, Grep
model: sonnet
---

You are a specialized agent for [task].
```

## Overlay Behavior

When used as an ACP session-config repo, contents are overlaid into the
workspace:

- Files are **added** to `.claude/` — they do not replace the entire directory
- If a workspace repo also has `.claude/` files, the config repo files are
  copied first, then the workspace repo's files take precedence
- `CLAUDE.md` at the root level is placed in the workspace root
- `.mcp.json` is placed in the workspace root

## Further Reading

- [Claude Code Settings](https://docs.anthropic.com/en/docs/claude-code/settings)
- [Memory and CLAUDE.md](https://docs.anthropic.com/en/docs/claude-code/memory)
- [Skills](https://docs.anthropic.com/en/docs/claude-code/skills)
- [Sub-agents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- [Hooks](https://docs.anthropic.com/en/docs/claude-code/hooks)
- [MCP Servers](https://docs.anthropic.com/en/docs/claude-code/mcp)

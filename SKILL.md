---
name: code
description: Wield Every Code (just-every/code, a fork of codex-cli) as a powerful auxiliary tool for multi-agent code generation, consensus planning, browser automation, and parallel AI orchestration. Use when tasks benefit from multiple AI perspectives (Claude+Gemini+GPT), browser testing, or automated coding workflows.
allowed-tools:
  - Bash
  - Read
  - Grep
  - Glob
---

<!-- Last verified: 2025-12-24 | CLI version: 0.6.14 -->
<!-- Model names in examples may need updating as new versions release -->

# Every Code CLI Integration Skill

This skill enables Claude Code to effectively orchestrate Every Code CLI (`code`) - the `just-every/code` package, a fork of OpenAI's Codex CLI with multi-agent consensus, browser integration, and enhanced automation features.

## Agent Handoff

Spawn the dedicated agent for CLI execution:

```
Task(subagent_type: "code", prompt: "[task]")
```

This keeps CLI output isolated and returns concise summaries.

## When to Use This Skill

### Ideal Use Cases

1. **Multi-Agent Consensus**
   - `/plan` - Get Claude, Gemini, and GPT to collaboratively plan code changes
   - `/solve` - Race multiple AIs to solve complex problems (fastest wins)
   - `/code` - Generate code with multi-agent consensus

2. **Second AI Perspective**
   - Code review from a different AI's viewpoint
   - Bug detection Claude might have missed
   - Alternative implementation approaches

3. **Browser Integration**
   - `/chrome` - Connect to external Chrome via CDP
   - `/browser` - Use internal headless browser
   - Visual testing and screenshot comparisons

4. **Auto-Drive Mode**
   - `/auto` - Hands-off multi-step task coordination
   - Background task execution
   - Automated workflows

5. **Parallel Processing**
   - Offload tasks while continuing other work
   - Run multiple code generations simultaneously

### When NOT to Use

- Simple, quick tasks (overhead not worth it)
- Tasks requiring immediate response
- When context is already loaded and understood
- Interactive refinement requiring conversation

## Core Instructions

### 1. Verify Installation

```bash
command -v code || which code
```

### 2. Basic Command Patterns

```bash
# Interactive mode with prompt
code "explain this codebase"

# Full-auto mode (no approval prompts)
code --full-auto "create a todo app"

# Non-interactive execution
code exec "fix all TypeScript errors"

# Pipe prompt via stdin
echo "analyze security" | code exec
```

### 3. Key CLI Flags

| Flag               | Description                                          |
| ------------------ | ---------------------------------------------------- |
| `--full-auto`      | Automatic execution, no approval prompts             |
| `--sandbox <mode>` | `read-only`, `workspace-write`, `danger-full-access` |
| `--model <name>`   | Override default model (e.g., `gpt-5.2-codex`)       |
| `--config key=val` | Override config values                               |
| `--read-only`      | Prevent file modifications                           |
| `-C, --cd <DIR>`   | Change working directory                             |

### 4. Sandbox Modes

| Mode                 | Use Case                             |
| -------------------- | ------------------------------------ |
| `read-only`          | Analysis, review, research (default) |
| `workspace-write`    | Apply local edits                    |
| `danger-full-access` | Network access, broad permissions    |

### 5. Multi-Agent Commands

These slash commands only work **inside an interactive `code` session**:

```bash
# First start an interactive session:
code

# Then use these commands within the session:
/plan "implement user authentication with OAuth"  # Consensus planning
/solve "why does deleting one user drop the database?"  # Racing solve
/code "add rate limiting to the API"  # Multi-agent code generation
/auto "refactor the authentication module and add tests"  # Auto-drive
```

### 6. Browser Integration (Interactive Session)

These commands work inside an interactive `code` session:

```bash
/chrome    # Connect to external Chrome via CDP
/browser   # Use internal headless browser
Ctrl+B     # ASCII preview in terminal
```

### 7. Session Management

```bash
# Resume last session
echo "continue with the refactor" | code exec resume --last

# Resume with additional context
echo "now add tests" | code exec resume --last
```

## Quick Reference Commands

### Analysis (Read-Only)

```bash
code --sandbox read-only "review this codebase for security issues"
```

### Code Generation

```bash
code --full-auto --sandbox workspace-write "create user authentication module"
```

### Multi-Agent Planning (Interactive Session)

```bash
# Inside a `code` session:
/plan "design a microservices architecture for this monolith"
```

### Problem Solving (Interactive Session)

```bash
# Inside a `code` session:
/solve "identify the root cause of the memory leak"
```

### Browser Testing (Interactive Session)

```bash
# Inside a `code` session:
/browser
# Then: "take a screenshot of the login page and check for accessibility issues"
```

## Configuration

### Config File Location

`~/.code/config.toml`

### Example Configuration

```toml
model = "gpt-5.2-codex"
approval_policy = "on-request"
sandbox_mode = "workspace-write"

[profiles.full_auto]
approval_policy = "on-request"
sandbox_mode = "workspace-write"

[profiles.readonly]
approval_policy = "never"
sandbox_mode = "read-only"
```

### Subagent Configuration

```toml
[[subagents.commands]]
name = "plan"
read_only = true
agents = ["claude-opus-4.5", "gemini", "gpt-5.2-codex"]

[[subagents.commands]]
name = "solve"
read_only = true
agents = ["claude-opus-4.5", "gemini", "gpt-5.2-codex"]
```

## Error Handling

### Command Failures

- Stop and report failures when `code` exits non-zero
- Request direction before retrying

### High-Impact Operations

Before using these flags, ask user for permission:

- `--full-auto`
- `--sandbox danger-full-access`

### Rate Limits

- CLI auto-retries with backoff
- Use appropriate models for task complexity

## Integration Workflow

### Standard Generate-Review Cycle

```bash
# 1. Generate with multi-agent consensus (in interactive session)
code  # Start session
/code "create REST API for user management"

# 2. Review the generated code (new session or standalone)
code --sandbox read-only "review the generated code for bugs and security"

# 3. Fix identified issues
code --full-auto --sandbox workspace-write "fix the issues identified"
```

### Cross-Validation with Claude

```bash
# 1. Claude generates code (using normal Claude Code tools)
# 2. Every Code reviews
code --sandbox read-only "review this code for issues: [paste code]"
```

## Unique Capabilities

These features are available only through Every Code:

1. **Multi-Agent Consensus** - Orchestrate Claude, Gemini, GPT together
2. **Auto-Drive Mode** - Automated multi-step workflows
3. **Browser Integration** - Chrome DevTools via CDP
4. **Auto-Review** - Background ghost-commit watcher
5. **Theme System** - Visual customization

## See Also

- `reference.md` - Complete command and flag reference
- `templates.md` - Prompt templates for common operations
- `patterns.md` - Advanced integration patterns
- `tools.md` - Built-in tools and subagent commands

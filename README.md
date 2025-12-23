# Every Code CLI Skill for Claude Code

A Claude Code skill that enables effective use of Every Code CLI (`just-every/code`) as a powerful multi-agent orchestration tool.

## What This Skill Does

This skill teaches Claude Code how to wield Every Code CLI for:

- **Multi-Agent Consensus** - Orchestrate Claude, Gemini, and GPT together
- **Code Generation** - Create apps, components, and modules with AI collaboration
- **Problem Solving** - Race multiple AIs to find solutions fastest
- **Browser Integration** - Chrome DevTools automation via CDP
- **Auto-Drive Mode** - Hands-off multi-step task coordination
- **Code Review** - Get alternative AI perspectives on code

## Prerequisites

- Every Code CLI installed and available as `code` on PATH
- Configured with valid credentials (OpenAI API key or ChatGPT login)
- For multi-agent features: Claude CLI and Gemini CLI configured

```bash
# Verify installation
code --version
```

## Files

| File           | Purpose                                                |
| -------------- | ------------------------------------------------------ |
| `SKILL.md`     | Main skill definition - when to use, core instructions |
| `reference.md` | Complete CLI command and flag reference                |
| `templates.md` | Reusable prompt templates for common tasks             |
| `patterns.md`  | Integration patterns and workflows                     |
| `tools.md`     | Built-in tools and subagent commands                   |

## Usage

Once installed, Claude Code automatically uses this skill when appropriate. Just ask:

```
"Use Every Code to plan this feature with multiple AIs"
"Have code review this module from a different perspective"
"Use /solve to figure out why this test is failing"
"Run /auto to refactor and add tests"
```

## Key Features

### Multi-Agent Commands

- `/plan` - Consensus planning (Claude + Gemini + GPT collaborate)
- `/solve` - Racing problem solving (fastest AI wins)
- `/code` - Multi-agent code generation
- `/auto` - Auto-drive for multi-step tasks

### Browser Integration

- `/chrome` - Connect to external Chrome via CDP
- `/browser` - Use internal headless browser
- `Ctrl+B` - ASCII preview in terminal

### Sandbox Modes

| Mode                 | Use Case                          |
| -------------------- | --------------------------------- |
| `read-only`          | Analysis, review, research        |
| `workspace-write`    | Apply local edits                 |
| `danger-full-access` | Network access, broad permissions |

## Quick Reference

```bash
# Multi-agent planning
/plan "implement OAuth authentication"

# Racing problem solver
/solve "why does the memory usage spike?"

# Code generation with consensus
/code "add rate limiting to API"

# Read-only analysis
code --sandbox read-only "review security"

# Full-auto code generation
code --full-auto --sandbox workspace-write "create user module"

# Browser testing
/browser
```

## Configuration

Config file: `~/.code/config.toml`

```toml
model = "gpt-5.2-codex"
approval_policy = "on-request"
sandbox_mode = "workspace-write"

[[subagents.commands]]
name = "plan"
agents = ["claude-opus-4.5", "gemini", "gpt-5.2-codex"]
```

## Why Use Every Code from Claude Code?

| Use Case              | Benefit                           |
| --------------------- | --------------------------------- |
| Multi-agent consensus | Claude + Gemini + GPT collaborate |
| Second opinion        | Different AI perspective on code  |
| Browser testing       | Chrome DevTools integration       |
| Auto-drive            | Hands-off multi-step workflows    |
| Parallel work         | Offload tasks while continuing    |

## Links

- [just-every/code GitHub](https://github.com/just-every/code)
- [Context7 Documentation](https://context7.com/just-every/code)

## License

MIT

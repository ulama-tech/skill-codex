# Every Code CLI Command Reference

Complete reference for Every Code CLI (just-every/code).

## Command Line Flags

### Essential Flags

| Flag          | Short | Description                                                        |
| ------------- | ----- | ------------------------------------------------------------------ |
| `--full-auto` |       | Auto-approve all tool calls, no prompts                            |
| `--sandbox`   |       | Sandbox mode: `read-only`, `workspace-write`, `danger-full-access` |
| `--model`     | `-m`  | Model selection (e.g., `gpt-5.2-codex`)                            |
| `--read-only` |       | Prevent file modifications                                         |
| `--config`    | `-c`  | Override config values: `key=value`                                |

### Execution Options

| Flag                 | Short | Description                                       |
| -------------------- | ----- | ------------------------------------------------- |
| `-C, --cd`           |       | Change working directory                          |
| `--ask-for-approval` |       | Approval mode: `on-request`, `never`, `untrusted` |
| `--timeout`          |       | Request timeout in ms                             |

### Reasoning Control

| Flag                 | Description             |
| -------------------- | ----------------------- |
| `--reasoning high`   | High reasoning effort   |
| `--reasoning medium` | Medium reasoning effort |
| `--reasoning low`    | Low reasoning effort    |

### Other Options

| Flag        | Short | Description         |
| ----------- | ----- | ------------------- |
| `--debug`   | `-d`  | Enable debug output |
| `--version` | `-v`  | Show version        |
| `--help`    | `-h`  | Show help           |

## Commands

### Interactive Mode

```bash
# Start with prompt
code "explain this codebase"

# Start with full-auto
code --full-auto "create a todo app"
```

### Non-Interactive Execution

```bash
# Execute prompt directly
code exec "fix all TypeScript errors"

# Pipe prompt via stdin
echo "analyze security" | code exec
```

### Session Management

```bash
# Resume last session
code exec resume --last

# Resume with new prompt
echo "continue refactoring" | code exec resume --last
```

### Subagent Commands (Multi-Agent)

```bash
# Consensus planning
/plan "implement user auth"

# Racing problem solver
/solve "why is this failing?"

# Multi-agent code generation
/code "add feature X"

# Auto-drive mode
/auto "refactor and test"
```

### Browser Commands

```bash
# Connect external Chrome
/chrome

# Internal headless browser
/browser

# Themes
/themes
```

### Sandbox Testing

```bash
# Test macOS sandbox
code sandbox macos [--full-auto] [COMMAND]...

# Test Linux sandbox
code sandbox linux [--full-auto] [COMMAND]...
```

## Configuration

### Config File Location

Primary: `~/.code/config.toml`
Legacy (read-only): `~/.codex/config.toml`

### Basic Configuration

```toml
# Model settings
model = "gpt-5.2-codex"
model_reasoning_effort = "medium"
model_verbosity = "low"

# Approval and sandbox
approval_policy = "on-request"
sandbox_mode = "workspace-write"
```

### Approval Policies

```toml
# Prompt for non-trusted commands
approval_policy = "untrusted"

# Retry outside sandbox on failure
approval_policy = "on-failure"

# Model decides when to escalate
approval_policy = "on-request"

# Never prompt (full auto)
approval_policy = "never"
```

### Sandbox Configuration

```toml
# Read-only mode
sandbox_mode = "read-only"

# Write to workspace
sandbox_mode = "workspace-write"

# Full access (dangerous)
sandbox_mode = "danger-full-access"

# Workspace-write with network
[sandbox_workspace_write]
network_access = true
allow_git_writes = false
```

### Profiles

```toml
[profiles.full_auto]
approval_policy = "on-request"
sandbox_mode = "workspace-write"

[profiles.readonly]
approval_policy = "never"
sandbox_mode = "read-only"

[profiles.dangerous]
approval_policy = "never"
sandbox_mode = "danger-full-access"
```

### Subagent Configuration

```toml
[[subagents.commands]]
name = "plan"
read_only = true
agents = ["claude-opus-4.5", "gemini", "gpt-5.2-codex"]
orchestrator_instructions = "Guidance for coordinator"
agent_instructions = "Preamble for each agent"

[[subagents.commands]]
name = "solve"
read_only = true
agents = ["claude-opus-4.5", "gemini", "gpt-5.2-codex"]

[[subagents.commands]]
name = "code"
read_only = false
agents = ["claude-opus-4.5", "gemini", "gpt-5.2-codex"]
```

### Agent Configuration

```toml
[[agents]]
name = "claude"
command = "claude"
enabled = true
read_only = false

[[agents]]
name = "gemini"
command = "gemini"
enabled = true
read_only = false

[[agents]]
name = "custom-llm"
command = "/usr/local/bin/custom-llm"
enabled = true
description = "Custom LLM implementation"
args = ["--config", "/path/to/config.json"]
env = { MODEL_PATH = "/models/custom.bin", TEMP = "0.7" }
```

### Reasoning Settings

```toml
# Enable reasoning summaries
model_supports_reasoning_summaries = true

# Disable reasoning summaries
model_reasoning_summary = "none"

# Hide reasoning in output
hide_agent_reasoning = true

# Show raw chain-of-thought
show_raw_agent_reasoning = true
```

## Environment Variables

| Variable         | Description                                    |
| ---------------- | ---------------------------------------------- |
| `CODE_HOME`      | Override config directory (default: `~/.code`) |
| `OPENAI_API_KEY` | API key for OpenAI                             |
| `CODEX_API_KEY`  | Override API key for `code exec`               |
| `RUST_LOG`       | Logging level configuration                    |

## Model Selection

### Default Model

The default model is `gpt-5.2-codex`.

### Usage

```bash
# Override model
code --model gpt-5.2 "analyze code"

# In config
model = "gpt-5.2-codex"
```

## Keyboard Shortcuts (Interactive)

| Shortcut | Function               |
| -------- | ---------------------- |
| `Ctrl+B` | Toggle browser preview |
| `Ctrl+D` | Open diff viewer       |
| `Ctrl+L` | Clear screen           |

## Troubleshooting

### Common Issues

| Issue                | Solution                            |
| -------------------- | ----------------------------------- |
| "Agent not found"    | Verify agent command path in config |
| Rate limit errors    | CLI auto-retries with backoff       |
| Sandbox restrictions | Use `--sandbox workspace-write`     |

### Debug Mode

```bash
code --debug "prompt"
```

### Log Location

```bash
# Monitor logs
tail -F ~/.code/log/codex-tui.log
```

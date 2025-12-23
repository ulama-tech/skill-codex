# Every Code Built-in Tools and Commands

Reference for Every Code's built-in tools, subagent commands, and unique capabilities.

## Subagent Commands

These commands orchestrate multiple AI agents for collaborative work.

### /plan

Consensus planning with all configured agents.

**Behavior:**

- All agents (Claude, Gemini, GPT) review the task
- Each proposes a plan
- Plans are consolidated into a unified approach

**Usage:**

```bash
/plan "Implement user authentication with OAuth"
```

**Best For:**

- Feature design
- Architecture decisions
- Complex implementation planning

---

### /solve

Racing problem solver - fastest agent wins.

**Behavior:**

- All agents race to solve the problem
- First valid solution is accepted
- Optimized for speed

**Usage:**

```bash
/solve "Why does the memory leak after 1000 requests?"
```

**Best For:**

- Debugging issues
- Root cause analysis
- Quick answers to complex questions

---

### /code

Multi-agent code generation.

**Behavior:**

- Agents collaborate on code generation
- Code is reviewed for consensus
- Best solution is applied

**Usage:**

```bash
/code "Create a rate-limiting middleware"
```

**Best For:**

- Feature implementation
- Code creation
- Adding new functionality

---

### /auto

Auto-drive mode for multi-step tasks.

**Behavior:**

- Executes multi-step workflows autonomously
- Maintains context across steps
- Self-corrects on failures

**Usage:**

```bash
/auto "Refactor module, add tests, update docs"
```

**Best For:**

- Complex refactoring
- Multi-file changes
- End-to-end implementations

---

## Browser Integration

### /browser

Launch internal headless browser.

**Capabilities:**

- Navigate to URLs
- Take screenshots
- Interact with elements
- Run accessibility checks

**Usage:**

```bash
/browser
# Then interactive browser commands
```

---

### /chrome

Connect to external Chrome via CDP.

**Requirements:**

- Chrome running with remote debugging enabled
- `--remote-debugging-port=9222`

**Usage:**

```bash
/chrome
```

---

### Ctrl+B

Toggle ASCII browser preview in terminal.

**Usage:**
Press `Ctrl+B` during interactive session.

---

## Interactive Commands

### /themes

Switch visual themes.

**Usage:**

```bash
/themes
```

---

### /model

Change AI model.

**Usage:**

```bash
/model gpt-5.2-codex
```

---

### /reasoning

Adjust thinking depth.

**Usage:**

```bash
/reasoning high
/reasoning medium
/reasoning low
```

---

### /settings

Open TUI settings overlay.

**Sections:**

- Model selection
- Theme customization
- Agent configuration
- Prompt management

---

## Built-in File Operations

### read_file

Read file content with pagination.

**Capabilities:**

- Text files
- Images (PNG, JPG, GIF, WEBP)
- PDF documents

---

### write_file

Write content to files.

**Requires:** `--sandbox workspace-write` or higher.

---

### apply_patch

Apply unified diff patches.

**Usage:**
Patches are applied via shell command with patch content as argument.

---

### list_directory

List files and subdirectories.

**Parameters:**

- `path`: Directory to list
- `ignore`: Glob patterns to exclude

---

### search_file_content

Fast content search (ripgrep-powered).

**Features:**

- Regex patterns
- Automatic output limiting
- Fast performance

---

### glob

Pattern-based file finding.

**Returns:**

- Absolute paths
- Sorted by modification time

---

## Session Management

### resume

Resume previous session.

**Usage:**

```bash
code exec resume --last
echo "continue" | code exec resume --last
```

**Behavior:**

- Preserves full context from previous session
- Uses same model, sandbox, and settings
- Allows continuation of multi-step work

---

## Comparison with Claude Code

| Capability      | Claude Code       | Every Code                         |
| --------------- | ----------------- | ---------------------------------- |
| File operations | Read, Write, Edit | read_file, write_file, apply_patch |
| Search          | Grep, Glob        | search_file_content, glob          |
| Multi-agent     | Task (subagents)  | **/plan, /solve, /code**           |
| Browser         | No                | **/browser, /chrome**              |
| Auto-drive      | No                | **/auto**                          |
| Consensus       | No                | **Multi-AI collaboration**         |
| Session resume  | No                | **resume --last**                  |

**Bold** = Every Code's unique advantage

---

## Unique Every Code Features

### 1. Multi-Agent Consensus

Orchestrate Claude, Gemini, and GPT together for better results.

```toml
[[subagents.commands]]
name = "plan"
agents = ["claude-opus-4.5", "gemini", "code-gpt-5.2-codex"]
```

### 2. Auto-Review

Background ghost-commit watcher reviews code changes automatically.

### 3. Browser Integration

Full Chrome DevTools control via CDP protocol.

### 4. Theme System

Visual customization with multiple built-in themes.

### 5. Reasoning Control

Adjust model thinking depth per-request.

### 6. Session Persistence

Resume any previous session with full context.

---

## Tool Configuration

### Enabling Agents

```toml
[[agents]]
name = "claude"
command = "claude"
enabled = true

[[agents]]
name = "gemini"
command = "gemini"
enabled = true
```

### Subagent Instructions

```toml
[[subagents.commands]]
name = "plan"
orchestrator_instructions = "Coordinate agents for planning"
agent_instructions = "Focus on practical, implementable solutions"
```

### Tool Restrictions

In interactive mode, tools can be restricted via settings or execution policy.

---

## Best Practices

### When to Use Multi-Agent

- Complex features requiring design
- Debugging difficult issues
- Code review and quality assurance

### When to Use Single Agent

- Simple tasks with clear requirements
- Quick edits and fixes
- Speed-critical operations

### When to Use Browser

- Visual testing
- E2E flow verification
- Screenshot comparisons
- Accessibility audits

### When to Use Auto-Drive

- Multi-step refactoring
- Feature implementation
- Documentation updates
- Test generation

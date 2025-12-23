# Every Code CLI Integration Patterns

Advanced patterns for orchestrating Every Code CLI effectively from Claude Code.

## Pattern 1: Multi-Agent Consensus Workflow

The most powerful pattern - leverage multiple AIs for quality results.

### Planning Phase

```bash
# Get all agents to collaborate on a plan
/plan "Implement feature X with requirements Y and Z"
```

### Implementation Phase

```bash
# Generate code with consensus
/code "Implement the plan from the previous step"
```

### Review Phase

```bash
# Have agents review the implementation
/solve "Review the implementation for bugs and security issues"
```

### Why It Works

- Different AI perspectives catch different issues
- Consensus reduces individual model biases
- Racing mode finds solutions faster

## Pattern 2: Claude Code + Every Code Collaboration

Use both tools synergistically.

### Claude Generates, Every Code Reviews

```bash
# 1. Claude writes code (using normal Claude Code tools)
# 2. Every Code reviews with multi-agent perspective
/solve "Review this code for bugs, security issues, and improvements"
```

### Every Code Generates, Claude Refines

```bash
# 1. Every Code generates with consensus
/code "Create authentication module"

# 2. Claude reviews and refines
# (Use Claude Code's normal edit capabilities)
```

### Parallel Processing

```bash
# Run Every Code in background for analysis
code --sandbox read-only "Analyze codebase architecture" &

# Continue working with Claude Code on other tasks
```

## Pattern 3: Browser-Driven Development

Use browser integration for visual verification.

### Visual Testing Flow

```bash
# 1. Connect browser
/browser

# 2. Navigate and capture
"Take screenshot of /dashboard after login"

# 3. Analyze results
"Check the screenshot for:
- Layout issues
- Missing elements
- Accessibility problems"
```

### End-to-End Testing

```bash
/browser
"Test the complete user flow:
1. Register new account
2. Verify email (mock)
3. Login
4. Update profile
5. Logout
Report any failures."
```

## Pattern 4: Auto-Drive for Complex Tasks

Hands-off multi-step automation.

### Refactoring Workflow

```bash
/auto "Refactor the payment module:
1. Extract shared types to types.ts
2. Create PaymentService class
3. Move validation to separate file
4. Update all imports
5. Run tests to verify
6. Fix any failing tests"
```

### Feature Implementation

```bash
/auto "Implement rate limiting:
1. Add rate-limit package
2. Create middleware
3. Apply to auth routes
4. Add tests
5. Update API documentation"
```

### Why Auto-Drive Works

- Maintains context across steps
- Automatically handles dependencies
- Self-corrects on failures

## Pattern 5: Generate-Review-Fix Cycle

Quality assurance through iteration.

```bash
# Step 1: Generate
/code "Create REST API for user management"

# Step 2: Review
code --sandbox read-only "Review the generated code for:
- Security vulnerabilities
- Missing error handling
- Performance issues"

# Step 3: Fix
code --full-auto --sandbox workspace-write "Fix all issues identified in the review"

# Step 4: Verify
/solve "Verify all fixes were applied correctly"
```

## Pattern 6: Sandbox Escalation

Start restrictive, escalate when needed.

### Read-Only First

```bash
# Analysis phase - no writes needed
code --sandbox read-only "Analyze this module"
```

### Escalate for Edits

```bash
# Implementation phase - writes required
code --full-auto --sandbox workspace-write "Apply the changes"
```

### Full Access When Required

```bash
# Network access needed (ask user first!)
code --sandbox danger-full-access "Install dependencies and verify"
```

## Pattern 7: Session Continuity

Build on previous context.

### Initial Analysis

```bash
code "Understand this codebase architecture"
# Session saved automatically
```

### Follow-Up Work

```bash
echo "Now implement the improvements you suggested" | code exec resume --last
```

### Iterative Refinement

```bash
echo "Add error handling to the new code" | code exec resume --last
echo "Now add tests" | code exec resume --last
echo "Review and polish" | code exec resume --last
```

## Pattern 8: Model Selection Strategy

Choose the right model for the task.

### Default Model

The default model is `gpt-5.2-codex`. For complex tasks, use multi-agent commands instead of switching models.

### Examples

```bash
# Complex: Use multi-agent
/plan "Design microservices architecture"

# Standard task: Use default model
code "Optimize this algorithm"

# Override model if needed
code --model gpt-5.2-codex "Format this JSON"
```

## Pattern 9: Error Recovery

Handle failures gracefully.

### Automatic Retry

Every Code auto-retries with backoff on rate limits.

### Manual Recovery

```bash
# If a step fails, resume with context
echo "The last step failed with [error]. Fix it and continue." | code exec resume --last
```

### Escalate Permissions

```bash
# If sandbox blocks needed action
code --sandbox workspace-write "Retry the operation with write permissions"
```

## Pattern 10: Background Execution

Run long tasks without blocking.

### Start in Background

```bash
# Run analysis in background
code --sandbox read-only "Deep analysis of all modules" &

# Get process ID
echo $!
```

### Monitor Progress

```bash
# Check output incrementally
tail -f ~/.code/log/codex-tui.log
```

### Parallel Analysis

```bash
# Run multiple analyses simultaneously
/plan "Analyze frontend architecture" &
/plan "Analyze backend architecture" &
/plan "Analyze database schema" &
wait
```

## Anti-Patterns to Avoid

### Don't: Skip the Planning Phase

Multi-agent planning catches issues early.

**Do**: Use `/plan` before complex implementations.

### Don't: Use Full Access by Default

Start with `read-only`, escalate when needed.

**Do**: Request only the permissions you need.

### Don't: Ignore Multi-Agent for Single Tasks

Even simple tasks benefit from different perspectives.

**Do**: Use `/solve` for debugging, `/code` for generation.

### Don't: Forget Session Context

Resuming preserves valuable context.

**Do**: Use `resume --last` for follow-up work.

### Don't: Trust Output Blindly

AI can make mistakes.

**Do**: Review generated code, run tests, verify behavior.

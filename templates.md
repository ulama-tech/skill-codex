# Every Code CLI Prompt Templates

Reusable prompt templates for common operations with Every Code CLI.

## Multi-Agent Commands

### Consensus Planning

```bash
/plan "Design [feature] with the following requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]
Consider edge cases and security implications."
```

**Example:**

```bash
/plan "Design user authentication with OAuth2:
- Support Google and GitHub providers
- Include session management
- Add rate limiting on login attempts
Consider edge cases and security implications."
```

### Racing Problem Solver

```bash
/solve "[Problem description]
Context: [Relevant context]
Expected behavior: [What should happen]
Actual behavior: [What is happening]"
```

**Example:**

```bash
/solve "Database connection pool exhaustion
Context: Express app with PostgreSQL, 50 max connections
Expected behavior: Connections released after request
Actual behavior: Connections accumulate until pool exhausts"
```

### Multi-Agent Code Generation

```bash
/code "Create [component type] that [functionality]:
- [Feature 1]
- [Feature 2]
Follow existing patterns in [file/directory]."
```

**Example:**

```bash
/code "Create a React hook useDebounce that:
- Accepts a value and delay in ms
- Returns debounced value
- Handles cleanup on unmount
Follow existing patterns in src/hooks/."
```

### Auto-Drive Mode

```bash
/auto "[Multi-step task description]
Steps:
1. [Step 1]
2. [Step 2]
3. [Step 3]
Verify each step before proceeding."
```

**Example:**

```bash
/auto "Refactor the authentication module:
1. Extract JWT logic into separate service
2. Add refresh token support
3. Write unit tests for new services
4. Update API documentation
Verify each step before proceeding."
```

## Code Analysis

### Security Review

```bash
code --sandbox read-only "Review [file/directory] for security vulnerabilities:
- XSS and injection attacks
- Authentication bypasses
- Insecure data handling
- Secrets exposure
Report findings with severity levels."
```

### Performance Analysis

```bash
code --sandbox read-only "Analyze [file/directory] for performance issues:
- Inefficient algorithms (O(n²) or worse)
- Memory leaks
- Unnecessary re-renders
- Blocking operations
Provide specific recommendations."
```

### Architecture Review

```bash
code --sandbox read-only "Review the architecture of this codebase:
- Identify design patterns in use
- Map component dependencies
- Find circular dependencies
- Suggest improvements"
```

## Code Generation

### Single Component

```bash
code --full-auto --sandbox workspace-write "Create [component] with:
- [Feature 1]
- [Feature 2]
- TypeScript types
- Unit tests
Output to [path]."
```

### Multi-File Feature

```bash
code --full-auto --sandbox workspace-write "Implement [feature]:
- Create model in src/models/
- Add service in src/services/
- Create API endpoint in src/routes/
- Add tests in tests/
Follow existing patterns."
```

### Test Generation

```bash
code --full-auto --sandbox workspace-write "Generate tests for [file]:
- Unit tests for all exported functions
- Edge cases (null, undefined, empty)
- Error handling scenarios
- Mock external dependencies
Use [Jest/Vitest/pytest] framework."
```

## Bug Fixing

### Fix Identified Issue

```bash
code --full-auto --sandbox workspace-write "Fix this issue in [file]:
Problem: [Description]
Expected: [Expected behavior]
Current: [Current behavior]
Apply the fix."
```

### Auto-Detect and Fix

```bash
code --full-auto --sandbox workspace-write "Analyze [file] for bugs:
- Logic errors
- Null pointer issues
- Type mismatches
- Race conditions
Fix all issues found."
```

## Refactoring

### Extract Function

```bash
code --full-auto --sandbox workspace-write "Refactor [file]:
- Extract [logic] into separate function
- Add proper typing
- Update all call sites
- Maintain existing behavior"
```

### Modernize Code

```bash
code --full-auto --sandbox workspace-write "Modernize [file]:
- Convert callbacks to async/await
- Replace var with const/let
- Use optional chaining
- Add TypeScript types
Maintain all existing functionality."
```

## Documentation

### API Documentation

```bash
code --full-auto --sandbox workspace-write "Document API endpoints in [file]:
- HTTP method and path
- Request parameters and body
- Response schema
- Example requests/responses
Output as JSDoc comments."
```

### README Generation

```bash
code --full-auto --sandbox workspace-write "Generate README.md for this project:
- Project description
- Installation instructions
- Usage examples
- API reference
- Contributing guidelines"
```

## Browser Testing

### Visual Verification

```bash
/browser
# Then:
"Navigate to [URL] and:
- Take screenshot of login page
- Check for accessibility issues
- Verify responsive layout
- Report any visual bugs"
```

### End-to-End Flow

```bash
/browser
# Then:
"Test the user registration flow:
1. Navigate to /register
2. Fill form with test data
3. Submit and verify redirect
4. Check for success message
Report any issues found."
```

## Session Continuation

### Resume with Context

```bash
echo "Continue with the previous task. Now:
- [Additional requirement 1]
- [Additional requirement 2]" | code exec resume --last
```

### Resume for Review

```bash
echo "Review the changes made in the last session.
Check for:
- Code quality issues
- Missing edge cases
- Security concerns" | code exec resume --last
```

## Template Variables

Use these placeholders in templates:

- `[file]` - File path
- `[directory]` - Directory path
- `[component]` - Component name
- `[feature]` - Feature description
- `[URL]` - Web URL for browser testing
- `[framework]` - Testing framework name

# [PROJECT_NAME] -- AI Agent Instructions

This file provides instructions for AI coding agents (Claude Code, Codex CLI, Cursor, etc.).
Tool-specific instructions go in CLAUDE.md or .cursorrules. Universal rules go here.

## Project Overview

[Brief description of what this project does and its key technologies]

## Architecture

[High-level architecture description]

### Directory Structure

```text
src/
  api/          -- [description]
  services/     -- [description]
  models/       -- [description]
  utils/        -- [description]
test/
  unit/         -- [description]
  integration/  -- [description]
```

## Development Commands

```bash
# Install dependencies
[INSTALL_COMMAND]

# Run tests
[TEST_COMMAND]

# Run linter
[LINT_COMMAND]

# Start development server
[DEV_COMMAND]
```

## Code Conventions

- [Key conventions any AI tool should follow]
- [e.g., "All API endpoints validate input before processing"]
- [e.g., "Use structured logging, never console.log in production code"]
- [e.g., "Database queries go in repository classes, not in route handlers"]

## Testing Requirements

- [What must be tested]
- [e.g., "All public API endpoints must have integration tests"]
- [e.g., "Business logic in services/ must have unit tests"]
- [e.g., "Run related tests before committing: `npm test -- --grep 'module name'`"]

## PR Guidelines

- Keep PRs small and focused (one concern per PR)
- Include issue number in PR descriptions
- All tests must pass before requesting review
- Lint must pass with zero violations

## Security Rules

- Never commit secrets, API keys, or credentials
- Validate all user input at system boundaries
- Use parameterized queries for database access
- Never log sensitive data (passwords, tokens, PII)

## Review Workflow

When addressing PR review comments (using `/address-review` or equivalent):

- Wait for the first full review pass to finish before pushing follow-up commits
- Batch review fixes into one follow-up push when practical -- do not create a new commit for each minor comment
- Treat as blocking only: correctness bugs, failing tests, regressions, and clear inconsistencies with adjacent code
- Verify reviewer claims locally before changing code in response to review comments
- Deduplicate repeated bot comments before acting on them -- fix the underlying issue once, then resolve the duplicates

## Shared Commands

The `/address-review` command and other shared commands are synced from
[claude-code-commands-skills-agents](https://github.com/shakacode/claude-code-commands-skills-agents).
Do not edit `.claude/commands/address-review.md` directly in this project.
Update the canonical copy in the boosters repo and re-sync.

## Common Mistakes to Avoid

- [Things that AI agents frequently get wrong in this project]
- [e.g., "Don't import from internal/ -- use the public API in index.ts"]
- [e.g., "The User model has soft-delete -- use .active scope, not .all"]

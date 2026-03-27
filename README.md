# claude-code-commands-skills-agents

ShakaCode Team Shared Claude Code commands plus cross-tool prompts, agents, skills, and tips.

## Quick Install

Copy what you need to your `~/.claude/` directory:

```bash
# Clone the repo
git clone https://github.com/shakacode/claude-code-commands-skills-agents.git
cd claude-code-commands-skills-agents

# Install all commands
mkdir -p ~/.claude/commands
cp commands/*.md ~/.claude/commands/

# Install all agents
mkdir -p ~/.claude/agents
cp agents/*.md ~/.claude/agents/

# Or install specific ones
cp commands/self-review.md ~/.claude/commands/
cp commands/merge-commit-msg.md ~/.claude/commands/
```

For project-level sharing, copy to your project's `.claude/commands/` or `.claude/agents/` directory instead.

## Commands

| Command | Description |
|---------|-------------|
| [`/address-review`](commands/address-review.md) | Fetch GitHub PR review comments, triage them, create todos for must-fix items, reply to comments, and resolve addressed threads |
| [`/review-all-prs`](commands/review-all-prs.md) | Review all open PRs or a specific PR, post reviews to GitHub |
| [`/self-review`](commands/self-review.md) | Comprehensive self-review of uncommitted changes before creating a PR |
| [`/merge-commit-msg`](commands/merge-commit-msg.md) | Generate a structured merge commit message from PR changes |
| [`/optimize`](commands/optimize.md) | Analyze code for performance issues with structured recommendations |
| [`/security-review`](commands/security-review.md) | Review code for security vulnerabilities (OWASP Top 10 checklist) |
| [`/file-by-file-review`](commands/file-by-file-review.md) | Review massive PRs file-by-file with parallel subagents (credit: [Romex91](https://github.com/Romex91/claude-code-file-by-file-review)) |

## Prompt Templates

Use these when you want a reusable workflow outside Claude Code's slash-command system:

| Prompt | Description |
|--------|-------------|
| [`address-review`](prompts/address-review.md) | Shared prompt for Codex, GPT, or another coding assistant that mirrors `/address-review` and falls back cleanly when terminal access is unavailable |

Prompt templates are not auto-installed commands. For Codex, point `AGENTS.md` at the prompt you want used. For GPT, paste the prompt into a session or add it to your project or custom instructions.

## Agents

| Agent | Description |
|-------|-------------|
| [`pr-testing-agent`](agents/pr-testing-agent.md) | Identify and run only the tests affected by PR changes |

Install to `~/.claude/agents/` (personal) or `.claude/agents/` (project).

## Skills

Skills are invoked via `/skill-name` in Claude Code. Install by adding this repo via `--add-dir`:

```bash
claude --add-dir /path/to/claude-code-commands-skills-agents/skills
```

Or configure in your project's `.claude/settings.json`:

```json
{
  "additionalDirectories": ["/path/to/claude-code-commands-skills-agents/skills"]
}
```

| Skill | Description |
| --- | --- |
| [`/docs`](skills/docs/SKILL.md) | Generate, audit, or update project documentation to a professional open-source standard. Covers README, quick start, API reference, config reference, migration guides, troubleshooting, LLMs.txt, and inline code docs (YARD/TSDoc). Benchmarked against Inertia Rails and Vite Ruby documentation. |

## Templates

Starter templates for new projects:

| Template | Description |
|----------|-------------|
| [`CLAUDE.md`](templates/CLAUDE.md) | Project-level Claude Code instructions template |
| [`AGENTS.md`](templates/AGENTS.md) | Cross-tool AI agent instructions template (works with Codex CLI, Cursor, etc.) |

## Documentation

| Guide | Description |
|-------|-------------|
| [Writing Effective CLAUDE.md](docs/claude-md-guide.md) | Memory hierarchy, what to include/exclude, path-specific rules, imports |
| [Custom Agents and Skills](docs/custom-agents-and-skills.md) | Creating custom agents, skills, slash commands, and agent teams |
| [Hooks Guide](docs/hooks-guide.md) | Lifecycle hooks for automation, quality gates, and safety |
| [Claude Code + Codex CLI](docs/claude-code-with-codex.md) | Using both tools together, shared instructions, workflows |
| [Tips and Tricks](docs/tips-and-tricks.md) | Context management, parallel sessions, effective prompting, common pitfalls |

## Scripts

| Script | Description |
|--------|-------------|
| [`bin/sync-commands`](bin/sync-commands) | Sync commands from this repo into a target project's `.claude/commands/` |
| [`bin/sync-skills`](bin/sync-skills) | Sync skills from this repo into a target project's `.claude/skills/` |
| [`bin/chrome-mcp`](bin/chrome-mcp) | Launch Chrome with a separate profile for MCP browser debugging |
| `bin/set-review-instructions` | Initialize file-by-file review with instructions and changed file list |
| `bin/print-git-diff` | Print diff, before/after, and review instructions for a single file |
| `bin/mark-git-diff-as-good` | Mark a reviewed file as GOOD with a reason |
| `bin/mark-git-diff-as-bad` | Mark a reviewed file as BAD with a reason |
| `bin/check-missing-reviews` | Check which files still need review |
| `bin/compose-summary` | Compose final GOOD/BAD summary report |
| `bin/get-number-of-changed-files` | Get count of changed files in the review |

## GitHub Actions

| Workflow | Description |
|----------|-------------|
| [Claude Code Review](.github/workflows/claude-code-review.yml) | Automatic PR review on open/sync |
| [Claude Code](.github/workflows/claude.yml) | Respond to `@claude` mentions in issues/PRs |

## Syncing to Your Project

This repo is the canonical source for shared commands and skills. Use the sync scripts to keep a project up to date.

### One-Time Setup

```bash
# From your project root
BOOSTERS=~/.claude/claude-code-commands-skills-agents

# Clone (or pull if already cloned)
if [ -d "$BOOSTERS" ]; then
  git -C "$BOOSTERS" pull --rebase
else
  git clone https://github.com/shakacode/claude-code-commands-skills-agents.git "$BOOSTERS"
fi

# Copy the commands you want into your project
mkdir -p .claude/commands
cp "$BOOSTERS/commands/address-review.md" .claude/commands/
```

### Keeping Up to Date

Run the sync scripts from this repo to pull the latest commands or skills into a target project:

```bash
# Sync all commands to a project
./bin/sync-commands ~/projects/my-app

# Sync a specific command
./bin/sync-commands ~/projects/my-app address-review

# Sync all skills to a project
./bin/sync-skills ~/projects/my-app

# Sync a specific skill
./bin/sync-skills ~/projects/my-app docs
```

### For AI Agents in Consuming Repos

Add this to your project's `CLAUDE.md` or `AGENTS.md` so agents know where shared commands come from:

```markdown
## Shared Commands and Skills

Commands and skills are synced from
[claude-code-commands-skills-agents](https://github.com/shakacode/claude-code-commands-skills-agents).
Do not edit `.claude/commands/` or `.claude/skills/` directly — update the
canonical copies in the boosters repo and re-sync.
```

See the [templates/](templates/) directory for starter `CLAUDE.md` and `AGENTS.md` files that include this pattern.

## Contributing

1. Add new commands to `commands/`
2. Add new prompt templates to `prompts/` when the workflow targets Codex, GPT, or other non-Claude tools
3. Add new agents to `agents/`
4. Add new skills to `skills/`
5. Add documentation to `docs/`
6. Keep everything generic -- project-specific instructions belong in project CLAUDE.md files
7. All files must end with a newline character

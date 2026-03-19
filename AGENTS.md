# claude-code-commands-skills-agents

## Project Overview

This repository stores reusable AI workflows and supporting documentation.

- `commands/`: Claude Code slash commands
- `prompts/`: shared prompt templates for Codex, GPT, and other non-Claude tools
- `agents/`: Claude agents
- `docs/`: usage guides and supporting documentation
- `templates/`: starter instruction files for other repositories

## Working Rules

- Keep reusable assets generic across repositories that use `gh`.
- Treat `commands/` as Claude-only slash commands.
- Treat `prompts/` as the canonical place for workflows meant to be pasted into Codex, GPT, or other tools without Claude slash commands.
- When the user asks to address PR review comments outside Claude slash commands, follow `prompts/address-review.md`.
- README is the human discovery surface. Update it whenever you add or rename a reusable asset.

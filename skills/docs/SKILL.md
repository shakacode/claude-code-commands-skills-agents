---
name: docs
description: Generate, audit, or update project documentation to a professional open-source standard. Use this skill whenever the user mentions docs, documentation, README, API reference, guides, migration guides, troubleshooting, llms.txt, doc audit, or wants to improve any written developer-facing content in a repository. Also trigger when the user says things like "document this", "write docs for", "update the docs", "our docs need work", or compares documentation quality to other projects. Covers Ruby (YARD), TypeScript (TSDoc/JSDoc), Markdown guides, configuration references, and doc site structure.
---

# Documentation Skill

Generate and maintain documentation that meets or exceeds the standard set by the best open-source Rails/JS projects (Inertia Rails, Vite Ruby, Rails itself).

## Reference: Quality Standard

!`cat "$(dirname "$0")/references/quality-standard.md"`

## Reference: Documentation Templates

!`cat "$(dirname "$0")/references/templates.md"`

## Reference: Competitive Landscape

!`cat "$(dirname "$0")/references/competitive-landscape.md"`

## Workflow

### Step 1: Assess the current state

- Scan the repo for existing docs: `docs/`, `README.md`, `CHANGELOG.md`, `CONTRIBUTING.md`, inline code comments, Wiki, and any hosted doc site config (VitePress, Docusaurus, Jekyll, etc.)
- Identify what exists, what is outdated, and what is missing
- Compare against the Quality Standard reference above

### Step 2: Determine scope

If the user gave a specific target (e.g., `/docs $ARGUMENTS`), focus there. Otherwise, present a prioritized gap analysis:

1. **Critical gaps** - Missing README sections, no quick start, no API reference
2. **High-value improvements** - Outdated guides, missing migration/upgrade docs, no troubleshooting
3. **Polish** - LLMs.txt, cookbook/recipes, configuration reference, contributor guide improvements

Ask the user which items to tackle (or do all if they say so).

### Step 3: Generate or rewrite documentation

Follow these principles for ALL documentation:

#### Voice and Style
- **Direct and concise.** Lead with what the reader needs. No filler.
- **Show, don't tell.** Every concept gets a code example. Prefer real-world examples over contrived ones.
- **Progressive disclosure.** Quick start first, then deeper guides, then API reference. Layer complexity.
- **Avoid em dashes** (use commas, parentheses, or separate sentences instead).
- **Use second person** ("you") for guides and tutorials. Use third person for API references.
- **Prefer active voice.** "Run `bundle install`" not "The bundle should be installed."

#### Structure by Doc Type

**README.md** (the front door):
- One-liner description + badges
- "What is this?" in 2-3 sentences
- Quick install (copy-paste ready)
- Minimal "Hello World" example that works
- Link table to deeper docs
- Requirements / compatibility matrix
- Community links (Slack, Discussions, Stack Overflow)
- Contributing pointer
- License

**Quick Start Guide** (< 15 minutes):
- Prerequisites with exact version requirements
- Step-by-step, numbered instructions
- Every command is copy-paste ready
- "You should see..." verification checkpoints after key steps
- Link to "next steps" at the end

**Conceptual Guides** (explain "why" and "how"):
- Start with a one-paragraph summary of what the reader will learn
- Use diagrams (Mermaid or ASCII) for architecture and data flow
- Break into logical sections with clear headings
- End each guide with "Related" links

**API / Helper Reference**:
- One page per module or helper group
- Signature, parameters table, return value, exceptions
- At least one usage example per method
- For Ruby: follow YARD conventions (`@param`, `@return`, `@example`)
- For TypeScript: follow TSDoc conventions (`@param`, `@returns`, `@example`)

**Configuration Reference**:
- Table format: option name, type, default, description
- Group by category
- Include example config file (annotated with comments)

**Migration / Upgrade Guide**:
- Version-to-version, with exact steps
- "Breaking changes" section at top
- "Deprecations" section
- Automated migration commands if available
- Before/after code comparisons

**Troubleshooting / FAQ**:
- Problem statement as the heading (what the user sees or encounters)
- Cause explanation (1-2 sentences)
- Solution with exact commands or code
- "Still stuck?" pointer to community support

**LLMs.txt** (AI-friendly docs):
- `/llms.txt` with a structured overview and links to key pages
- `/llms-full.txt` with complete documentation in a single Markdown file
- Follow the llms.txt specification: title, description, sections with URLs
- Include on every docs page: "Are you an LLM? View /llms.txt for optimized documentation"

### Step 4: Cross-reference and link

- Every guide should link to related guides
- Every API method mentioned in a guide should link to its reference page
- Add a "See also" or "Related" section at the bottom of each page
- Verify no dead links (check file paths exist)

### Step 5: Review with the user

Present the generated docs and ask:
- "Does this match how your project actually works?"
- "Any terminology or naming I got wrong?"
- "Anything missing for your users?"

## Targeting Specific Files

When invoked as `/docs <target>`:
- If `<target>` is a file path: generate/update docs FOR that code file (inline comments, module-level docs, method docs)
- If `<target>` is a directory: generate/update docs for the entire module
- If `<target>` is a doc type keyword (e.g., "readme", "api", "quickstart", "migration", "troubleshooting", "llms.txt", "audit"): generate that specific doc type
- If `<target>` is "audit": run a full gap analysis against the Quality Standard reference above and report findings

## Language-Specific Conventions

### Ruby
- Use YARD doc format for all public methods and classes
- `@param name [Type] description`
- `@return [Type] description`
- `@raise [ExceptionClass] when condition`
- `@example` with realistic usage
- `@see` for cross-references
- Document `@option` for hash parameters

### TypeScript / JavaScript
- Use TSDoc for TypeScript, JSDoc for JavaScript
- `@param name - description`
- `@returns description`
- `@throws {ErrorType} description`
- `@example` blocks with realistic usage
- Export documentation: what is public API vs. internal
- Document generic type parameters

### Markdown Docs
- Use ATX headings (`#`, `##`, `###`) not Setext
- Fenced code blocks with language identifiers (```ruby, ```typescript, ```bash)
- Use reference-style links for repeated URLs
- Tables for configuration options and API parameter lists
- Admonitions for warnings and tips (use blockquote style: `> **Note:** ...` or `> **Warning:** ...`)

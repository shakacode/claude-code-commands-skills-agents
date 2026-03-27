# Documentation Quality Standard

This checklist represents the bar set by the best Rails/JS open-source projects. Use it when auditing existing docs or planning new documentation.

## Benchmarks

The following projects represent the gold standard we aim to match or exceed:

**Inertia Rails** (inertia-rails.dev):
- Dedicated docs site with VitePress
- Clear sidebar: Introduction > Installation > Core Concepts > Basics > Data & Props > Security > Advanced
- LLMs.txt and llms-full.txt for AI-friendly access
- Cookbook section with practical recipes
- "Awesome" curated ecosystem list
- Demo application with source code
- Upgrade guide between major versions
- Every page has "Edit on GitHub" link

**Vite Ruby** (vite-ruby.netlify.app):
- Clean structure: Introduction > Getting Started > Development > Deployment > Advanced > Plugins
- Configuration reference as a dedicated page with every option documented
- Framework-specific integration pages (Rails, Hanami, Padrino)
- Recommended plugins page
- Troubleshooting section
- Overview page explaining internals for curious developers

**Rails Guides** (guides.rubyonrails.org):
- Numbered, progressive guides
- "What you will learn" box at the start of each guide
- Consistent voice and structure across all guides
- Version switcher

## Audit Checklist

### Tier 1: Must-Have (blocks adoption if missing)

- [ ] **README.md** with: one-liner, install command, minimal example, link table to docs
- [ ] **Quick Start** that works in < 15 minutes on a fresh project
- [ ] **Installation guide** with exact version requirements and copy-paste commands
- [ ] **At least one complete tutorial** walking through a real use case end-to-end
- [ ] **API/Helper reference** for all public-facing methods
- [ ] **Configuration reference** with every option, its type, default, and description
- [ ] **CHANGELOG.md** or equivalent release notes
- [ ] **LICENSE** file

### Tier 2: Expected (users will notice if missing)

- [ ] **Upgrade / Migration guide** for each major version
- [ ] **Troubleshooting / FAQ** covering the top 10 issues from GitHub Issues
- [ ] **Contributing guide** (CONTRIBUTING.md)
- [ ] **Architecture / How it works** explainer with a diagram
- [ ] **Server-side rendering (SSR) guide** (if applicable)
- [ ] **Deployment guide** for common platforms (Heroku, Render, Docker, Kamal)
- [ ] **Testing guide** showing how to test components/integration
- [ ] **Code of Conduct**

### Tier 3: Differentiator (sets you apart)

- [ ] **Dedicated docs site** (VitePress, Docusaurus, or similar)
- [ ] **LLMs.txt** for AI agent consumption
- [ ] **AI agent instructions** file for coding assistants (AGENTS.md or similar)
- [ ] **Cookbook / Recipes** section with copy-paste solutions to common tasks
- [ ] **Comparison page** vs. alternatives (honest, factual)
- [ ] **Demo application** with source code and live deployment
- [ ] **Video walkthroughs** or links to conference talks
- [ ] **Ecosystem / Awesome list** of community plugins, tools, and integrations
- [ ] **Versioned docs** with a version switcher
- [ ] **Search functionality** on the docs site
- [ ] **"Edit this page on GitHub"** links on every page
- [ ] **i18n / Localization** guide (if the project supports it)

## Doc Site Structure Template

For projects that have or want a dedicated docs site, the recommended sidebar structure is:

```
Getting Started
  ├── Introduction (what, why, who)
  ├── Quick Start (< 15 min)
  ├── Installation (detailed)
  └── Demo Application

Core Concepts
  ├── How It Works (architecture diagram)
  ├── Key Terminology
  └── Comparison with Alternatives

Guides
  ├── Tutorial (full walkthrough)
  ├── Server-Side Rendering
  ├── TypeScript Integration
  ├── Styling / CSS
  ├── Testing
  ├── Deployment
  └── [Project-specific topics]

API Reference
  ├── Ruby API (View Helpers, Configuration, Generator)
  ├── JavaScript API (Client module, Registration, Hooks)
  └── CLI / Rake Tasks

Configuration
  └── Full Configuration Reference

Advanced
  ├── Performance Optimization
  ├── Code Splitting
  ├── Custom Webpack/Rspack Configuration
  └── Extending / Plugin Development

Resources
  ├── Upgrade Guide
  ├── Troubleshooting / FAQ
  ├── Cookbook / Recipes
  ├── Contributing
  ├── Changelog
  └── Ecosystem / Awesome List
```

## Writing Quality Signals

When reviewing docs, check for these quality signals:

**Good signs:**
- Every code example is copy-paste ready and tested
- Verification checkpoints ("You should see...")
- Real-world examples, not `foo`/`bar`
- Consistent heading hierarchy
- Cross-links between related pages
- Clear prerequisites at the start of each guide
- "Next steps" at the end of each page

**Red flags:**
- Stale version numbers in examples
- Broken links or references to removed features
- "TODO" or "Coming soon" placeholders
- Examples that assume context not provided
- Inconsistent terminology (using different names for the same concept)
- Missing code language identifiers on fenced blocks
- Walls of text with no code examples
- Em dashes (prefer commas or separate sentences)

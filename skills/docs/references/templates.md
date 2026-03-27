# Documentation Templates

Structural templates for each doc type. Adapt these to the specific project. Do not copy them verbatim; they are skeletons to fill in with real content.

---

## README.md Template

```markdown
# Project Name

[![Gem Version](badge-url)](gem-url)
[![npm version](badge-url)](npm-url)
[![Build Status](badge-url)](ci-url)
[![License: MIT](badge-url)](license-url)

One-sentence description of what this project does and why it matters.

## Why Project Name?

2-3 sentences expanding on the value proposition. What problem does it solve?
How does it differ from alternatives?

## Quick Install

\`\`\`bash
# Ruby
bundle add project_name --strict

# JavaScript
yarn add project-name
\`\`\`

## Hello World

Minimal, complete, working example in < 20 lines total.

\`\`\`ruby
# In your Rails view
<%= react_component("HelloWorld", props: { name: "Reader" }, prerender: false) %>
\`\`\`

\`\`\`typescript
// In your component file
import React from 'react';

const HelloWorld = ({ name }: { name: string }) => (
  <h1>Hello, {name}!</h1>
);

export default HelloWorld;
\`\`\`

## Documentation

| Topic | Link |
|-------|------|
| Quick Start (15 min) | [docs/quick-start.md](docs/quick-start.md) |
| Full Tutorial | [docs/tutorial.md](docs/tutorial.md) |
| API Reference | [docs/api/README.md](docs/api/README.md) |
| Configuration | [docs/configuration.md](docs/configuration.md) |
| Upgrade Guide | [docs/upgrade.md](docs/upgrade.md) |
| Troubleshooting | [docs/troubleshooting.md](docs/troubleshooting.md) |

## Requirements

- Ruby >= 3.0
- Rails >= 6.1
- Node >= 18
- Shakapacker >= 6.0 (or Rspack)

## Community

- [GitHub Discussions](link)
- [Slack Channel](link)
- [Stack Overflow Tag](link)

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT. See [LICENSE](LICENSE).
```

---

## Quick Start Guide Template

```markdown
# Quick Start

Get your first [component/feature] running in under 15 minutes.

## Prerequisites

- Ruby [version] and Rails [version] (verify: `ruby -v && rails -v`)
- Node [version] and Yarn [version] (verify: `node -v && yarn -v`)
- A Rails application (or create one: `rails new myapp --skip-javascript`)

## Step 1: Install dependencies

\`\`\`bash
bundle add project_name --strict
bundle add shakapacker --strict
\`\`\`

## Step 2: Run the generator

\`\`\`bash
rails generate project_name:install
\`\`\`

> **You should see:** Output confirming files were created, including
> `app/javascript/...` and configuration files.

## Step 3: Start the development server

\`\`\`bash
bin/dev
\`\`\`

> **You should see:** Both Rails and the Webpack dev server start.
> Visit `http://localhost:3000` in your browser.

## Step 4: Verify it works

Navigate to `http://localhost:3000/hello_world`. You should see a React
component rendering with a greeting.

## Step 5: Make a change

Open `app/javascript/src/HelloWorld.jsx` and change the greeting text.
Save the file. The browser should update automatically (HMR).

## Next Steps

- [Full Tutorial](tutorial.md) - Build a complete feature
- [Server-Side Rendering](ssr.md) - Enable SSR for SEO
- [Configuration Reference](configuration.md) - Customize your setup
```

---

## API Reference Entry Template

```markdown
# `method_name`

Brief one-line description of what this method does.

## Signature

\`\`\`ruby
method_name(component_name, options = {}) -> String
\`\`\`

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `component_name` | `String` | Yes | - | The registered name of the React component |
| `options` | `Hash` | No | `{}` | Configuration options (see below) |

### Options

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| `:props` | `Hash` | `{}` | Props passed to the React component |
| `:prerender` | `Boolean` | `false` | Enable server-side rendering |
| `:trace` | `Boolean` | `false` | Add HTML comments for debugging |

## Return Value

Returns an HTML `String` containing the rendered component markup and
the JavaScript needed to hydrate it on the client.

## Examples

### Basic usage

\`\`\`ruby
<%= react_component("UserProfile", props: { user: @user }) %>
\`\`\`

### With server-side rendering

\`\`\`ruby
<%= react_component("UserProfile",
  props: { user: @user.as_json(only: [:id, :name, :email]) },
  prerender: true
) %>
\`\`\`

## Notes

- Component must be registered with `ReactOnRails.register({ UserProfile })`
  before it can be rendered.
- When using `prerender: true`, ensure your component does not depend on
  browser-only APIs during initial render.

## See Also

- [`react_component_hash`](react_component_hash.md)
- [Server-Side Rendering Guide](../guides/ssr.md)
```

---

## Configuration Reference Template

```markdown
# Configuration Reference

All configuration options for Project Name, with types, defaults,
and descriptions.

## Ruby Configuration

Set these in `config/initializers/react_on_rails.rb`:

\`\`\`ruby
ReactOnRails.configure do |config|
  config.server_bundle_js_file = "server-bundle.js"
  config.prerender = false
end
\`\`\`

### Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `server_bundle_js_file` | `String` | `""` | JS bundle used for server rendering. Relative to `generated_assets_dir`. |
| `prerender` | `Boolean` | `false` | Default SSR setting for all components. Can be overridden per-component. |
| `random_dom_id` | `Boolean` | `true` | Generate random DOM IDs for component containers. Set to `false` for deterministic IDs (useful in testing). |

## JavaScript Configuration

Configure in your webpack/rspack entry file:

\`\`\`typescript
import ReactOnRails from 'react-on-rails';

ReactOnRails.setOptions({
  traceTurbolinks: true,
});
\`\`\`

### Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `traceTurbolinks` | `boolean` | `false` | Log Turbolinks events for debugging. |

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `TRACE_REACT_ON_RAILS` | - | Enable verbose logging |
```

---

## Troubleshooting Template

```markdown
# Troubleshooting

Common issues and their solutions. If your problem is not listed here,
search [GitHub Issues](link) or ask in [Discussions](link).

## Component not rendering

**What you see:** The page loads but the React component area is blank
or shows raw HTML.

**Common causes:**
1. The component is not registered. Make sure you call
   `ReactOnRails.register({ MyComponent })` in your entry file.
2. The entry file is not included in the page. Check your
   `javascript_pack_tag` or Shakapacker configuration.

**Fix:**

\`\`\`javascript
// app/javascript/packs/application.js
import ReactOnRails from 'react-on-rails';
import MyComponent from '../components/MyComponent';

ReactOnRails.register({ MyComponent });
\`\`\`

---

## SSR fails with "ReferenceError: window is not defined"

**What you see:** Server-side rendering crashes with a reference error
for `window`, `document`, or other browser globals.

**Cause:** Your component (or a dependency) accesses browser APIs
during the initial render pass, which runs in a Node/ExecJS context
where those globals do not exist.

**Fix:** Guard browser-only code:

\`\`\`typescript
const isBrowser = typeof window !== 'undefined';

useEffect(() => {
  // Safe to use window here (only runs in browser)
}, []);
\`\`\`

---

## Still stuck?

- Run `VERBOSE=true rake react_on_rails:doctor` for a diagnostic report
- Search [GitHub Issues](link)
- Ask in the [React + Rails Slack](link)
- [Book a call with ShakaCode](link) for direct support
```

---

## LLMs.txt Template

```
# Project Name

> One-sentence description

Project Name is [expanded description in 2-3 sentences].

## Documentation

- [Quick Start](https://example.com/docs/quick-start): Get running in 15 minutes
- [Installation](https://example.com/docs/installation): Detailed setup instructions
- [Tutorial](https://example.com/docs/tutorial): Build a complete feature step by step
- [API Reference](https://example.com/docs/api): All public methods and helpers
- [Configuration](https://example.com/docs/configuration): Every config option explained
- [SSR Guide](https://example.com/docs/ssr): Server-side rendering setup and optimization
- [Troubleshooting](https://example.com/docs/troubleshooting): Common issues and fixes
- [Upgrade Guide](https://example.com/docs/upgrade): Migration between versions

## Optional

- [Architecture](https://example.com/docs/architecture): How it works under the hood
- [Cookbook](https://example.com/docs/cookbook): Recipes for common patterns
- [Contributing](https://example.com/contributing): How to contribute
- [Changelog](https://example.com/changelog): Release history
```

---

## Migration / Upgrade Guide Template

```markdown
# Upgrading from vX to vY

This guide covers breaking changes, deprecations, and the steps to
upgrade your application.

## Breaking Changes

### 1. Feature/API that changed

**Before (vX):**

\`\`\`ruby
# Old way
config.old_option = true
\`\`\`

**After (vY):**

\`\`\`ruby
# New way
config.new_option = true
\`\`\`

**Migration:** Replace all occurrences of `old_option` with `new_option`
in your initializer.

### 2. Removed feature

`some_deprecated_method` has been removed. Use `new_method` instead.

## Deprecations

The following are deprecated in vY and will be removed in v(Y+1):

| Deprecated | Replacement | Remove in |
|-----------|-------------|-----------|
| `old_helper` | `new_helper` | vZ |

## Automated Migration

Run the generator to update configuration files automatically:

\`\`\`bash
rails generate project_name:install
\`\`\`

> **Warning:** Review the diff before committing. The generator may
> overwrite custom configurations.

## Step-by-Step Upgrade

1. Update your Gemfile: `gem "project_name", "~> Y.0"`
2. Run `bundle update project_name`
3. Run `rails generate project_name:install` and review changes
4. Update JavaScript: `yarn upgrade project-name@^Y.0`
5. Run your test suite: `bundle exec rspec`
6. Check for deprecation warnings in your Rails logs

## Need Help?

- [Troubleshooting Guide](troubleshooting.md)
- [GitHub Discussions](link)
- [ShakaCode Support](link)
```

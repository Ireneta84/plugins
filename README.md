# Canva Plugin for Claude Code

Skills for working with Canva — brand package creation, client delivery, MCP tool usage, and edit-vs-create discipline.

## Install

```
/plugin marketplace add Ireneta84/plugins
```

Then install `canva` from the plugin manager.

## Skills

- **canva-knowledge** — Canva features, tools, plan tiers, sharing limits, export formats
- **canva-mcp** — How to use the Canva MCP tools correctly (sequences, gotchas, tool selection)
- **canva-brand-package** — Full workflow: brand kit → templates → client delivery (including plan-aware fallbacks)
- **canva-edit-refine** — When to edit existing designs vs. create new ones

## Hooks

- **warn-generate-design** — Intercepts generate-design calls when refining existing work
- **commit-reminder** — Reminds to commit after editing operations

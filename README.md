# Claude Code Plugins

Personal Claude Code plugins by Irene Deu.

Each plugin lives in its own subfolder. Install any plugin locally with:

```bash
claude --plugin-dir ~/Projects/plugins/<plugin-name>
```

Or clone the repo and point to the subfolder.

## Plugins

| Plugin | Description |
|---|---|
| [canva](./canva/) | Canva skills for brand package creation, client delivery, and correct MCP usage |

## Testing

```bash
claude --plugin-dir ./canva
```

Then use `/reload-plugins` to pick up changes during development.

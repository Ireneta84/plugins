---
name: canva-mcp
description: This skill should be used when working with the Canva MCP tools — creating designs, editing designs, exporting, managing brand kits, uploading assets, or searching Canva content. Provides correct tool sequencing, parameter guidance, and gotchas for all Canva MCP operations.
version: 0.1.0
---

# Canva MCP Guide

The Canva MCP gives direct API access to Canva designs, brand kits, folders, and AI tools. All tools are prefixed `mcp__claude_ai_Canva__` in Claude Code.

## Tool Categories

### Discovery & Reading
| Tool | Purpose |
|---|---|
| `search-designs` | Find designs by keyword in the user's account |
| `get-design` | Get design metadata (title, dimensions, page count) |
| `get-design-content` | Get full content tree — elements, text, colors, layers |
| `get-design-pages` | List pages with thumbnails |
| `get-design-thumbnail` | Get preview image of a design |
| `list-folder-items` | List contents of a Canva folder |
| `search-folders` | Find folders by name |
| `resolve-shortlink` | Convert a canva.com short URL to a full design ID |
| `help` | Get Canva MCP capability overview |

### Brand & Templates
| Tool | Purpose |
|---|---|
| `list-brand-kits` | List all brand kits in the account |
| `get-brand-template-dataset` | Get data fields for a brand template |
| `search-brand-templates` | Find brand templates by keyword |
| `get-assets` | List brand assets (logos, images) from a brand kit |

### Creating Designs
| Tool | Purpose |
|---|---|
| `generate-design` | Create a new design from a text prompt |
| `generate-design-structured` | Create a new design with structured data input |
| `create-design-from-brand-template` | Create from a brand template with data injection |
| `create-design-from-candidate` | Create from a candidate/suggestion |
| `copy-design` | Duplicate an existing design |
| `import-design-from-url` | Import a design from a URL |
| `merge-designs` | Combine multiple designs |

### Editing Designs (Transaction Pattern)
| Tool | Purpose |
|---|---|
| `start-editing-transaction` | Open design for editing — returns transaction_id |
| `perform-editing-operations` | Apply changes within a transaction |
| `commit-editing-transaction` | Save changes and close transaction |
| `cancel-editing-transaction` | Discard changes and revert |
| `resize-design` | Create a resized copy for a new format |

### Export & Output
| Tool | Purpose |
|---|---|
| `export-design` | Export to PNG, JPG, PDF, MP4, GIF, PPTX, SVG |
| `get-export-formats` | List available export formats for a design |

### Assets
| Tool | Purpose |
|---|---|
| `upload-asset-from-url` | Upload an image/file to Canva from a URL |

### Organization
| Tool | Purpose |
|---|---|
| `create-folder` | Create a new Canva folder |
| `move-item-to-folder` | Move a design into a folder |

### Comments & Review
| Tool | Purpose |
|---|---|
| `comment-on-design` | Add a comment to a design |
| `list-comments` | List all comments on a design |
| `list-replies` | List replies to a comment |
| `reply-to-comment` | Reply to a comment |
| `request-outline-review` | Request review of a design outline |
| `get-presenter-notes` | Get presenter notes from a presentation |

## Key Sequences

### Find an existing design
```
search-designs(query) → pick from results → get-design(design_id)
```
If the user has a canva.com URL: `resolve-shortlink(url)` → design_id

### Create a new design from scratch
```
generate-design(prompt, format) → design_id
```
Or with structured content: `generate-design-structured(data)`

### Edit an existing design
```
get-design-content(design_id)            # understand current state
start-editing-transaction(design_id)     # open transaction
perform-editing-operations(tx_id, ops)   # apply changes
commit-editing-transaction(tx_id)        # save
```

### Create a brand package from brand template
```
list-brand-kits()                                    # find the brand kit
search-brand-templates(query)                        # find matching templates
get-brand-template-dataset(template_id)             # understand data fields
create-design-from-brand-template(template_id, data) # create with data
```

### Export a design
```
get-export-formats(design_id)            # check available formats
export-design(design_id, format, pages)  # export
```

### Organize into folders
```
search-folders(name) or create-folder(name)   # find or create folder
move-item-to-folder(design_id, folder_id)     # move design
```

## Gotchas

**`generate-design` creates new, never edits** — calling it on a refinement request destroys the existing design. See `canva-edit-refine` skill for the correct edit pattern.

**Transaction IDs expire** — if a transaction is left open too long without being committed or cancelled, it may expire. Always commit or cancel.

**`resize-design` creates a copy** — it does not modify the original. The resized design is a separate design with a new ID.

**Brand templates need a Pro/Teams account** — `search-brand-templates` and `create-design-from-brand-template` only work if brand templates exist in the account.

**`get-design-content` can be large** — for complex multi-page designs, the content tree can be very long. Request specific pages when possible.

**Export takes time** — `export-design` is async. The response includes a URL when ready; poll or wait if needed.

**Asset upload requires a public URL** — `upload-asset-from-url` needs a publicly accessible URL, not a local file path.

## Additional Resources

- **`references/mcp-tools.md`** — Complete parameter reference for each tool

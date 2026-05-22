# Canva MCP — Tool Parameter Reference

## generate-design

Creates a brand new design from a text prompt.

```
generate-design(
  prompt: str,          # Text description of the design
  format?: str          # "instagram_post", "presentation", "document", etc.
)
→ design_id: str
```

**When to use**: Only for creating new designs. Never for refining existing ones.

---

## generate-design-structured

Creates a new design with structured data (more control than generate-design).

```
generate-design-structured(
  title: str,
  content: dict,        # Structured content per page/section
  format?: str
)
→ design_id: str
```

---

## start-editing-transaction

Opens an existing design for editing. Required before any editing operations.

```
start-editing-transaction(
  design_id: str
)
→ transaction_id: str
```

**Note**: Store the transaction_id — needed for all subsequent editing calls. Transactions expire if left open too long.

---

## perform-editing-operations

Applies structured changes within an open transaction.

```
perform-editing-operations(
  transaction_id: str,
  operations: list[Operation]
)
→ result: dict
```

Operations describe what to change: text content, colors, fonts, visibility, position, size. Multiple calls can be chained within the same transaction.

---

## commit-editing-transaction

Saves all changes and closes the transaction.

```
commit-editing-transaction(
  transaction_id: str
)
→ success: bool
```

**Never skip this** — changes are not persisted until committed.

---

## cancel-editing-transaction

Discards all changes since the transaction was opened. Reverts to original.

```
cancel-editing-transaction(
  transaction_id: str
)
→ success: bool
```

---

## get-design

Gets metadata for a design.

```
get-design(
  design_id: str
)
→ { title, dimensions, page_count, created_at, updated_at }
```

---

## get-design-content

Gets the full content tree of a design — all elements, text, colors, layers.

```
get-design-content(
  design_id: str,
  page?: int            # Optional: get specific page only
)
→ content_tree: dict
```

Can be large for complex designs. Request a specific page when possible.

---

## get-design-pages

Lists all pages in a design with thumbnails.

```
get-design-pages(
  design_id: str
)
→ pages: list[{ page_id, title, thumbnail_url }]
```

---

## get-design-thumbnail

Gets a preview image URL for a design.

```
get-design-thumbnail(
  design_id: str,
  page?: int
)
→ thumbnail_url: str
```

---

## search-designs

Finds designs in the user's Canva account by keyword.

```
search-designs(
  query: str,
  limit?: int
)
→ designs: list[{ design_id, title, thumbnail_url }]
```

---

## copy-design

Creates a duplicate of an existing design.

```
copy-design(
  design_id: str,
  title?: str           # Title for the copy
)
→ new_design_id: str
```

Use when creating a variant while preserving the original.

---

## export-design

Exports a design to a file format.

```
export-design(
  design_id: str,
  format: str,          # "png", "jpg", "pdf", "mp4", "gif", "pptx", "svg"
  pages?: list[int],    # Optional: export specific pages only
  quality?: str         # "regular" or "print" (PDF only)
)
→ export_url: str
```

Export is async — response returns when ready.

---

## get-export-formats

Lists available export formats for a design.

```
get-export-formats(
  design_id: str
)
→ formats: list[str]
```

---

## resize-design

Creates a resized copy of a design for a different format. Does NOT modify original.

```
resize-design(
  design_id: str,
  format: str           # Target format/size
)
→ new_design_id: str
```

---

## create-folder

Creates a new folder in the user's Canva account.

```
create-folder(
  name: str,
  parent_folder_id?: str
)
→ folder_id: str
```

---

## move-item-to-folder

Moves a design into a folder.

```
move-item-to-folder(
  item_id: str,         # design_id
  folder_id: str
)
→ success: bool
```

---

## list-folder-items

Lists contents of a folder.

```
list-folder-items(
  folder_id: str
)
→ items: list[{ id, type, title }]
```

---

## search-folders

Finds folders by name.

```
search-folders(
  query: str
)
→ folders: list[{ folder_id, name }]
```

---

## list-brand-kits

Lists all brand kits in the account.

```
list-brand-kits()
→ brand_kits: list[{ brand_kit_id, name, colors, fonts }]
```

Requires Pro or Teams account.

---

## get-assets

Lists brand assets (logos, images) from a brand kit.

```
get-assets(
  brand_kit_id: str
)
→ assets: list[{ asset_id, name, url, type }]
```

---

## search-brand-templates

Finds brand templates by keyword.

```
search-brand-templates(
  query: str
)
→ templates: list[{ template_id, name, thumbnail_url }]
```

Requires Pro/Teams. Brand templates must exist in the account.

---

## get-brand-template-dataset

Gets the data fields for a brand template (what content can be filled in).

```
get-brand-template-dataset(
  template_id: str
)
→ fields: list[{ field_id, name, type, required }]
```

---

## create-design-from-brand-template

Creates a new design from a brand template with data injected.

```
create-design-from-brand-template(
  template_id: str,
  data: dict            # { field_id: value } mapping
)
→ design_id: str
```

---

## upload-asset-from-url

Uploads an image or file to Canva from a public URL.

```
upload-asset-from-url(
  url: str,             # Must be publicly accessible
  name?: str
)
→ asset_id: str
```

---

## resolve-shortlink

Converts a canva.com short URL to a design ID.

```
resolve-shortlink(
  url: str              # e.g. "https://www.canva.com/design/ABC123/..."
)
→ design_id: str
```

---

## comment-on-design / list-comments / reply-to-comment

Standard commenting tools for design review workflows. Use when managing feedback or review cycles with clients.

---

## help

Returns an overview of Canva MCP capabilities. Call at the start of a session if unsure what's available.

```
help()
→ capabilities: str
```

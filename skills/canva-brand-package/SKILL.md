---
name: canva-brand-package
description: This skill should be used when the user wants to "create a brand package for a client", "build brand kit in Canva", "create social post templates", "build a Canva brand kit", "make presentation templates", "set up client templates in Canva", or "deliver a brand package". Guides the full workflow from brand kit creation to client delivery, including plan-aware sharing options.
version: 0.1.0
---

# Canva Brand Package Workflow

A brand package in Canva consists of: a brand kit (colors, fonts, logos) + a set of templates (social posts, presentations, documents) + a delivery method suited to the client's Canva plan.

## Step 1 — Set Up the Brand Kit

### Collect brand assets first
Before opening Canva, confirm:
- Primary + secondary colors (hex codes)
- Fonts (primary heading font, body font)
- Logo files (PNG with transparent background preferred)

### Create the brand kit
Brand kits are managed in Canva's brand settings, not via the MCP directly. Use `list-brand-kits` to confirm it exists and get its ID for template work.

If creating from scratch: guide the user to Canva → Brand Hub → Create a brand kit. The MCP can then reference it via `list-brand-kits` and `get-assets`.

## Step 2 — Create a Brand Folder

Organize all client templates in one place:
```
create-folder("Client Name — Brand Package")
```

This folder becomes the delivery unit — everything goes here.

## Step 3 — Build the Template Set

### Standard social post templates (minimum set)
Create one master template per format, then adapt:

| Template | Size | MCP call |
|---|---|---|
| Instagram Square | 1080×1080px | generate-design or create-design-from-brand-template |
| Instagram Stories/Reels | 1080×1920px | generate-design |
| LinkedIn Post | 1200×627px | generate-design |

For each template:
1. `generate-design(prompt, format)` — create the base design with brand colors/fonts in the prompt
2. Review with `get-design-thumbnail`
3. Edit with the transaction pattern if adjustments needed
4. `move-item-to-folder(design_id, folder_id)` — add to brand folder

### Presentation template
```
generate-design("professional presentation template, [brand colors], [brand fonts], clean minimal", format="presentation")
```
Then edit key slides: cover, content, section divider, closing.

### Document / one-pager (optional)
Useful for service menus, proposals, client guides.

## Step 4 — Apply Brand Kit to Templates

After creating templates, apply the brand kit:
1. `list-brand-kits()` — get brand kit ID
2. In each template via editing transaction: replace placeholder colors with brand colors, apply brand fonts

Or: include the brand hex codes and font names directly in the `generate-design` prompt to get closer to brand from the start.

## Step 5 — Deliver to Client

**The delivery method depends on the client's Canva plan.**

### If client has Canva Pro or Teams
→ Share the folder with edit or template access
→ They can see the brand kit and apply it themselves
→ Best for clients who will create their own content

### If client has Canva Free
→ **Cannot see brand kits** — share as template links instead
→ For each template: get the "Use this template" link
→ Client gets a copy of each template with the styles baked in (colors/fonts embedded, not from brand kit)
→ They can edit their copy freely

### If client has no Canva account
→ Export everything as PDF or PNG
→ Create a brand guide PDF (one-pager with colors, fonts, logo, template previews)
→ Deliver as a ZIP or Google Drive folder

### Universal fallback — Brand Guide PDF
Always create a brand guide document in Canva that includes:
- Color palette with hex codes
- Font names and weights
- Logo variations
- Template previews with usage instructions

Export as PDF (print quality). This works for any client regardless of plan.

```
generate-design("brand guide document, color palette, typography, logo usage, [brand name]", format="document")
```

## Step 6 — Final Checklist

Before delivering:
- [ ] All templates are in the client folder (`list-folder-items` to verify)
- [ ] Each template has a thumbnail that looks correct (`get-design-thumbnail`)
- [ ] Brand guide PDF exported
- [ ] Delivery method matches client's Canva plan
- [ ] Template links generated (if Free client)
- [ ] Folder shared with correct permissions

## Working with Existing Brand Materials

If the client already has a Canva account with existing designs:
```
search-designs(client_name)   # find existing work
search-folders(client_name)   # find existing folders
```
Review before creating — adapt existing rather than starting from scratch when possible.

## Additional Resources

- **`references/delivery-options.md`** — Detailed sharing scenarios, plan constraints, step-by-step delivery instructions per client plan

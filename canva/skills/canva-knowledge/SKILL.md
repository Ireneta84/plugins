---
name: canva-knowledge
description: This skill should be used when the user asks what Canva can do, mentions Canva features, asks "can Canva do X", wants to know Canva limits, asks about Canva plan differences, asks about sharing or collaboration in Canva, or starts any Canva design session. Provides comprehensive Canva product knowledge so Claude never has to guess about capabilities, tools, or constraints.
version: 0.1.0
---

# Canva Knowledge

Canva is a web-based design platform with a drag-and-drop editor, AI-powered tools, and a large template library. It runs in the browser and has iOS/Android apps. The MCP integration gives direct API access to designs, brand kits, and export functions.

## Design Editor

The Canva editor supports:
- **Pages**: Multi-page designs (presentations, documents, social carousels)
- **Elements**: Shapes, lines, frames, grids, tables, charts, graphs, stickers, icons
- **Text**: Heading/body/subheading styles, 1,000+ fonts, text effects (shadow, glow, lift, hollow, splice, echo, neon, glitch)
- **Media**: Upload images/videos, stock library (photos, videos, audio), AI image generation
- **Background**: Solid color, gradient, image, video, or pattern
- **Layers**: Z-order management, group/ungroup, lock elements

Key editor capabilities:
- Smart resize (resize design to any format, auto-adapts content)
- Brand kit application (one-click apply fonts/colors/logos)
- AI tools: Magic Write (text), Magic Edit (image editing), Magic Eraser, Background Remover, Magic Expand, Magic Grab
- Animations per element or per page
- Grids and alignment guides

## Templates

- 250,000+ templates across all categories
- Filterable by format, style, color, theme
- Brand templates: custom templates locked to brand kit (Pro/Teams only)
- Template links: shareable "Use this template" links — recipient gets a copy, not the original

## Brand Kits

**What they are**: A centralized set of colors, fonts, and logos applied across all designs.

**Plan requirements**:
- **Free**: 1 brand kit, limited fonts
- **Pro**: Multiple brand kits, custom fonts, brand controls
- **Teams**: Shared brand kits across all team members, brand controls, locking

**Key constraint**: Brand kits are not visible to people without a Canva Pro/Teams account. If you share a design that uses a brand kit with a Free user, they see the design but cannot access or apply the brand kit. This is the #1 sharing limitation for client work.

## Sharing & Collaboration

Four ways to share a design:

| Method | What recipient gets | Edit access | Requires Canva account |
|---|---|---|---|
| View link | Read-only | No | No |
| Edit link | Full edit access | Yes | Yes (Free ok) |
| Template link | Their own copy | Yes (on their copy) | Yes (Free ok) |
| Brand template | Guided fill-in | Limited | Yes (Pro for brand templates) |

**Key limits**:
- Brand kits: only Pro/Teams users can see and apply them
- Brand templates: only visible to users in the same Teams workspace
- Shared folders: only visible to users with Canva accounts
- Free users can edit shared designs but cannot use Pro features (premium elements, brand kit, etc.)

## Export Formats

| Format | Use case | Notes |
|---|---|---|
| PNG | Social media, web images | Transparent background option |
| JPG | Photos, web images | Smaller file size |
| PDF (standard) | Sharing, printing | Compressed |
| PDF (print) | Professional printing | High quality, includes bleed marks |
| MP4 | Video designs, animations | Up to 30fps |
| GIF | Animated social posts | Loops |
| PPTX | PowerPoint export | Editable slides |
| SVG | Vector graphics | Pro only |

Export options: choose pages, resolution (1x, 2x, 4x), transparent background (PNG only), file compression.

## Canva Plans

| Feature | Free | Pro | Teams |
|---|---|---|---|
| Storage | 5GB | 1TB | 1TB |
| Brand kits | 1 | Multiple | Multiple (shared) |
| Custom fonts | No | Yes | Yes |
| Background remover | No | Yes | Yes |
| Magic AI tools | Limited | Full | Full |
| Premium templates | No | Yes | Yes |
| SVG export | No | Yes | Yes |
| Scheduled publishing | No | Yes | Yes |
| Brand controls (lock elements) | No | No | Yes |
| Price | Free | ~€13/mo | ~€30/mo/user |

## AI Tools in Canva

- **Magic Write**: AI text generation inside text boxes
- **Magic Design**: Generate full design from a prompt or image
- **Magic Edit**: Edit specific parts of an image with AI
- **Magic Eraser**: Remove objects from photos
- **Magic Expand**: Extend image backgrounds
- **Magic Grab**: Separate subjects from backgrounds
- **Magic Animate**: Auto-animate designs
- **Background Remover**: Remove image backgrounds (Pro)
- **Text to Image**: Generate images from prompts (limited credits on Free)
- **DALL-E / Imagen integration**: Via Canva AI (credit-based)

## Social Post Sizes (Standard)

| Format | Size | Use |
|---|---|---|
| Instagram Square | 1080×1080px | Feed posts |
| Instagram Portrait | 1080×1350px | Feed posts (recommended) |
| Instagram Stories / Reels | 1080×1920px | Stories, Reels |
| LinkedIn Post | 1200×627px | Feed posts |
| LinkedIn Story | 1080×1920px | Stories |
| Facebook Post | 1200×630px | Feed posts |
| Facebook Cover | 820×312px | Profile cover |
| Pinterest | 1000×1500px | Pins |
| Twitter/X Post | 1600×900px | Feed posts |

## Canva Limitations to Know

- **No offline editing** — browser/app only, requires internet
- **No real version history** — only "Version History" (Pro) which saves versions manually
- **Brand kits not portable** — can't export a brand kit; must recreate in another tool
- **Free users see watermarks** on Pro elements if used in a shared design
- **No API for direct pixel manipulation** — AI edits are non-deterministic
- **Template links create copies** — changes to the original don't update the copy
- **Videos export as MP4** — no WebM or MOV

## Additional Resources

- **`../canva-mcp/references/mcp-tools.md`** — Full Canva MCP tool reference with descriptions and usage patterns
- **`references/sharing-guide.md`** — Detailed sharing scenarios, plan constraints, and client delivery options

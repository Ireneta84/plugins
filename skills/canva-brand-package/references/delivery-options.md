# Brand Package Delivery — Options by Client Plan

## Decision Tree

```
Does client have Canva?
├── No → Export everything (PDF + PNG) + brand guide PDF
└── Yes → What plan?
    ├── Teams → Share folder + brand templates in their workspace
    ├── Pro → Share folder + template links + brand guide PDF
    └── Free → Template links only + brand guide PDF + instructions
```

## Delivery Package by Plan

### For Teams clients
1. Create all templates in Canva
2. Create a shared folder: `create-folder("Client — Brand Package")`
3. Add all designs to folder: `move-item-to-folder` for each
4. Share folder with client (view + edit or template access)
5. If they want brand templates: recreate key templates as brand templates in their workspace
6. Export brand guide PDF as backup

### For Pro clients
1. Create all templates in Canva
2. Create a folder and add all designs
3. Share folder — client can see designs and copy them
4. Generate "Use this template" links for each key template
5. Export brand guide PDF
6. Send: folder link + template links + PDF

### For Free clients
1. Create all templates in Canva
2. For each template, get the "Use this template" link (share → template link)
3. Export brand guide as PDF
4. Create a simple instruction guide: which template to use for which occasion
5. Send: template links list + brand guide PDF + instructions
6. Note: client's copies will have brand colors/fonts baked in, not linked to a brand kit

### For no-Canva clients
1. Export all social templates as PNG (2x resolution)
2. Export presentation as PPTX (if they use PowerPoint) or PDF
3. Export brand guide as PDF
4. Package in Drive folder or ZIP
5. Include: brand guide PDF + all template images + font download links if using free fonts

## Brand Guide PDF — What to Include

A brand guide document in Canva should have these sections:

1. **Logo usage** — primary logo, variations, clear space rules, what not to do
2. **Color palette** — each color with hex code, name, and usage context
3. **Typography** — heading font + body font, sizes, weights, line height
4. **Social post templates** — screenshot/preview of each template with usage note
5. **Tone of voice** — 3-5 adjectives that describe the brand voice (optional but useful)

Keep it to 4-6 pages. Clean, visual, scannable.

## Template Links — How to Generate

For each design in Canva:
1. Open the design
2. Share → "Use as template"
3. Copy the template link
4. The link format: `canva.com/design/[ID]/template`

Recipients who click this get their own copy. They can edit freely without affecting the original.

## Post-Delivery Checklist

- [ ] Brand guide PDF exported and included
- [ ] All template links tested (open in incognito to verify)
- [ ] Folder permissions set correctly (not accidentally public)
- [ ] Client has instructions for how to use each template
- [ ] Master copies saved in Irene's Canva account (keep originals)
- [ ] Client folder labelled clearly in Canva (`clients/[name]/`)

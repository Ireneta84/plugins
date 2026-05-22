---
name: canva-edit-refine
description: This skill should be used when the user asks to "refine", "adjust", "tweak", "update", "change", "fix", "improve", or "modify" an existing Canva design — or when iterating on something already created. Prevents the critical mistake of creating a new design instead of editing the existing one. Teaches the correct editing transaction pattern.
version: 0.1.0
---

# Canva Edit vs. Create Discipline

## The Core Rule

**When refining an existing design: always edit in place. Never call `generate-design` or `generate-design-structured`.**

`generate-design` creates a brand new design from scratch. Calling it when the user says "adjust this" or "make it more minimal" destroys their work and replaces it with something unrelated.

## How to Detect Intent

**Create new** → user starts fresh, no existing design in context:
- "Create a social post for X"
- "Generate a brand kit template"
- "Make me a new Instagram carousel"

**Edit existing** → user references something already made:
- "Refine this", "adjust the colors", "make it more minimal"
- "Change the font", "update the headline", "fix the layout"
- "I don't like X, can you change it", "make it feel more Y"
- "Can you try a different version of this" (still edit — create a copy first if needed)

When in doubt: ask "Should I edit the existing design or create a new one?" — never assume create.

## The Editing Transaction Pattern

All edits to existing designs follow this sequence:

```
1. start-editing-transaction  →  opens the design for editing, returns transaction ID
2. perform-editing-operations →  applies changes (can call multiple times)
3. commit-editing-transaction →  saves and closes the transaction
```

If something goes wrong:
```
cancel-editing-transaction   →  discards all changes, reverts to original
```

**Never skip `commit-editing-transaction`** — changes are not saved until committed.

## Step-by-Step Edit Workflow

### 1. Get the current design state
```
get-design           → basic metadata (title, dimensions, page count)
get-design-content   → full content tree (elements, text, colors, layers)
get-design-pages     → page list with thumbnails
```
Read the content before editing. Know what's there before changing it.

### 2. Open the editing transaction
```
start-editing-transaction(design_id)
→ returns: transaction_id
```
Store the `transaction_id` — needed for all subsequent calls.

### 3. Apply changes
```
perform-editing-operations(transaction_id, operations=[...])
```
Operations are structured JSON describing what to change: text content, colors, fonts, element positions, visibility, etc.

Multiple `perform-editing-operations` calls can be chained within the same transaction.

### 4. Commit
```
commit-editing-transaction(transaction_id)
```
Design is saved. Transaction is closed.

## When to Copy Instead of Edit

If the user wants to "try a different version" while keeping the original:
```
copy-design(design_id)  →  creates a duplicate
```
Then edit the copy, leave the original untouched.

Use copy-design when:
- User explicitly wants to preserve the original
- Creating a variant for A/B comparison
- Generating a client version from a master template

## Common Mistake Pattern to Avoid

❌ **Wrong flow:**
```
user: "Can you make the headline bigger and change the blue to green?"
→ generate-design("headline bigger, green instead of blue")  ← WRONG: creates new design
```

✅ **Correct flow:**
```
user: "Can you make the headline bigger and change the blue to green?"
→ get-design-content(design_id)          # read current state
→ start-editing-transaction(design_id)   # open for editing
→ perform-editing-operations(...)        # change font size + color
→ commit-editing-transaction(...)        # save
```

## Resize is Not Editing

`resize-design` creates a new design sized for a different format — it does not modify the original. Use it intentionally when adapting a design to a new format (e.g. square post → story format). The resized version is a separate design.

# `tree`

The `tree` block represents a semantic hierarchical file tree.

It is not an ASCII-art code block. Renderers should understand folders, files, hierarchy, change state, and annotations as structured data.

## Syntax

```md
:::tree
root src

folder notes
  added NoteService.ts
    note: Note persistence and retrieval

  changed NotePage.tsx
    note: Add tag filtering

relevant app.ts
  note: Existing route registration
:::
```

## Statements

### `root <path>`

Declares the displayed root.

### `folder <name>`

Creates a folder node. Nested statements belong to that folder.

### File states

A file node may use one of:

- `added <name>`
- `changed <name>`
- `removed <name>`
- `relevant <name>`

The state is semantic. A renderer may choose its own icons, colours, labels, or other affordances.

### `note`

Adds a concise annotation to a node.

```text
changed settings.ts
  note: Add notification defaults
```

## Renderer guidance

Interactive renderers should support collapsing and expanding folder nodes.

Renderers may select file icons based on extension or file identity. The specification does not define a mandatory icon set.

A renderer should preserve:

- hierarchy
- file/folder identity
- change state
- annotations

A renderer should not flatten the tree into preformatted ASCII unless richer rendering is unavailable.

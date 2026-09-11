# GlanceMD

**Markdown for technical information you should be able to understand in 60 seconds.**

GlanceMD keeps normal Markdown, but adds a few structured blocks for things that are hard to scan as prose.

```md
# Notes feature

Add tagging to notes.

:::model
table Note
  id: uuid
  title: text

table Tag
  id: uuid
  name: text

relationship Note many -> many Tag
:::

:::api
POST /notes/{id}/tags
  auth: user
  purpose: Add a tag to a note
:::

:::tree
root src

folder notes
  changed NoteService.ts
  added TagPicker.tsx
:::
```

A GlanceMD-aware client can turn those blocks into a compact data model, API view, and collapsible file tree.

A normal Markdown client can still show the source as readable text.

## The idea

> **The document stays Markdown. The renderer makes structured parts easier to digest.**

GlanceMD does **not** define a visual design system. Different clients can render the same block differently.

The source stays:

- readable
- editable
- diffable
- easy for LLMs to generate
- portable between clients

## Blocks

| Block | Use it for |
| --- | --- |
| `model` | Tables/entities and important fields |
| `api` | Endpoints, auth, purpose, responses |
| `mcp` | MCP tools, resources, inputs, outputs, approvals |
| `tree` | Hierarchical files/folders with change state |
| `changeset` | What is expected to change and why |
| `embed` | Display an external artifact inline |
| `wireframe` | Screens, controls, states, viewports and interactions |

Most blocks are **inline**. `embed` and `wireframe` may point to external artifacts when needed.

## Why not just Markdown / Mermaid / OpenAPI?

GlanceMD is not trying to replace them.

It is for the middle ground where a document needs more structure than prose, but a full schema, diagram, design tool, or generated app is too much.

The goal is comprehension, not documentation volume.

## Wireframes

`wireframe` is a small semantic UI language rather than HTML.

```md
:::wireframe
viewport: phone

screen settings
  text heading "Settings"

  field notifications
    type: switch
    label: Notifications
    value: true

  field theme
    type: select
    label: Theme
    options: System, Light, Dark

  button save
    label: Save changes
    variant: primary
:::
```

A renderer can choose its own visual style while still understanding that this contains a heading, switch, select and primary button.

Wireframes can also describe multiple screens, phone/tablet/desktop viewports, tabs, images, forms, cards, alerts, tables and simple interactions such as `goto`.

See [`blocks/wireframe.md`](./blocks/wireframe.md).

## For LLMs

When creating GlanceMD:

```text
Keep normal explanation in Markdown.
Use GlanceMD only where structured information is easier to scan.
Keep model, api, mcp, tree and changeset inline.
Use embed or wireframe for richer external/interactive content when needed.
Describe meaning, not visual styling.
Keep blocks concise and human-readable in source form.
Preserve unknown GlanceMD fields when editing existing documents.
```

An LLM should prefer ordinary Markdown unless a GlanceMD block makes the information materially easier to understand.

Full syntax: [`SPEC.md`](./SPEC.md)

## For renderer authors

A minimal renderer can be built in six steps:

1. Parse Markdown normally.
2. Detect `:::<block>` ... `:::` regions.
3. Parse each supported block into semantic data.
4. Render it using the host client's own UI conventions.
5. Preserve unsupported blocks as source text.
6. Keep the original source round-trippable.

A renderer may support only some GlanceMD blocks.

### Renderer rules

- Keep the experience document-first, not dashboard-first.
- Do not require a particular framework, icon set or CSS system.
- Trees may use native file icons and collapsing.
- Wireframes may switch between declared viewports and screens.
- `height` on `embed` and `wireframe` is a renderer hint only.
- External executable content should be sandboxed.
- Unknown properties should be preserved where possible.

### Conformance

**Preserve** — recognise and retain GlanceMD source.  
**Understand** — parse supported blocks semantically.  
**Render** — provide richer native rendering for supported blocks.

## Design rules

1. **Document first** — it should still feel like Markdown.
2. **Inline by default** — external artifacts are the exception.
3. **Semantic, not visual** — the spec defines meaning, not pixels.
4. **Renderer freedom** — clients choose presentation and interaction.
5. **Readable source** — rendering should enhance comprehension, not be required for it.
6. **60-second test** — GlanceMD should reduce time-to-understanding, not add ceremony.

## Status

GlanceMD is an early draft. Syntax may change before a stable release.

Start with [`SPEC.md`](./SPEC.md), or browse the individual block specifications in [`blocks/`](./blocks/).

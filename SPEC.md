# GlanceMD Specification

Status: **Draft 0.1**

GlanceMD extends Markdown with semantic fenced blocks intended to make technical documents faster to understand while remaining readable as source.

The specification defines syntax and semantics. It does not define a visual design system.

## 1. Core syntax

A block begins with `:::<type>` and ends with `:::`.

```md
:::api
GET /items
  purpose: List items
:::
```

Block names are lowercase ASCII identifiers.

The current standard block types are:

- `model`
- `api`
- `mcp`
- `tree`
- `changeset`
- `embed`
- `wireframe`

Unknown blocks must be preserved by tools that edit or round-trip GlanceMD documents.

## 2. Parsing model

Inside a block, GlanceMD uses a deliberately small indentation-based grammar.

### 2.1 Statements

A statement is a non-empty line beginning at the current indentation level.

Examples:

```text
table User
GET /items
folder src
button continue
```

### 2.2 Properties

Properties use `key: value` syntax and belong to the closest preceding parent statement at a lower indentation level.

```text
button continue
  label: Continue
  variant: primary
```

### 2.3 Repeated properties

A property name may appear more than once when the block specification permits it.

```text
alternative: Option A
alternative: Option B
```

Parsers should preserve order.

### 2.4 Quoted text

Double quotes may be used where text needs to preserve surrounding whitespace or contain syntax-like characters.

```text
text heading "Create account"
```

Renderers should display the unquoted value.

### 2.5 Lists

Some properties accept comma-separated values.

```text
options: Small, Medium, Large
```

A block-specific specification may also define repeated child statements instead.

## 3. Inline and external content

GlanceMD uses two content models.

### 3.1 Inline semantic blocks

The following blocks are expected to be inline by default:

- `model`
- `api`
- `mcp`
- `tree`
- `changeset`

Their source should remain useful without a renderer.

### 3.2 Artifact blocks

The following blocks may reference external artifacts:

- `embed`
- `wireframe`

External paths are resolved relative to the containing Markdown document unless a host client defines another resolution mechanism.

Clients must not silently execute untrusted external content.

## 4. Renderer hints

Renderer hints influence presentation but do not change semantic meaning.

Examples include:

```text
height: 480
viewport: desktop
```

A conforming renderer may ignore unsupported hints.

`height` is explicitly non-semantic and should be treated as an initial or preferred height only. Interactive renderers may allow users to resize `embed` and `wireframe` blocks.

## 5. Source preservation

Tools that edit GlanceMD should preserve:

- unknown block types
- unknown properties
- property order where practical
- block order
- ordinary Markdown surrounding the blocks

A tool must not delete unknown syntax merely because it cannot render it.

## 6. Fallback behaviour

A non-GlanceMD Markdown viewer may display the block source as plain text.

A GlanceMD-aware renderer that does not support a specific block should provide one of:

1. the raw block source
2. a neutral unsupported-block representation containing the source

It must not hide the content entirely.

## 7. Conformance

### Level 1 — Preserve

A client:

- detects GlanceMD blocks
- preserves unsupported block source
- does not corrupt surrounding Markdown

### Level 2 — Understand

A client:

- parses one or more block types into semantic structures
- distinguishes semantic values from renderer hints

### Level 3 — Render

A client:

- provides a native presentation for one or more supported blocks
- preserves the source meaning
- provides accessible interaction where relevant

Clients should state block support explicitly, for example:

```text
GlanceMD Render support: api, tree, wireframe
GlanceMD Understand support: model, mcp, changeset
```

## 8. Design requirements

A standard GlanceMD block should meet these requirements:

1. **Readable in source form.**
2. **Semantic rather than visual.**
3. **Useful across different renderers.**
4. **More expressive for its task than ordinary prose or a generic code block.**
5. **Small enough for humans and language models to edit safely.**
6. **Independent of a specific framework, client, or vendor.**

## 9. Versioning

Until a stable specification exists, documents should not assume forward compatibility between draft versions.

A future stable version may introduce a document-level declaration. Draft 0.1 intentionally avoids requiring front matter or a global version marker.

## 10. Block specifications

Normative details are defined in:

- [Model](./blocks/model.md)
- [API](./blocks/api.md)
- [MCP](./blocks/mcp.md)
- [Tree](./blocks/tree.md)
- [Change Set](./blocks/changeset.md)
- [Embed](./blocks/embed.md)
- [Wireframe](./blocks/wireframe.md)

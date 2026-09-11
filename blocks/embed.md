# `embed`

The `embed` block references an external artifact for inline presentation inside the document.

It is intentionally simple. `embed` presents an artifact; it does not describe the artifact's internal semantics.

## Syntax

```md
:::embed
src: ./artifacts/demo.html
height: 420
:::
```

## Properties

### `src`

Required. Path or URI of the external artifact.

Relative paths are resolved relative to the containing Markdown document unless the host client defines another resolution mechanism.

### `height`

Optional renderer hint representing an initial or preferred height.

It is not semantic. Interactive renderers may allow users to resize the embedded region.

### `mode`

Optional hint describing the preferred presentation mode.

Examples:

```text
mode: static
mode: interactive
```

Clients may ignore unsupported modes.

## Security

A renderer must not blindly execute untrusted embedded content.

Clients should apply appropriate sandboxing, origin restrictions, content policies, and user-consent rules for executable artifacts.

## Renderer guidance

A renderer may:

- display HTML in a sandboxed frame
- render SVG or images directly
- show a static preview
- provide an open-in-new-view action
- allow vertical resizing

If the artifact cannot be displayed, the renderer should show the source reference rather than hiding the block.

# `mcp`

The `mcp` block represents an MCP server in MCP terms rather than disguising it as an HTTP API.

## Syntax

```md
:::mcp
server notes-mcp

tool get_note
  access: read
  input: noteId
  output: Note
  approval: none

tool delete_note
  access: write
  input: noteId
  output: Result
  approval: required

resource note://{id}

capability prompts: supported
capability sampling: false
:::
```

## Statements

### `server <name>`

Declares the server being described.

### `tool <name>`

Declares a tool.

Common properties:

- `access` — `read`, `write`, or another concise permission description
- `input` — input shape or important arguments
- `output` — output shape
- `approval` — `none`, `required`, or another explicit policy
- `purpose` — optional short human-readable purpose

### `resource <uri-template>`

Declares an MCP resource URI or template.

### `capability <name>: <value>`

Declares server capabilities relevant to understanding the integration.

## Semantics

The MCP block should make these concepts visible when present:

- server identity
- tools
- resources
- inputs and outputs
- read/write intent
- approval boundaries
- capabilities

A renderer may group or collapse tools, but it should not translate MCP concepts into unrelated HTTP terminology.

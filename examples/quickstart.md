# Personal notes application

This example shows several GlanceMD blocks in one document while keeping the surrounding explanation as ordinary Markdown.

## Data model

:::model
table Note
  id: uuid
  title: text
  body: text
  createdAt: datetime

table Tag
  id: uuid
  name: text

relationship Note many -> many Tag
:::

## API

:::api
GET /notes
  auth: user
  purpose: List notes
  responses: 200

POST /notes
  auth: user
  purpose: Create a note
  input: CreateNote
  output: Note
  responses: 201, 422

DELETE /notes/{id}
  auth: user
  purpose: Delete a note
  responses: 204, 404
:::

## MCP

:::mcp
server notes-mcp

tool get_note
  access: read
  input: noteId
  output: Note
  approval: none

tool create_note
  access: write
  input: title, body
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

## Files

:::tree
root src

folder notes
  added NoteService.ts
    note: Note persistence and retrieval

  added NotePage.tsx
    note: Main notes screen

  added NoteEditor.tsx
    note: Create and edit notes

changed app.ts
  note: Register notes routes

relevant types.ts
  note: Shared application types
:::

## Expected changes

:::changeset
added component NoteService
  reason: Own note persistence and retrieval

added api POST /notes
  reason: Create notes

added ui NoteEditor
  reason: Create and edit note content

changed file src/app.ts
  reason: Register notes routes
:::

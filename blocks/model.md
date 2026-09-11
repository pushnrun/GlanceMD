# `model`

The `model` block presents the important shape of data without requiring a full ERD.

It is intentionally table/entity first. Relationships are secondary.

## Syntax

```md
:::model
table User
  id: uuid
  name: text
  email: text

table Post
  id: uuid
  userId: fk User
  title: text

relationship User 1 -> many Post
:::
```

## Statements

### `table <name>`

Defines a table or entity.

Indented `field: type` pairs define its important fields.

```text
table User
  id: uuid
  email: text
```

A renderer may choose to show only a subset initially when the block is large, but it must preserve access to all declared fields.

### `relationship <expression>`

Defines a lightweight relationship between declared tables/entities.

```text
relationship User 1 -> many Post
relationship Post many -> many Tag
```

The relationship expression is intentionally human-readable in Draft 0.1. Renderers should not require database-specific cardinality notation.

## Semantics

The `model` block is for comprehension, not schema generation.

It does not replace database migration files, ORM models, JSON Schema, or DDL.

Renderers may:

- show tables in a grid
- visually distinguish foreign keys
- reveal relationships on demand
- collapse large field lists
- link table names to relevant source files when host context is available

Renderers should avoid turning small models into dense ER diagrams by default.

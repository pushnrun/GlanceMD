# `changeset`

The `changeset` block describes expected implementation impact across different kinds of technical artifacts.

It is broader than a file diff. A change set may include files, components, APIs, entities, UI, configuration, or other named targets.

## Syntax

```md
:::changeset
added component NoteService
  reason: Own note persistence and retrieval

changed api POST /notes
  reason: Validate tags before persistence

changed file src/app.ts
  reason: Register note routes
:::
```

## Change statements

Each change begins with a state, target type, and target name.

```text
added component NoteService
changed api POST /notes
removed file src/legacy.ts
```

Standard states are:

- `added`
- `changed`
- `removed`

Target types are intentionally open-ended. Common values include:

- `file`
- `component`
- `api`
- `entity`
- `ui`
- `config`
- `test`

## Properties

### `reason`

Short explanation of why the target changes.

### `risk`

Optional human-readable risk level or description.

### `depends-on`

Optional dependency on another change target.

## Semantics

The block communicates implementation intent, not an exact patch.

Renderers may group changes by state or target type, but should preserve original order when order carries meaning.

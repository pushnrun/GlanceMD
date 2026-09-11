# `api`

The `api` block presents an API surface in a form optimised for human comprehension rather than exhaustive machine description.

It is not a replacement for OpenAPI.

## Syntax

```md
:::api
GET /notes
  auth: user
  purpose: List notes
  responses: 200

POST /notes
  auth: user
  purpose: Create a note
  responses: 201, 422
:::
```

## Endpoint statement

An endpoint begins with an HTTP method followed by a path.

```text
GET /notes/{id}
```

Standard methods include `GET`, `POST`, `PUT`, `PATCH`, and `DELETE`.

## Standard properties

### `purpose`

Short human-readable description of the operation.

### `auth`

Human-readable access requirement.

Examples:

```text
auth: public
auth: user
auth: admin
auth: api-key
```

### `responses`

Comma-separated important response codes.

```text
responses: 200, 404
```

### `input`

Short description or named schema representing request input.

```text
input: CreateNote
```

### `output`

Short description or named schema representing the successful response.

```text
output: Note
```

### `processing`

Optional concise explanation of important processing steps.

```text
processing: validate -> persist -> publish
```

## Rendering guidance

A renderer may:

- group endpoints by path or resource
- visually distinguish methods
- expand request and response examples
- show status codes and auth in compact columns
- collapse less important operations

The default presentation should favour method, path, purpose, and auth over exhaustive protocol detail.

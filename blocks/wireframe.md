# `wireframe`

The `wireframe` block describes low-fidelity user interfaces as semantic structure rather than HTML or pixel coordinates.

Its purpose is to let a document contain inspectable UI ideas that different clients can render in their own visual style.

`wireframe` is intentionally not a replacement for production UI code or a design tool.

## Example

```md
:::wireframe
height: 620
viewport: desktop
viewports: phone, tablet, desktop
screen: profile
interactive: true

section Profile
  text heading "Edit profile"
  text body "Update your personal details"

  image avatar
    ratio: 1:1
    placeholder: Profile image

  field name
    type: text
    label: Name
    value: Alex Morgan

  field theme
    type: select
    label: Theme
    options: System, Light, Dark
    value: System

  row
    field notifications
      type: switch
      label: Notifications
      value: true

    field newsletter
      type: checkbox
      label: Email newsletter
      value: false

  row
    button cancel
      label: Cancel
      variant: secondary

    button save
      label: Save
      variant: primary
      action: goto confirmation

screen confirmation
  text heading "Saved"
  text body "Your profile has been updated."

  button done
    label: Done
    variant: primary
:::
```

## Top-level properties

### `height`

Optional renderer hint for initial block height.

Interactive renderers may provide a vertical resize handle. The chosen height may be remembered locally by the host client.

### `viewport`

Initial viewport name.

```text
viewport: desktop
```

### `viewports`

Comma-separated supported viewports.

```text
viewports: phone, tablet, desktop
```

Standard names are currently:

- `phone`
- `tablet`
- `desktop`

These names describe responsive presentation classes, not physical device models or exact pixel sizes.

### `screen`

Initial named screen when the block defines multiple screens.

### `interactive`

Boolean hint indicating that supported actions should be interactive when the renderer permits it.

## Screens

A named screen is declared with:

```text
screen payment
```

All nested content belongs to that screen until the next statement at the same or lower indentation level.

If a block contains no explicit `screen`, a renderer may treat its direct content as one implicit screen.

## Layout primitives

### `section <label>`

Logical document/UI section.

### `aside <label>`

Secondary content region.

### `row`

Groups child controls horizontally where the viewport permits it.

On narrow viewports, renderers may stack row children vertically.

### `layout <kind>`

Declares a larger layout arrangement.

Draft 0.1 defines:

```text
layout split
```

Renderers decide exact proportions and responsive behaviour unless future properties explicitly describe them.

## Text

```text
text heading "Account settings"
text strong "Current plan"
text body "Manage your account preferences."
```

Standard text styles:

- `heading`
- `strong`
- `body`

Renderers may support additional styles but should preserve unknown ones.

## Images

```text
image hero
  ratio: 16:9
  placeholder: Cover image
```

An image may also reference a source:

```text
image avatar
  src: ./assets/avatar.jpg
  alt: Profile avatar
```

Common properties:

- `src`
- `alt`
- `ratio`
- `placeholder`

A renderer may use a neutral placeholder when `src` is absent.

## Fields

Fields use:

```text
field <id>
  type: <type>
  label: <label>
```

Draft 0.1 field types:

- `text`
- `textarea`
- `select`
- `checkbox`
- `radio`
- `switch`

### Common field properties

- `label`
- `value`
- `placeholder`
- `options`
- `disabled`
- `required`
- `help`
- `error`

Example:

```text
field country
  type: select
  label: Country
  options: France, Germany, Italy
  value: France
```

Renderers should represent field intent rather than emulate browser controls exactly.

## Buttons

```text
button continue
  label: Continue
  variant: primary
  action: goto payment
```

Common variants:

- `primary`
- `secondary`
- `quiet`
- `danger`

Variants are semantic emphasis hints. Renderers own visual styling.

## Tabs

```text
tabs account-tabs
  tab profile "Profile"
  tab security "Security"
  tab billing "Billing"
```

The first tab may be treated as active unless another state is specified.

Renderers may make tabs interactive.

## Supporting UI primitives

### Badge

```text
badge state
  label: Draft
```

### Progress

```text
progress setup
  value: 60
```

`value` is interpreted as a percentage from 0 to 100 in Draft 0.1.

### Card

```text
card summary
  text strong "Basic plan"
  text body "Renews monthly"
```

A card represents grouping, not a mandatory visual card style. A document-oriented renderer may use a border, divider, indentation, or another lightweight grouping treatment.

### Alert

```text
alert warning
  tone: warning
  text: Your session will expire soon
```

Common tones:

- `info`
- `success`
- `warning`
- `danger`

## Actions

Actions describe interaction intent.

Draft 0.1 defines:

### `goto <screen>`

```text
action: goto confirmation
```

Moves the wireframe to another named screen.

### `set <key>=<value>`

```text
action: set status=draft
```

Updates local wireframe state.

A renderer that does not support interaction may display action intent without executing it.

Future versions may add other actions. Tools must preserve unknown action expressions.

## Interaction state

Wireframes may model values such as switches, selected options, active screens, validation errors, and progress.

This state is illustrative only. It must not be treated as application data or executed against external systems.

## Renderer guidance

A renderer should:

- keep wireframes visibly low fidelity
- avoid implying production-ready visual design
- support declared viewport switching when practical
- allow navigating named screens where interaction is supported
- allow vertically resizing the block where practical
- adapt rows and split layouts responsively
- keep controls recognisable while following the host client's visual language
- preserve the surrounding document flow

A renderer may provide:

- a dedicated expanded canvas
- annotations
- named scenarios
- state inspection
- keyboard navigation
- reset controls

These renderer features do not change the underlying block semantics.

## Why not HTML?

HTML describes a rendered document/application structure and can contain arbitrary behaviour.

`wireframe` deliberately describes a smaller set of UI intent:

- what controls exist
- how they are grouped
- which screens exist
- which responsive viewport classes matter
- what simple interactions are expected

This makes wireframes easier to generate, edit, review, diff, and render safely across different clients.

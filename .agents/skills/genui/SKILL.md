---
name: genui
description: Author GenUI fences and inline Markdown icons and badges.
---

# GenUI authoring

Use Markdown for prose, lists, and tables. Use a `genui` fence for catalog
layouts, controls, or dynamic values. Keep controls and displays sharing state
in one fence, even across cards.

Declare state before the JSX-like markup with
`{@state const [x, setX] = useState(init)}`. Read `x` in expressions. Write with
`setX(value)` or `setX(prev => prev + 1)`. Slots keep committed values across
revisions. While streaming, complete opening tags render and the unfinished
tail stays hidden.

Use `prop="text"`, `prop={expr}`, or bare `prop` for true. Keep tags in markup.
Use `{expr}` for text and prop values, including ternaries. For variable-length
lists, join strings inside one `text` tag. Keep JSX, fragments, and statements
out of expression holes. Arrow callback bodies can use statements.

## Inline Markdown

`GENUI_INLINE_TAGS` allows `<icon name="info" />` and
`<badge tone="warning">\*Pending\*</badge>` in prose, lists, and table cells.
Write them directly, outside backticks. Use quoted literal props and plain-text
badge labels. Escape visible Markdown punctuation. Braces in labels are literal.
Use a fence for state, callbacks, nested markup, or dynamic labels and tones.

Icons take a kebab-case Lucide `name` and optional `color`
(danger/success/warning/accent). Unknown names render nothing. Inline size is
14 px. Use fenced `size={20}` for custom sizing. The `inline` prop is ignored.

## Catalog index

- `card` groups a section. `heading` takes `level` 1–6 (default 3).
- `row` wraps and centers vertically. `column` stacks. Both take numeric `gap` in px.
- `divider` is self-closing. `spacer` fills space with optional minimum `size` in px.
- `text` takes boolean `muted`. Text trims at expression boundaries. Preserve
  spaces with one template literal, e.g. ``<text>{`Current value: ${value}%`}</text>``.
- `badge` takes `tone`: neutral (default), success, warning, danger, running.
- `icon` takes the props above and, in a fence, numeric `size` in px.
- `button`: `onClick={() => setX(init)}`, `variant`, `size`.
- `input`: string `value`, `onValueChange={(v) => setX(v)}`, `placeholder`.
- `checkbox` / `switch`: boolean `checked`, `onCheckedChange` (boolean).
- `select`: string `value`, `onValueChange` (string or null), `placeholder`,
  `items` (strings or `{value, label}` objects).
- `slider`: numeric `value`, `onChange` (number), `min` (0), `max` (100), `step` (1).

Bind controls to state and call the setter with the event value. All controls
accept boolean `disabled`. Button variants: secondary (default), primary,
ghost, destructive, link. Sizes: medium (default), mini, small, large.

See [expressions](references/expressions.md) for advanced state, supported JS,
capabilities, and diagnostics.

## Validate before shipping

In chat, an unmountable surface falls back to its fenced code block.
Diagnostics stay hidden from readers.

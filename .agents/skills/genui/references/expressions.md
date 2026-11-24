# GenUI expressions

An initializer may read earlier slots. For local variables, use an arrow IIFE:
`{@state const [x, setX] = useState((() => { const n = 2; return n * 3; })())}`.
Functional setters read the latest committed value, including earlier writes
in the same callback. Each write re-evaluates the view. Callbacks capture
their scope. Compute derived values in expressions.

Supported JS includes literals, operators, template strings, arrows, calls,
member access, and destructuring in declarations. Array methods include `map`,
`filter`, `find`, `findIndex`, `findLast`, `forEach`, `every`, `some`, `flatMap`,
`sort`, `reduce`, and `reduceRight` with arrows.
Example: `items.filter(x => x.active).map(x => x.label).join(', ')`.

Globals: `Math`, `JSON`, `Number`, `String`, `Boolean`, `Array`,
`Object.keys/values/entries/assign/fromEntries`, `isNaN`, `isFinite`,
`parseFloat`, `parseInt`, `undefined`, `NaN`, `Infinity`. No browser globals,
imports, async, or prototype access. Use only `lody.*` capabilities the host
provides. A missing capability yields a diagnostic.

## Error shapes

- Invalid state directive: `state`.
- Invalid markup or attribute: `jsx`. Intact parts can still render.
- Unknown tag: `catalog` and a visible `<tag>` placeholder.
- Thrown expression or exceeded step budget: `eval`.

Chat hides diagnostics, withholds the unfinished streaming tail, and falls
back to the fenced code block if the surface cannot mount. A direct
`GenuiSurface` without `fallback` can show its diagnostics view.

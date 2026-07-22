---
name: dyslexia-friendly-code
description: Shape generated and reformatted code so a reader with dyslexia can scan it easily. Use this skill whenever writing, editing, or reformatting code, data literals, config, or JSON — including object/array literals, function signatures, imports, and inline collections. Favor vertical layout (one item per line) over long horizontal lines, keep names visually distinct, and align consistently. Trigger on any coding task, even when the user did not explicitly ask for it.
---

# dyslexia-friendly-code

The reader has dyslexia. Code is not just correct — it is laid out so the eye can track it without losing its place. Dense, horizontally-packed lines force re-reading. Vertical, evenly-spaced structure does not.

## What dyslexia is

Dyslexia is a common, lifelong difference in how the brain processes written language. It is not about intelligence or effort. It mainly affects the speed and accuracy of connecting written symbols to sound and meaning, so reading takes more effort and mistracking a line or transposing similar shapes is easy. It often comes with slower reading, weaker working memory for text, and quick visual fatigue on dense material. Layout that reduces the amount the eye has to scan and track directly reduces that load — which is what every rule in this skill is for.

## What dyslexia changes about reading code

Four facts drive every rule below:

1. Long horizontal lines are hard to track. The eye loses its place scanning left-to-right across many tokens. One item per line removes the scan.
2. Visually similar names blur together. `list`/`lst`, `id`/`Id`/`iD`, `data`/`date`, single-letter names, and `l`/`I`/`1` or `O`/`0` are read wrong.
3. Inconsistent spacing breaks the rhythm. When indentation and alignment shift, the reader re-anchors on every line.
4. Walls of text hide structure. Blank lines and grouping let the shape of the code carry meaning the words don't have to.

## Rules

### 1. One property per line in object and data literals

Any object literal with 2 or more properties goes vertical: opening brace, one property per line, closing brace. This is the single highest-impact rule. Single-property objects may stay inline — they are already one thing.

Bad:
```ts
{ name: "Aino", model: "/models/aino.glb", tier: "owned", level: 20 }
```

Good:
```ts
{
  name: "Aino",
  model: "/models/aino.glb",
  tier: "owned",
  level: 20
}
```

This applies to arrays of records, JSON files, config objects, and inline options — anywhere fields are packed onto one line.

### 2. One item per line in arrays and parameter lists

If a collection or signature runs long, break it so each element sits on its own line. Short, obviously-scannable lists (2–3 primitives) can stay inline.

Bad: `function make(name, model, tier, level, poster, alt) {`

Good:
```ts
function make(
  name,
  model,
  tier,
  level,
  poster,
  alt,
) {
```

### 3. Names must be visually distinct

Spell names out. Avoid abbreviations that collapse into each other, single letters, and sequences of look-alike characters. A name should be recognizable by shape, not by careful spelling-out.

Bad: `const l = lst.filter(x => x.id !== iD)`
Good: `const activeUsers = users.filter(user => user.id !== currentId)`

Avoid `l`, `I`, `O` as standalone names. Prefer distinct multi-character names.

Prefer camelCase for names. It is strongly preferred in the dyslexic community: the case changes give each word a distinct shape and a built-in boundary the eye can catch, without the low-contrast gaps of `snake_case` or the shouting uniformity of `SCREAMING_CASE`. Use `activeUsers`, not `active_users` or `activeusers`. Follow the language's hard conventions where they exist (e.g. PascalCase for React components and types, UPPER_SNAKE for true constants if the project already does so), but default to camelCase everywhere there is a choice.

### 4. Consistent, predictable spacing

Keep indentation uniform (match the file's existing width). Align related structure so the eye anchors in the same column every line. Never mix tabs and spaces. Do not hand-pack lines to "save space."

### 5. Group with blank lines

Separate logical chunks with a single blank line. Imports, then a blank line. Constants, then a blank line. One idea per paragraph of code. Blank lines are structure, not waste.

### 6. Comment above, not trailing

Put a comment on its own line above the code it describes, not trailing at the end of a long line. Trailing comments push the line wider and force a horizontal scan to find them.

Bad: `const MAX = 90; // ascension ceiling`

Good:
```ts
// Ascension ceiling
const MAX = 90
```

### 7. No comment blocks except licences

Never write a large block of comments to explain code. A wall of comment text is as hard to scan as a wall of code. Keep explanations to a single short line above the code. The only place a multi-line comment block belongs is a file's licence header.

Bad:
```ts
/*
 * This function walks the character list, sorts it by tier,
 * then by level descending, and finally alphabetically. It is
 * used by the render loop below to decide display order...
 */
```

Good:
```ts
// Display order: want first, then level desc, then A–Z
```

### 8. Title every file with its own name

Every file opens with a header comment naming the file. If the file carries a licence, the licence goes in the same block, under the filename. This gives the reader a fixed anchor at the top of every file.

```ts
/* genshin/page.tsx
 * MIT Licence — (c) Clove Twilight
 */
```

With no licence, the filename alone is enough:

```ts
/* genshin/page.tsx */
```

Use the comment syntax of the file's language (`/* */` for TS/JS/CSS, `#` for shell/Python, `<!-- -->` for HTML). The filename is always the first line.

The licence line is persistent. Never drop or alter an existing licence header when editing a file — carry it through unchanged. When creating a new file, reuse the licence already used elsewhere in the project. If the licence is unclear or the project has none, ask which licence to use, and leave the licence line blank (filename only) until told.

## Reformatting existing code

When asked to make a file dyslexia-friendly:

1. Only expand object literals that have 2+ properties. Leave single-property objects alone.
2. Preserve exact values — strings, template literals, type annotations, nested calls. Split only top-level commas, never commas inside quotes, brackets, parens, or backticks.
3. Do not reorder keys or change logic. Layout only.
4. Verify after: run the type checker / linter and validate JSON. Layout changes must never change behavior.

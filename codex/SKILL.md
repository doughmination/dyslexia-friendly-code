---
name: dyslexia-friendly-code
description: Format generated, edited, and refactored code for easy visual scanning by a reader with dyslexia. Apply on all coding tasks, including code generation, formatting, JSON, config files, literals, imports, signatures, and collections. Prioritize vertical structure, distinct naming, consistent spacing, and low visual density.
---

# Dyslexia-Friendly Code

When writing or modifying code, optimize for visual tracking as well as correctness.

The goal is to reduce:
- long horizontal scans
- visually similar identifiers
- inconsistent spacing
- dense blocks of code

Prefer layouts where the structure is obvious from the shape of the code.

## Formatting Rules

### Objects and data literals

Use vertical formatting for objects with two or more properties.

Prefer:

```ts
const character = {
  name: "Aino",
  model: "/models/aino.glb",
  tier: "owned",
  level: 20,
}
```

Avoid:

```ts
const character = { name: "Aino", model: "/models/aino.glb", tier: "owned", level: 20 }
```

Apply this to:

- object literals
- JSON
- configuration objects
- arrays of objects
- inline options

Do not expand single-property objects unless needed for clarity.

### Arrays and parameters

Use one item per line when lists become difficult to scan.

Prefer:

```ts
function createCharacter(
  name,
  model,
  tier,
  level,
  poster,
  alt,
) {
}
```

Avoid:

```ts
function createCharacter(name, model, tier, level, poster, alt) {
}
```

Short lists of 2–3 simple values may remain inline.

### Naming

Choose names that are visually distinct.

Prefer:

```ts
const activeUsers = users.filter(
  user => user.id !== currentId,
)
```

Avoid:

```ts
const l = lst.filter(x => x.id !== iD)
```

Rules:

- Avoid single-letter variable names except conventional cases (`i` in very small loops, mathematical notation).
- Never use ambiguous names such as `l`, `I`, `O`, `0`.
- Avoid abbreviations that collapse into similar shapes.
- Prefer descriptive camelCase names.
- Preserve language conventions where required:
  - PascalCase for React components/types/classes
  - project-specific constant styles
  - framework conventions

### Spacing and grouping

Keep code visually predictable.

Rules:

- Match the existing indentation style.
- Never mix tabs and spaces.
- Do not compress lines to save vertical space.
- Use blank lines between logical sections.

Preferred structure:

```ts
import something from "something"

const defaultConfig = {
  enabled: true,
}

function runTask() {
}
```

### Comments

Place comments above code.

Prefer:

```ts
// Maximum ascension level
const maxLevel = 90
```

Avoid:

```ts
const maxLevel = 90 // Maximum ascension level
```

Keep comments short. Avoid large explanatory comment blocks.

Allowed:

- short comments above complex code
- licence headers

Avoid:

- paragraphs explaining obvious code
- comment walls

### File headers

Every new file should begin with a filename header.

JavaScript/TypeScript/CSS:

```ts
/* path/to/file.ts */
```

Python/shell:

```py
# path/to/file.py
```

HTML:

```html
<!-- path/to/file.html -->
```

If the project uses a licence header:

- preserve existing licence headers exactly
- place the filename first
- do not remove or rewrite licence text

If creating a file in a project with an unclear licence:

- use only the filename header
- do not invent a licence

## Reformatting Existing Code

When asked to make code dyslexia-friendly:

1. Change layout only.
2. Preserve:
   - values
   - logic
   - ordering
   - types
   - imports
   - behavior
3. Expand objects with 2+ properties.
4. Split lists only at safe boundaries.
5. Never split:
   - strings
   - template literals
   - nested expressions
   - function calls
   - brackets or grouped expressions
6. After formatting:
   - run available validation
   - run type checks or linters when available
   - validate JSON/config syntax

Formatting must never change program behavior.

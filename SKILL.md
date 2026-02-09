---
name: scss-bem-standards
description: Use when writing, reviewing, or refactoring Angular component styles (SCSS/CSS). Triggers on BEM naming issues, deep nesting, non-flat selectors, or hard-coded values instead of design tokens.
---

# SCSS BEM Standards

## Overview

Use this skill to keep component styles predictable, reusable, and easy to review.
Prefer component-scoped BEM classes and keep selectors flat by default.

## Workflow

1. Identify the component selector and define one block name.
2. Map required elements and modifiers before editing template or style files.
3. Implement classes in template first, then write SCSS with flat selectors.
4. Validate against the checklist in `references/review-checklist.md`.
5. If selector context needs more than one descendant level, split into child components.

## Core Rules

1. Use one BEM block per component and keep the block name stable.
2. Use only `block`, `block__element`, `block--modifier`, `block__element--modifier`.
3. Keep nesting depth to two levels in naming; do not create `block__element__sub`.
4. Keep selectors flat by default; allow at most one descendant level only when it improves readability.
5. If using a descendant selector, keep both sides in the same block context (for example `.block__a .block__b`).
6. Do not chain descendants beyond one level (for example `.block__a .block__b .block__c` is invalid).
7. Allow `>`, `+`, `~` when used within the same block context and kept to one level.
8. Avoid tag-qualified selectors and id selectors for component styling.
9. Use modifiers for variants and states; keep base class present at the same time.
10. Use global design tokens (for example `var(--space-*)`, `var(--color-*)`) instead of hard-coded values.
11. Keep component styles in `*.component.scss`; do not move feature-specific styles to global files.

## Angular Integration Rules

1. Bind modifiers with class bindings, for example `[class.card--active]="isActive()"`.
2. Keep template class names semantic and aligned with BEM map.
3. Prefer modifier classes first; use one-level descendant selectors only when necessary.
4. Use Angular native control flow (`@if`, `@for`, `@switch`) without changing class semantics.

## One-Level Descendant Pattern

Use this pattern only when a context rule is clearer than adding many one-off modifiers.

Valid:

```scss
.card {
  &__header &__badge {
    margin-left: var(--space-2);
  }

  &__row > &__cell {
    padding: var(--space-2);
  }

  &__title + &__meta {
    margin-top: var(--space-1);
  }

  &__field ~ &__field {
    margin-top: var(--space-2);
  }
}
```

Invalid:

```scss
.card {
  &__header &__meta &__icon {
    color: var(--color-zinc-500);
  }
}
```

## Output Contract

When implementing or refactoring, produce:

1. A short class map (`block`, `elements`, `modifiers`).
2. Updated template snippets with BEM classes.
3. Updated SCSS snippets using flat BEM selectors.
4. A checklist result that marks pass/fail items from `references/review-checklist.md`.

## References

Use these references when needed:

1. `references/review-checklist.md` for review criteria and fix patterns.

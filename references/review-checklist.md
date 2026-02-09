# SCSS + BEM Review Checklist

Use this checklist after creating or refactoring component styles.

## 1) Block Scope

- [ ] Define exactly one primary block for the component.
- [ ] Match block intent to component responsibility.
- [ ] Keep block naming in kebab-case.

Fix pattern:

- If two unrelated blocks appear in one component, split into child components.

## 2) Element and Modifier Naming

- [ ] Use `block__element` for internal parts.
- [ ] Use `block--modifier` or `block__element--modifier` for variants.
- [ ] Keep base class present when applying modifiers.
- [ ] Avoid presentational element names (`left`, `red`, `big`).

Fix pattern:

- Rename positional names to semantic names (`left` -> `actions`, `title-row` -> `header`).

## 3) Selector Architecture

- [ ] Prefer flat selectors first (`.block__item`, `.block__item--state`).
- [ ] Allow descendant selectors only up to one level (`.block__a .block__b`).
- [ ] Keep descendant selectors inside the same block context.
- [ ] Do not chain descendants beyond one level (`.block__a .block__b .block__c`).
- [ ] Allow `>`, `+`, `~` only within the same block context and one level.
- [ ] Avoid tag-qualified selectors (`div.block`) and id selectors for component styling.
- [ ] Keep selectors class-based.

Fix pattern:

- Prefer explicit element/modifier classes.
- If a context rule is truly needed, keep it to one descendant level only.

## 4) Nesting Depth

- [ ] Do not create `block__element__subelement`.
- [ ] Keep SCSS nesting shallow and readable.
- [ ] Split child UI sections into separate components when context depth grows beyond one descendant level.

Fix pattern:

- Extract reusable section into a child component with its own block.

## 5) Token and Value Discipline

- [ ] Use design tokens for spacing, colors, radius, and typography.
- [ ] Avoid hard-coded spacing/color values unless explicitly approved.
- [ ] Preserve project spacing scale.

Fix pattern:

- Replace literal values with `var(--space-*)`, `var(--color-*)`, `var(--radius-*)`.

## 6) Angular Binding Pattern

- [ ] Apply modifiers using class bindings where state-driven.
- [ ] Keep state names consistent between TS signal/computed names and class modifiers.
- [ ] Do not let structural control flow change class naming logic.

Fix pattern:

- Move state-to-class logic into explicit bindings, not selector side effects.

## 7) Completion Gate

Approve only when all checks pass or each failing check has an explicit reason and follow-up action.

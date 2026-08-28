# Conventions

## Style (enforced by ESLint — build fails on any warning)

- 4-space indent, single quotes, semicolons, no trailing commas (`comma-dangle: never`).
- `operator-linebreak: before` (operators start the next line).
- One import per line (`import-newlines`), imports grouped and alphabetized
  (`import-x/order`): builtin+external, then internal, parent, sibling, index; blank line between groups;
  named imports alphabetized with types last.
- `consistent-type-imports` — use `import type { ... }`.
- `no-inferrable-types` except on properties.
- Max 2 statements per line; nonblock statement body goes on the next line.
- **Never** add an inline `eslint-disable` comment (hard project rule).

## Comments

- Only when the WHY is non-obvious (hidden constraint, workaround, invariant). No WHAT narration,
  no task/PR references. Existing code follows this — match it.

## Widget pattern

- Each widget is a class implementing `Widget` (`src/types/Widget.ts`): `getDefaultColor`,
  `getDescription`, `getDisplayName`, `getEditorDisplay`, `render`, `supportsRawValue`,
  `supportsColors`; optional `renderEditor`, `getCustomKeybinds`, `getHideableStates`,
  `handleEditorAction`, `getNumericValue`, `getCategory`.
- Register in `src/utils/widgets.ts` `widgetRegistry` map (type string -> instance).
- `render()` returns `string | null`; `null` = widget produced nothing (hidden / not applicable).
- Hiding uses the shared hideable system: `src/widgets/shared/hideable.ts`
  (`isHidden(item, key)`, `HideableState` constants like `NO_GIT_HIDEABLE_STATE`). A widget
  declares supported states via `getHideableStates()`; user selections stored in `item.metadata.hide`
  (comma-separated keys).

## Dual-runtime

- Guard Bun-specific APIs with a Node fallback (see stdin handling in `src/ccstatusline.ts`).

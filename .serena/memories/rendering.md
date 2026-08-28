# Rendering (src/utils/renderer.ts)

Large file. Read symbol bodies, not the whole file.

## Pipeline

1. `preRenderAllWidgets` — renders every widget once per line to `PreRenderedWidget[]`
   (`content`, `plainLength`, `widget`). Separators get empty content (handled later).
   `applyMergeTargetHiding` collapses decorative items (custom-text/custom-symbol) whose
   merge target rendered empty.
2. `calculateMaxWidthsFromPreRendered` — column widths for multi-line alignment.
3. `renderStatusLine` (non-powerline) or `renderPowerlineStatusLine` (powerline mode,
   `settings.powerline.enabled`).

## renderStatusLine assembly

- Builds `elements[]` (skips widgets whose pre-rendered `content` is falsy — they contribute
  nothing, but their `widget.merge` flag still influences neighbors).
- Explicit `separator` widgets: walk BACKWARD to find preceding content; spacing-only
  separators (`character: " "` or blank) get collapsed when they only trail empty widgets
  (`replacesSpacingSeparator`). There is NO forward look.
- `flex-separator` -> literal `'FLEX'` element; replaced later by distributed spaces
  (width known) or by `chalk.gray(' | ')` fallback when terminal width is undetected
  (piped/no-TTY — the common case under Claude Code).
- Trailing separators trimmed via a `while` loop at end of element build.
- `defaultPadding` (settings) + `defaultPaddingSide` ("both"/"left"/"right") wrap each
  non-separator element; `merge: 'no-padding'` omits padding between merged items,
  `merge: true` keeps it.
- Whole-line foreground gradient applied AFTER truncation (`maybeApplyForegroundGradient`).

## Separator spacing helpers

- `formatSeparator`: `|`->` | `, ` `->` `, `,`->`, `, `-`->` - `, else verbatim.
- `isSpacingSeparator`: separator whose char trims to empty.

## Known gotcha

A spacing-only separator that sits before a widget which renders nothing, followed by a
`flex-separator`, is not trimmed (backward-only collapse logic). In the no-width flex
fallback this yields a visible double space before the ` | `. Tests:
`src/utils/__tests__/renderer-separator-collapse.test.ts`, `renderer-flex-width.test.ts`.

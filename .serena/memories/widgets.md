# Widgets

## Registry

- `src/utils/widgets.ts` — `widgetRegistry: Map<string, Widget>`. `getWidget(type)`,
  `getAllWidgetTypes()`, `isKnownWidgetType(type)`.
- `src/utils/widget-manifest.ts` — metadata/manifest for the TUI widget picker.
- `src/widgets/index.ts` — barrel.

## Interface

`src/types/Widget.ts` — see `mem:conventions` for the method list. `render(item, context, settings)`
returns `string | null`.

## Shared helpers (src/widgets/shared/)

- `hideable.ts` — hide-state system. `HideableState` constants: `NO_GIT_HIDEABLE_STATE`,
  `NO_JJ_HIDEABLE_STATE`, `NO_REMOTE_HIDEABLE_STATE`, `NO_UPSTREAM_HIDEABLE_STATE`,
  `MERGE_TARGET_HIDDEN_HIDEABLE_STATE`. `isHidden(item, key, defaultEnabled?)`,
  `parseHideStates`/`getEnabledHideStates`/`setEnabledHideStates`. Selections stored in
  `item.metadata.hide` (comma-separated). Widget-local states (e.g. `zero`, `no-data`) are
  defined in the widget file itself.
- `symbol-override.ts` — user-overridable symbols/slots (`getSlotSymbol`, `SymbolSlot`,
  `renderSymbolSlotsEditor`, `formatSymbolPrefix`).
- `max-width.ts` — per-widget max width truncation + editor.
- `metadata.ts` — `isMetadataFlagEnabled` etc. for boolean metadata flags.
- `editor-display.ts` — `makeModifierText` for the "(modifier)" suffix in the editor list.
- `progress-bar.ts`, `context-slider.ts`, `context-inverse.ts`, `raw-or-labeled.ts`,
  `currency.ts`, `usage-display.ts`, `cache-metrics.ts`, `cache-scope.ts`, `git-remote.ts`.

## Families

Git (`Git*`), jujutsu (`Jj*`), tokens (`Tokens*`), context (`Context*`), speed (`*Speed`),
usage/cost (`*Usage`, `SessionCost`, `ExtraUsage*`, `Weekly*`), timers (`*Timer`, `SessionClock`),
Claude metadata (`Model`, `Version`, `OutputStyle`, `ThinkingEffort`, `VoiceStatus`, ...),
custom (`CustomText`, `CustomCommand`).

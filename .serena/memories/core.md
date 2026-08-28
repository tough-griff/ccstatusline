# ccstatusline — Core

Customizable status line formatter for Claude Code CLI. Dual mode:
- **Piped mode**: reads Claude Code status JSON from stdin, prints one formatted status line.
- **Interactive TUI mode**: React/Ink config editor when run with no stdin.

Also ships a hook handler and update checker.

## Entry point

- `src/ccstatusline.ts` — detects piped vs interactive (cross-platform stdin: Bun vs Node),
  routes to renderer or TUI. Also handles hook subcommands.

## Source map

- `src/tui/` — Ink TUI. `index.tsx` bootstraps, `App.tsx` is root nav/state, `components/` are screens.
- `src/widgets/` — one file per widget class implementing the `Widget` interface (`src/types/Widget.ts`).
  Shared widget helpers in `src/widgets/shared/`. Registry in `src/utils/widgets.ts` (see `mem:widgets`).
- `src/utils/renderer.ts` — status line assembly. Large file; two paths: `renderStatusLine`
  (non-powerline) and `renderPowerlineStatusLine`. See `mem:rendering`.
- `src/utils/config.ts` — settings load/save (`~/.config/ccstatusline/settings.json`) + `migrations.ts`.
- `src/utils/git.ts`, `git-remote.ts`, `git-review-cache.ts` — git integration via `execSync`.
- `src/utils/jj*.ts` — jujutsu (jj) VCS integration, parallels git.
- `src/utils/jsonl*.ts` — transcript (JSONL) parsing for token/block/speed metrics.
- `src/utils/claude-settings.ts` — Claude Code settings.json integration; respects `CLAUDE_CONFIG_DIR`.
- `src/utils/powerline*.ts` — powerline font detection/config.
- `src/types/` — shared types; `Widget.ts`, `Settings.ts`, `RenderContext.ts`, `StatusJSON.ts`.

## Project-wide invariants

- Must run on both Bun and Node 14+ (npm distribution target). No Bun-only APIs in runtime paths
  without a Node fallback.
- Runtime deps are bundled at build time (`--packages=external` only for the npm package meta).
- Never disable a lint rule via inline comment (project rule).
- Config lives outside the repo; never commit user settings.

See also: `mem:tech_stack`, `mem:suggested_commands`, `mem:conventions`, `mem:task_completion`,
`mem:rendering`, `mem:widgets`.

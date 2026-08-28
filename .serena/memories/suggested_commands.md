# Suggested Commands

Run from project root. Bun only.

- `bun install` — install deps (applies the ink patch).
- `bun run start` — launch interactive TUI.
- `bun run src/ccstatusline.ts` with piped JSON — test piped mode, e.g.
  `echo '{"model":{"id":"claude-sonnet-4-5-20250929[1m]"},"transcript_path":"test.jsonl"}' | bun run src/ccstatusline.ts`
  (`[1m]` suffix on model id selects the 1M context window).
- `bun run example` — pipes `scripts/payload.example.json` into the renderer.
- `bun test` / `bun test --watch` — run the Vitest suite.
- `bun run lint` — `bun tsc --noEmit` + ESLint, no writes. Use for type + lint check.
- `bun run lint:fix` — same but applies ESLint autofixes. Only when autofix is intended.
- `bun run build` — bundle to `dist/` then `postbuild` swaps `__PACKAGE_VERSION__` via
  `scripts/replace-version.ts`.

Do NOT invoke `eslint`, `npx eslint`, `tsc`, `bun tsc`, `tsx`, `vitest` directly — always the
`bun run` scripts above.

## Windows notes (dev machine is Windows 11, PowerShell)

- Shell is PowerShell; a Bash tool is also available for POSIX scripts.
- `build` script uses `rm -rf dist/*` — relies on a unix-ish shell (Bash tool / Git Bash), not cmd.
- Config path: `C:\Users\<user>\.config\ccstatusline\settings.json`.

# Tech Stack

- **Language**: TypeScript (strict; `typescript-eslint` strictTypeChecked + stylisticTypeChecked).
- **Runtime**: Bun for dev; output must also run on Node.js >= 14 (`--target-version=14` in build).
- **Package manager**: Bun (`bun install`). Do not use npm/yarn/pnpm.
- **TUI**: React 19 + Ink 6.2.0 (+ ink-gradient, ink-select-input).
- **Test runner**: Vitest API, executed via `bun test`. `vitest.config.ts` includes `src/**/*.test.{ts,tsx}`.
- **Lint**: ESLint 10 flat config (`eslint.config.js`), `@stylistic` (4-space indent, single quotes,
  semicolons), `import-x` (enforced import ordering + one-item-per-line via `import-newlines`).
- **Validation**: zod 4 for settings/JSON schemas.
- **Build**: `bun build` bundling `src/ccstatusline.ts` -> `dist/ccstatusline.js`.
- **Docs**: typedoc. **Video**: Remotion (`remotion/`), not part of normal dev.

## Version pins that matter

- `ink@6.2.0` is patched via `patchedDependencies` (`patches/ink@6.2.0.patch`) to fix macOS
  backspace (`\x7f`) being treated as delete. Applied automatically on `bun install`.
- `react`/`react-dom` pinned to exact `19.2.8`.

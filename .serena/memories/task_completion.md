# Task Completion Checklist

Run before considering a code change done:

1. `bun run lint` — type check (`bun tsc --noEmit`) + ESLint with `--max-warnings=0`.
   Must be clean. Fix root causes; never add `eslint-disable`.
2. `bun test` — full Vitest suite must pass. Add/adjust tests for behavior changes
   (tests live in `src/**/__tests__/`).
3. If renderer/settings behavior changed, sanity-check manually via piped input
   (`bun run example` or an `echo '{...}' | bun run src/ccstatusline.ts`).

Do not run `bun run build` unless packaging/distribution is the task.
Only commit when the user explicitly asks.

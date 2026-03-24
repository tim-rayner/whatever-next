# whatever-next

An opinionated Next.js harness for building full-stack apps with tRPC, Material UI, and first-class LLM tooling support.

## Stack

| Layer | Library |
|-------|---------|
| Framework | Next.js (App Router) + TypeScript |
| API | tRPC v11 |
| Validation | Zod |
| UI | Material UI (MUI) v7 + Emotion |
| Data fetching | TanStack Query (via tRPC) |

## Getting started

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## Project structure

```
src/
  api/          tRPC routers and server setup
  app/          Next.js App Router pages and layouts
  lib/          tRPC client/server utilities
  theme/        MUI theme and providers
```

Each route follows the server/client split pattern:

```
src/app/pages/example/
  page.tsx          Server Component — data fetching, metadata
  ExampleClient.tsx Client Component — interactivity
```

---

## LLM rules

This repo ships context rules for AI coding tools so they understand the stack conventions from the start. Rules are written once in a canonical location and synced to every tool's expected format.

### Canonical source

```
llm/
  config.json        Target tools + module-to-path mapping
  rules/
    root.md          Project-wide rules (stack, conventions, layout)
    api.md           tRPC router conventions
    app.md           Next.js App Router conventions
    lib.md           tRPC client/server usage
    theme.md         MUI theme conventions
  sync.mjs           Generator script
```

Edit files in `llm/rules/`. Never edit the generated files directly.

### Generated outputs

Running the sync produces:

| File | Tool |
|------|------|
| `CLAUDE.md` | Claude Code |
| `AGENTS.md` | OpenAI Codex |
| `.github/copilot-instructions.md` | GitHub Copilot |
| `.windsurfrules` | Windsurf |
| `.clinerules` | Cline / Roo |
| `.cursor/rules/*.mdc` | Cursor (one per module, glob-scoped) |
| `src/*/CLAUDE.md` | Claude Code module-level context |

Cursor rules use frontmatter to scope each file to its directory — e.g. the `api.mdc` rule only activates when you're working in `src/api/**`. The root rule uses `alwaysApply: true`. Tools that don't support sub-module scoping (Copilot, Windsurf, Cline) receive the project-wide root rules only.

### Syncing

After editing any rule file, regenerate only the target you use:

```bash
npm run sync-llm-rules -- --target cursor
```

Generated outputs are intentionally local-only and are gitignored. Commit only the canonical source files in `llm/rules/` and `llm/config.json`.

### Adding a module

1. Create `llm/rules/{name}.md`
2. Add an entry to `llm/config.json`:
   ```json
   { "rule": "{name}.md", "path": "src/{name}", "description": "..." }
   ```
3. Run `npm run sync-llm-rules -- --target <tool>`

### Toggling tools

Set any target to `false` in `llm/config.json` to disable generation for that tool:

```json
"targets": {
  "claudeCode": true,
  "cursor": true,
  "copilot": false,
  ...
}
```

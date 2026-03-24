<!-- WORKFLOW PROTOCOL - READ THIS FIRST -->

# Before ANY Code Changes

**Step 1**: Announce active rules and relevant skills

```text
Active Rules: [list rules from .cursor/rules/ that apply to files you will touch]
Relevant Skills: [list relevant built-in/platform skills for the current task context]
```

For this repository, rule activation is typically:
- `root.mdc` always applies
- `api.mdc` for `src/api/**`
- `app.mdc` for `src/app/**`
- `lib.mdc` for `src/lib/**`
- `theme.mdc` for `src/theme/**`

**Step 2**: After completing changes

If you changed a public API, hook signature, data contract, or exports:

1. Search for references in canonical and generated rule docs:
   - `rg "symbolName" llm/rules .cursor/rules README.md`
2. Propose documentation updates immediately.
3. If rule intent changed, update canonical files in `llm/rules/*.md` and re-sync outputs.

**Step 3**: Before finishing

- Offer: "Validate changes against rules/skills?"

---

## Commands

```bash
# Dev server
npm run dev

# Lint
npm run lint

# Build (includes type validation from Next.js toolchain)
npm run build

# Optional explicit TypeScript check
npx tsc --noEmit

# Re-generate tool-specific rule outputs
npm run sync-llm-rules -- --target cursor
```

## Project Structure

- `src/api/` - tRPC routers and server setup
- `src/app/` - Next.js App Router pages and layouts
- `src/lib/` - Shared tRPC client/server utilities
- `src/theme/` - MUI theme and providers
- `llm/rules/` - Canonical LLM rule sources
- `llm/sync.mjs` - Rule generator for agent/tool outputs

## Tech Stack

- Next.js (App Router) + TypeScript
- React 19
- tRPC v11
- TanStack Query v5
- MUI v7 + Emotion
- Zod

## Core Principles

- User-first: Follow requirements precisely.
- Complete: No TODOs or placeholders in finished code.
- Readable over clever.
- Avoid overengineering.
- Prefer project conventions over introducing new patterns.

## Code Style

Follow `.cursor/rules/root.mdc` and module rules for details.

Key points:

- Keep TypeScript strict (no `any`, avoid type assertions unless unavoidable)
- Server Components by default; add `"use client"` only when needed
- Use early returns to reduce nesting
- Remove unused imports and debugging logs
- Avoid hardcoded design tokens; use the MUI theme
- Use comments only when logic is non-obvious

## Naming Conventions

- Directories: kebab-case
- Components: PascalCase symbols with `{Name}Client.tsx` for interactive route clients
- Functions/consts: camelCase
- Event handlers: `handle` prefix
- Domain terms: follow glossary terms from `ubiquitous-language.md`

## Documentation Standards

- Prefer self-explanatory code over excessive comments
- Use short, targeted comments for complex logic only
- Keep README and rule docs aligned with behavior changes
- Edit canonical rules in `llm/rules/*.md`, then regenerate outputs (do not hand-edit generated files as source of truth)

## Git Workflow

- Branch naming: `feature/`, `fix/`, `chore/`
- Commit messages: conventional commits preferred
- Run lint/build before commit when possible
- Never commit secrets or environment files

## Boundaries

**Always do:**

- Route API behavior through tRPC (`src/api/*`)
- Validate tRPC inputs with `zod` objects
- Keep theme values in `src/theme/theme.ts` (no hardcoded palette/spacing in feature code)
- Respect server/client boundaries in App Router files

**Ask first:**

- Adding new dependencies
- Introducing new top-level architecture patterns
- Modifying shared cross-cutting infrastructure

**Never do:**

- Add raw Next.js API handlers that bypass tRPC
- Commit secrets or API keys
- Edit generated files as canonical source for rules

---

## Rules & Skills

- **Rules** (`.cursor/rules/`)
  - `root.mdc` - always-on project conventions and DDD language checks
  - `api.mdc` - `src/api/**` tRPC conventions
  - `app.mdc` - `src/app/**` App Router conventions
  - `lib.mdc` - `src/lib/**` tRPC client/server usage
  - `theme.mdc` - `src/theme/**` MUI theme usage

- **Skills**
  - Use relevant platform skills based on task type (planning, coding, review, docs, migrations).
  - Prefer project rules first, then augment with a skill when task-specific depth is required.

---

## Hallucination Guardrails

**CRITICAL: Do not assume these without verification in code.**

- There is no Nx workspace here; use `npm` scripts and Next.js tooling.
- Do not create raw API route handlers for business APIs; use tRPC routers/procedures.
- Do not fetch initial route data with client `useEffect` when a Server Component can fetch it.
- Do not hardcode colors/spacing/typography in feature components; use MUI theme tokens.
- Do not hand-edit generated rule outputs as source of truth; update `llm/rules/*.md` and run sync.
- Do not introduce unapproved domain synonyms when glossary terms already exist.

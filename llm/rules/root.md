# Project Rules

This is a Next.js application using the App Router, tRPC for type-safe APIs, and Material UI for components.

## Stack

- **Framework**: Next.js (App Router) with TypeScript
- **API**: tRPC v11 with Zod validation
- **UI**: Material UI (MUI) v7 with Emotion
- **Data fetching**: TanStack Query via tRPC hooks

## General conventions

- Use TypeScript strict mode — no `any`, no type assertions unless unavoidable
- Server Components by default; add `"use client"` only when needed (event handlers, hooks, browser APIs)
- All API routes go through tRPC — do not create raw Next.js API route handlers
- Use `zod` for all runtime validation at API boundaries
- No hardcoded design tokens (colors, spacing) — use the MUI theme
- Only use comments when the code cannot be self described clear enough in itself. this may be for complex algorithms, regex, or other non-human readable code blocks.

## Directory layout

<!-- sync-llm-rules:directory-layout:start -->

- `src/api/` — tRPC API routers and setup
- `src/app/` — Next.js App Router pages and layouts
- `src/lib/` — Shared utilities and tRPC client setup
- `src/theme/` — MUI theme configuration
<!-- sync-llm-rules:directory-layout:end -->

## Page structure

Each route lives in `src/app/pages/{name}/`:

- `page.tsx` — Server Component; handles data fetching and exports metadata
- `{Name}Client.tsx` — Client Component; handles interactivity, passed data as props

## DDD terminology checklist

Before writing or refactoring domain-facing code, check:

- Which glossary terms from `ubiquitous-language.md` apply to this change?
- Are names in code, API contracts, and tests aligned with approved domain terms?
- Did this change introduce a synonym for an existing term? If yes, rename it.
- If a new term is required, add it to the glossary first and then apply it consistently.

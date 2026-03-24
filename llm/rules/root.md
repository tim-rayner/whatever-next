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

## Directory layout

- `src/api/` — tRPC routers and server setup
- `src/app/` — Next.js App Router pages and layouts
- `src/lib/` — tRPC client/server utilities and shared helpers
- `src/theme/` — MUI theme definition and providers

## Page structure

Each route lives in `src/app/pages/{name}/`:
- `page.tsx` — Server Component; handles data fetching and exports metadata
- `{Name}Client.tsx` — Client Component; handles interactivity, passed data as props

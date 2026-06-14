---
name: stack-conventions
description: Apply the user's personal stack conventions and preferred patterns when writing or reviewing code in their main technologies (Svelte/SvelteKit, Next.js/React, Django, Go, Rust, NestJS/Node). Use whenever generating non-trivial code in these stacks so output matches how the user actually works.
---

# Stack Conventions

These are the user's standing preferences. Apply them by default; the project's own conventions
always win if they conflict (read the repo first). **Fill in / correct the TODOs over time** —
this is a living file.

## General (all stacks)
- Prefer clarity over cleverness; small, named functions over deep nesting.
- Validate at boundaries; never trust external input.
- Errors are explicit and typed; no silent catches.
- Tests alongside non-trivial logic; follow the repo's existing test style.
- No new dependency without a reason; prefer the stack's standard library.

## Frontend — SvelteKit
- TODO: component structure, state management (stores/runes), data loading (`load` vs client).
- TODO: styling approach (Tailwind? scoped CSS?), a11y baseline.
- Use the **svelte** MCP for up-to-date API; use **context7** for examples.

## Frontend — Next.js / React
- TODO: App Router vs Pages, Server vs Client Components default, data fetching pattern.
- TODO: state lib, form lib, styling.
- Deploy/runtime questions → **vercel** MCP. API docs → **context7**.

## Backend — Django
- TODO: project layout (apps), DRF vs plain, serializer/validation pattern, settings split.
- TODO: migration policy, async usage, task queue.

## Backend — Go
- TODO: project layout, error wrapping style (`%w`), context usage, router/framework.
- TODO: interfaces at consumer, testing style (table-driven).

## Backend — Rust
- TODO: async runtime (tokio), error crate (anyhow/thiserror), web framework (axum?), workspace
  layout.

## Backend — NestJS / Node
- TODO: module structure, DI patterns, DTO/validation (class-validator?), ORM (Prisma/TypeORM).

## How to use this skill
1. Read the repo to learn its actual conventions.
2. Apply the matching section above where the repo is silent.
3. If you notice the user repeatedly correcting something, surface it so a TODO here gets filled.

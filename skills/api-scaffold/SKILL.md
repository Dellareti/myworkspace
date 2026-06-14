---
name: api-scaffold
description: Scaffold a complete new API endpoint following the project's existing conventions — route, input validation, service/handler, error handling, and a test. Use when the user asks to add an endpoint, route, controller, resolver, or "create an API for X".
---

# API Scaffold

Generate a new endpoint that looks like it was written by the team — not a generic template.

## Step 1 — Learn the conventions first (do not skip)
Before writing anything, inspect the repo:
- Find an existing endpoint of the same kind (Grep for routes/controllers/resolvers).
- Identify the layering: where routing, validation, business logic, and data access each live.
- Identify the patterns for: input validation, the error/response envelope, auth/authz guards,
  DTO/serialization, and how tests are structured (fixtures, factories, client helpers).
- Note naming, file placement, and import style.

State the conventions you found in 2–3 lines, then build to *those*, not to an ideal.

## Step 2 — Produce the endpoint
Create each layer the project uses, typically:
1. **Route/registration** wired into the existing router.
2. **Input validation** at the boundary, using the project's validation lib, covering every
   field (type, required, range/length, enum).
3. **Handler/service** with the business logic; side effects isolated; errors mapped to the
   standard envelope and correct status codes.
4. **AuthZ** guard consistent with sibling endpoints (ownership/tenant/role check, not just authn).
5. **Test** mirroring an existing test: happy path + at least one validation failure + one
   authz/forbidden case.

## Step 3 — Verify
- Run the project's test command for the new test and the type-checker/linter.
- Report what passed and any follow-ups (e.g. migration needed, OpenAPI/schema to update).

## Guardrails
- Match existing style exactly; do not introduce a new validation lib, error format, or folder
  structure.
- No business logic in the route layer; no DB calls in the controller if the project uses a
  service layer.
- If a field maps to persistence, check whether a migration is also required and say so.

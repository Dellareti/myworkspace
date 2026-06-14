---
name: deploy-checklist
description: Run a pre-deploy / pre-release safety checklist before shipping to staging or production. Use when the user is about to deploy, release, cut a tag, merge to main, or asks "are we ready to ship". Covers tests, migrations, rollback, env/secrets, and observability.
---

# Deploy Checklist

Walk the change through these gates **before** it ships. Adapt to the project's actual stack —
read the CI config, deploy scripts, and infra files first to ground each item in reality. Report
each gate as ✅ pass / ⚠️ needs attention / ❌ blocker, then a go / no-go verdict.

## 1. Code & tests
- [ ] CI is green on this commit (lint, type-check, unit, integration).
- [ ] New behavior has tests; no skipped/`.only` tests left behind.
- [ ] No debug logging, commented-out blocks, or `TODO: remove before deploy` left in the diff.

## 2. Database & data
- [ ] Migrations are reviewed, reversible, and lock-safe (see db-migration-reviewer).
- [ ] Migration order vs. code: does the new code work both *before* and *after* the migration
      (for zero-downtime / rolling deploys)? Expand-then-contract, not a breaking rename.
- [ ] Backfills are batched and tested on prod-like data volume.

## 3. Config & secrets
- [ ] New env vars are documented and set in every target environment.
- [ ] No secrets in the diff, logs, or client bundle.
- [ ] Feature flags default to a safe state; risky changes are behind a flag.

## 4. Rollback & blast radius
- [ ] There is a one-step rollback (revert image/tag) and it actually works with the migration.
- [ ] Irreversible steps (data deletion, destructive migration) are explicitly approved.
- [ ] Change is scoped — can it be rolled out gradually (canary / % traffic)?

## 5. Observability
- [ ] Logs/metrics/traces exist for the new path; you can tell if it's healthy post-deploy.
- [ ] Alerts cover the new failure modes; on-call knows what changed.
- [ ] A concrete "is it working?" check is defined (a metric, endpoint, or query to watch).

## 6. Comms
- [ ] Breaking API/contract changes are communicated to consumers.
- [ ] Deploy window and owner are clear.

## Output
A checklist with status per item, the blockers called out first, and an explicit **GO** or
**NO-GO** with the one or two things that must happen before GO.

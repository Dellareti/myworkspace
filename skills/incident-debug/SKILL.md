---
name: incident-debug
description: Structured production incident debugging — go from a symptom to a root cause without guessing. Use when something is broken in production/staging: errors spiking, latency up, a service down, data wrong, or "it works locally but not in prod".
---

# Incident Debug

A disciplined loop to find root cause fast. Resist the urge to change code before you understand
the failure. Form a hypothesis, then seek evidence that would *disprove* it.

## Step 0 — Stabilize first
If users are actively impacted and a safe mitigation exists (rollback, feature flag off, scale
up, failover), do that **before** deep diagnosis. Note it; you still find root cause after.

## Step 1 — Pin the symptom
- What exactly is wrong, observed how (error message, metric, user report)? Get the exact text.
- When did it start? Correlate with the last deploy, config change, migration, or traffic shift.
- Scope: all users or some? One region/tenant/endpoint? Constant or intermittent?

## Step 2 — Gather evidence (use the MCPs)
- **Errors/stack traces** → `sentry` MCP. Get the exact exception, frequency, first-seen, release.
- **Logs/metrics/traces** → `cloudflare-observability` / app logs; look at the failing path's
  latency and error rate, not just averages (p95/p99).
- **Infra state** → `kubernetes` (pod restarts, OOMKills, pending), `docker`, `digitalocean`,
  `vercel` (build/deploy logs) as relevant.
- **DB** → `postgres`/`supabase`: slow queries, locks, connection saturation, recent migration.

## Step 3 — Form & test hypotheses
- Write the top 1–3 hypotheses ranked by likelihood given the timeline ("started right after
  deploy X" → suspect that diff first).
- For each, name the single piece of evidence that would confirm or kill it, then go get it.
- Bisect: narrow by layer (client → edge → app → db → external dep) and by time (what changed).

## Step 4 — Root cause & fix
- State the actual root cause in one sentence, supported by evidence (not "probably").
- Propose the minimal correct fix + how to verify it resolves the symptom.
- Note the mitigation that's currently in place and when it can be safely removed.

## Step 5 — Follow-ups
- What monitoring/alert would have caught this sooner?
- Is there a class of bug here worth a guard (test, validation, runbook)?

## Output
Timeline → evidence → root cause (one line) → fix → verification → prevention. No speculation
presented as fact; mark anything still unconfirmed as a hypothesis.

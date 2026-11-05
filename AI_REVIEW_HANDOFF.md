# AMC-EOS Independent AI Review Handoff

## Purpose

This repository is intended to be reviewed by an independent AI coding agent or human engineering team.

Do not assume the previous build claims are correct. Verify them directly from source and by executing the repository where dependencies and PostgreSQL are available.

## Current Product Goal

Prove the Supported Living pilot workflow end-to-end:

1. Authenticate a tenant user.
2. Create a referral.
3. Complete eligibility review.
4. Accept the referral.
5. Start an admission.
6. Reserve a bed safely.
7. Complete admission.
8. Create the canonical resident.
9. Submit a daily-service note.
10. Review the note as a manager.
11. Resolve/escalate operational follow-ups.
12. Reconcile and close a shift only when critical blockers are resolved.

## Highest-Priority Independent Checks

### P0 — Reproducible Build

Run from a clean checkout:

```bash
corepack enable
corepack prepare pnpm@10.15.0 --activate
pnpm install
pnpm typecheck
```

Confirm that the lockfile is legitimate and that all workspace packages resolve.

### P0 — Prisma / PostgreSQL

Run:

```bash
pnpm --filter @amc-eos/api prisma:format
pnpm --filter @amc-eos/api prisma:generate
pnpm --filter @amc-eos/api prisma:validate
pnpm --filter @amc-eos/api prisma:migrate
```

Then inspect all migrations for destructive behavior and verify the canonical pilot models.

### P0 — Core Pilot Integration

Run:

```bash
pnpm --filter @amc-eos/api test:core-pilot:integration
```

Verify:
- accepted referral -> admission -> resident
- concurrent admission completion cannot create duplicate residents
- bed reservation cannot double-book
- tenant isolation on daily-service notes
- audit/outbox evidence is emitted

### P0 — Manager Operations Integration

Run:

```bash
pnpm --filter @amc-eos/api test:manager-operations:integration
```

Verify:
- blocked shift reconciliation persists blocker evidence
- cross-tenant shift access is rejected
- successful reconciliation closes the shift
- outbox and audit evidence are emitted once

### P1 — Authentication

Run all authentication unit, PostgreSQL, HTTP, abuse, coverage, and Playwright suites.

Review:
- issuer/audience verification
- refresh rotation
- refresh reuse detection
- password-reset single use
- session revocation
- rate limiting
- tenant membership enforcement

### P1 — Golden Path UI

Run the Playwright core-pilot flow and manually review:
- referral intake
- admission readiness
- bed selection
- resident creation
- DSP documentation
- manager review
- manager command center

## Areas That Need Skeptical Review

1. Prisma schema contains many historical/version-suffixed models. Determine which models are canonical for the pilot and identify duplicate or abandoned write paths.
2. Offline semantic diagnostics used declaration stubs. They are diagnostic aids only and must not be treated as proof of a real TypeScript build.
3. Verify every `findMany`, mutation, and transaction using real generated Prisma types.
4. Check tenant isolation at both read and write boundaries.
5. Test race conditions in bed reservations, admission completion, refresh rotation, follow-up assignment, and shift reconciliation.
6. Verify migrations can apply to a blank PostgreSQL database and can also upgrade the previous schema safely.
7. Confirm manager reconciliation logic matches operational policy and cannot be bypassed through another endpoint.
8. Review whether `DAILY_SERVICE` task-based documentation targets reflect the actual business requirement.

## Files to Inspect First

- `apps/api/src/production-referrals/`
- `apps/api/src/production-admissions/`
- `apps/api/src/daily-service-delivery/`
- `apps/api/src/manager-operations/`
- `apps/api/src/auth/`
- `apps/api/prisma/schema.prisma`
- `apps/api/prisma/migrations/`
- `apps/api/test/integration/core-pilot/`
- `apps/api/test/integration/manager-operations/`
- `apps/e2e/tests/`
- `.github/workflows/dependency-backed-api-build.yml`

## Independent Review Output Requested

Ask the reviewing AI to return:

1. Build status: PASS / FAIL / BLOCKED.
2. Exact commands executed.
3. Compiler errors grouped by root cause.
4. Prisma errors and migration risks.
5. Test failures with file/line references.
6. Security and tenant-isolation findings.
7. Concurrency/race-condition findings.
8. Dead or duplicate model/write-path findings.
9. P0/P1/P2 remediation queue.
10. Estimated effort to reach a genuinely deployable pilot.

## Important

The source repository contains substantial offline validation and source-level test scaffolding, but dependency-backed runtime verification is the critical remaining proof point. Treat all unexecuted runtime claims as unverified until independently reproduced.

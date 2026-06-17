# data-migration — migration / backfill / bulk update / import-export

A migration that isn't re-runnable, has no dry-run, and no rollback is how you corrupt prod. These are the rows skipped under "just update the rows".

## Ask first
- **Prod or staging? Reversible?** — confirm target before anything
- One-time or repeatable? Online (live traffic) or maintenance window?
- Data volume — fits in memory, or must batch?

## Safety (non-negotiable)
- [ ] **Backup / snapshot before mutating** — and verified restorable
- [ ] **Dry-run mode** — report what *would* change, change nothing; run it first
- [ ] **Idempotent / re-runnable** — safe to run twice; guard already-migrated rows
- [ ] **Rollback plan** — reverse script or restore path, written before running
- [ ] **Resumable** — checkpoint/cursor so a crash mid-run resumes, not restarts
- [ ] Run on **staging first** with prod-like data

## Correctness
- [ ] **Validate before AND after** — count rows in, rows out, rows skipped; assert they reconcile
- [ ] Handle nulls / missing / malformed / unexpected legacy values explicitly
- [ ] Encoding (UTF-8, accents fr-CA), timezones, number/format drift
- [ ] Schema/constraint compatibility (uniqueness, FKs) before write
- [ ] Transaction boundaries — don't leave half-written state on failure

## Scale & ops
- [ ] **Batch** large sets (don't load all in memory / one giant txn); throttle
- [ ] Avoid long locks on live tables; online-migration pattern if traffic
- [ ] **Progress logging** (N/total, ETA) + structured error log of skipped/failed rows
- [ ] Time estimate; downtime window communicated if needed
- [ ] Rate-limit external calls; retry with backoff

## Project-specific (adapt)
- [ ] Multiple backends (e.g. demo + real)? — which target, and are DB rules/indexes unaffected?
- [ ] Regulated data (HIPAA/GDPR): no PII/PHI in logs; encryption preserved; access scoped
- [ ] Data residency — don't move data across regions if residency is required

## Before you say done
- [ ] Dry-run output reviewed by a human
- [ ] Post-run validation counts reconcile
- [ ] Rollback tested (or explicitly accepted as one-way with sign-off)

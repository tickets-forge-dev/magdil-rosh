# spec — PRD / story / requirements / design doc

A spec people can't act on, or that hides the hard parts, is the most expensive miss — it propagates into wrong code.

## Ask first
- Who's the audience/approver, and what decision does this unblock?
- Scope: net-new, or change to existing behavior?
- Hard deadline or constraints (legal, platform, dependency) shaping it?

## Must cover
- [ ] **Problem + why now** — the user pain, not the solution
- [ ] **Goals + non-goals** — explicit out-of-scope (the #1 omission; prevents scope creep)
- [ ] **Acceptance criteria** — testable, per requirement ("given/when/then"), not vague
- [ ] **Edge cases + error states** — empty, failure, permission-denied, concurrent, limits (specs almost always document only the happy path)
- [ ] **States** — loading/empty/error/success for any UI surface
- [ ] **Non-functional** — performance, scale, security, privacy, a11y, i18n
- [ ] **Data** — model/schema changes, migration, retention
- [ ] **Dependencies + assumptions** — what must exist first; what you're assuming
- [ ] **Rollout** — flag, phased, migration, backward-compat, rollback
- [ ] **Success metrics** — how you'll know it worked
- [ ] **Open questions** — list them, don't paper over (assign owner if possible)
- [ ] **Who's affected** — roles/personas/segments, including the ones easy to forget

## Walter specifics
- [ ] Roles: family, caregiver, agency admin — does each have its own flow?
- [ ] US + Canada (en/fr-CA); CASL/HIPAA implications called out
- [ ] Two-env (demo memory + real Firestore) impact
- [ ] References the existing prototype/design where UI is involved

## Quality
- [ ] Concrete, not aspirational; no "etc." hiding undefined behavior
- [ ] Each requirement is testable and singular
- [ ] Deferred items listed as deferred, not silently dropped

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

## Project-specific (adapt)
- [ ] Distinct user roles/personas — does each have its own flow?
- [ ] Markets/locales (e.g. en, fr-CA); any legal regime (HIPAA/GDPR/CASL) called out
- [ ] If you run demo + real backends, the impact on both
- [ ] References the existing prototype/design system where UI is involved

## Quality
- [ ] Concrete, not aspirational; no "etc." hiding undefined behavior
- [ ] Each requirement is testable and singular
- [ ] Deferred items listed as deferred, not silently dropped

# magdil-rosh

> מגדיל ראש — *do more than the literal ask.*

A Claude Code skill that fixes the most common failure mode: under a short request ("add Google login", "write the welcome email", "migrate the table"), the agent ships the **happy path** and silently skips the states, edge cases, and failure paths that make a thing actually production-ready.

The knowledge of what "complete" means already exists in the model. This skill is the **forcing function** that makes it apply that knowledge instead of cutting corners — and that asks the right scoping questions *before* building, then reports tersely.

## What it does

When you ask for a feature/spec/campaign/script, the skill:

1. **Matches the request to a domain** (auth, email, forms, CRUD, upload, search, payments, API, real-time, modals — plus spec, outreach-email, data-migration).
2. **Loads that domain's checklist** of commonly-forgotten rows (e.g. email → mobile + dark mode + plaintext + locale + idempotent send, not just desktop HTML).
3. **Asks ≤3 sharp questions** — only the forks that change the build (delete semantics, auth model, legal scope), recommended option first.
4. **Covers every row or defers it out loud** — no silent gaps.
5. **Reports terse**: ✅ covered / ⏭️ deferred (why) / ❓ open.

It deliberately **skips** trivial work (questions, lookups, one-line edits) so it doesn't get in the way.

## Install

Copy the skill folder into your Claude Code skills directory:

```bash
# personal (all projects)
cp -r magdil-rosh ~/.claude/skills/

# or cross-runtime
cp -r magdil-rosh ~/.agents/skills/

# or per-project
cp -r magdil-rosh /path/to/project/.claude/skills/
```

It loads automatically — Claude triggers it from the `description` when a request matches.

## Structure

```
magdil-rosh/
├── SKILL.md            # router + core behaviors (loads on trigger)
├── universal.md        # cross-cutting rows every feature forgets (states, a11y, mobile, security)
├── ux.md               # UI/UX polish layer (feel, not just function)
├── auth.md  email.md  forms.md  crud.md  file-upload.md
├── search-filter.md  payments.md  api-endpoint.md  realtime.md  modal-dialog.md
├── spec.md  outreach-email.md  data-migration.md   # non-code deliverables
└── adding-domains.md   # how to extend with new domains
```

Only `SKILL.md` loads on trigger; each domain file loads **on demand**, so the token cost stays low.

## Extending

Hit a feature with no matching domain? Build it thoroughly, then capture the gap as a new `<domain>.md` — see `magdil-rosh/adding-domains.md`. Best source for the checklist: run the request past a fresh agent with no checklist, diff its plan against complete — the diff is what gets forgotten.

## Built for WalterCare

Domain files carry WalterCare-specific rows inline (two-env demo+Firestore, HIPAA no-PHI-logging, US+Canada en/fr-CA, CASL for Canada outreach, design-prototype-first). Strip or adapt these for other projects.

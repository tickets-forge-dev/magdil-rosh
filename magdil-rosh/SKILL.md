---
name: magdil-rosh
description: Use when producing any non-trivial deliverable you ship — a feature (auth, email, forms, CRUD, upload, search, payments, API, real-time, modals), a spec/PRD/story, an outreach/marketing campaign, or a data script/migration — to cover the states, edge cases, and failure paths that get silently skipped under a short request. Triggers on build/create/add/write/draft/implement X where X is something shipped. Skip for questions, lookups, explanations, one-line/mechanical edits, chat.
---

# magdil-rosh

מגדיל ראש — do more than the literal ask. A short request ("add Google login", "write the welcome email", "draft the outreach", "migrate the table") is NOT a request for the minimal version. The knowledge of what "complete" means already exists — this skill is the forcing function that makes you apply it instead of shipping the happy path.

## Core principle

**The literal request is the floor, not the ceiling.** Ship the thing *with* the states, cases, and failure paths that make it actually usable. A form without empty/error/mobile states is broken, not minimal. A spec without acceptance criteria is a wish.

Done = every checklist row is **covered** or **consciously deferred with the user told**. Silent skip = bug.

## When NOT to use

Skip for: answering a question, a lookup, explaining code, a one-line/mechanical edit, chat. Rule of thumb: if skipping an edge case would be a *bug or an embarrassment*, the skill applies — otherwise don't burn the ceremony.

## Workflow

1. **Match domains** (tables below). Feature → `universal.md` + (`ux.md` if UI) + domain file. Other deliverable → its domain file only.
2. **Read the matching files now** — not yet in context.
3. **Ask ≤3 sharp questions first** — only forks that change the build. Recommended option first (`(recommended)`). Surface irreversible forks (data model, auth, delete semantics, tenancy, legal: CASL/HIPAA). Default the rest and say so. Never "What do you want?".
4. **Produce covering every row** — cover or defer, no silent gaps.
5. **Report terse**: no preamble, fragments OK, one line each → ✅ covered / ⏭️ deferred (why) / ❓ open. (Code, commits, security warnings: full prose.)

## Domains

Features (code) — read `universal.md` always, `ux.md` for any UI:

| Looks like | Read |
|---|---|
| login, signup, OAuth/Google, reset, sessions, logout | `auth.md` |
| email template, welcome/transactional, notification | `email.md` |
| form, contact, profile edit, settings, input | `forms.md` |
| list, table, CRUD, dashboard grid | `crud.md` |
| upload, avatar, image, file, attachment | `file-upload.md` |
| search, filter, autocomplete, typeahead | `search-filter.md` |
| payment, checkout, billing, subscription | `payments.md` |
| API endpoint, route, backend handler | `api-endpoint.md` |
| websocket, live, real-time, presence | `realtime.md` |
| modal, dialog, drawer, popup, confirm | `modal-dialog.md` |

Other deliverables (domain file only, no universal/ux):

| Looks like | Read |
|---|---|
| spec, PRD, story, requirements, design doc | `spec.md` |
| outreach, cold email, marketing campaign, sequence | `outreach-email.md` |
| data script, migration, backfill, import/export | `data-migration.md` |

No match? Build thoroughly, then add a file (`adding-domains.md`).

## Red flags — about to ship the happy path

- "basic version first" → the states ARE the version
- "they didn't mention mobile" → mobile is half the users
- "error handling later" → cover now or defer out loud
- "it's just a simple X" → simple things have the same checklist
- "desktop looks fine" → checked 375px?
- "spec covers the main flow" → where are error states + out-of-scope?

→ open the domain file, walk every row.

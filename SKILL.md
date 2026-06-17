---
name: magdil-rosh
description: Use when building, implementing, extending, or "quickly adding" any feature — auth/login/OAuth, email templates, forms, lists/tables/CRUD, file upload, search/filter, payments, API endpoints, real-time, modals — to cover the states, error paths, and edge cases that get silently skipped under a short request. Trigger on "add X", "build X", "create X", "make a X" for any of these.
---

# magdil-rosh

מגדיל ראש — do more than the literal ask. A short request ("add Google login", "make a welcome email") is NOT a request for the minimal version. The user wants the *complete, production* version. The knowledge of what's complete already exists — this skill is the forcing function that makes you apply it instead of shipping the happy path.

## Core principle

**The literal request is the floor, not the ceiling.** "Add a contact form" means add a contact form *with* its empty/loading/error/success states, validation, double-submit guard, mobile layout, and a11y — because a form without those is broken, not minimal.

A feature is done when every row of its domain checklist is either **covered** or **consciously deferred with the user told**. Silently skipping a row = bug.

## Workflow

1. **Identify domains.** Match the request to one or more files below. Most features hit `universal.md` + one domain file.
2. **Load the checklists.** Read `universal.md` (always), `ux.md` (any UI feature), + each matching domain file. These are not loaded until now — read them.
3. **Ask great questions FIRST** (see below). Block coding on the answers that change the build.
4. **Build covering every row.** Cover it or defer it — no silent gaps.
5. **Report terse** (see Communication). One line: covered / deferred / questions.

## Ask great questions

Before building, ask only the questions whose answers **change what you build**. Use the AskUserQuestion tool. Rules:

- **Max 3 questions.** If you have more, you're asking things you should default.
- **Never ask what you can default.** "Should the button be blue?" — pick and move. Ask only forks: which auth providers, soft vs hard delete, who can see this, which locales.
- **Offer a recommended option first**, marked `(recommended)`, so the user can one-click.
- **Surface the expensive forks**: anything that's hard to reverse later (data model, auth model, delete semantics, multi-tenancy scope).
- **A defaulted decision is still a decision** — state it in the report, don't bury it.

Bad: "What do you want?" Good: "Link Google to an existing email/password account automatically, or require explicit confirmation? (takeover risk if auto)"

## Communication — terse, like caveman

Output is to-the-point. No preamble, no "I'd be happy to", no restating the request.

- Report = checklist receipt. Group: ✅ covered, ⏭️ deferred (why), ❓ open.
- One line per item. Fragments OK. Drop articles/filler.
- Code, commit messages, security warnings: write normal full prose.
- Don't narrate what you're about to do — do it, then give the receipt.

## Domains

| Request looks like | Read |
|---|---|
| *any* feature | `universal.md` (always) |
| *any* feature with a UI | `ux.md` (feel/polish, not just function) |
| login, signup, OAuth/Google, password reset, sessions, logout | `auth.md` |
| email template, welcome/transactional email, notification | `email.md` |
| form, contact form, profile edit, settings, input | `forms.md` |
| list, table, CRUD, create/edit/delete, dashboard grid | `crud.md` |
| upload, avatar, image, file, attachment | `file-upload.md` |
| search, filter, autocomplete, typeahead | `search-filter.md` |
| payment, checkout, billing, subscription | `payments.md` |
| API endpoint, route, backend handler | `api-endpoint.md` |
| websocket, live, real-time, presence, notifications feed | `realtime.md` |
| modal, dialog, drawer, popup, confirm | `modal-dialog.md` |

No file matches the feature? Use `universal.md`, build thoroughly, then add a new domain file (see `adding-domains.md`).

## Red flags — you are about to ship the happy path

- "I'll just wire up the basic version first" → the states ARE the version
- "They didn't mention mobile" → mobile is not optional, it's half the users
- "Error handling can come later" → later never comes; cover it now or defer out loud
- "It's just a simple form/email/list" → simple features have the same checklist
- "Desktop looks fine" → did you check 375px wide?

All of these mean: open the domain file, walk every row.

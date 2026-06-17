<p align="center">
  <img src="icon.png" alt="magdil-rosh — a head opening to reveal many watching eyes" width="160">
</p>

<h1 align="center">magdil-rosh</h1>

<p align="center"><b>מגדיל ראש</b> — <i>do more than the literal ask.</i></p>

<p align="center">
  <a href="https://github.com/tickets-forge-dev/magdil-rosh"><img alt="license" src="https://img.shields.io/badge/license-MIT-ff6a2b"></a>
  <img alt="claude code plugin" src="https://img.shields.io/badge/Claude%20Code-plugin-5ee08a">
  <a href="https://tickets-forge-dev.github.io/magdil-rosh/"><img alt="landing page" src="https://img.shields.io/badge/landing-page-6cb6ff"></a>
</p>

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

### Recommended — as a Claude Code plugin

In Claude Code, run:

```
/plugin marketplace add tickets-forge-dev/magdil-rosh
/plugin install magdil-rosh
```

One command, versioned, updatable. Restart the session and the skill is live.

### Manual — copy the skill folder

```bash
git clone https://github.com/tickets-forge-dev/magdil-rosh.git

# personal (all your projects)
cp -r magdil-rosh/skills/magdil-rosh ~/.claude/skills/

# or cross-runtime
cp -r magdil-rosh/skills/magdil-rosh ~/.agents/skills/
```

Either way it loads automatically — Claude triggers it from the `description` when a request matches. No API key, no config.

> The repo root holds the landing page, plugin manifests, and docs; the skill itself lives in `skills/magdil-rosh/`.

## Structure

```
magdil-rosh/                 # repo root: landing page + plugin manifests
├── .claude-plugin/
│   ├── plugin.json          # plugin metadata
│   └── marketplace.json     # makes `/plugin marketplace add` work
├── index.html               # landing page
└── skills/
    └── magdil-rosh/         # ← the skill Claude loads
        ├── SKILL.md          # router + core behaviors (loads on trigger)
        ├── universal.md      # cross-cutting rows every feature forgets
        ├── ux.md             # UI/UX polish layer (feel, not just function)
        ├── auth.md  email.md  forms.md  crud.md  file-upload.md
        ├── search-filter.md  payments.md  api-endpoint.md  realtime.md  modal-dialog.md
        ├── spec.md  outreach-email.md  data-migration.md   # non-code deliverables
        └── adding-domains.md # how to extend with new domains
```

Only `SKILL.md` loads on trigger; each domain file loads **on demand**, so the token cost stays low.

## Extending

Hit a feature with no matching domain? Build it thoroughly, then capture the gap as a new `<domain>.md` — see `magdil-rosh/adding-domains.md`. Best source for the checklist: run the request past a fresh agent with no checklist, diff its plan against complete — the diff is what gets forgotten.

## Built for WalterCare

Domain files carry WalterCare-specific rows inline (two-env demo+Firestore, HIPAA no-PHI-logging, US+Canada en/fr-CA, CASL for Canada outreach, design-prototype-first). Strip or adapt these for other projects.

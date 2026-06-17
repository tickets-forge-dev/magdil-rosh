# ux — UI/UX polish (cross-cutting)

Read for ANY feature with a UI, alongside `universal.md`. `universal.md` = does it *work* (states/a11y/errors). This = does it feel *good*. These are the craft details that separate "an AI built this" from "a designer built this." Mostly forgotten.

## Feedback & latency
- [ ] **Every action gets immediate feedback** within 100ms (press state, spinner, optimistic update) — no dead clicks
- [ ] **Optimistic UI** for likely-success actions; reconcile/rollback on failure — feels instant
- [ ] Skeleton screens > spinners for content loads (perceived speed)
- [ ] **Don't flash loaders** for fast responses — delay spinner ~300ms so quick loads don't blink
- [ ] Disable + spinner on in-flight buttons (also the double-submit guard)
- [ ] Success confirmation that doesn't nag — toast auto-dismiss, inline check; destructive/important = persistent

## Forms feel (beyond forms.md validation)
- [ ] **Autofocus the first field** on a focused task (login, search modal)
- [ ] Don't validate-error a field the user hasn't finished/touched; validate on blur, clear error on fix
- [ ] Show requirements up front (password rules) — don't punish after submit
- [ ] Inline errors next to the field, not one banner at top
- [ ] Enter submits single-field/simple forms; preserve input on error
- [ ] Smart defaults + autocomplete so the user types less

## Empty / first-run
- [ ] Empty state = **onboarding moment**: explain + one clear CTA + maybe sample/illustration, never a blank void
- [ ] First-run differs from returning-user; zero-data ≠ error

## Hierarchy & clarity
- [ ] **One primary action per screen** — visually dominant; secondary actions quieter
- [ ] Destructive actions: distinct (red/outline), never the default focus, require confirm naming the object
- [ ] Scannable: whitespace, alignment, grouping; consistent spacing scale (no random px)
- [ ] Button/label text says the outcome ("Send invite", not "Submit"/"OK")
- [ ] Consistent component reuse — don't reinvent buttons/inputs per screen

## Motion & feel
- [ ] Transitions 150–300ms, ease-out; purposeful, not decorative
- [ ] Animate entering/leaving list items, modal open/close — but **respect `prefers-reduced-motion`**
- [ ] No layout shift (CLS): reserve space for images/async content

## Microcopy
- [ ] Human, specific copy — errors say what to DO ("Check your card number"), not "Error 402"
- [ ] No jargon/internal codes leaked to user
- [ ] Tone consistent (Walter: warm, caregiver-facing — not corporate cold)

## Touch & input ergonomics
- [ ] Touch targets ≥44px; spacing so fat-fingers don't mis-tap
- [ ] Primary actions reachable by thumb on mobile (bottom, not top corners)
- [ ] Correct mobile keyboard per input (email/tel/number); `autocapitalize`/`autocorrect` sane
- [ ] Hover-only affordances have a tap/focus equivalent

## Trust & state persistence
- [ ] Remember user choices (filters, sort, dismissed banners, theme) across sessions
- [ ] Don't lose work: drafts/unsaved-guard (see forms.md), restore scroll position
- [ ] Show "last saved" / sync state for autosave
- [ ] Confirm before anything destructive or irreversible

## Quick gut-check before "done"
- [ ] Used it at 375px wide?
- [ ] Used it keyboard-only?
- [ ] Used it with slow 3G throttle — do the loading states hold up?
- [ ] Every button: pressed → something visibly happens?
- [ ] Matches the existing prototype/design system (Walter design rule)?

# universal — every feature

Applies to *every* feature regardless of domain. These are the rows skipped most often. Walk all of them.

## States (the #1 forgotten thing)
- [ ] **Loading** — skeleton/spinner while data fetches; never a blank flash
- [ ] **Empty** — no data yet; show a real empty state + call-to-action, not a blank list
- [ ] **No-results vs empty** — "you have no items" ≠ "your filter matched nothing"; distinct copy
- [ ] **Error + retry** — fetch/action failed; show message + a retry affordance, not a crash or silent nothing
- [ ] **Partial / slow** — some data loaded, some failed; timeout after N seconds with a message
- [ ] **Success** — confirm the action happened (toast/inline), then leave a sensible clean state

## Responsive (always — not optional)
- [ ] **Mobile** — test at 375px wide; no horizontal scroll; content reflows
- [ ] **Touch targets** — ≥44px; buttons/links tappable, not just clickable
- [ ] **Desktop + tablet** — wide layout doesn't stretch ugly; breakpoints sane
- [ ] **Dark mode** — if the app/email has it, the feature respects it (colors + logos work on both)

## Accessibility
- [ ] Every input has a real `<label>`; controls have accessible names
- [ ] Keyboard-only: full flow works, visible focus ring, no keyboard trap, Enter submits
- [ ] Focus management: focus first error on failed submit; return focus after modal close
- [ ] Errors/success announced via `aria-live`; `aria-invalid` on bad fields
- [ ] State not conveyed by color alone; sufficient contrast
- [ ] `prefers-reduced-motion` respected for animation/spinners

## Input handling
- [ ] Trim whitespace; reject whitespace-only as empty
- [ ] Very long input — truncate/wrap, don't break layout
- [ ] Unicode / emoji / accents (Walter: fr-CA) — UTF-8 safe
- [ ] Paste of formatted/huge content
- [ ] Escape all user content on render (XSS); never trust client input on server

## Network & concurrency
- [ ] **Double-submit** — disable control in-flight; idempotency key on mutations
- [ ] **Timeout / offline** — detect, message, allow retry; preserve user input on failure (never clear)
- [ ] **401 mid-session** — detect expiry, redirect to login, preserve location, non-alarming message
- [ ] **429 rate limit** — friendly "too many attempts" message
- [ ] **409 conflict** — concurrent edit / stale data; prompt reload
- [ ] **Race / out-of-order** — last response wins; cancel stale requests

## Security & permissions
- [ ] Route/feature gated behind auth where required
- [ ] **Server-side authorization on every mutation** — never rely on hidden UI; UI hiding ≠ enforcement
- [ ] Scope queries to the user's tenant/org (no reading others' data)
- [ ] CSRF protection on cookie-auth mutations
- [ ] Rate limit sensitive endpoints
- [ ] **Walter: HIPAA** — never log PII/PHI; encrypt sensitive data at rest

## i18n & locale (Walter is US + Canada, en + fr-CA)
- [ ] Strings externalized, not hardcoded
- [ ] Timezone-correct display of dates/times
- [ ] Locale-aware number/phone/date formats

## Observability & tests
- [ ] Log success/failure (without secrets/PII); analytics event for the key action
- [ ] Tests: happy path **+ at least one failure path**
- [ ] Match the existing HTML prototype before building UI (Walter design rule)

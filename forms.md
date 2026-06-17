# forms — contact / profile edit / settings / input

Read `universal.md` too.

## Ask first
- Edit (pre-populated) or create (empty)? Public or authed?
- Which fields are required, and any uniqueness/format constraints?
- Explicit save or autosave?

## Validation
- [ ] **Typed schema (e.g. Zod) as single source of truth — shared client + server**
- [ ] Server validates too — never trust client
- [ ] Per-field: required, min/max length, email/phone/URL format, char allowances
- [ ] **Timing**: validate on blur, re-validate on change once touched, validate all on submit
- [ ] Inline error per field, tied via `aria-describedby`; `aria-invalid`
- [ ] Map server-side field errors back onto the right inputs
- [ ] Length counter + max enforcement on free-text fields

## States
- [ ] Profile edit: loading skeleton while fetching, fetch-error + retry
- [ ] Pristine vs dirty tracking
- [ ] Submit button: disabled when invalid (or unchanged on edit), in-flight spinner, **disabled during submit (double-submit guard)**
- [ ] Success: toast + reset to new clean baseline (contact: clear; edit: keep saved as pristine)
- [ ] Generic/network error banner with retry — **preserve input, never clear on error**

## Edge cases
- [ ] Idempotency key / guard against duplicate submit on retry
- [ ] **Unsaved-changes guard** — warn on navigate-away / tab close when dirty (beforeunload + router block)
- [ ] Cancel/discard → confirm when dirty
- [ ] Trim/normalize (whitespace, phone, email casing) before submit
- [ ] All-whitespace input rejected; empty optional → consistent null vs ""
- [ ] No-op submit (unchanged profile) prevented or short-circuited
- [ ] Session expiry mid-edit → re-auth, preserve unsaved input
- [ ] 409 concurrent-edit → prompt reload
- [ ] Unicode/emoji/RTL, huge paste, leading/trailing spaces

## A11y & mobile (beyond universal)
- [ ] `autocomplete` attributes (name/email/tel) for autofill
- [ ] Correct input types + mobile keyboards (`type=email`, `inputmode=tel`)
- [ ] Focus first invalid field on failed submit; descriptive button text (not bare "Submit")

## Security
- [ ] CSRF on submit; authz (user edits only own profile)
- [ ] Public contact form: **honeypot + CAPTCHA/Turnstile + server rate limit**
- [ ] Email-header-injection prevention on contact backend
- [ ] No logging of sensitive form data (Walter HIPAA)

## Backend & tests
- [ ] Endpoint returns structured field errors + success payload
- [ ] Contact: delivery/notification (+ optional confirmation email)
- [ ] Tests: schema unit, each state (empty/invalid/submitting/success/error), axe a11y, e2e happy + failure

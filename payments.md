# payments — checkout / billing / subscription

Read `universal.md` + `forms.md` (card form) too. Money bugs are the most expensive bugs. Never ship the happy path here.

## Ask first
- Provider? (Stripe / etc.) — dictates tokens, webhooks, SCA handling
- One-time charge or subscription/recurring?
- Markets/currencies + tax? (Walter: US + Canada → GST/HST/PST)

## Core safety (non-negotiable)
- [ ] **Never trust a client-sent amount** — compute/verify price server-side
- [ ] **Idempotency key on every charge** — double-click / retry must NOT double-charge
- [ ] **PCI: never touch raw card data** — use provider tokens/elements; card never hits your server
- [ ] **Confirm payment via webhook, not the checkout-return redirect** — user may close tab; redirect is unreliable
- [ ] Verify webhook signature; handle **duplicate + out-of-order** webhooks idempotently
- [ ] Reconcile: source of truth = provider, not your DB; job to detect drift

## States & errors
- [ ] Card declined / insufficient funds / expired card → specific, non-shaming message + retry
- [ ] **3DS / SCA challenge** (required in EU; possible everywhere) → handle the redirect/iframe flow
- [ ] Processing/pending state — charge not instant; show pending, don't assume success
- [ ] Network drop mid-charge → idempotent retry, never re-charge
- [ ] Partial auth / currency mismatch
- [ ] Provider outage → graceful failure, don't lose the order

## Subscriptions (if recurring)
- [ ] Trial → conversion; proration on upgrade/downgrade
- [ ] **Failed renewal → dunning** (retry schedule + email), grace period, then downgrade/suspend
- [ ] Cancellation: immediate vs end-of-period; reactivation
- [ ] Plan change mid-cycle; quantity/seat change
- [ ] Webhook-driven state sync (don't poll); handle `subscription.updated/deleted`

## Tax / currency / locale
- [ ] Tax computed server-side per region (US sales tax, CA GST/HST/PST)
- [ ] Currency formatting + minor-units (cents) — never float math on money; integer cents
- [ ] Invoice/receipt with legal entity, address, tax breakdown

## Compliance & records
- [ ] **Receipt email** on success (see `email.md`)
- [ ] Refunds: full + partial; reflect in records + notify user
- [ ] Disputes/chargebacks: webhook + internal alert
- [ ] **Audit log every money event** (who/what/when/amount); immutable
- [ ] Walter HIPAA: keep payment data separate from PHI; no card/PII in logs

## Tests
- [ ] Success, decline, SCA, duplicate webhook, idempotent retry, refund, failed renewal, signature-forgery rejection

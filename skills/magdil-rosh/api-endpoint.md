# api-endpoint — backend route / handler

Read `universal.md` too.

## Ask first
- Auth required? Which roles/scopes?
- Read or mutation? Idempotent?
- Expected request volume (rate-limit/pagination needs)?

## Contract
- [ ] Input validation on **every** field (typed schema); reject unknown fields or ignore by policy
- [ ] **Authn + authz** — is the caller logged in AND allowed to touch THIS resource (ownership/tenant)?
- [ ] Consistent error shape: `{code, message, fields?}`; correct HTTP status (400/401/403/404/409/422/429/500)
- [ ] Don't leak internals in errors (stack traces, SQL) to client
- [ ] Pagination on list responses (cursor/offset, max cap)
- [ ] Idempotency key for unsafe-retryable mutations (POST creating resources)

## Edge cases
- [ ] Missing/extra/malformed body; wrong content-type; empty body
- [ ] Oversized payload → 413 + limit
- [ ] Resource not found → 404 (not 500)
- [ ] Concurrent update → optimistic-concurrency / 409
- [ ] Partial failure in multi-step → transaction or compensating cleanup (no half-writes)
- [ ] Null vs missing vs empty-string semantics consistent

## Cross-cutting
- [ ] **Rate limiting** + abuse protection
- [ ] CORS scoped to known origins
- [ ] Timeouts on downstream calls; retries with backoff + circuit-break
- [ ] Structured logging (request id, no secrets/PII); metrics + alerting on error spikes
- [ ] N+1 / unbounded query guards; index the filtered columns
- [ ] If you run demo + real backends, keep DB rules in sync with server authz; regulated data — no PII/PHI in logs

## Tests
- [ ] Happy path, each error status, authz denial, validation failure, rate limit

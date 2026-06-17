# auth — login / signup / OAuth / sessions

Read `universal.md` too. Auth is the domain where the happy path looks done but is dangerously incomplete.

## Ask first
- Which providers? (Google/email-password/both/SSO) — and is this *adding* to an existing method?
- **Account linking policy**: same verified email already exists → auto-link or require explicit confirm? (auto = takeover risk)
- Session model: cookie (httpOnly) or token? "log out everywhere" needed?

## Screens / states
- [ ] Login (all enabled methods) + Signup
- [ ] Redirecting/loading state during OAuth round-trip (disable button, prevent double-click)
- [ ] Callback landing spinner while session established
- [ ] Logged-in affordances (name/avatar, logout) + logged-out state
- [ ] "Session expired, sign in again" state
- [ ] Account-linking confirm screen (if policy requires)
- [ ] Generic auth-error toast/screen

## OAuth flow (server-side)
- [ ] Authorization Code + **PKCE**; scopes `openid email profile` only (don't over-request)
- [ ] `state` param — random, single-use, bound to pre-auth session; validate on callback (CSRF)
- [ ] `nonce` — replay protection; reject reused state/nonce
- [ ] Validate ID token: signature via JWKS, issuer, audience, expiry, clock-skew tolerance
- [ ] Require `email_verified: true` before provisioning
- [ ] Find-or-create by stable `sub`, **not email**; update stored email if it changed at provider
- [ ] App session = signed httpOnly+Secure+SameSite cookie; never expose provider tokens to client
- [ ] Session lifecycle: issue, sliding + absolute expiry, server-side revocation (kill switch)
- [ ] Logout: clear cookie + revoke server session
- [ ] Client/secret in backend secrets, never in frontend bundle
- [ ] Redirect URIs configured per env (local/staging/prod)

## Error & edge cases
- [ ] User cancels/denies consent (`error=access_denied`) → clean return to login
- [ ] Invalid/missing/expired `state` → reject + log
- [ ] Code exchange failure (network, reused code) → message
- [ ] `email_verified:false` → refuse + explain
- [ ] Email registered with different provider → linking policy / conflict UX
- [ ] Provider account suspended/deleted → re-auth
- [ ] Provider outage / timeout → graceful error page
- [ ] Popup blocked → fall back to full-page redirect
- [ ] Direct nav to callback URL with no flow → reject
- [ ] Banned/disabled app user after successful provider auth → block with clear message
- [ ] Cookies disabled / third-party-cookie restrictions → detect + message
- [ ] Multiple tabs / concurrent logins → idempotent

## Cross-cutting
- [ ] HTTPS everywhere; CORS to frontend origin only
- [ ] Audit log: login/logout/link/failures (no tokens)
- [ ] Account deletion removes linked identity data (privacy)
- [ ] `returnTo` deep link preserved through the whole round-trip
- [ ] Tests: token validation, provisioning, callback integration, each error case

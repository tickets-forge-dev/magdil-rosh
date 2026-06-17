# email — templates / transactional / notifications

Read `universal.md` too. The classic miss: building only the desktop HTML, no mobile/dark-mode/plaintext.

## Ask first
- Which recipients/roles? (different copy + CTA per role)
- Locales? (e.g. en, fr-CA — accents must encode)
- Transactional or marketing? (changes compliance + unsubscribe rules)

## Variants (don't ship one)
- [ ] **Plaintext (text/plain) alternative for every HTML variant** — multipart MIME
- [ ] Role-based copy/CTA variants
- [ ] Locale variants (en-US / en-CA / fr-CA)
- [ ] State variants (verified vs needs-verification, OAuth vs password signup)

## Rendering (where "desktop only" bugs live)
- [ ] **Mobile** — ~600px max width, responsive, large tappable CTA, scalable fonts
- [ ] **Dark mode** — color overrides; logo works on light AND dark
- [ ] Table-based layout + **inline CSS** (no flexbox/grid/external stylesheets)
- [ ] Tested across Gmail, Outlook (Word engine), Apple/iOS Mail, Android
- [ ] Web-safe font stack with fallback (no web-font reliance)
- [ ] Images on absolute HTTPS URLs + **alt text + layout survives blocked images**
- [ ] Preheader / preview text (hidden) tuned for inbox

## Content
- [ ] Single clear primary CTA (button) + raw fallback URL beneath
- [ ] Personalization tokens, all **HTML-escaped** (injection)
- [ ] Missing first-name → graceful fallback ("Hi there")
- [ ] Very long name/agency → truncate/wrap without breaking layout
- [ ] Footer: company name + **physical mailing address** + unsubscribe/preferences

## Delivery & compliance
- [ ] Subject + from-name + from-address per variant/locale; real reply-to (not no-reply void)
- [ ] **List-Unsubscribe header (+ one-click)**
- [ ] SPF / DKIM / DMARC alignment on sending domain (dependency)
- [ ] Send async via queue with **retry/backoff** — don't block the triggering request
- [ ] **Idempotency** — re-triggered signup must not spam duplicate emails
- [ ] Bounce/complaint handling + suppression-list respect
- [ ] CAN-SPAM (US) + **CASL (Canada)** — identification, unsubscribe, address
- [ ] Log send success/failure + message ID; alert on failures

## Testing
- [ ] Render unit test across token combos + missing-name fallback
- [ ] Snapshot of rendered HTML
- [ ] Cross-client check (Litmus/Email-on-Acid)
- [ ] Local preview route + send-to-self on staging before prod

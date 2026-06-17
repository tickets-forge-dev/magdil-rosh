# outreach-email — cold email / marketing campaign / sequence

Read `email.md` too for the rendering/deliverability mechanics. This = the campaign layer. A one-shot blast with no follow-up, no segmentation, no compliance is wasted send + legal risk.

## Ask first
- Audience + segment? (one list or split by role/region/stage)
- One email or a **sequence** (follow-ups)? How many touches?
- Market? (Walter: **Canada = CASL, express consent + teeth**; US = CAN-SPAM)

## Campaign structure
- [ ] **Segmentation** — don't send one generic blast; split by persona/region/stage
- [ ] **Follow-up sequence** — most replies come from touch 2–4; define cadence + stop-on-reply
- [ ] **Personalization tokens** (name, company, role) + **fallback for every token** (missing data ≠ "Hi {{first_name}}")
- [ ] Clear single CTA per email; one ask
- [ ] Subject + preheader; **A/B subject variants**
- [ ] Send-time / timezone-aware scheduling
- [ ] Plain, human, short — not a brochure (cold email)

## Compliance (not optional)
- [ ] **CASL (Canada)**: express/implied consent basis documented; sender identification; physical address; **unsubscribe honored ≤10 days**
- [ ] CAN-SPAM (US): truthful headers, address, opt-out
- [ ] **List-Unsubscribe header + visible unsubscribe link**
- [ ] Suppression list respected; never email opt-outs/bounces again

## Deliverability
- [ ] SPF/DKIM/DMARC aligned (see `email.md`)
- [ ] Domain/IP warmup if new sender; volume ramp (don't blast cold)
- [ ] Spam-trigger check (words, link ratio, image-heavy, no-text)
- [ ] Bounce handling: hard → suppress, soft → retry then suppress

## Tracking & ops
- [ ] Open/click/reply tracking; per-variant + per-segment metrics
- [ ] **Reply handling / routing** — who answers, how fast
- [ ] List hygiene: dedupe, validate, remove role/invalid addresses pre-send
- [ ] Test send to self + spam-score tool before launch

## Walter specifics
- [ ] CASL holds Canada outreach — confirm consent basis before any CA send
- [ ] Assets live in `outreach/`; reuse existing templates/positioning (moat story)

# realtime — websocket / live / presence / notifications feed

Read `universal.md` too.

## Ask first
- What's pushed, how often? Per-user or broadcast?
- Delivery guarantee needed (at-least-once / ordered)?
- Transport: WebSocket / SSE / polling fallback?

## Connection lifecycle
- [ ] **Reconnect with backoff** on drop; cap attempts; jitter
- [ ] **Resync on reconnect** — fetch missed state / catch-up since last cursor (don't assume continuity)
- [ ] Connecting / connected / reconnecting / offline UI states
- [ ] Heartbeat/ping to detect dead connections
- [ ] Clean teardown on unmount/navigation (no leaked sockets/listeners)
- [ ] Polling/SSE fallback when WS blocked (proxies, corp networks)

## Messaging
- [ ] **Auth on the socket** (not just initial HTTP); re-auth on token expiry mid-connection
- [ ] Authz per message/channel — user only receives what they may see
- [ ] **Out-of-order / duplicate messages** — sequence ids, idempotent apply
- [ ] Backpressure: bursty updates → batch/throttle render, don't freeze UI
- [ ] Optimistic local update reconciled with server echo

## Edge cases
- [ ] Multiple tabs/devices — consistent state, no double-count
- [ ] Stale data after long background/sleep → full resync
- [ ] Server restart / deploy → mass reconnect (thundering herd) handled with jittered backoff
- [ ] Message for a resource the user just lost access to → drop

## Tests
- [ ] Reconnect, resync, dropped message, out-of-order, authz on channel

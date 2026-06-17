# modal-dialog — modal / dialog / drawer / popup / confirm

Read `universal.md` too. Modals are an a11y minefield; most hand-rolled ones are broken.

## Behavior
- [ ] Open/close state; close on Esc, on backdrop click (unless destructive/dirty), on explicit button
- [ ] **Dirty-guard**: confirm before closing if it contains unsaved input
- [ ] Loading state for async content inside; error + retry
- [ ] Only one modal logic; nested-modal policy decided (usually avoid)
- [ ] Scroll lock on body while open; restore scroll position on close

## Accessibility (the usual misses)
- [ ] **Focus trap** — Tab/Shift-Tab cycle stays inside; **focus moves into modal on open**
- [ ] **Return focus to the trigger element on close**
- [ ] `role="dialog"` + `aria-modal="true"` + `aria-labelledby`/`aria-describedby`
- [ ] Esc closes; screen reader announces open
- [ ] Background content `inert`/`aria-hidden` while open

## Mobile / responsive
- [ ] Full-screen or bottom-sheet on small viewports (not a tiny clipped box)
- [ ] Content scrolls within modal; sticky header/footer with actions
- [ ] Touch-friendly close target

## Confirm dialogs
- [ ] Name the specific object/action ("Delete *Invoice #42*?")
- [ ] Destructive action visually distinct; safe action is default focus
- [ ] Disable confirm + show spinner during the async action; handle its failure

## Tests
- [ ] Open/close paths, focus trap + return, Esc, dirty-guard, mobile layout

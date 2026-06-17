# search-filter — search / filter / autocomplete / typeahead

Read `universal.md` too.

## Ask first
- Search what fields? Exact, prefix, or full-text/fuzzy?
- Server-side or client-side? Scale of dataset?

## Behavior
- [ ] **Debounce input** (~250–300ms); don't fire per keystroke
- [ ] **Cancel stale requests / last-response-wins** (out-of-order races)
- [ ] Loading indicator without flicker on fast responses
- [ ] **Empty query** → sensible default (recent/all/nothing), not an error
- [ ] **No-results state** with the query echoed + suggestion to broaden
- [ ] Min-chars threshold before searching (if applicable)
- [ ] Preserve query/filters in URL (shareable, survives refresh)

## Edge cases
- [ ] Whitespace-only / trim query
- [ ] Special chars, regex/glob metachars, SQL/NoSQL injection — escape/parametrize
- [ ] Unicode/accents/case-insensitive (fr-CA: é = e?); diacritic folding decision
- [ ] Very long query
- [ ] Pagination of results; stable ordering
- [ ] Combined filters → clear "active filters" chips + clear-all
- [ ] Result count shown; truncation/"showing N of M"

## A11y
- [ ] Combobox/listbox ARIA roles for autocomplete; arrow-key navigation; Esc to close
- [ ] Results announced via `aria-live`
- [ ] Highlighted match doesn't break screen-reader text

## Performance / server
- [ ] Index the searched columns; cap result size
- [ ] Rate limit; cache hot queries
- [ ] Authz: results scoped to what the user may see (no leaking others' data via search)

## Tests
- [ ] Empty, no-results, special chars, debounce/race, authz scoping

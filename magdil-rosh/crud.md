# crud — list / table / create / edit / delete

Read `universal.md` + `forms.md` (create/edit forms) too.

## Ask first
- **Soft delete or hard delete?**
- Who can create/edit/delete — owner only, roles, org-scoped?
- Pagination expected at what scale? Bulk actions needed?

## List view states
- [ ] Loading skeleton
- [ ] **Empty (no items)** with create CTA
- [ ] **Empty search-result** (items exist, filter matched none) — distinct from true empty
- [ ] Error + retry
- [ ] Populated rows + per-row actions (edit/delete), optional bulk select
- [ ] Pagination/infinite scroll; total count; **stable ordering (tiebreak by id) to avoid jitter**
- [ ] Sort + filter/search
- [ ] **Filters/sort/page persisted in URL** (survives refresh, shareable)
- [ ] Long-text fields truncated in list, full view on detail/edit
- [ ] 404 state for non-existent item id

## Create / edit
- [ ] Create: optimistic insert or refetch on success; preserve input on failure
- [ ] Edit: prefill; **refetch on open**, handle item deleted/changed by someone else
- [ ] Edit: detect no-changes (disable save); **optimistic-concurrency (version/updatedAt) to prevent lost updates**
- [ ] Optimistic update with rollback on failure
- [ ] (forms.md covers validation/double-submit/cancel)

## Delete
- [ ] **Confirmation dialog naming the item** (destructive)
- [ ] Loading state during delete; disable trigger
- [ ] Optimistic removal + rollback + error toast on failure
- [ ] **Already-deleted (404) → treat as success, remove from list**
- [ ] Soft delete → exclude soft-deleted from list queries

## Data & API
- [ ] Model: id, fields, createdAt/updatedAt, createdBy, ownerId/orgId, soft-delete flag
- [ ] Endpoints: list (paginate/filter/sort), get-one, create, update, delete
- [ ] **Server-side authz on EVERY endpoint** (not just list); scope to tenant/org
- [ ] Server validation; consistent error shape mapped to fields
- [ ] Create idempotency; uniqueness constraints + conflict UX (409)
- [ ] Pagination: cursor or offset, default page size + max cap
- [ ] **Walter two-env**: implement in-memory (demo) AND Firestore (real); update Firestore security rules to match server authz

## Cross-cutting
- [ ] Audit: createdBy/updatedBy/timestamps; who deleted
- [ ] Toasts for every action success/failure
- [ ] Reconcile optimistic UI with server truth after mutations
- [ ] Modal a11y (see `modal-dialog.md`) for create/edit/delete dialogs
- [ ] Tests: validation unit, endpoint+authz integration, e2e list/create/edit/delete + delete-confirm

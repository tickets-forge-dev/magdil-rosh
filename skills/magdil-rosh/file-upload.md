# file-upload — avatar / image / attachment

Read `universal.md` too.

## Ask first
- Allowed types + max size? Single or multiple?
- Where stored (S3/GCS/Firebase Storage) — direct-to-storage or through backend?
- Public or access-controlled URLs?

## Client
- [ ] **Client-side type + size validation before upload** (with clear errors)
- [ ] Image preview before/after upload
- [ ] **Upload progress** indicator; cancel in-flight
- [ ] Remove/replace; default/fallback (e.g. default avatar)
- [ ] Drag-drop + click-to-pick; paste image
- [ ] Disable submit until upload complete; double-submit guard
- [ ] Failed upload → error + retry, don't lose the rest of the form

## Edge cases
- [ ] Wrong type / oversized → rejected with specific message
- [ ] **0-byte / corrupt / truncated file**
- [ ] Filename: unicode, spaces, very long, path-traversal chars sanitized
- [ ] Duplicate filename collisions
- [ ] Network drop mid-upload → resumable or clean retry
- [ ] Slow connection → progress + timeout
- [ ] EXIF orientation (photos sideways); strip EXIF GPS (privacy)

## Server / storage
- [ ] **Re-validate type by content (magic bytes), not just extension/MIME header**
- [ ] Enforce size limit server-side (don't trust client)
- [ ] Virus/malware scan if user-facing
- [ ] Store outside web root / use signed URLs; **never trust client-provided content-type for serving**
- [ ] Generate thumbnails/resizes async; strip metadata
- [ ] Authz: who can read this file; signed/expiring URLs for private
- [ ] Quota per user; orphan cleanup when record deleted
- [ ] Regulated data (HIPAA/GDPR): encrypt at rest, no PII/PHI in filenames/logs

## Tests
- [ ] Valid upload, oversized, wrong type, corrupt, network failure, authz denial

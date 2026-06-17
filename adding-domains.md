# adding-domains — extend magdil-rosh

When a feature has no matching domain file, build it thoroughly from `universal.md`, then capture what you learned so the next build doesn't re-forget.

## How to add a domain
1. Create `<domain>.md` in this skill folder.
2. Structure: `## Ask first` (the 2–3 forks that change the build) → checklist sections grouped by concern (states / behavior / edge cases / server / a11y / tests).
3. **Mine real gaps, not theory.** Best source: run the feature request past a fresh agent ("plan thoroughly, no checklist"), diff its plan against a complete one — the diff is what gets forgotten. That diff is the high-value part of the file.
4. Bold the rows that are *commonly skipped* — those are the reason the file exists.
5. Add a row to the Domains table in `SKILL.md`.
6. Keep Walter specifics inline where relevant (two-env memory+Firestore, HIPAA no-PHI-logging, en/fr-CA, design-prototype-first).

## Quality bar
- Every row is checkable (covered / deferred), not vague advice.
- Cross-reference sibling files instead of repeating (`see forms.md`).
- If a row is enforceable by lint/CI, note it — don't rely on memory.

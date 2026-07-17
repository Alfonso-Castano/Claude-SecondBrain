# Log

Append-only record of every wiki operation — ingestion, lint, reconciliation, and ad-hoc filing. Newest entry first (prepend, don't append to the bottom) so recent activity is visible without scrolling.

**Format:** one line per operation —
`YYYY-MM-DD | <ingest|lint|reconcile|file> | <short description> | <files touched>`

**Rotation trigger:** past ~500 entries, rotate this file to `log-YYYY.md` (starting a fresh `log.md`) and check for this during lint passes — mirrors `index.md`'s own size trigger.

---

No operations logged yet.

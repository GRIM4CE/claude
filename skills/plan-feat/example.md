# Plan: CSV export for reports

**What we will do:**
- Add an `/export.csv` endpoint reusing the existing report query, streamed via the stdlib csv writer.
- Files to touch: `routes/reports.py`, `services/report_query.py`, `tests/test_export.py`.

**Out of scope:** XLSX, scheduled exports, column selection.

**Risks:** Large reports could hold a DB cursor open too long.

**What we gain:** Users stop copy-pasting tables; unblocks finance's monthly close.

**Open questions / assumptions:** Assumes reports stay under 100k rows; no project-conventions skill found.

**Rejected alternative:** Client-side export — fails on paginated data.

**Done when:**
- [ ] Endpoint returns valid CSV for every report type
- [ ] Empty-report case tested
- [ ] Export button documented

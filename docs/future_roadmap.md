# Future Roadmap

## What This Proof of Concept Doesn't Handle

The current workflow is designed for recurring reports with consistent, predictable dataset structures. It works well for that use case. But real organizational data is messier and more complex.

---

## Phase 2 — Context Analyzer

**The problem it solves:**
Right now the workflow is hardcoded to Furniture Bank's specific field names. If the dataset changes — different column names, a new status value, a different date field — the workflow breaks and needs manual reconfiguration.

**The proposed solution:**
Add an AI node before the Code node that reads the dataset first and automatically identifies:
- Which field is the primary key
- Which field is the date
- Which field is the status
- Which status values should count as "served"

This makes the pipeline reusable across any program or dataset without reconfiguration.

**Why it wasn't built yet:**
This is a higher-cost AI step — it sends the full dataset to the model to understand structure before analysis. For simple recurring reports, this cost isn't justified. The right approach is to use the Context Analyzer only when onboarding a new dataset type, confirm the field mappings once with a human, save them to the workflow config, and run the cheap hardcoded version every cycle after that.

---

## Phase 3 — Production-Grade Architecture

For real organizational scale — tens of thousands of records, multiple data sources, quarterly audit requirements — the n8n workflow needs to sit on top of proper data infrastructure:

**Recommended stack:**

| Layer | Tool | Purpose |
|-------|------|---------|
| Source of truth | SQL database (PostgreSQL) | Single, versioned, auditable data store |
| Cleaning & counting | SQL queries or Python | Deterministic, reproducible, version-controlled |
| Orchestration | n8n | Scheduling, triggers, routing, notifications |
| AI | LLM (Gemini / GPT-4) | Board summaries, anomaly explanation only |
| Reporting | Google Docs / Power BI | Stakeholder-facing output |

**Key principle:** Counting logic must be deterministic and version-controlled — not prompt-dependent. AI handles communication, not computation.

---

## Phase 4 — Scheduled Runs + Audit Trail

- Workflow triggers automatically before each board reporting cycle
- Every run logs: timestamp, input record counts, cleaned count, gap, anomalies, analyst who reviewed
- Historical comparison: "Last quarter we served 35 families. This quarter: 41. Here's what changed."
- Alerts if gap exceeds a defined threshold — flags for immediate human review

---

## Summary

| Phase | What it adds | Cost level |
|-------|-------------|------------|
| Current (v1) | Hardcoded pipeline for recurring reports | Near-zero |
| Phase 2 | Context Analyzer for new/unfamiliar datasets | Low-medium |
| Phase 3 | SQL infrastructure for production scale | Medium (setup) |
| Phase 4 | Scheduled runs + audit trail | Low (operational) |

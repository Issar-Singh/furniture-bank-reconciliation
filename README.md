# Furniture Bank — Data Reconciliation Pipeline

A working proof of concept for automating the reconciliation of Salesforce CRM data against published annual reports — built as part of the Analytics & Data Associate hiring process.

---

## The Problem

The board wants to know how many families Furniture Bank helped last year. The number in Salesforce doesn't match the number in the annual report. Someone needs to figure out why — quickly, accurately, and in a way the board can understand.

This happens every reporting cycle. Without a structured process, it takes hours of manual work, and the result depends entirely on who's doing the analysis.

---

## What This Project Does

This pipeline automates the boring, repetitive parts of that investigation:

1. **Pulls both data sources** — Salesforce export and annual report figure
2. **Cleans the data using code** — filters by status, date range, and deduplicates by family
3. **Flags every anomaly** — with the specific record ID and reason
4. **Generates a board-ready summary** — one paragraph, plain language, no jargon

A human reviews the output, applies ground-level judgment, and makes the final call.

---

## Results on Synthetic Dataset

| Step | Count |
|------|-------|
| Raw Salesforce records | 50 |
| After removing non-Completed statuses | 39 |
| After removing out-of-range dates | 37 |
| Unique families served (deduplicated) | **35** |
| Annual Report states | **38** |
| Gap requiring investigation | **3** |

15 anomalies were flagged with specific Record IDs. The 3-family gap was identified as likely due to families tracked outside Salesforce — a data entry gap, not a counting error.

---

## How It Works

```
Google Sheets (Salesforce Export)  ──┐
                                     ├──► Code Node (clean + count) ──► AI Node (board summary) ──► Google Docs
Google Sheets (Annual Report)      ──┘
```

**Code does the counting. AI does the communication.**

Sending raw datasets to an LLM for counting is expensive and unreliable. This pipeline uses deterministic JavaScript logic for all cleaning and counting, and only passes a small cleaned summary to the AI for plain-language generation.

---

## When To Use This

**Best for:** Recurring reports with consistent dataset structure — same fields, same status values, same date logic every cycle. Run it quarterly, get results in seconds.

**Not designed for:** Complex multi-source analysis or unfamiliar dataset structures. Those require a higher-cost Context Analyzer approach (see `docs/future_roadmap.md`).

---

## Repo Structure

```
data/          → synthetic datasets used for testing
output/        → reconciliation result and AI summary
workflow/      → n8n workflow JSON + canvas screenshot
prompt/        → reusable prompt template
docs/          → technical notes and future roadmap
```

---

## The Human Judgment Layer

This pipeline surfaces the numbers and flags the anomalies. It does not make the final decision.

A human reviewer is responsible for:
- Deciding which AI-suggested explanations apply to the real operational context
- Determining whether to retract or defend a published number
- Verifying flagged families with case workers before backfilling records
- Approving the board summary before it goes to leadership

AI accelerates the analysis. The analyst owns the recommendation.

---

Built by Issar — CS Student, University of Lethbridge | Data Science & Machine Learning

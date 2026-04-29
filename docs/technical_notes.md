# Technical Notes

## Workflow Stack

- **Automation:** n8n (self-hosted via Docker, v2.17.6)
- **Data sources:** Google Sheets (via Google Sheets API)
- **Cleaning logic:** JavaScript Code node
- **AI model:** Google Gemini 2.0 Flash
- **Output:** Google Docs (via Google Docs API)

---

## Field Assumptions (Current Hardcoded Version)

The current workflow assumes the following field names in the Salesforce export:

| Field | Purpose |
|-------|---------|
| `Family_ID` | Primary key — used for deduplication |
| `Status` | Must equal `Completed` to be counted |
| `Delivery_Date` | Must fall within reporting period |
| `Record_ID` | Row identifier for anomaly reporting |
| `Family_Name` | Label for anomaly reporting only |

The annual report sheet must contain:
- `Reported_Value` — the published number
- `Reporting_Period_Start` — format YYYY-MM-DD
- `Reporting_Period_End` — format YYYY-MM-DD

---

## Known Limitations

1. **Hardcoded field names** — workflow breaks if Salesforce export uses different column names
2. **Single status value** — currently only counts `Completed` as valid; other valid statuses would need code changes
3. **Gemini free tier quota** — hits daily limits on high-volume testing; paid tier required for production
4. **No error handling** — if either Google Sheet is empty or missing, workflow fails silently
5. **No audit logging** — results are not stored historically; each run overwrites the output doc

---

## Cost Estimate

| Component | Cost |
|-----------|------|
| Google Sheets read | Free |
| JavaScript Code node | Free |
| Gemini 2.0 Flash (summary only ~500 tokens) | ~$0.000038 per run |
| Google Docs write | Free |
| **Total per quarterly run** | **< $0.001** |

For recurring reports, this approach is effectively free.

---

## APIs Enabled (Google Cloud Console)

- Google Sheets API
- Google Drive API
- Google Docs API

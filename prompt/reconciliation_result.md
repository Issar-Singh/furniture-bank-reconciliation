RECONCILIATION REPORT - 2024-01-01 to 2024-12-31

BOARD SUMMARY:
After a thorough review of our 2024 records, we have confirmed that we served 35 unique families
this year, following the removal of duplicate entries, canceled requests, and services that occurred
outside the reporting window. This leaves a small gap of three families compared to the 38 cited in
the Annual Report, which most likely occurred because the report included families who were referred
to us but had not yet received their final services. To ensure our reporting remains fully accurate,
we recommend performing a final month-end check to verify that only completed deliveries are counted
toward our annual impact totals.

RAW NUMBERS:
- Salesforce Raw Count: 50
- After Status Filter: 39
- After Date Filter: 37
- Unique Families Served: 35
- Annual Report Value: 38
- Gap: 3

ANOMALIES FLAGGED:
SF-013 (Kowalski Family): Delivery date '2023-12-01' outside reporting period
SF-050 (Murphy Family): Delivery date '2025-01-14' outside reporting period
SF-003 (Nguyen Family): Status is 'Referral' - excluded
SF-006 (Wilson Family): Status is 'Cancelled' - excluded
SF-011 (Taylor Family): Status is 'In Progress' - excluded
SF-015 (Harris Family): Status is 'Referral' - excluded
SF-019 (Walker Family): Status is 'Cancelled' - excluded
SF-024 (Okonkwo Family): Status is 'Referral' - excluded
SF-029 (Adams Family): Status is 'In Progress' - excluded
SF-035 (Turner Family): Status is 'Referral' - excluded
SF-039 (Evans Family): Status is 'Cancelled' - excluded
SF-045 (Rogers Family): Status is 'Referral' - excluded
SF-049 (Bell Family): Status is 'In Progress' - excluded
SF-009 (Ahmed Family): Duplicate Family_ID FAM-101 - counted once only
SF-032 (Ahmed Family): Duplicate Family_ID FAM-101 - counted once only

---

ANALYST REVIEW NOTES:

AI assumption flagged for human review:
The AI suggested the 3-family gap is likely due to Referral/In Progress records being included
in the annual report count. This is plausible but unverified. Other likely causes based on
operational knowledge:
- 3 families tracked in a case worker spreadsheet and included in the report but never entered into Salesforce
- Partner agency deliveries counted in the report but logged under a different system

Recommended action:
Do not retract the published figure of 38. Contact case workers to identify and backfill the
3 missing Salesforce records. Once verified, standardize the policy: no family counted in the
annual report without a corresponding Completed record in Salesforce.

AI duplicate logic error caught:
During review, the AI was found to be matching duplicates by family name rather than Family_ID
in an earlier test run. This was corrected. Always use the primary key for deduplication — never names.

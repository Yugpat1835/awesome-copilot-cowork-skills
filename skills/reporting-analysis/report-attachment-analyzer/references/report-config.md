# Report configuration

Each H2 block below defines one recurring emailed report to track. Copy the template block, fill in every line, and set `Status: active`. Keep the H2 heading in kebab-case: it becomes the working folder name under `/Documents/Cowork/output/report-attachment-analyzer/`. The completed example at the bottom stays at `Status: example` and is never run.

If you prefer, leave this file untouched: on first run the skill asks for these values in conversation and writes the block for you.

## your-report-name

- Status: paused
- Sender: reports@example.com
- Subject contains: REPLACE WITH TEXT THE SUBJECT ALWAYS CONTAINS
- Attachment type: xlsx
- Attachment filename contains: (optional, leave blank if the email has only one attachment)
- Cadence: weekly
- Data location: sheet "Sheet1", headers in row 1 (for PDF: describe the table, for example "the KPI table on page 1")
- Period field: column "Week ending" (or write "email received date" if the file carries no date)
- Metrics: Metric A, Metric B, Metric C
- Anomaly threshold: 15
- First-run history: 90 days

Field notes:

- **Status**: `active` (run it), `paused` (keep config, skip runs), `example` (never run).
- **Sender**: the exact from-address of the report email.
- **Subject contains**: a stable fragment of the subject line; date suffixes that change each week are fine to omit.
- **Attachment type**: one of `xlsx`, `csv`, `pdf`.
- **Data location**: where the numbers live inside the attachment.
- **Period field**: which value labels the reporting period in trends.xlsx.
- **Metrics**: comma-separated column or row labels, exactly as they appear in the attachment. These become the columns of trends.xlsx.
- **Anomaly threshold**: percentage change versus the previous period that gets flagged in the summary. Default 15.
- **First-run history**: how far back the first inbox search goes. Default 90 days.

## weekly-sales-summary

- Status: example
- Sender: salesops@contoso.com
- Subject contains: Weekly Sales Summary
- Attachment type: xlsx
- Attachment filename contains: sales
- Cadence: weekly
- Data location: sheet "Summary", headers in row 1
- Period field: column "Week ending"
- Metrics: Revenue, Units sold, Refund rate
- Anomaly threshold: 15
- First-run history: 90 days

---
name: report-attachment-analyzer
description: Tracks a recurring emailed report end to end. It finds new report emails in the inbox, extracts data from their attachments, appends each reporting period to a trends spreadsheet, and rewrites a summary document with period-on-period deltas and flagged anomalies. Use when the user asks to update or analyse trends for a report that arrives by email on a schedule, or asks what changed in the latest weekly or monthly report.
---

# Report Attachment Analyzer

## PURPOSE

Turn a recurring emailed report (a weekly sales export, a monthly cost CSV, a weekly KPI PDF) into a maintained trend spreadsheet and a refreshed written summary. On each run, find report emails not seen before, extract the configured metrics from their attachments, append one row per reporting period to trends.xlsx, and produce a DRAFT summary document with deltas against the previous period and flagged anomalies. All state lives in OneDrive files, so every run continues exactly where the previous run stopped, in any conversation.

## WHEN TO RUN

- The user asks to update, refresh or check trends for a report that arrives by email on a schedule.
- The user asks what changed in the latest weekly or monthly report, or whether the latest numbers look unusual.
- The user asks to set up tracking for a recurring emailed report (first-run configuration).

Do not run this skill for a one-off email attachment. Summarising a single attachment once is a plain Email plus Excel task and needs no trend state.

## INPUTS YOU GATHER

1. The configuration file references/report-config.md (relative to this skill folder). Each H2 block with `Status: active` defines one tracked report: sender, subject pattern, attachment type, cadence, data location, period field, metrics, anomaly threshold and first-run history window.
2. If no block has `Status: active`, stop and gather the configuration in conversation: ask the user for each field listed in references/report-config.md, then write a completed block into that file. Show the block to the user and get a yes before saving, because this edits an existing file.
3. If the config defines several active reports and the user did not name one, ask which report to run. If the user says all, run the full workflow once per report.
4. Existing state in the working folder (defined below): trends.xlsx and processed-log.md, if they exist.

## WORKFLOW

The working folder for a report is the OneDrive path `/Documents/Cowork/output/report-attachment-analyzer/<report-name>/`, where `<report-name>` is the kebab-case H2 heading from the config. Call this WORK below. Always pass these full explicit paths to every built-in skill; never accept a session folder as a save location.

1. Read references/report-config.md and resolve the report block to run. If any required field is missing, ask the user for it before continuing.
2. Ensure WORK exists. On the first run for a report:
   a. Use the Excel built-in to create `WORK/trends.xlsx` with one sheet named Trends and this header row: Period, Received date, Source file, then one column per configured metric in config order.
   b. Create `WORK/processed-log.md` containing the table header shown in OUTPUT ARTIFACTS below.
3. Read `WORK/processed-log.md`. Collect every logged identity tuple (received timestamp, sender, subject, attachment filename) and the most recent received date. The log is keyed on these observable fields, not on email message IDs, which the built-in skills do not expose.
4. Use the Email built-in to search the inbox for messages from the configured sender whose subject contains the configured subject pattern. Search window: from the most recent logged received date minus 7 days (the overlap catches late-logged stragglers). On the first run, search back over the configured first-run history window (default 90 days). Discard any message whose received timestamp, sender, subject and attachment filename together match a row already in processed-log.md. Sort the remainder oldest first.
5. If no new messages remain: tell the user there are no new instances since the last logged date, state the full paths of trends.xlsx and the most recent summary, and stop. Offer to regenerate the summary from existing data if the user wants one anyway.
6. For each new message, oldest first:
   a. Identify the report attachment. If the message has several attachments, use the configured attachment filename pattern; if it is still ambiguous, ask the user which file is the report.
   b. Attempt to save a copy of the attachment to `WORK/attachments/YYYY-MM-DD-<original-filename>`, where the date is the message received date, then verify the file exists at that path. Saving an attachment to a chosen folder is not guaranteed by the built-in skills: if the save fails or cannot be verified, note "copy unavailable" in that message's processed-log.md row and continue with metric extraction. Never claim a copy was saved without verifying it.
   c. Extract the configured metrics. For xlsx or csv attachments, use the Excel built-in to open the saved copy (or read the attachment content directly when no copy could be saved) and read the values from the configured sheet and metric columns. For PDF attachments, use the PDF built-in to extract the table described in the config and read the metric values from it.
   d. Determine the reporting period from the configured period field; if the file has no usable date, use the email received date and note this in the run report.
   e. If a configured metric is missing or unreadable, leave that cell blank and record a data gap. Never estimate or fill in a value.
7. Use the Excel built-in to append one row per extracted period to the Trends sheet of `WORK/trends.xlsx`. Appending new rows is allowed; never modify or delete existing rows. If the period already exists in the sheet, do not overwrite it: tell the user a duplicate or resend arrived for that period and ask whether to append it as an extra row with "(revised)" after the period value, or to ignore it.
8. After all messages are processed, compute from the Trends sheet, for each metric: latest value, previous value, absolute change, and percentage change. Flag a metric as an anomaly when the absolute percentage change meets or exceeds the configured anomaly threshold (default 15 percent). When the sheet holds four or more periods, also compare the latest value to the average of all prior periods and note any metric more than the threshold away from that average.
9. Use the Word built-in to write `WORK/summary-YYYY-MM-DD.docx` (today's date), following the section structure in references/summary-structure.md. The document title must start with DRAFT.
10. Ask the user: replace summary-latest.docx with today's summary? Only after an explicit yes, use the Word built-in to write the same content to `WORK/summary-latest.docx`. If the user declines or does not answer, leave summary-latest.docx untouched; the dated file already exists either way.
11. Append one row to `WORK/processed-log.md` for every message handled in this run, including skipped and unreadable ones, using the statuses defined below. Fill in the identity columns (Received, Sender, Subject, Attachment) exactly as observed, since the next run's dedupe in step 4 matches on them.
12. Verify each file written in this run exists at its named WORK path (attachment copies already marked "copy unavailable" in step 6b are exempt). If any output landed in a session folder instead, copy it to the named WORK path and report both locations; do not delete the stray copy without approval.
13. Report in the conversation: how many new messages were found, how many rows were appended, which metrics were flagged as anomalies, the full OneDrive path of every file written or updated, and whether summary-latest.docx was replaced or only the dated summary was saved.

## OUTPUT ARTIFACTS

All under `/Documents/Cowork/output/report-attachment-analyzer/<report-name>/` in OneDrive:

- `trends.xlsx`: sheet Trends, append-only, one row per reporting period. Columns: Period, Received date, Source file, then one column per configured metric.
- `summary-YYYY-MM-DD.docx`: new versioned summary written every run, structure per references/summary-structure.md, title starts with DRAFT.
- `summary-latest.docx`: same content, written only after explicit user approval in step 10.
- `processed-log.md`: markdown table with header `| Received | Sender | Subject | Attachment | Period | Status | Processed on |`. Status is one of: appended, duplicate-skipped, revised-appended, unreadable, data-gap; add "copy unavailable" to the Status cell when the audit copy in step 6b could not be saved.
- `attachments/YYYY-MM-DD-<original-filename>`: dated copy of each source attachment, kept for audit where the platform allows saving attachments; messages whose copy could not be saved are marked "copy unavailable" in processed-log.md.

## FALLBACKS AND EDGE CASES

- Email search finds nothing but the user says the report arrived: retry the subject pattern with the Enterprise Search built-in, and tell the user exactly which sender, subject pattern and date window were searched so they can correct the config.
- Attachment will not open or PDF table extraction fails: attempt the dated copy as in step 6b, log the message with status unreadable, list it in the run report, and move on. Never guess values from a failed extraction.
- A metric column was renamed in the source file: leave the cell blank, log status data-gap, and suggest the user update the Metrics line in references/report-config.md.
- A resend or correction arrives for an already-logged period: handled in step 7; never silently replace existing figures.
- Outputs saved into a session folder instead of WORK: handled in step 12; always re-state the explicit path when calling a built-in.
- This skill never writes to Planner or To Do, so there is no silent-failure path: every piece of state is one of the files listed above, and step 13 names each one.
- The skill folder was added mid-conversation: Cowork only discovers skills when a new conversation starts, so tell the user to start a new conversation if discovery seems to have failed.

## SAFETY RULES

- Never delete or overwrite any file without explicit user approval in the conversation. trends.xlsx is append-only: adding rows is allowed, changing or removing existing rows is not, without approval.
- summary-latest.docx is overwritten only after the user says yes in step 10. The dated summary is always written first as a new file.
- Every generated document is labelled DRAFT until a human reviews it.
- Use the Email built-in for reading and searching only. This skill never sends email and never creates email drafts.
- Never invent, estimate or extrapolate a metric value. Blanks stay blank and are reported as data gaps.
- Edits to references/report-config.md are shown to the user and approved before saving.

## QUALITY SELF-CHECK

- [ ] Every message handled this run now has a row in processed-log.md with a status
- [ ] No existing row in trends.xlsx was modified or deleted
- [ ] The increase in Trends row count equals the number of appended rows reported to the user
- [ ] Every metric value in the new rows matches the source attachment exactly
- [ ] The dated summary file exists; summary-latest.docx was changed only after an explicit yes
- [ ] The summary title starts with DRAFT and follows references/summary-structure.md
- [ ] The conversation report lists the full OneDrive path of every file written or updated
- [ ] No value was invented for missing or unreadable data; all gaps are listed in the summary

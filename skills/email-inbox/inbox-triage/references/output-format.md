# Triage output format

The inbox-triage skill copies this structure when writing triage-YYYY-MM-DD.md.
Replace every value in curly braces. Omit a category section only if its count
is zero; keep the zero in the summary table either way.

---

# Inbox triage report, {YYYY-MM-DD}

DRAFT until reviewed.

Scope: {folder}, {time window}, {n} messages read. {Note if any were left untriaged because of the cap.}
Mode: {rules applied | report-only, no active rules}.

## Summary

| Category | Count |
|---|---|
| needs-reply-today | {n} |
| needs-reply-this-week | {n} |
| waiting-on-others | {n} |
| FYI | {n} |
| noise | {n} |

## Needs reply today

| From | Subject | Received | Why | Draft created |
|---|---|---|---|---|

## Needs reply this week

| From | Subject | Received | Why | Draft created |
|---|---|---|---|---|

## Waiting on others

| From | Subject | Received | Waiting for |
|---|---|---|---|

## FYI

| From | Subject | Received |
|---|---|---|

## Noise

| From | Subject | Received | Matched rule, if any |
|---|---|---|---|

## Drafts created

| Reply subject | Note |
|---|---|

{List any needs-reply messages not drafted, with the reason.}

## Rule actions

| Message | Rule | Action | Result |
|---|---|---|---|

{In report-only mode write: "Report-only mode, nothing was moved or archived."}

## Rules skipped

{List ambiguous or malformed rules and move rules whose target folder is missing, or write "None."}

## Files written

| File | OneDrive location |
|---|---|

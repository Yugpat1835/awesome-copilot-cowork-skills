# Change Journal Format

How the no-delete-guardrail skill writes /Documents/Cowork/output/change-journal.md on the user's OneDrive. The journal is append-only: add rows at the bottom, never edit or remove existing rows.

## Creating the journal

When the journal file does not exist yet, create it with this exact header:

```
# Cowork Change Journal

Append-only log written by the no-delete-guardrail skill. One row per create, modify, move, rename, archive or delete, including refused and pending operations. Do not edit existing rows.

| Timestamp (UTC) | Item | Operation | Approval | Result |
|---|---|---|---|---|
```

## Column rules

- Timestamp (UTC): ISO 8601, for example 2026-06-10T14:32:00Z.
- Item: full OneDrive or SharePoint path for files and folders; subject line plus mailbox folder for email; event title plus date for calendar items.
- Operation: one of create, modify, move, rename, archive, delete.
- Approval: one of not-required (safe create or new versioned file), approved (quote the user's approving words in brackets), refused (bulk destructive), pending (listed but not yet approved).
- Result: one of done, failed (add a one-line reason), refused, skipped.

## Example rows

| Timestamp (UTC) | Item | Operation | Approval | Result |
|---|---|---|---|---|
| 2026-06-10T09:14:00Z | /Documents/Cowork/output/q3-summary-v2.docx | create | not-required (versioned copy, original untouched) | done |
| 2026-06-10T09:21:00Z | /Documents/Projects/old-draft.docx | delete | approved ("yes, delete the old draft") | done |
| 2026-06-10T09:25:00Z | /Documents/Archive/ (all 47 files) | delete | refused (bulk destructive) | refused |

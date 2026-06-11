# File Templates: project.md, decisions.md, links.md

Use these as the initial content when scaffolding a new project folder. Replace `<Project name>` and the date placeholders with real values; set every field the user has not supplied to TBC. The risks.md template lives separately in references/raid-log-template.md.

Shared conventions:

- Every file starts with a Changes section. Prepend one dated line per update run: date, what was added or revised, sources scanned and window.
- Logs are newest first.
- Decision Status values: Agreed, Superseded by D-xxx. Superseded decisions stay in the table.
- Never delete rows or log entries; mark them Superseded instead.

---

## Template: project.md

```markdown
# Project: <Project name>

## Changes

- YYYY-MM-DD: File created.

## Overview

- Project name: <Project name>
- Folder name: <project-name>
- Aliases (other names used in email and Teams): TBC
- Sponsor: TBC
- Project lead: TBC
- Start date: TBC
- Target end date: TBC
- Goal (one sentence): TBC

## Current status

- Overall: Green / Amber / Red (pick one)
- Summary (3 lines maximum): TBC

## Milestones

| Milestone | Target date | Status |
|-----------|-------------|--------|
| TBC | YYYY-MM-DD | Not started |

## Progress log (newest first)

- YYYY-MM-DD: TBC (source: TBC)
```

---

## Template: decisions.md

```markdown
# Decision log: <Project name>

## Changes

- YYYY-MM-DD: File created.

## Decisions (newest first)

| ID | Date | Decision | Context (why) | Decided by | Source | Status |
|----|------|----------|---------------|------------|--------|--------|
| D-001 | YYYY-MM-DD | TBC | TBC | TBC | TBC | Agreed |
```

Note: decision IDs (D-001) and dependency IDs in risks.md (also D-001) are separate sequences in separate files; when cross-referencing, write "decisions.md D-001" or "risks.md D-001" to avoid ambiguity.

---

## Template: links.md

```markdown
# Links and key files: <Project name>

## Changes

- YYYY-MM-DD: File created.

## Links (newest first)

| Added | Title | Type | Location | Why it matters |
|-------|-------|------|----------|----------------|
| YYYY-MM-DD | TBC | SharePoint doc / Teams thread / email / external URL | TBC | TBC |
```

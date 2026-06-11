---
name: project-status-tracker
description: Maintains living project files (project.md, decisions.md, risks.md, links.md) in a per-project OneDrive folder from emails, Teams channels and meeting transcripts, and generates a weekly DRAFT status document in Word. Use when the user asks to set up tracking for a project, update a project's status files, log a decision or risk, or produce a weekly status report for a named project.
---

## PURPOSE

Keep one OneDrive folder per project as the single source of truth: four living Markdown files (project.md, decisions.md, risks.md, links.md) that you update from email, Teams and meeting transcripts, plus a weekly status document generated from those files. This skill composes the Email, Enterprise Search, Meetings and Word built-in skills. It does not duplicate Daily Briefing: Daily Briefing is a cross-everything daily summary with no memory, this skill maintains durable per-project state between sessions.

## WHEN TO RUN

- The user asks to start or set up tracking for a named project.
- The user asks to update a project's files, or to catch a project up from recent email, Teams or meetings.
- The user asks to log a specific decision, risk, issue or link against a project.
- The user asks for a weekly status report, status doc or status update for a project.

## INPUTS YOU GATHER

Ask only for what is missing; never guess.

1. Project name. Convert it to kebab-case for the folder name (for example "Helios Migration" becomes helios-migration). If more than one existing folder under /Documents/Cowork/projects/ could match, list the candidates and ask before writing anything.
2. Aliases: other names the project goes by in email subjects and Teams (codenames, ticket prefixes). Store them in project.md so later runs search for them too.
3. Time window to scan. Default: since the most recent dated entry in the Changes section of project.md. On the first update after scaffolding, default to the last 14 days. Confirm the window with the user before scanning.
4. What they want this run: scaffold only, update the files, generate the status doc, or update then generate.
5. For the status doc, the audience if stated (for example steering committee or team), used only to set the level of detail in the Summary section.

## WORKFLOW

1. Resolve the project folder at /Documents/Cowork/projects/<project-name>/ in the user's OneDrive. Check whether it exists.

2. First run (folder does not exist): create the folder and scaffold exactly four files:
   - project.md, decisions.md and links.md from the templates in references/file-templates.md
   - risks.md from the RAID template in references/raid-log-template.md
   Fill in any header fields the user has already given you (name, aliases, sponsor, dates, goal); set every unknown field to TBC. Date the first Changes entry in each file with today's date. Report the four exact paths created. Stop here unless the user also asked for an update or a status doc in the same request.

3. Update run, gather sources for the agreed window:
   a. Use the Email built-in skill to search the user's mailbox for messages mentioning the project name or any alias from project.md. Read only: do not move, reply to or send anything.
   b. Use the Enterprise Search built-in skill to find Teams channel messages and SharePoint documents mentioning the project name or aliases.
   c. Use the Meetings built-in skill to pull transcripts or recaps of meetings whose title or content matches the project name or aliases.

4. Classify each finding into exactly one category:
   - progress or status update: goes to the Progress log in project.md
   - decision: goes to the Decision log in decisions.md
   - risk, assumption, issue or dependency: goes to the matching RAID table in risks.md
   - useful file, thread or URL: goes to the table in links.md
   Every item records a date, a one-line summary, its source (for example "Teams #helios-migration, 9 June 2026" or "email from A. Sponsor, 8 June 2026") and an owner where one is stated. Never invent owners, dates or facts; write TBC for anything not stated in a source.

5. Update the four files using append-and-revise:
   - Prepend a dated entry to the Changes section at the top of each file you touch: today's date, what was added or revised, which sources were scanned and for what window.
   - Append new items to the relevant section or table. Never silently delete existing content. When an item is out of date, set its Status to Superseded with today's date and a pointer to the replacement entry; do not remove the row.
   - Treat content the user has edited by hand as authoritative: merge around it, never reformat or rewrite their entries.
   - In risks.md, follow the conventions in references/raid-log-template.md: continue the ID sequences (R-, A-, I-, D-), and give every Open risk an owner and a review date. If no owner was stated, set Owner to TBC and carry the risk into the Asks section of the next status doc.
   - Save each file back to its exact path under /Documents/Cowork/projects/<project-name>/ and verify the save landed there (see FALLBACKS AND EDGE CASES).

6. Generate the weekly status document when the user asked for it:
   - Compute the ISO 8601 week number for today, zero-padded to two digits. Filename: status-YYYY-WW.docx (for example status-2026-24.docx for the week starting Monday 8 June 2026).
   - Use the Word built-in skill to create the document in /Documents/Cowork/projects/<project-name>/ with these sections in order: Summary (5 lines maximum, lead with the Green/Amber/Red status from project.md), Progress this week, Decisions taken, Top risks (maximum 5, each with owner and mitigation, taken from Open and Mitigating rows in risks.md), Asks (including any risks with Owner TBC).
   - Put "DRAFT, not yet reviewed" in the document header and after the title.
   - Build the document only from the four files plus this run's classified findings. Add no new claims.
   - If status-YYYY-WW.docx already exists in the folder, do not overwrite it: write status-YYYY-WW-v2.docx (then -v3 and so on) and tell the user both filenames.

7. Report. End every run with: each artifact written and its full OneDrive path, the sources scanned and the window used, the number of items added or revised per file, any sources you could not access, and any TBC fields that need the user's input.

## OUTPUT ARTIFACTS

All artifacts live in /Documents/Cowork/projects/<project-name>/ in the user's OneDrive:

| File | Content | When written |
|------|---------|--------------|
| project.md | Overview, aliases, Green/Amber/Red status, milestones, progress log | Scaffolded on first run, updated every run |
| decisions.md | Decision log with context, decider, source and status | Scaffolded on first run, updated when decisions found |
| risks.md | RAID log (risks, assumptions, issues, dependencies) | Scaffolded on first run, updated when RAID items found |
| links.md | Key files, threads and URLs with why each matters | Scaffolded on first run, updated when links found |
| status-YYYY-WW.docx | Weekly DRAFT status document | Only when the user asks for a status doc |
| actions.md | Action items with owner and due date | Only when the user asks for action tracking (see fallback below) |

## FALLBACKS AND EDGE CASES

- Save location drift: outputs sometimes land in session folders instead of the named path. After every write, confirm the file exists at its stated /Documents/Cowork/projects/<project-name>/ path. If it landed anywhere else, save it again to the project folder and report both locations. Never end a run without stating where each file actually is.
- Planner and To Do: writes to Planner and Microsoft To Do can fail silently. If the user asks to track actions or tasks, write them to actions.md in the project folder first (the file is the record), then attempt Planner or To Do only if the user asked for it, verify the items actually appear there, and report which path succeeded.
- No findings in the window: say so plainly, add a dated "no new items" entry to the Changes section of project.md only, and leave the other three files untouched.
- Folder exists but a file is missing: recreate only the missing file from its template and note the recreation in that file's Changes section.
- Inaccessible sources (missing transcript, restricted channel, search returning nothing for a known-active project): record exactly what could not be read in the Changes entry so the gap is visible, and list it in the end-of-run report.
- Ambiguous classification (an item that is both a decision and a risk): record the decision in decisions.md and any residual exposure as a risk in risks.md, cross-referencing the IDs.
- Very long progress logs: when project.md exceeds about 250 lines, propose archiving older Progress log entries to project-archive-YYYY-MM.md in the same folder. Only do it after the user approves, and leave a pointer line in project.md.

## SAFETY RULES

- Never delete or overwrite any file without the user's explicit approval in the conversation. Prefer new versioned files (-v2, -v3).
- The four living files are append-and-revise only: mark items Superseded, never remove them.
- Email is read-only in this skill. If the user wants the status sent by email, create a Draft only, never send.
- Every generated document carries the DRAFT label until the user confirms they have reviewed it.
- Never invent progress, decisions, risks, owners, dates or links. Anything not stated in a source is TBC.

## QUALITY SELF-CHECK

Before reporting completion, verify:

- [ ] Every file touched this run has a new dated entry at the top of its Changes section.
- [ ] No existing content was removed; superseded items are marked, not deleted.
- [ ] Every new item has a date and a source, and an owner where one was stated; nothing was invented.
- [ ] Every Open risk in risks.md has an owner and a review date, or appears under Asks.
- [ ] The status doc (if generated) contains only material traceable to the four files and is labelled DRAFT.
- [ ] Every artifact was verified at its full /Documents/Cowork/projects/<project-name>/ path and all paths were reported to the user.
- [ ] No email was sent, no file was overwritten without approval, and any Planner or To Do attempt was verified and reported.

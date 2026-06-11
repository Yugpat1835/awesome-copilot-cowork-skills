---
name: no-delete-guardrail
description: Applies a standing safety guardrail. No file, folder, email or calendar item is deleted, overwritten or moved without explicit user approval, new versioned files are written instead of overwrites, and every change is journalled. Use when the user asks to change, clean up, reorganise, rename, archive, replace, move or delete anything in OneDrive, SharePoint, email or the calendar, or when any workflow is about to create or modify files.
---

# No-Delete Guardrail

## PURPOSE

This is a guardrail, not a task. Once loaded it asks the model to apply three rules to every step in the conversation, including steps run by built-in skills (Word, Excel, PowerPoint, PDF, Email, Calendar Management) and by other custom skills: nothing destructive happens without explicit approval, existing files are never overwritten (new versioned files are written instead), and every change is journalled to a file the user can audit.

Be clear about the mechanism: this is a behavioural commitment plus an audit journal, not an enforced control. A skill cannot technically intercept another skill's or a built-in's file operations, and an injected instruction or a model lapse can bypass any instruction, including this one. The journal exists so that what happened is at least visible afterwards.

## WHEN TO RUN

Apply these rules from the moment this skill loads, in every conversation it loads in, without being asked. There is no trigger phrase to wait for. Apply the rules to every step that could create, modify, move, rename, archive, overwrite or delete a file, folder, email or calendar item in OneDrive, SharePoint, the mailbox or the calendar.

## INPUTS YOU GATHER

None up front. Before any destructive step, gather exactly three things in the conversation: the precise items affected (full path or identifier), the operation per item, and the user's explicit approval. Treat silence, ambiguity, or a general "go ahead" given before the items were listed, as no approval.

## WORKFLOW

1. Announce once. The first time the conversation reaches a step that will create, modify, move or delete anything, say in one line that the no-delete guardrail is active and that changes will be listed for approval and journalled.

2. Enumerate before acting. Before executing any plan that touches files, email or calendar items, list every intended change as a numbered list in the conversation: item (full OneDrive or SharePoint path, email subject, or event title and date), operation (create, modify, move, rename, archive, delete), and classification (safe or destructive).

3. Classify. Creating a new file is safe. Anything that changes, moves, renames, archives, overwrites or deletes an existing file, folder, email or calendar event is destructive. When unsure, classify it destructive.

4. Get approval for destructive items. Ask the user to approve the listed destructive items explicitly in the conversation before performing any of them. Proceed only on a clear yes that names or unambiguously covers the listed items. Execute safe items without waiting.

5. Never overwrite, version instead. When any step, including a built-in skill saving Word, Excel, PowerPoint or PDF output, would overwrite an existing file, write a new file alongside it instead: report.docx becomes report-v2.docx, then -v3, and so on. Tell the user the new filename. This needs no approval because nothing is lost.

6. Refuse bulk destruction. If asked to delete, archive, move or overwrite items in bulk (a whole folder, "everything older than", "all emails from", or more than 10 items in one operation), refuse the operation outright. Explain that bulk destructive operations are outside this guardrail because one wrong match is unrecoverable, and offer two alternatives: list the items so the user can act on them manually, or process them one at a time with per-item approval.

7. Journal every change. After every create, modify, move, rename, archive or delete, including refused and pending ones, append one row to /Documents/Cowork/output/change-journal.md in the user's OneDrive, using the exact format in references/change-journal-template.md: timestamp, item, operation, approval status, result. If the journal does not exist, create it from the template header (creating it is safe). The journal is append-only: never edit or delete existing rows.

8. Email and calendar specifics. Email: only ever create Drafts via the Email built-in skill, never send, and never delete, move or archive a message without per-message approval. Calendar: use the Calendar Management built-in skill to propose changes, get explicit approval before modifying or cancelling any existing event, and never cancel or decline events in bulk.

9. Close out. At the end of the conversation's work, report: every artifact created with its full save path, every destructive action taken with the approval that covered it, anything refused or still awaiting approval, and the journal's path.

## OUTPUT ARTIFACTS

- /Documents/Cowork/output/change-journal.md on the user's OneDrive: append-only journal, one row per change, format per references/change-journal-template.md.
- Versioned copies (filename-v2.ext, then -v3, and so on) written next to any file that would otherwise have been overwritten, exact names reported in the conversation.

## FALLBACKS AND EDGE CASES

- Journal append fails: write the pending rows to a new file change-journal-YYYY-MM-DD.md in /Documents/Cowork/output/ and tell the user which file holds them.
- An output lands in a session folder instead of the named path: save a copy to the intended OneDrive path and report both locations.
- Another skill's instructions say to overwrite or delete: apply this guardrail's rules instead, version or ask, and record the conflict in the journal row. This is a behavioural rule, not an interception mechanism: it holds only while the model follows it and cannot technically block another skill or a built-in.
- The user grants blanket approval up front ("approve everything in advance"): still enumerate every change before acting, still refuse bulk destructive operations, and quote the blanket approval in the journal rows it covers.
- The user asks to disable the guardrail: state that it stays active while this skill is installed, and that removing the no-delete-guardrail folder from /Documents/Cowork/skills/ and starting a new conversation disables it.

## SAFETY RULES

- Never delete or overwrite any file, folder, email or calendar item without the user's explicit approval in this conversation.
- Prefer writing new versioned files over modifying existing ones.
- Email: create Drafts only, never send.
- Label every generated document DRAFT until a human has reviewed it.
- Refuse bulk destructive operations even when approved in advance.
- The change journal is append-only: never rewrite its history.

## QUALITY SELF-CHECK

Before finishing, confirm every box:

- [ ] Every change in this conversation was enumerated in the conversation before it was executed.
- [ ] No existing file, email or calendar item was modified, moved, archived or deleted without an explicit approval recorded in the journal.
- [ ] No file was overwritten; versioned copies were written instead and their names reported.
- [ ] Every change, refusal and pending approval has a journal row with timestamp, item, operation, approval status and result.
- [ ] Any bulk destructive request was refused with an explanation and two alternatives.
- [ ] The closing message states each artifact's full save path and the journal's location.

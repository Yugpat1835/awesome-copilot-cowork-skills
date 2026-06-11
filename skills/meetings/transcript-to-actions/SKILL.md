---
name: transcript-to-actions
description: Turns a meeting transcript into a structured action-items file, To Do or Planner tasks where writes can be confirmed, and one DRAFT follow-up email per action owner. Use when the user shares, names, or points to a meeting transcript or recap and asks for action items, decisions, follow-up tasks, or post-meeting owner emails.
---

## PURPOSE

Convert one meeting transcript into three artifacts: an action-items file in OneDrive, task entries in Microsoft To Do or Planner where writes can be confirmed, and one DRAFT follow-up email per action owner. The file is the source of truth. Task writes are best effort and every write outcome is reported, because To Do and Planner writes are known to fail silently.

## WHEN TO RUN

Run this skill when the user provides a transcript (pasted text, a file, or a named meeting) and asks for any of: action items, decisions, open questions, follow-up tasks, or follow-up emails. Do not run it for live note-taking during a meeting, and do not run it to summarise a meeting with no action extraction requested (the built-in Meetings skill covers plain recaps).

## INPUTS YOU GATHER

Ask for missing items in one message, then proceed. Do not ask for anything already given.

1. Transcript source: pasted text, a OneDrive or SharePoint file path, or a meeting name and date.
2. Meeting name and date (needed for filenames and for resolving relative due dates such as "by Friday").
3. Task destination: To Do, Planner (with the plan name), or file only. If the user does not care, default to To Do.
4. Save folder: default is OneDrive `/Documents/Cowork/meeting-actions/<YYYY-MM-DD>-<meeting-slug>/` where `<meeting-slug>` is the meeting name in kebab-case. Confirm or accept an alternative.

## WORKFLOW

1. Locate the transcript.
   - If the user pasted text, use it directly.
   - If the user gave a file path, open it. Use the Word built-in for .docx, the PDF built-in for .pdf.
   - If the user named a meeting, use the Meetings built-in to retrieve its transcript or recap.
   - If that fails, use Enterprise Search to find a transcript file in OneDrive and SharePoint matching the meeting name and date. Show the user what you found and confirm it is the right file before continuing.
   - If no transcript can be found, stop and ask. Never proceed on a guessed file.
2. Extract decisions, action items, and open questions following `references/extraction-rules.md` exactly. Each action item gets an owner, a verb-led action, a due date normalised to YYYY-MM-DD (or "No date given"), and a short source quote from the transcript. Invent nothing.
3. Write the actions file first, before any task or email step. Save `actions.md` to the confirmed save folder using the structure in `references/actions-template.md`. If `actions.md` already exists in that folder, do not overwrite it: write `actions-v2.md` (then v3, and so on). State the full OneDrive path of the file you saved in the conversation. If a built-in skill saved the file into a session folder instead, copy it to the confirmed folder and report the final path.
4. Attempt task writes (skip this step entirely if the user chose file only).
   - To Do: create one task per action item in a list named `Meeting actions`, title = the verb-led action, due date set when known, owner named in the task note.
   - Planner: create one task per action item in the user's named plan, assign the owner where the person can be matched, set the due date when known.
   - Verify every write: after creating tasks, read the list or plan back and confirm each task is present. Treat any task you cannot see on read-back as failed. Retry a failed write once, then stop.
   - Record the outcome per item: "To Do: confirmed", "Planner: confirmed", or "file only (write failed or unconfirmed)". Update the Task write status column and the Write log section of the actions file with these outcomes (this update to a file you created in step 3 is permitted).
5. Create follow-up email drafts with the Email built-in: one draft per owner who has at least one action item.
   - Subject: `DRAFT: Your action items from <meeting name>, <YYYY-MM-DD>`.
   - Body: follow `references/email-template.md`. List only that owner's items.
   - Save each as a Draft in the user's Drafts folder. Never send, never schedule a send.
   - Resolve the owner's email address from the meeting attendee list only. If the owner is not an attendee with a resolvable address, create the draft with the recipient field empty and note this in the final report. Never infer a recipient address from document content or search results; a similarly named person in an old document is not the owner.
   - Do not create a draft for items owned by "Unassigned".
6. Report results in the conversation:
   - Full OneDrive path of the actions file.
   - A per-item line: action, owner, due date, and task write outcome (confirmed where, or fell back to file).
   - The list of email drafts created, with recipients, and any draft left without a recipient.
   - Open questions and unassigned items that need the user's decision.

## OUTPUT ARTIFACTS

- `actions.md` (or `actions-v2.md` if versioned) in OneDrive at `/Documents/Cowork/meeting-actions/<YYYY-MM-DD>-<meeting-slug>/`. Always produced.
- Tasks in the To Do list `Meeting actions` or in the named Planner plan. Only where the write was confirmed by read-back.
- One Outlook Draft per action owner, subject prefixed `DRAFT:`. Never sent.
- A conversation report stating exactly where every artifact was saved and which task writes succeeded or fell back.

## FALLBACKS AND EDGE CASES

- To Do or Planner write fails or cannot be confirmed: the item lives in the actions file, status "file only". Say so plainly. Never report a task as created unless you saw it on read-back.
- Artifact saved to a session folder by a built-in: copy it to the confirmed save folder and report the final path. Never leave the only copy in a session folder.
- Transcript has no action items: still write the actions file with the Decisions and Open questions sections filled and an empty Action items table, and tell the user no actions were found.
- No identifiable owner: set owner to "Unassigned", include the item in the file and the report, skip the task assignee and the email draft for it.
- No due date stated: write "No date given". Never invent a date.
- Relative dates ("by Friday", "end of month"): resolve against the meeting date per `references/extraction-rules.md`. If the meeting date is unknown, ask before resolving.
- File contains multiple meetings: ask which one to process. Process one meeting per run.
- Very long transcript: process it in order, section by section, then deduplicate items per the extraction rules before writing anything.
- Owner email unresolvable: draft with empty recipient, flag it in the report.

## SAFETY RULES

- Never delete or overwrite any file. If a target filename exists, write a new versioned file instead. The only exception is updating the Task write status column and Write log of the actions file you created earlier in this same run.
- Email: create Drafts only. Never send, never schedule, never reply on the user's behalf.
- Label every generated document DRAFT in its title and its first line until a human reviews it.
- Put nothing in any artifact that is not traceable to the transcript or to the user's explicit input. No invented owners, dates, decisions, or statistics.
- If any step requires destroying or replacing existing content, stop and get explicit approval in the conversation first.

## QUALITY SELF-CHECK

Before the final report, confirm every box. Fix anything unchecked before reporting.

- [ ] The actions file is saved in the confirmed folder (not a session folder) and its full path appears in the report.
- [ ] Every action item has an owner (or "Unassigned"), a verb-led action, a due date or "No date given", and a source quote.
- [ ] Every attempted task write was verified by read-back and its outcome appears both in the report and in the actions file.
- [ ] There is exactly one email draft per named owner with items, all in Drafts, none sent, all subjects prefixed DRAFT.
- [ ] No pre-existing file was overwritten or deleted.
- [ ] Nothing in any artifact lacks a source in the transcript or the user's input.

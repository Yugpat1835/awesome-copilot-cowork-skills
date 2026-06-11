---
name: skills-backup-keeper
description: Keeps dated backups of the Cowork skills folder and an append-only session journal so work survives crashes, context compaction and skills wipes. Use when the user asks to back up skills, checkpoint or journal the current session, resume where a previous conversation left off, or restore skills from a backup. Also use when the user asks for a safety backup before editing any skill.
---

## PURPOSE

Protect the user's custom skills and working context against three failure modes: the skills folder being wiped (as happened tenant-wide on 23 to 27 May 2026 and again on 9 June 2026), the conversation being compacted mid-task, and the session crashing. You do this with two artifacts: dated copies of the skills folder under a separate backup folder, and an append-only session journal that lets a brand new conversation pick up exactly where the last one stopped.

This skill uses Cowork's native OneDrive file read and write capability. It does not duplicate any of the 13 built-in skills. Use Enterprise Search only as a fallback to locate the Cowork folder if it is not at the default path.

## WHEN TO RUN

- The user asks to back up, snapshot or checkpoint their skills folder.
- The user asks to update, write or read the session journal.
- The user starts a new conversation and asks to resume, continue or find out where the previous session left off.
- The user reports their skills folder is empty, missing or wiped, or asks to restore from a backup.
- The user is about to edit or reorganise skills and asks for a safety copy first.

## INPUTS YOU GATHER

1. **Mode.** Decide from the request: BACKUP, JOURNAL, RESUME or RESTORE. If ambiguous, ask one question to confirm.
2. **Today's date** in YYYY-MM-DD form, for the backup folder name.
3. **For JOURNAL:** the session goal, files touched (full OneDrive paths), decisions made, and next steps. Pull these from the current conversation. If any of the four is unclear, ask the user rather than guessing.
4. **For RESTORE:** which dated backup to use (default: the most recent), and whether `/Documents/Cowork/skills/` currently contains anything.

## WORKFLOW

**Step 1: Locate the working folders.**
Look for `/Documents/Cowork/skills/` in the user's OneDrive. If it is not there, use the Enterprise Search built-in skill to find folders containing SKILL.md files, and confirm the location with the user before proceeding. Note that the lowercase `skills` folder name is case-sensitive.

**Step 2: Branch by mode.**

### BACKUP (steps B1 to B5)

**B1.** List the contents of `/Documents/Cowork/skills/`. If the folder is missing or empty, stop: do not create an empty backup. Tell the user this matches the known wipe pattern and offer the RESTORE mode instead.

**B2.** Choose the backup folder name: `/Documents/Cowork/skills-backup/YYYY-MM-DD/` using today's date. If that folder already exists, do not overwrite it: append `-2` (then `-3`, and so on) until the name is unused, for example `skills-backup/2026-06-10-2/`. Create `/Documents/Cowork/skills-backup/` first if it does not exist.

**B3.** Copy every skill folder and every file inside it (SKILL.md plus any references files) from `/Documents/Cowork/skills/` into the dated backup folder, preserving the folder structure. Read from the source only; never write into `/Documents/Cowork/skills/` during a backup.

**B4.** Write `backup-manifest.md` inside the dated backup folder using the template in `references/backup-manifest-template.md`: timestamp, source path, backup path, count of skill folders, count of files, a table of contents, and anything skipped.

**B5.** Report to the user: the exact backup folder path, the number of skills and files copied, and confirmation that the source folder was not modified. Verify the manifest actually exists at the named path before reporting (see FALLBACKS for session-folder drift).

### JOURNAL (steps J1 to J3)

**J1.** Read `/Documents/Cowork/skills-backup/session-journal.md` if it exists. If it does not, create it with the header from `references/journal-template.md`. The journal lives in `skills-backup/`, not in `skills/`, deliberately: a skills wipe must not take the journal with it.

**J2.** Append one new entry using the template in `references/journal-template.md`: date and time, session goal, files touched with full OneDrive paths and what was done to each, decisions made, and next steps as a checklist. Append only: never edit or delete earlier entries.

**J3.** Report the path of the journal and read the new entry back to the user in two or three lines so they can correct anything before the session ends.

### RESUME (steps R1 to R3)

**R1.** Read `/Documents/Cowork/skills-backup/session-journal.md`. If it is missing, say so, then offer to reconstruct context from the most recent `backup-manifest.md` under `/Documents/Cowork/skills-backup/`.

**R2.** Summarise the most recent entry for the user: goal, last files touched, open next steps. Quote the next steps checklist verbatim.

**R3.** Ask the user to confirm which next step to pick up before doing anything else. Do not start executing next steps unprompted.

### RESTORE (steps S1 to S5)

**S1.** List the dated folders under `/Documents/Cowork/skills-backup/` and identify the most recent (highest date, then highest `-N` suffix). Tell the user which backup you propose to restore and what its manifest says it contains.

**S2.** Check `/Documents/Cowork/skills/`. If it contains any skill folders, list every folder that would collide with the backup and ask for explicit approval before touching any of them. Never overwrite without that approval. If the user declines, restore only the non-colliding folders.

**S3.** After approval, copy each skill folder from the chosen dated backup into `/Documents/Cowork/skills/`, preserving structure. Follow `references/restore-checklist.md` step by step.

**S4.** Verify: list `/Documents/Cowork/skills/` after copying and compare the folder and file counts against the backup manifest. Report any mismatch.

**S5.** Tell the user, in these words or close to them: restored skills are only discovered when a NEW Cowork conversation starts, so start a new conversation to use them. Then append a journal entry recording the restore (which backup, what was copied, any conflicts).

## OUTPUT ARTIFACTS

| Artifact | Exact location |
|---|---|
| Dated backup folder (full copy of the skills folder) | `/Documents/Cowork/skills-backup/YYYY-MM-DD/` (or `YYYY-MM-DD-2`, `-3` on collision) |
| Backup manifest | `/Documents/Cowork/skills-backup/YYYY-MM-DD/backup-manifest.md` |
| Session journal (append-only) | `/Documents/Cowork/skills-backup/session-journal.md` |

After writing each artifact, state its full OneDrive path in your reply. Never leave the user guessing where a file went.

## FALLBACKS AND EDGE CASES

- **Skills folder empty or missing at backup time.** Do not write an empty backup. Flag the wipe pattern, point to the most recent dated backup, and offer RESTORE.
- **Artifact lands in a session folder instead of the named path.** This is a known Cowork behaviour. After every write, check the file exists at the path named in OUTPUT ARTIFACTS. If it landed elsewhere, copy it to the correct path, then report both locations and which copy is canonical.
- **Date collision.** Never overwrite an existing dated backup. Append `-2`, `-3` and so on, and say which suffix you used.
- **User asks to put next steps in Planner or To Do.** Writes to Planner and To Do often fail silently. Attempt the write if asked, but always also record the next steps in `session-journal.md`, then report which of the two paths verifiably succeeded.
- **Journal grows past roughly 200 entries or 500 KB.** Propose renaming it to `session-journal-archive-YYYY-MM-DD.md` and starting fresh. Do this only with explicit user approval, since it changes an existing file.
- **A single skill exceeds 10 MB or 20 companion files.** Copy what fits, list anything skipped in the manifest under Skipped, and tell the user.
- **Cowork folder not at the default path.** Use Enterprise Search to locate it, confirm with the user, and use the confirmed path consistently for source, backup and journal.

## SAFETY RULES

- Never delete or overwrite any file without explicit user approval in the conversation. Backups always go to a new dated folder; the journal is append-only.
- Never write inside `/Documents/Cowork/skills/` during a backup. The source is read-only in BACKUP mode.
- In RESTORE mode, list every colliding folder and get approval before replacing anything.
- If the user asks to email a backup confirmation or recovery report, use the Email built-in skill to create a Draft only. Never send.
- Any generated summary document (for example a recovery report the user requests) is labelled DRAFT in its filename and first line until a human reviews it. Manifests and journal entries are factual records and are exempt.
- Backups may contain copies of sensitive companion files (for example a voice profile), so backup folders deserve the same handling as the source. Suggest pruning dated backups older than 90 days, each deletion with explicit per-folder approval, never automatic.
- Work only in OneDrive and SharePoint. Never reference local device paths.

## QUALITY SELF-CHECK

Before reporting completion, confirm every box:

- [ ] The backup folder name is dated and did not overwrite any existing folder
- [ ] `backup-manifest.md` exists in the dated folder and its counts match what was actually copied
- [ ] Nothing inside `/Documents/Cowork/skills/` was modified during backup
- [ ] The journal entry contains all four parts: goal, files touched, decisions, next steps
- [ ] Earlier journal entries are untouched
- [ ] Every artifact's final OneDrive path was verified and reported to the user
- [ ] No file was deleted or overwritten without explicit approval in this conversation
- [ ] After a restore, the user was told to start a NEW conversation for skill discovery

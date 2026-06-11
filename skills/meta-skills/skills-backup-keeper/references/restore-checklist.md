# Restore checklist

Follow these steps in order when restoring skills from a backup. Do not skip the approval gates.

1. **List available backups.** Enumerate the dated folders under `/Documents/Cowork/skills-backup/`. Sort by date, then by `-N` suffix (`2026-06-10-2` is newer than `2026-06-10`).
2. **Propose one backup.** Default to the most recent. Open its `backup-manifest.md` and tell the user the created timestamp, skill count and file count. Wait for confirmation of the choice.
3. **Check the target.** List `/Documents/Cowork/skills/`. Record which skill folders already exist there.
4. **Approval gate.** If any existing folder would be replaced by the restore, list every collision by name and ask for explicit approval. Without approval, restore only non-colliding folders and say which were left alone.
5. **Copy.** Copy each approved skill folder from the dated backup into `/Documents/Cowork/skills/`, preserving structure (each skill folder with its SKILL.md and any references files).
6. **Verify.** List `/Documents/Cowork/skills/` after the copy. Compare folder and file counts against the manifest. Report any mismatch instead of declaring success.
7. **Journal it.** Append a session-journal entry: which backup was restored, what was copied, any collisions and how they were resolved.
8. **Remind about discovery.** Tell the user that restored skills are only discovered when a NEW Cowork conversation starts, so they must start a new conversation to use them.

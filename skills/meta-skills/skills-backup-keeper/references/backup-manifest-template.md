# Backup manifest template

Write this file as `backup-manifest.md` inside every dated backup folder, filled in with real values:

```markdown
# Backup manifest

- **Created:** YYYY-MM-DD HH:MM (user's timezone)
- **Source:** /Documents/Cowork/skills/
- **Backup folder:** /Documents/Cowork/skills-backup/YYYY-MM-DD/
- **Skill folders copied:** N
- **Files copied:** N
- **Skipped:** none

## Contents

| Skill folder | Files | Notes |
|---|---|---|
| skill-name-1 | 3 | SKILL.md plus 2 references files |
| skill-name-2 | 1 | SKILL.md only |
```

Rules:

- Counts must match what was actually copied, verified by listing the backup folder after the copy, not by assuming the copy worked.
- If anything was skipped (over size limits, unreadable), replace `none` with one line per skipped item and the reason.
- One table row per skill folder. Files column counts every file in that folder including references.

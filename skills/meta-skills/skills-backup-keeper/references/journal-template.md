# Session journal template

Use this header once, when creating `/Documents/Cowork/skills-backup/session-journal.md` for the first time:

```markdown
# Session journal

Append-only record maintained by the skills-backup-keeper skill.
Newest entry at the bottom. Never edit or delete earlier entries.
```

Append one entry per session or checkpoint, exactly in this shape:

```markdown
---

## Session: YYYY-MM-DD HH:MM (user's timezone)

**Goal:** One sentence describing what this session set out to do.

**Files touched:**
- /Documents/Cowork/skills/<skill-name>/SKILL.md (created | edited | read)
- /Documents/<other-path> (created | edited | read)

**Decisions:**
- Decision made and the reason, one line each.

**Next steps:**
- [ ] First open action, specific enough to act on in a fresh conversation
- [ ] Second open action
```

Rules for entries:

- Every file path is a full OneDrive path. No bare filenames.
- Decisions record the why, not just the what, in one line each.
- Next steps must be executable by someone with no memory of this conversation.
- Keep each entry under 25 lines. Detail belongs in the files themselves.

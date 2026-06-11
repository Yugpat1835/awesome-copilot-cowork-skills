# Frontline Skeptic Reviewer

> Pressure-test your rollout plan against the people who will actually have to live with it, before it meets a busy Tuesday.

## What it produces

A structured review document, `<artifact-name>-frontline-skeptic-review.docx`, saved to `/Documents/Cowork/reviews/` in your OneDrive, containing:

- **VERDICT**: ready, ready with conditions, or not ready
- **TOP FINDINGS**: each one quotes or cites the exact part of your document it is about, no generic feedback; where the document is silent, the finding records an open question rather than an invented fact
- **RISKS**: from the frontline lens (adoption collapse, workaround creation, training without cover, workload stacking, initiative fatigue)
- **WHAT WOULD CHANGE MY MIND**: the specific evidence and commitments that would move the verdict up
- **5 INTERROGATION QUESTIONS**: the questions the people on the ground are likely to ask in the room

The persona lives in `references/persona.md`: mandate, ten probes, red flags, what convinces an experienced frontline veteran and what gets dismissed, plus documented blind spots so a validator can challenge the feedback where the archetype distorts it.

## Install in 60 seconds

1. Copy this folder (`frontline-skeptic-reviewer`) into your OneDrive at `/Documents/Cowork/skills/` (the lowercase `skills` folder name is case-sensitive).
2. Start a NEW Cowork conversation. Skills are discovered at conversation start, not mid-conversation.
3. Use one of the trigger phrases below, naming the file you want reviewed.

## Example triggers

- "Run a frontline skeptic review on crm-rollout-plan.docx"
- "What will the team on the ground actually say about this deck?"
- "Pressure-test this process change from the people who have to do the work"
- "Before I present this rollout, find where the team will work around it"

## Why this exists

The Executive Review Board suite ships seven C-suite reviewers, but plenty of plans clear the boardroom and then die on the floor. This skill is a bench persona for that suite: it extends the board below the C-suite to the person who does the work the document describes, asks where the extra clicks go, who covers the desk during training, and what got taken away to make room. It works standalone; you do not need the rest of the suite installed.

## Seat this persona on the review board

This skill works standalone, and its persona can also join the full [review-board](../review-board/) skill as a bench member:

1. Copy `references/persona.md` from this folder into your INSTALLED review-board skill folder in OneDrive, renamed to the pattern the board expects: `/Documents/Cowork/skills/review-board/references/persona-frontline-skeptic.md`.
2. Start a NEW conversation (skills and their files are discovered at conversation start).
3. Convene it by name: "run the review board with the CFO, CISO and Frontline Skeptic".

The board ships with 11 reference files plus its README, and Cowork allows 20 companion files per skill. Microsoft does not say whether the README counts towards that limit, so at least 8 bench personas fit at once; to seat all 9 safely, delete README.md from your installed copy of review-board (Cowork only needs SKILL.md and the references folder).

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---------|------------|-----------------|
| 1.0 | 2026-06-10 | Initial version |

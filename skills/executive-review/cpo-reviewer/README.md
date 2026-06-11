# CPO Reviewer

> Pressure-test your product plan against a CPO archetype before the real one asks where the users are.

## What it produces

A structured review document, `<artifact-name>-cpo-review.docx`, saved to `/Documents/Cowork/reviews/` in your OneDrive, containing:

- **VERDICT**: ready, ready with conditions, or not ready
- **TOP FINDINGS**: each one quotes or cites the exact part of your document it is about, no generic feedback
- **RISKS**: from the product lens (adoption failure, roadmap opportunity cost, scope creep, missing kill criteria)
- **WHAT WOULD CHANGE MY MIND**: the specific evidence that would move the verdict up
- **5 INTERROGATION QUESTIONS**: the questions the real CPO is likely to ask in the room

The persona lives in `references/persona.md`: mandate, ten probes, red flags, what convinces a CPO and what gets dismissed, plus documented blind spots so a validator can challenge the feedback where the archetype distorts it.

## Install in 60 seconds

1. Copy this folder (`cpo-reviewer`) into your OneDrive at `/Documents/Cowork/skills/` (the lowercase `skills` folder name is case-sensitive).
2. Start a NEW Cowork conversation. Skills are discovered at conversation start, not mid-conversation.
3. Use one of the trigger phrases below, naming the file you want reviewed.

## Example triggers

- "Run a CPO review on q3-roadmap-proposal.docx"
- "What would a Chief Product Officer say about this business case?"
- "Pressure-test this deck from a product lens, I present to the product council on Monday"
- "I'm pitching our CPO next week. Find the adoption holes in this plan first."

## Why this exists

This skill is a bench persona for the Executive Review Board suite (see the [review-board](../review-board/) folder, which orchestrates the core reviewers and ships the org profile template). The core board covers the executives who gate most approvals; bench personas extend it with the other seats at the table, and the CPO seat asks the questions the rest of the board does not: who has this problem, what do they do about it today, what does adoption cost them, and which roadmap bets this displaces. It works standalone; you do not need the rest of the suite installed.

## Seat this persona on the review board

This skill works standalone, and its persona can also join the full review-board skill as an extra reviewer:

1. Copy `references/persona.md` from this folder into your INSTALLED review-board skill folder in OneDrive, renamed to the pattern the board expects: `/Documents/Cowork/skills/review-board/references/persona-cpo.md`.
2. Start a NEW Cowork conversation (skills and their companion files are discovered at conversation start).
3. Convene it by name: "run the review board with the CFO, CISO and Chief Product Officer".

On capacity: the board ships with 11 reference files plus its README, and Cowork allows 20 companion files per skill. Microsoft does not say whether the README counts towards that limit, so at least 8 bench personas fit at once; to seat all 9 safely, delete README.md from your installed copy of review-board (Cowork only needs SKILL.md and the references folder).

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---------|------------|-----------------|
| 1.0 | 2026-06-10 | Initial version |

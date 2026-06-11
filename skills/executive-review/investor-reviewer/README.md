# Investor Reviewer

> Pressure-test your business case against the person whose capital is at stake, before you ask for the money in the room.

## What it produces

A structured review document, `<artifact-name>-investor-review.docx`, saved to `/Documents/Cowork/reviews/` in your OneDrive, containing:

- **VERDICT**: ready, ready with conditions, or not ready (conditions phrased as terms: gates, tranches, evidence required)
- **TOP FINDINGS**: each one quotes or cites the exact part of your document it is about, no generic feedback; where your document is silent, the finding records the open question rather than inventing an answer
- **RISKS**: from the capital lens (capital at risk before first evidence, opportunity cost, missing staging, downside and unwind costs)
- **WHAT WOULD CHANGE MY MIND**: the specific evidence or restructuring of the ask that would move the verdict up
- **5 INTERROGATION QUESTIONS**: the questions a real investor is likely to ask in the room

The persona lives in `references/persona.md`: mandate, ten probes, red flags, what convinces an investor and what gets dismissed, plus documented blind spots so a validator can challenge the feedback where the archetype distorts it.

## Install in 60 seconds

1. Copy this folder (`investor-reviewer`) into your OneDrive at `/Documents/Cowork/skills/` (the lowercase `skills` folder name is case-sensitive).
2. Start a NEW Cowork conversation. Skills are discovered at conversation start, not mid-conversation.
3. Use one of the trigger phrases below, naming the file you want reviewed.

## Example triggers

- "Run an investor review on platform-funding-case.docx"
- "What would an investor say about this business case before I ask for the budget?"
- "Pressure-test this deck from a capital lens, I pitch the investment committee next week"
- "We're asking the board sponsor for the full amount upfront. Find the holes first."

## Why this exists

This skill is a bench persona for the Executive Review Board suite (see the [review-board](../review-board/) folder, which orchestrates the core reviewers and ships the org profile template). The core board reviews from inside the org chart: can we run this, secure it, staff it, fund it from this year's budget. The investor reviews from outside it: should this capital be committed at all, in what stages, and what does failure cost. Proposals that survive every operational reviewer still die on that question, so the bench extends the board beyond the C-suite to the people whose money is actually on the table. It works standalone; you do not need the rest of the suite installed.

## Seat this persona on the review board

This skill works standalone, and its persona can also join the full review-board skill as a bench member:

1. Copy `references/persona.md` from this folder into your INSTALLED review-board skill folder in OneDrive, renamed to the pattern the board expects: `/Documents/Cowork/skills/review-board/references/persona-investor.md`.
2. Start a NEW Cowork conversation (the board only discovers new persona files at conversation start).
3. Convene it by name: "run the review board with the CFO, CISO and Investor".

The board ships with 11 reference files plus its README, and Cowork allows 20 companion files per skill. Microsoft does not say whether the README counts towards that limit, so at least 8 bench personas fit at once; to seat all 9 safely, delete README.md from your installed copy of review-board (Cowork only needs SKILL.md and the references folder).

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---------|------------|-----------------|
| 1.0 | 2026-06-10 | Initial version |

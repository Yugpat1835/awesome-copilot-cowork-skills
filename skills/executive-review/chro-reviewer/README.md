# CHRO Reviewer

> Pressure-test your plan against a CHRO archetype before the real one asks who actually loses their job on slide 12.

## What it produces

A structured review document, `<artifact-name>-chro-review.docx`, saved to `/Documents/Cowork/reviews/` in your OneDrive, containing:

- **VERDICT**: ready, ready with conditions, or not ready
- **TOP FINDINGS**: each one quotes or cites the exact part of your document it is about, no generic feedback; where the document is silent, the finding is recorded as an open question, never an invented fact
- **RISKS**: from the people lens (change load, consultation exposure, skills gaps, manager load, attrition, survivor morale)
- **WHAT WOULD CHANGE MY MIND**: the specific evidence that would move the verdict up
- **5 INTERROGATION QUESTIONS**: the questions the real CHRO is likely to ask in the room

The persona lives in `references/persona.md`: mandate, ten probes, red flags, what convinces a CHRO and what gets dismissed, plus documented blind spots so a validator can challenge the feedback where the archetype distorts it.

## Install in 60 seconds

1. Copy this folder (`chro-reviewer`) into your OneDrive at `/Documents/Cowork/skills/` (the lowercase `skills` folder name is case-sensitive).
2. Start a NEW Cowork conversation. Skills are discovered at conversation start, not mid-conversation.
3. Use one of the trigger phrases below, naming the file you want reviewed.

## Example triggers

- "Run a CHRO review on ops-restructure-plan.docx"
- "What would HR say about this operating model deck before the people committee sees it?"
- "Pressure-test this rollout plan from a people lens, the works council meets next month"
- "I present this to our CHRO on Tuesday. Find the people holes first."

## Why this exists

This skill is a bench persona for the Executive Review Board suite (see the [review-board](../review-board/) folder, which orchestrates the board and ships the org profile template). The board ships with a fixed set of reviewers; the bench extends it with additional executive lenses you seat only when the document warrants them. The CHRO lens matters whenever a plan changes who does what: restructurings, operating model shifts, automation cases and anything with "freed capacity" in it. Those documents tend to be precise about the savings and vague about the people, and that vagueness is exactly what the real CHRO interrogates. It works standalone; you do not need the rest of the suite installed.

## Seat this persona on the review board

This skill works standalone, and its persona can also join the full review-board skill as a bench member:

1. Copy `references/persona.md` from this folder into your INSTALLED review-board skill folder in OneDrive, renamed to the pattern the board expects: `/Documents/Cowork/skills/review-board/references/persona-chro.md`.
2. Start a NEW Cowork conversation (skills and their files are discovered at conversation start).
3. Convene it by name: "run the review board with the CFO, CISO and CHRO".

The board ships with 11 reference files plus its README, and Cowork allows 20 companion files per skill. Microsoft does not say whether the README counts towards that limit, so at least 8 bench personas fit at once; to seat all 9 safely, delete README.md from your installed copy of review-board (Cowork only needs SKILL.md and the references folder).

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---------|------------|-----------------|
| 1.0 | 2026-06-10 | Initial version |

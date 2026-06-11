# Customer Advocate Reviewer

> Pressure-test your plan against the paying customers who are never in the room when it gets approved.

## What it produces

A structured review document, `<artifact-name>-customer-advocate-review.docx`, saved to `/Documents/Cowork/reviews/` in your OneDrive, containing:

- **VERDICT**: ready, ready with conditions, or not ready
- **TOP FINDINGS**: each one quotes or cites the exact part of your document it is about, no generic feedback; where your document is silent, it records an open question instead of inventing an answer
- **RISKS**: from the customer lens (churn triggers, exported customer effort, promises with no owner, the failure path)
- **WHAT WOULD CHANGE MY MIND**: the specific evidence that would move the verdict up
- **5 INTERROGATION QUESTIONS**: the questions a customer advocate would ask in the room

The persona lives in `references/persona.md`: mandate, ten probes, red flags, what convinces a customer advocate and what gets dismissed, plus documented blind spots so a validator can challenge the feedback where the archetype distorts it.

## Install in 60 seconds

1. Copy this folder (`customer-advocate-reviewer`) into your OneDrive at `/Documents/Cowork/skills/` (the lowercase `skills` folder name is case-sensitive).
2. Start a NEW Cowork conversation. Skills are discovered at conversation start, not mid-conversation.
3. Use one of the trigger phrases below, naming the file you want reviewed.

## Example triggers

- "Run a customer advocate review on q3-migration-plan.docx"
- "What would our customers say about this pricing change before we announce it?"
- "Pressure-test this deck from the customer's side, every benefit in it is internal"
- "We're sunsetting the old portal. Review the plan as the customer who has to live with it."

## Why this exists

This skill is a bench persona for the Executive Review Board suite (see the [review-board](../review-board/) folder, which orchestrates the seven C-suite reviewers and ships the org profile template). The C-suite covers the people who approve a plan; it does not cover the people the plan happens to. The customer advocate holds that seat: every claim about what customers want, will tolerate or will keep paying for gets challenged before the document ships, not after the churn shows up. It works standalone; you do not need the rest of the suite installed.

## Seat this persona on the review board

This skill works on its own, and its persona can also join the full review board:

1. Copy `references/persona.md` from this folder into your INSTALLED review-board skill folder in OneDrive, renamed to the pattern the board expects: `/Documents/Cowork/skills/review-board/references/persona-customer-advocate.md`.
2. Start a NEW conversation (skills and their files are discovered at conversation start).
3. Convene it by name, for example: "run the review board with the CFO, CISO and Customer Advocate".

The board ships with 11 reference files plus its README, and Cowork allows 20 companion files per skill. Microsoft does not say whether the README counts towards that limit, so at least 8 bench personas fit at once; to seat all 9 safely, delete README.md from your installed copy of review-board (Cowork only needs SKILL.md and the references folder).

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---------|------------|-----------------|
| 1.0 | 2026-06-10 | Initial version |

# General Counsel Reviewer

> Pressure-test your proposal against a General Counsel archetype before the real one asks where the liability cap went.

## What it produces

A structured review document, `<artifact-name>-general-counsel-review.docx`, saved to `/Documents/Cowork/reviews/` in your OneDrive, containing:

- **VERDICT**: ready, ready with conditions, or not ready
- **TOP FINDINGS**: each one quotes or cites the exact part of your document it is about; where your document is silent, the finding records an open question rather than inventing terms
- **RISKS**: from the legal lens (contractual exposure, liability and indemnities, IP ownership, regulatory standing, signing authority, termination)
- **WHAT WOULD CHANGE MY MIND**: the documents and written confirmations that would move the verdict up
- **5 INTERROGATION QUESTIONS**: the questions the real General Counsel is likely to ask in the room

The persona lives in `references/persona.md`: mandate, ten probes, red flags, what convinces a General Counsel and what gets dismissed, plus documented blind spots so a validator can challenge the feedback where the archetype distorts it.

## Install in 60 seconds

1. Copy this folder (`general-counsel-reviewer`) into your OneDrive at `/Documents/Cowork/skills/` (the lowercase `skills` folder name is case-sensitive).
2. Start a NEW Cowork conversation. Skills are discovered at conversation start, not mid-conversation.
3. Use one of the trigger phrases below, naming the file you want reviewed.

## Example triggers

- "Run a general counsel review on vendor-partnership-proposal.docx"
- "What would legal say about this deal before I send it to the counterparty?"
- "Pressure-test this business case from a legal lens, contract review is on Friday"
- "I present this plan to our GC next week. Find the legal holes first."

## Why this exists

This skill is a bench persona for the Executive Review Board suite (see the [review-board](../review-board/) folder, which orchestrates the core reviewers and ships the org profile template). The board's core bench covers the C-suite roles most proposals meet first; bench personas extend it to the reviewers a specific document actually faces. Plans that involve a counterparty, a regulator or anything that gets signed eventually cross the General Counsel's desk, and the questions asked there (who owns the IP, where the liability cap sits, who had authority to promise that) are cheaper to answer before the meeting than during it. It works standalone; you do not need the rest of the suite installed.

## Seat this persona on the review board

This skill works on its own, and its persona can also join the full review-board skill as an extra seat:

1. Copy `references/persona.md` from this folder into your INSTALLED review-board skill folder in OneDrive, renamed to the pattern the board expects: `/Documents/Cowork/skills/review-board/references/persona-general-counsel.md`.
2. Start a NEW Cowork conversation (the board only discovers new personas at conversation start).
3. Convene it by name: "run the review board with the CFO, CISO and General Counsel".

The board ships with 11 reference files plus its README, and Cowork allows 20 companion files per skill. Microsoft does not say whether the README counts towards that limit, so at least 8 bench personas fit at once; to seat all 9 safely, delete README.md from your installed copy of review-board (Cowork only needs SKILL.md and the references folder).

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---------|------------|-----------------|
| 1.0 | 2026-06-10 | Initial version |

# Procurement Reviewer

> Pressure-test your proposal against a Head of Procurement archetype before the real one reads the order form line by line.

## What it produces

A structured review document, `<artifact-name>-procurement-review.docx`, saved to `/Documents/Cowork/reviews/` in your OneDrive, containing:

- **VERDICT**: ready, ready with conditions, or not ready
- **TOP FINDINGS**: each one quotes or cites the exact part of your document it is about, no generic feedback; where the document is silent on a probe, an open question is recorded rather than an assumption
- **RISKS**: from the commercial lens (lock-in and switching cost, renewal and escalator exposure, single-source dependence, supplier continuity)
- **WHAT WOULD CHANGE MY MIND**: the specific terms and evidence that would move the verdict up
- **5 INTERROGATION QUESTIONS**: the questions the real Head of Procurement is likely to ask in the room

The persona lives in `references/persona.md`: mandate, ten probes, red flags, what convinces a procurement lead and what gets dismissed, plus documented blind spots so a validator can challenge the feedback where the archetype distorts it.

## Install in 60 seconds

1. Copy this folder (`procurement-reviewer`) into your OneDrive at `/Documents/Cowork/skills/` (the lowercase `skills` folder name is case-sensitive).
2. Start a NEW Cowork conversation. Skills are discovered at conversation start, not mid-conversation.
3. Use one of the trigger phrases below, naming the file you want reviewed.

## Example triggers

- "Run a procurement review on crm-renewal-proposal.docx"
- "What would our Head of Procurement say about this vendor contract before we sign?"
- "Pressure-test this pricing deck from a commercial lens, the renewal lands next month"
- "I take this sourcing plan to the contracts committee on Tuesday. Find the holes first."

## Why this exists

This skill is a bench persona for the Executive Review Board suite (see the [review-board](../review-board/) folder, which orchestrates the seven core reviewers and ships the org profile template). The core suite covers the C-suite, but many proposals stall one level out from it: the vendor contract, the renewal, the statement of work that procurement will take apart clause by clause. Bench personas extend the board beyond the C-suite to those gatekeepers, one role at a time. This one reviews the commercial substance of any document that commits the organisation to a counterparty. It works standalone; you do not need the rest of the suite installed.

## Seat this persona on the review board

This skill works standalone, and its persona can also join the full review-board skill as an extra seat.

1. Copy `references/persona.md` from this folder into your INSTALLED review-board skill folder in OneDrive, renamed to the pattern the board expects: `/Documents/Cowork/skills/review-board/references/persona-procurement.md`.
2. Start a NEW conversation (skills and their files are discovered at conversation start).
3. Convene it by name: "run the review board with the CFO, CISO and Head of Procurement".

The board ships with 11 reference files plus its README, and Cowork allows 20 companion files per skill. Microsoft does not say whether the README counts towards that limit, so at least 8 bench personas fit at once; to seat all 9 safely, delete README.md from your installed copy of review-board (Cowork only needs SKILL.md and the references folder).

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---------|------------|-----------------|
| 1.0 | 2026-06-10 | Initial version |

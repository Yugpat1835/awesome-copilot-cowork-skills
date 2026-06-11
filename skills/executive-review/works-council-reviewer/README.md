# Works Council Reviewer

> Pressure-test your rollout plan against a Works Council Representative archetype before the real consultation meeting does it for you.

## What it produces

A structured review document, `<artifact-name>-works-council-review.docx`, saved to `/Documents/Cowork/reviews/` in your OneDrive, containing:

- **VERDICT**: ready, ready with conditions, or not ready
- **TOP FINDINGS**: each one quotes or cites the exact part of your document it is about, no generic feedback; where your document is silent, the finding is an open question, never an invented fact
- **RISKS**: from the employee-representative lens (consultation sequence, employee data and monitoring exposure, workload and performance pressure, voluntariness, precedent)
- **WHAT WOULD CHANGE MY MIND**: the written commitments and consultation steps that would move the verdict up
- **5 INTERROGATION QUESTIONS**: the questions the real representative is likely to ask in the room

The persona lives in `references/persona.md`: mandate, ten probes, red flags, what convinces a works council representative and what gets dismissed, plus documented blind spots so a validator can challenge the feedback where the archetype distorts it.

## Install in 60 seconds

1. Copy this folder (`works-council-reviewer`) into your OneDrive at `/Documents/Cowork/skills/` (the lowercase `skills` folder name is case-sensitive).
2. Start a NEW Cowork conversation. Skills are discovered at conversation start, not mid-conversation.
3. Use one of the trigger phrases below, naming the file you want reviewed.

## Example triggers

- "Run a works council review on copilot-rollout-plan.docx"
- "What would the works council say about this deck before I take it to consultation?"
- "Pressure-test this business case from an employee-representative lens, we brief the staff council next month"
- "We present the new tooling plan to employee reps on Thursday. Find the holes first."

## Why this exists

This skill is a bench persona for the Executive Review Board suite (see the [review-board](../review-board/) folder, which orchestrates the core reviewers and ships the org profile template). The board's core reviewers cover the C-suite, but plenty of proposals that survive finance and security review stall at employee consultation, because nobody read the document the way an elected employee representative will. This persona does that read before the meeting: consultation sequence, employee data, monitoring capability, whose hours the savings come from, and what precedent the decision sets. It works standalone; you do not need the rest of the suite installed.

## Seat this persona on the review board

This skill works standalone, and its persona can also join the full review-board skill as a bench member:

1. Copy `references/persona.md` from this folder into your INSTALLED review-board skill folder in OneDrive, renamed to the pattern the board expects: `/Documents/Cowork/skills/review-board/references/persona-works-council.md`.
2. Start a NEW Cowork conversation (skills and their files are discovered at conversation start).
3. Convene the persona by name, for example: "run the review board with the CFO, CISO and Works Council Representative".

The board ships with 11 reference files plus its README, and Cowork allows 20 companion files per skill. Microsoft does not say whether the README counts towards that limit, so at least 8 bench personas fit at once; to seat all 9 safely, delete README.md from your installed copy of review-board (Cowork only needs SKILL.md and the references folder).

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---------|------------|-----------------|
| 1.0 | 2026-06-10 | Initial version |

# CDO Reviewer

> Pressure-test your business case against a Chief Data Officer archetype before the real one asks where your numbers actually come from.

## What it produces

A structured review document, `<artifact-name>-cdo-review.docx`, saved to `/Documents/Cowork/reviews/` in your OneDrive, containing:

- **VERDICT**: ready, ready with conditions, or not ready
- **TOP FINDINGS**: each one quotes or cites the exact part of your document it is about, no generic feedback; where your document is silent on a probe, the finding becomes an open question, never an invented fact
- **RISKS**: from the data lens (measurement integrity, data quality, lawful basis and privacy, vendor data flows, AI and model governance)
- **WHAT WOULD CHANGE MY MIND**: the specific evidence and definitions that would move the verdict up
- **5 INTERROGATION QUESTIONS**: the questions the real CDO is likely to ask in the room

The persona lives in `references/persona.md`: mandate, ten probes, red flags, what convinces a CDO and what gets dismissed, plus documented blind spots so a validator can challenge the feedback where the archetype distorts it.

## Install in 60 seconds

1. Copy this folder (`cdo-reviewer`) into your OneDrive at `/Documents/Cowork/skills/` (the lowercase `skills` folder name is case-sensitive).
2. Start a NEW Cowork conversation. Skills are discovered at conversation start, not mid-conversation.
3. Use one of the trigger phrases below, naming the file you want reviewed.

## Example triggers

- "Run a CDO review on customer-360-business-case.docx"
- "What would a Chief Data Officer say about this analytics proposal?"
- "Pressure-test the data and AI governance claims in this deck before the steering committee sees it"
- "Every number in this plan needs a source. Interrogate it like a CDO would."

## Why this exists

The Executive Review Board suite ships with a core bench of C-suite reviewers (see the [review-board](../review-board/) folder, which orchestrates them and ships the org profile template). Bench personas like this one extend the board beyond that core line-up to the executives who interrogate a specific dimension of a proposal. The CDO seat covers the questions the core bench leaves thinnest: whether the headline metrics have definitions and source systems, whether the data is fit and lawfully usable, and whether the AI components are governed rather than just mentioned. It works standalone; you do not need the rest of the suite installed.

## Seat this persona on the review board

This skill works standalone, and its persona can also join the full review-board skill so the board convenes with this lens included:

1. Copy `references/persona.md` from this folder into your INSTALLED review-board skill folder in OneDrive, renamed to the pattern the board expects: `/Documents/Cowork/skills/review-board/references/persona-cdo.md`.
2. Start a NEW conversation (skills and their companion files are discovered at conversation start).
3. Convene it by name: "run the review board with the CFO, CISO and Chief Data Officer".

The board ships with 11 reference files plus its README, and Cowork allows 20 companion files per skill. Microsoft does not say whether the README counts towards that limit, so at least 8 bench personas fit at once; to seat all 9 safely, delete README.md from your installed copy of review-board (Cowork only needs SKILL.md and the references folder).

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---------|------------|-----------------|
| 1.0 | 2026-06-10 | Initial version |

# Review Board

> Seven C-suite personas review your proposal independently, a red team strikes their weak findings, they argue out the rest, and you get the report plus every question to prepare for, before any real executive sees the document.

## What it produces

- `/Documents/Cowork/reviews/<artifact-name>-YYYY-MM-DD/executive-review-<artifact-name>-YYYY-MM-DD.docx`: executive summary with an overall verdict against your stated decision, consolidated findings ranked by how many personas raised them, unresolved conflicts framed as decisions for you, and an appendix showing exactly which findings the red-team pass struck and why.
- `/Documents/Cowork/reviews/<artifact-name>-YYYY-MM-DD/interrogation-questions.md`: the full question bank grouped by role, ready to forward or rehearse against.

The pipeline runs six stages: intake, organisation context (from your own `/Documents/Cowork/org-profile.md` if you create one), seven independent persona reviews (CFO, COO, CTO, CMO, CRO, CBO, CISO), red-team validation of every review before any persona cross-reads, a cross-comment round, and synthesis. It reads your artifact with the built-in Word, PowerPoint, PDF or Excel skill, finds it with Enterprise Search, and writes the report with the built-in Word skill. All seven persona files ship inside this folder, so it works with nothing else installed.

## Install in 60 seconds

1. Copy this folder into your OneDrive at `/Documents/Cowork/skills/` (the lowercase `skills` folder name matters), so you have `/Documents/Cowork/skills/review-board/SKILL.md`. This folder contains `SKILL.md` plus 11 reference files in `references/` (the seven personas, the templates and the worked example); copy the entire folder, because the board loads each persona from `references/` at run time.
2. Start a NEW Cowork conversation (skills are only discovered when a conversation starts).
3. Use one of the trigger phrases below, pointing at a proposal, business case, deck or plan in OneDrive or SharePoint, or paste the text.
4. Optional, recommended: copy `references/org-profile-template.md` to `/Documents/Cowork/org-profile.md` and fill it in (worked example in `references/example-org-profile.md`). Without it, personas treat every organisation fact as unknown, and findings that depend on missing context become open questions.

## Example triggers

- "Run the review board on my Q3 platform proposal before Thursday's steering committee."
- "Stress-test this business case the way our exec team would."
- "What will the CFO and CISO say about this deck? Give me their questions."
- "Red-team this plan: full board, the decision is budget approval."

## Why this exists

This is the flagship skill of this repository, built to show the one thing a Cowork skill can do that no prompt or chat agent can: multi-stage orchestration with state. A single prompt, like the executive personas in our prompts collection (https://github.com/kesslernity/awesome-microsoft-copilot-prompts), can play one reviewer in one chat turn. It cannot run seven independent reviews, validate each against the artifact before cross-reading, hold a cross-comment round, and file a versioned report with an audit trail of what the red team struck. That takes a pipeline with stages and saved artifacts, which is exactly what a skill is.

## Suite or standalone

Each persona here also exists as a standalone sibling skill in this repository's `executive-review` category: `cfo-reviewer`, `coo-reviewer`, `cto-reviewer`, `cmo-reviewer`, `cro-reviewer`, `cbo-reviewer`, `ciso-reviewer`, plus `red-team-validator` for challenging any single review. Install a standalone when you want one fast persona pass in chat; install `review-board` when you want the full pipeline and a filed report. This skill bundles all seven persona files in `references/`, so it never depends on the siblings being installed, and you can convene a subset ("just the CFO and CISO") without installing anything extra.

## Extend the board

The board is not fixed at seven. A persona is one Markdown file: copy `references/persona-template.md`, fill in the six sections (mandate, what I probe first, red flags, what convinces me, vocabulary and tone, known blind spots), save it as `references/persona-<role>.md` inside your installed copy of this skill, and convene it by role name in your next new conversation.

You do not have to write one from scratch. Nine bench personas ship as standalone skills in this category: `chro-reviewer`, `general-counsel-reviewer`, `cpo-reviewer`, `cdo-reviewer`, `procurement-reviewer`, `investor-reviewer`, `customer-advocate-reviewer`, `frontline-skeptic-reviewer` and `works-council-reviewer`. To seat one on the board, copy its `references/persona.md` into your installed `review-board` folder as `references/persona-<role>.md` (for example `references/persona-chro.md`), start a NEW conversation, and convene it by role name. The board ships with 11 reference files plus this README, and Cowork allows 20 companion files per skill. Microsoft does not say whether the README counts towards that limit, so at least 8 bench personas fit at once; to seat all 9 safely, delete README.md from your installed copy of review-board (Cowork only needs SKILL.md and the references folder).

Two rules carry over from the shipped personas: archetypes only, never a real named individual; and fill in KNOWN BLIND SPOTS honestly, because the red-team stage uses that section to challenge the persona's own findings. If you build a persona others would benefit from, contribute it: a single persona file is the smallest PR this repository accepts (see [CONTRIBUTING](../../../CONTRIBUTING.md)).

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---------|------------|-----------------|
| 1.0 | 2026-06-10 | Initial version |

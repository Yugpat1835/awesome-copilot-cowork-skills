# Red-Team Validator

> A sceptical reviewer for any draft: every claim gets a verdict, every filler sentence gets named, before the document leaves the building.

## What it produces

A dated validation memo (`validation-memo-YYYY-MM-DD.md`) saved next to the document it reviewed, containing:

- an overall verdict: PASS, PASS WITH CORRECTIONS or FAIL
- a verdict table with one row per checkable claim (numbers, names, dates, quotes, causal assertions), each classified SUPPORTED, UNSUPPORTED, CONTRADICTED or UNVERIFIABLE against the sources you put in scope
- a list of generic-filler sentences that fail the so-what test, quoted verbatim
- a list of internal contradictions, both sides quoted
- a prioritised corrections section

It never edits your document. Corrections live in the memo; only with your explicit approval will it write a separate corrected copy as a new DRAFT file, leaving the original untouched.

## Install in 60 seconds

1. Copy this folder into OneDrive at `/Documents/Cowork/skills/red-team-validator/` (the lowercase `skills` folder name matters).
2. Start a NEW Cowork conversation (skills are only discovered when a conversation starts).
3. Use one of the trigger phrases below and name the file to check, plus the source files it should be checked against.

## Example triggers

- "Red-team this board update before I send it. Sources are the Q2 actuals spreadsheet and the project charter."
- "Validate every number in proposal-draft.docx against the pricing workbook."
- "Pressure-test this performance review: flag anything unsupported or generic."
- "Fact-check the claims in the steering committee deck against the files in the Apollo folder."

## Why this exists

Microsoft is explicit that custom Cowork skills are not validated, and a recurring question in community threads (see r/microsoft_365_copilot) is the same one in different clothes: how do I know what the AI wrote is actually true? This skill is the answer applied to your own documents: a repeatable checking pass that separates what the sources support from what merely sounds plausible. Within the Executive Review Board suite in this repository, the review-board skill runs its own inline version of this pass; install this skill to run the same scepticism standalone on any single document, including a finished board report.

## Status

Tested in Cowork: pending (June 2026). Format-validated against the Agent Skills spec.

## Changelog

| Version | Date | Notes |
|---|---|---|
| 1.0 | 2026-06-10 | Initial version |

# Report skeleton: executive review board

Use this structure for the synthesis Word document `executive-review-<artifact-name>-YYYY-MM-DD.docx`. Replace every {placeholder}. Keep the section order exactly as below. The title must start with DRAFT.

---

# DRAFT Executive Review: {artifact title}

Reviewed: {D Month YYYY} | Personas convened: {list, for example CFO, COO, CTO, CMO, CRO, CBO, CISO} | Decision under review: {the decision the user named at intake} | Org context: {/Documents/Cowork/org-profile.md loaded | template defaults, no org profile found}

## 1. Executive summary and overall verdict

{Three to six sentences: what the artifact proposes, the strongest part of the case, the weakest part of the case, and where the board converged or split.}

**Overall verdict on the stated decision: {ready to proceed | proceed with the listed conditions | not ready, gaps listed below}.**

{If conditions: numbered list of the specific conditions, each traceable to a finding below.}

This report was produced by synthetic role archetypes, not real executives. It is decision preparation for a human, not a decision.

## 2. Consolidated findings, ranked by board weight

Ranked by how many personas independently raised the issue, highest first. Ties broken by severity.

| Rank | Finding | Raised by ({n} of {total}) | Artifact location | Severity |
|------|---------|----------------------------|-------------------|----------|
| 1 | {one-line finding} | {for example CFO, COO, CBO (3 of 7)} | {section, slide, page or cell} | {blocker / major / minor} |

{Then one short paragraph per top finding: what each persona said, in its own terms, with the citation.}

## 3. Unresolved conflicts: decisions for you

Genuine disagreements the board could not resolve. Do not average these; pick a side or ask for more evidence. If there are none, state "No unresolved conflicts: the validated reviews agree."

### Conflict {n}: {short label}

- **Position A ({persona}):** {the position, with its citation and reasoning}
- **Position B ({persona}):** {the opposing position, with its citation and reasoning}
- **What would settle it:** {the evidence or decision that resolves the conflict}
- DECIDE: [ ]

## 4. Changed assessments

Where one persona revised its view after reading another's validated review. For each: who moved, from what to what, and which argument moved them. If none, state "No persona changed its assessment in the cross-comment round."

## 5. Interrogation question bank, by role

The questions to prepare answers for before facing a real review. Grouped by persona, in the persona's own voice, each tied to a gap in the artifact.

### {Persona name}

1. {question} (prompted by {artifact location or gap})

## 6. Appendix: red-team strikes and downgrades

Findings removed or downgraded before personas saw each other's reviews, with reasons. This is the quality log of the review itself.

| Persona | Original finding | Action | Reason |
|---------|------------------|--------|--------|
| {role} | {one line} | {struck / downgraded to flagged} | {cites nothing specific / contradicts artifact section X / invents a number / known blind spot: {which one}} |

{If nothing was struck: "The red-team pass removed nothing; all findings cited the artifact." or "{n} findings were struck and {n} downgraded, as listed."}

---

## Standalone file: interrogation-questions.md

Step 9 of the workflow saves the question bank as its own file in the same review folder, so the user can forward it or work through it without opening the report. It contains only the questions that survived the red-team pass.

- Header line: `# DRAFT Interrogation questions: {artifact title}, {D Month YYYY}`
- Group the questions by role: one `## {Persona name}` heading per convened persona, in the same order as section 5.
- Under each question, one line naming the gap that prompted it: `Gap: {the artifact location or missing answer this question targets}`

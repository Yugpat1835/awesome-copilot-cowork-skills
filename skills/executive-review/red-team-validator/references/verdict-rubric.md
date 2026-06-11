# Verdict Rubric

Every claim in the inventory receives exactly one of four verdicts. There are no blended verdicts, no percentages of confidence and no "mostly". Apply these definitions, then the tie-break rules.

## The four verdicts

### SUPPORTED

A specific passage, cell, slide or record in an in-scope source states the claim, or the figure can be recomputed from in-scope data and matches.

Requirements:
- Cite the exact location of the support (file, then section, page, slide or cell range).
- For recomputed figures, show the recomputation: which cells, what operation, what result.
- For quotes, the source wording must match verbatim. A paraphrase presented inside quotation marks is not SUPPORTED; verdict it UNSUPPORTED and suggest removing the quotation marks or restoring the exact wording.

### UNSUPPORTED

No in-scope source states the claim and it cannot be recomputed from in-scope data, yet the artifact presents it as fact. Nothing contradicts it; nothing backs it either.

Requirements:
- State where you looked (which sources, which sections) so the author can either supply a source or cut the claim.
- The default suggested correction is "remove or source this claim". Never invent a replacement figure.

### CONTRADICTED

An in-scope source, or another part of the artifact itself, states something incompatible with the claim.

Requirements:
- Quote both sides verbatim: the claim and the conflicting statement, each with its location.
- If the conflict is numeric, show both numbers and, where recomputable, which one the in-scope data supports.

### UNVERIFIABLE

The claim is about something outside the in-scope sources: external market data, competitor figures, future intentions, private conversations, industry benchmarks. The sources could not contain the answer, so absence of support is not the author's failure to cite, it is a scope boundary.

Requirements:
- State why it is out of scope in one clause (for example "external market figure, no in-scope source covers it").
- If the user authorised a web check, claims checked via the Deep Research built-in skill are still recorded with one of the other three verdicts but marked EXTERNAL in the evidence column.

## Tie-break rules (the sceptical defaults)

1. If a claim qualifies as both UNSUPPORTED and CONTRADICTED, it is CONTRADICTED.
2. If you cannot decide between SUPPORTED and UNSUPPORTED, it is UNSUPPORTED.
3. If you cannot decide between UNSUPPORTED and UNVERIFIABLE, ask: could an in-scope source reasonably have contained this? If yes, UNSUPPORTED. If no source of this kind is in scope, UNVERIFIABLE.

## Edge guidance

- **Rounding:** a rounded figure is SUPPORTED if it matches the source within the rounding the artifact itself displays (a source value of 47.3% supports "47%"; it does not support "around 50%", which is UNSUPPORTED as written).
- **Derived figures:** totals, averages, growth rates and deltas must be recomputed, not pattern-matched. A total that disagrees with the sum of its own line items is CONTRADICTED even if a source states the same wrong total.
- **Causal assertions:** "X caused Y" needs a source that asserts causation. A source showing X and Y both happened supports the events, not the causation; verdict the causal claim UNSUPPORTED and suggest rewording to "X preceded Y" or similar.
- **Superlatives:** "largest", "first", "only" are claims about everything else in the category. They are SUPPORTED only if a source states the superlative itself; otherwise UNSUPPORTED or UNVERIFIABLE per tie-break rule 3.
- **Dates and deadlines:** check both the date itself and its consistency with every other date in the artifact (the contradiction pass).
- **Attributed opinions:** "the CFO believes margins will recover" is a claim that the CFO said so, not a claim about margins. Check the attribution against the sources; verdict the underlying prediction UNVERIFIABLE.
- **Hedged claims:** "approximately", "we estimate", "around" do not exempt a number from checking. Check the underlying figure; the hedge only loosens the rounding tolerance, it does not remove the need for a source.

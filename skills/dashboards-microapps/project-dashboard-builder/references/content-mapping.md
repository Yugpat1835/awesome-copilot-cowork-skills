# Content mapping rules

How tracker files in /Documents/Cowork/projects/<project>/ map to dashboard sections. Apply these rules exactly; where a tracker file uses different headings, map by meaning and say so when confirming scope with the user.

## File to section map

| Tracker file | Dashboard section | What to extract |
|---|---|---|
| project.md, Current status section | Status banner | Overall colour (Green, Amber, Red), one headline sentence, a 2 to 3 sentence summary, reporting period or as-of date |
| project.md, Milestones table | Milestones table | Milestone name, due date (the tracker's Target date column), owner where recorded, state |
| risks.md | Risks heat list | Risk description, severity, mitigation if recorded |
| decisions.md | Decisions log | Decision date, decision text, owner or decider |
| links.md | Links list | Link label and URL, in the order listed |
| actions.md | Not rendered | Do not render open actions as a section; if the user asks for them, suggest adding an open-actions count to the status summary sentence instead |
| any other .md | Background only | Use for understanding context; never render content the user has not asked for |

## Status colour rules

1. If the Current status section of project.md states a colour (Green, Amber, Red, or RAG wording such as "we are amber"), use it.
2. If not stated, propose a colour and ask the user to confirm before generating:
   - propose Amber if any milestone is marked late or at risk, or any open risk is High severity
   - propose Green otherwise
3. Never propose Red. Red appears only when the tracker states it or the user says it.
4. `{{STATUS_WORD}}` in the template is the capitalised word (Green, Amber, Red); `{{STATUS_CLASS}}` is the lowercase class (green, amber, red).

## Milestones

- Keep tracker order unless the tracker is clearly unordered, in which case sort by due date ascending.
- State must be one of: Done, On track, At risk, Late. Map tracker wording to the closest of these four; if a milestone has no state, use the tracker's own words verbatim rather than guessing.
- Dates render as written in the tracker; do not reformat or infer missing dates.

## Risks heat list

- Severity must be one of High, Medium, Low. Map tracker wording (for example critical to High, minor to Low). If a risk has no severity, place it after the Low items with severity rendered as "Unrated" and the `sev-low` class.
- Sort High, then Medium, then Low, then Unrated. Within a band keep tracker order.
- Cap at 10 items. If truncated, fill the count line: "Showing 10 of N risks; full list in risks.md". If not truncated, delete the count line.
- Closed or resolved risks are excluded unless the user asks for them.

## Decisions log

- Newest first, capped at 10, with the same count-line pattern: "Showing 10 of N decisions; full list in decisions.md".
- A decision with no date renders with the date cell containing "Undated".

## Links

- Render only links found in links.md or given by the user in this conversation. Never add links you believe exist (SharePoint sites, Teams channels) without a URL from a source.
- If a link has no label, use the visible URL as the label.

## Pasted-summary mode

When building from a pasted summary instead of tracker files:

- Parse the summary into the same five sections by meaning.
- Any section the summary does not cover renders as "No data provided".
- Severity, state and colour rules above still apply; ask rather than guess.
- `{{SOURCE_DESCRIPTION}}` in the footer becomes "a summary supplied in conversation".

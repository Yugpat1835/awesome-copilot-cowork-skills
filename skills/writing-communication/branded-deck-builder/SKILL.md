---
name: branded-deck-builder
description: Builds PowerPoint decks on the user's own company template and checks every slide against written brand rules (colours with hex codes, fonts, logo placement, banned visuals). Use when the user asks for a branded, on-brand, CI-compliant or corporate-template presentation, or wants a deck that follows company design guidelines. Confirms an outline first, then builds slide by slide and saves a DRAFT deck to OneDrive.
---

## PURPOSE

Cowork has no BrandKit or corporate identity support. This skill closes that gap with three explicit inputs: the user's own .pptx template (dropped into this skill folder), a written brand rules file (references/brand-rules.md, created from references/brand-rules-template.md), and a slide-by-slide compliance pass before delivery. It composes the PowerPoint built-in skill for deck construction and the Word, Excel, PDF and Enterprise Search built-ins for source content. It produces three artifacts: a DRAFT deck, the approved outline, and a brand compliance report.

## WHEN TO RUN

Run when the user asks for a presentation that must follow company branding or corporate identity (CI), a deck built "on our template", slides for an executive or external audience where brand compliance matters, or a rebuild of off-brand slides onto the company template. Do not run for throwaway slides where the user says branding does not matter: hand those straight to the PowerPoint built-in skill.

## INPUTS YOU GATHER

1. Brand rules. Read references/brand-rules.md from this skill folder. If it does not exist, read references/brand-rules-template.md and check whether the bracketed placeholders have been filled in place. If neither file contains real values, stop and run first-run setup (see FALLBACKS AND EDGE CASES).
2. Company template. Locate exactly one .pptx file in this skill folder root. If there are several, list them and ask the user which to use. If there are none, see FALLBACKS AND EDGE CASES.
3. From the user, in one message where possible: deck topic and purpose, audience, target slide count (default 10 if unstated), deadline if any, and source material (OneDrive or SharePoint file paths, or a description of what to find).
4. Source content. Read .docx sources with the Word built-in, figures and tables with the Excel built-in, and PDFs with the PDF built-in. If the user describes sources without paths ("the latest QBR report"), locate them with the Enterprise Search built-in and confirm the matches with the user before reading.

## WORKFLOW

1. Load the brand rules file and confirm the template, as described in INPUTS YOU GATHER. Tell the user which brand rules file and which .pptx template you are using, by exact filename.
2. Gather and read the source content using the Word, Excel, PDF and Enterprise Search built-ins. List the sources you read back to the user.
3. Draft the outline. One line per slide: slide number, archetype (taken from the Slide archetypes section of the brand rules), slide title, a one-sentence content summary, and the source file it draws on. Respect any per-archetype word limits in the brand rules. Save the outline as a Markdown file (see OUTPUT ARTIFACTS).
4. Confirm the outline with the user in the conversation. Ask for approval or edits. Do not build any slide until the user explicitly approves. Apply requested changes to the outline file before continuing.
5. Build the deck with the PowerPoint built-in skill. Start from a copy of the user's template; never edit the original template file. Build slide by slide in outline order. For each slide: use the template layout named for that archetype in the brand rules where one exists, apply the heading and body fonts and the hex colour values from the brand rules, place the logo as the brand rules specify, and keep within any word limits. Put the word DRAFT on the title slide, in the subtitle or below the title.
6. Run the compliance pass. Re-read references/brand-rules.md, then review the finished deck against every section of it (colours, fonts, logo placement, slide archetypes, tone, banned visuals). Record one row per slide with a verdict per rule area: PASS, FIXED (state what you changed), or MANUAL CHECK for anything the PowerPoint built-in cannot verify or set exactly, such as precise logo coordinates or image styling. Fix every violation you can. Never silently skip a rule.
7. Save all three artifacts to /Documents/Cowork/output/ using the exact filenames in OUTPUT ARTIFACTS. Then state in the conversation the full saved path of each artifact. If any artifact landed in a session folder instead of the named path, say so explicitly and give the actual location.

## OUTPUT ARTIFACTS

All artifacts are saved to OneDrive at /Documents/Cowork/output/. Derive topic-slug as a lowercase kebab-case version of the deck topic, five words maximum, for example q3-sales-review.

- <topic-slug>-deck-v1-DRAFT.pptx: the deck, built on a copy of the user's template, DRAFT on the title slide. For rebuilds, increment to v2, v3; never overwrite an earlier version.
- <topic-slug>-outline.md: the approved outline, updated with any changes the user requested.
- <topic-slug>-brand-compliance.md: the compliance report, one row per slide, every rule area marked PASS, FIXED or MANUAL CHECK, with a short summary of open MANUAL CHECK items at the top.

## FALLBACKS AND EDGE CASES

- First-run setup not done (no filled brand rules, or no .pptx in the folder): stop before building. Tell the user exactly what to do: copy references/brand-rules-template.md to references/brand-rules.md and replace the bracketed placeholders, drop the company .pptx template into this skill folder, then start a NEW Cowork conversation, because skill contents are only rediscovered when a new conversation starts.
- Filled brand rules but no .pptx template: offer to build on a blank deck applying the fonts and colours from the rules. If the user accepts, head the compliance report "TEMPLATE MISSING: reduced compliance" and mark logo placement and all layout rules as MANUAL CHECK.
- Multiple .pptx files in the folder: list them by name and ask the user which one is the template before doing anything else.
- The template has no layout matching an archetype named in the brand rules: use the closest available layout, and record a MANUAL CHECK row for that slide naming the substitution.
- A rule cannot be applied or verified exactly through the PowerPoint built-in (for example an exact hex on a chart series, or logo position in centimetres): do not claim compliance. Log it as MANUAL CHECK with a one-line instruction for the human reviewer.
- /Documents/Cowork/output/ does not exist or the save fails: create the folder first; if creation also fails, save to the session folder and report the actual full path of every artifact so nothing is lost.
- A source file is unreadable, or Enterprise Search cannot find it: build the affected slide with the placeholder [CONTENT NEEDED: name the missing source] and list it in the compliance report. Do not fill the gap with invented content.

## SAFETY RULES

- Never modify or overwrite the user's original .pptx template. Always build on a copy.
- Never delete or overwrite any file without explicit user approval in the conversation. Write new versioned files (v1, v2, v3) instead.
- The title slide carries DRAFT and the filename ends in -DRAFT.pptx until the user confirms they have reviewed the deck. Remove the label only when asked, and save the result as a new file without DRAFT in the name; do not overwrite the draft.
- If the user asks to email the deck, use the Email built-in to create a draft with the file attached. Never send.
- Never invent statistics, quotes, client names or sources to fill a slide. Mark gaps [CONTENT NEEDED] instead.

## QUALITY SELF-CHECK

- [ ] The outline was explicitly approved by the user before any slide was built
- [ ] The deck was built on a copy of the user's template and the original is untouched
- [ ] Every slide was checked against every section of references/brand-rules.md
- [ ] Every rule area on every slide is marked PASS, FIXED or MANUAL CHECK; nothing was silently skipped
- [ ] The title slide shows DRAFT and the deck filename ends in -DRAFT.pptx
- [ ] All three artifacts were saved and their exact full paths were reported in the conversation
- [ ] No statistics, quotes or sources in the deck were invented; every gap is marked [CONTENT NEEDED]

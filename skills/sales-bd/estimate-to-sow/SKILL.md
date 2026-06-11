---
name: estimate-to-sow
description: Converts a priced estimate spreadsheet into a populated statement of work document using the user's own SOW template. Validates that line items, hours, rates and totals add up before drafting, flags every discrepancy, and produces a DRAFT-labelled Word document plus a validation report. Use when the user asks to turn an estimate, quote or pricing spreadsheet into an SOW, statement of work, or scope document.
---

## PURPOSE

Convert one estimate spreadsheet (.xlsx) into one DRAFT statement of work (.docx) built from the SOW template the user has placed in this skill folder. Every scope item, deliverable and fee in the draft must trace back to a row in the estimate. Validate the arithmetic before writing a single sentence of the SOW.

Known limitation: the Word built-in regenerates a document from content you write; it does not edit the template file in place. The output is a regenerated document, so formatting, tables and numbering may differ from the template. Copy boilerplate and legal wording verbatim, and the user must compare the draft against the template before any signature.

## WHEN TO RUN

Run when the user asks to turn an estimate, quote, pricing workbook or rate card spreadsheet into a statement of work, SOW, scope document or engagement document. Do not run for proposals without pricing, for invoices, or for editing an existing SOW (that is a Word task, not this skill).

## INPUTS YOU GATHER

1. The estimate spreadsheet: a OneDrive or SharePoint path or a file name the user gives you. If they give only a name, use Enterprise Search to find candidates and ask the user to confirm which file before reading it.
2. The sheet to use, if the workbook has more than one tab with pricing data.
3. The SOW template: the first .docx file in this skill folder (`/Documents/Cowork/skills/estimate-to-sow/`). If there is more than one .docx, ask which one is the template. If there is none, stop and follow FALLBACKS AND EDGE CASES.
4. Client name and project name, if not present in the estimate or already filled in the template.
5. Project start date (only needed if the template has schedule or date placeholders; never invent dates).
6. Payment terms and currency, if the template has placeholders for them and the estimate does not state them.

## WORKFLOW

1. Locate both inputs. Use Enterprise Search if the user gave a file name rather than a path. List the .docx files in `/Documents/Cowork/skills/estimate-to-sow/` to find the template. Confirm both file choices with the user in one short message before reading anything.
2. Read the estimate with the Excel built-in skill. Identify the header row and map columns to the canonical fields (line item, phase, hours, rate, amount, role, notes) using the column recognition table in `references/sow-mapping-template.md`. Report back in one message: number of line items, number of phases, the grand total you read, and the currency. Ask the user to confirm before continuing.
3. Validate the arithmetic, all checks, before any drafting:
   - For each line: hours multiplied by rate equals the line amount, allowing rounding to 2 decimal places.
   - Each phase subtotal equals the sum of its lines.
   - The grand total equals the sum of phase subtotals.
   - Flag: blank rate or blank hours on a line with a non-zero amount, negative values, duplicate line items, more than one currency symbol, and any gap between the spreadsheet's stated total and your recalculated total (a common sign of hidden rows).
4. Write the validation report `estimate-validation-YYYY-MM-DD.md` (see OUTPUT ARTIFACTS for location). It lists every check, its result, and each discrepancy with the cell reference and both values (stated versus recalculated).
5. If any discrepancy was found, stop and present the list to the user. Offer exactly two routes: (a) they fix the spreadsheet and you re-run from step 2, or (b) they choose stated totals or recalculated totals and you proceed. Record the choice in the validation report. Never proceed silently past a discrepancy.
6. Read the SOW template with the Word built-in skill. Detect placeholders using the conventions in `references/sow-mapping-template.md` (both `{{SNAKE_CASE}}` and `[BRACKETED CAPS]` forms). If the template has no recognisable placeholders, use the heading fallback rules in that file instead.
7. Build the SOW content strictly from the validated estimate, following the mapping table in `references/sow-mapping-template.md`: scope of work from phases and line item descriptions, deliverables from line items, schedule from phases and hours (dates only if the user gave a start date), fees table from lines, subtotals and the validated grand total. You may tidy grammar in copied descriptions. You must not add, merge away or reword the meaning of any scope item, and you must not invent assumptions, exclusions or terms. Anything the template needs that the estimate does not contain becomes `[TBC: field_name]`.
8. Create the output document with the Word built-in skill: the full template content with placeholders populated, saved as a new file named `DRAFT-SOW-<Client>-<YYYY-MM-DD>-v1.docx`. Insert one line at the top of the body: "DRAFT generated <date> from <estimate filename>. Not for signature until reviewed." Before saving, check whether that filename already exists; if it does, increment to v2, v3 and so on. Never overwrite the template or any existing file.
9. Report completion in the conversation: the full saved path of both artifacts, the discrepancy count and which route the user chose, the list of remaining `[TBC]` items, any section of the draft whose length differs materially from the corresponding template section (a sign of paraphrased or truncated boilerplate), a reminder that the draft is a regenerated document the user must compare against the template, and that the document stays DRAFT until a human reviews it. If the files landed anywhere other than the intended folder (for example a session folder), say so explicitly and give the actual path.

## OUTPUT ARTIFACTS

Save both files to the OneDrive folder that contains the estimate spreadsheet. If the estimate lives on SharePoint or that folder is not writable, save to `/Documents/Cowork/output/estimate-to-sow/` instead and tell the user which location was used.

1. `DRAFT-SOW-<Client>-<YYYY-MM-DD>-v1.docx`: the populated statement of work, DRAFT-labelled in both the filename and the first line of the body.
2. `estimate-validation-YYYY-MM-DD.md`: every arithmetic check with results, each discrepancy with cell references, and the user's chosen resolution route.

Always state the full path of each saved file in your final message.

## FALLBACKS AND EDGE CASES

- No .docx template in the skill folder: stop and tell the user to drop their SOW template into `/Documents/Cowork/skills/estimate-to-sow/` and start a new conversation. If they want to proceed without one, offer the default section structure listed in `references/sow-mapping-template.md`, label the result "generic structure, replace with your firm's template", and get their approval first.
- Multiple sheets with pricing data: list the sheet names and ask which to use. Never sum across sheets without instruction.
- Estimate columns you cannot map (no rate column, daily rates instead of hourly, lump sums): describe what you found and ask the user how to interpret it. Do not guess units.
- Mixed currencies or no currency: flag it in the validation report and ask before drafting fees.
- More than 25 line items: in the deliverables section, group bullets by phase instead of one bullet per line, and say you did so.
- The spreadsheet's stated total differs from the visible rows: this often means hidden rows. Report the gap; do not pick a side without the user's choice in step 5.
- If the user asks you to send the SOW to the client, use the Email built-in skill to create a Draft only, attach nothing automatically, and tell the user a draft is waiting in their Drafts folder. Never send.

## SAFETY RULES

- Never delete or overwrite any file. Outputs are always new, versioned files (v1, v2, ...). The user's template is read-only to you.
- Never invent scope items, deliverables, assumptions, dates, rates or terms that are not in the estimate or given by the user. Gaps are marked `[TBC: field_name]`, never filled with plausible text.
- Never alter legal or boilerplate wording when copying it from the template; copy it verbatim. The output is a regenerated document, not the template file edited in place, so the user must compare the draft against the template before any signature.
- Email: Drafts only, never send.
- Every generated document is labelled DRAFT in the filename and body until a human reviews it.
- Never proceed past a failed validation without the user's explicit choice in the conversation.

## QUALITY SELF-CHECK

Before reporting completion, confirm every box:

- [ ] Every scope item, deliverable and fee in the draft traces to a specific row in the estimate.
- [ ] All arithmetic checks ran; every discrepancy is in the validation report with cell references; the user chose the resolution route.
- [ ] The fees table in the SOW matches the validated totals exactly, to the penny.
- [ ] Every template placeholder is either filled or marked `[TBC: field_name]`; none were silently deleted.
- [ ] The draft's heading list and section count match the template's, and any section whose length differs materially from the template's is flagged in the final report.
- [ ] The output filename starts with DRAFT-SOW-, includes client, date and version, and did not overwrite anything.
- [ ] The DRAFT notice line appears at the top of the document body.
- [ ] The final message states the full saved path of both artifacts and names any fallback path taken.

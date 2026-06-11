---
name: project-dashboard-builder
description: Generates a self-contained single-file HTML project dashboard (status banner, milestones, risks heat list, decisions log, links) from the tracker files in /Documents/Cowork/projects/, saved as dashboard-<project>-YYYY-MM-DD.html. Use when the user asks for a project dashboard, a shareable or pinnable status page, an HTML project overview, or a one-page visual summary of milestones, risks and decisions.
---

# Project Dashboard Builder

## PURPOSE

Turn the Markdown tracker files maintained by the project-status-tracker skill into one polished, self-contained HTML dashboard that anyone can open in a browser with no internet connection, no login and no software beyond the browser itself. The dashboard is a snapshot, not a live page: it is regenerated on demand and saved with the date in the filename so older snapshots are preserved.

This skill composes Cowork's OneDrive file access (read tracker files, write the HTML file), the Enterprise Search built-in (locate the project folder when the direct path is not found) and the Email built-in (optional draft to share the result, Drafts only). It does not use the Word, PowerPoint or PDF built-ins: the output is HTML by design.

## WHEN TO RUN

Run when the user asks for any of:

- a dashboard, status page or one-pager for a named project
- "something I can pin in Teams" or "something I can send the steering committee" summarising a project
- an HTML view of the milestones, risks or decisions tracked in /Documents/Cowork/projects/<project>/
- a refresh of an existing dashboard file

Do not run for a plain written status report (that is the project-status-tracker skill's update flow) or for anything that needs live data, charts from Excel, or interactivity beyond what static HTML and CSS provide.

## INPUTS YOU GATHER

1. **Project name.** Required. If the user did not name one, list the folders under /Documents/Cowork/projects/ and ask which project to use. The kebab-case folder name becomes <project> in the output filename.
2. **Overall status colour.** Green, Amber or Red. Take it from the Current status section of project.md if stated there. If the tracker does not state a colour, propose one using the rules in references/content-mapping.md and ask the user to confirm. Never assign Red without the tracker or the user saying so.
3. **Reporting period or as-of date.** Default to today's date in YYYY-MM-DD format. Ask only if the user mentions a different period.
4. **Audience line (optional).** A subtitle such as "Steering committee, June 2026". Skip if not offered.
5. **Pasted summary (fallback mode only).** If no tracker files exist, ask the user to paste a status summary into the conversation and build from that instead. See FALLBACKS AND EDGE CASES.

## WORKFLOW

1. **Locate the project folder.** Open /Documents/Cowork/projects/<project>/ in OneDrive. If that path does not resolve, use the Enterprise Search built-in to find files named project.md, decisions.md or risks.md whose path contains the project name, and confirm the folder you found with the user before reading anything.
2. **Read the tracker files.** From the project folder, read every Markdown file present. Expected names: project.md, decisions.md, risks.md, links.md, actions.md (the names the project-status-tracker skill scaffolds; the status banner and milestones live inside project.md). Treat any other .md files as background context only.
3. **Report what you found and confirm scope.** Tell the user which files exist, which dashboard sections they will fill, and which sections will show "No data in tracker". Confirm the status colour per INPUTS YOU GATHER. Wait for the user's go-ahead before generating.
4. **Build the content model.** Map file content to dashboard sections exactly as specified in references/content-mapping.md: status banner, milestones table, risks heat list (High severity first, capped at 10), decisions log (newest first, capped at 10), links list. Use only facts found in the tracker files or stated by the user in this conversation. Never invent a milestone, risk, decision, date, owner or link.
5. **Generate the HTML.** Start from the skeleton in references/dashboard-template.md. Replace every {{PLACEHOLDER}}, repeat the row blocks as needed, delete unused example rows. Hard requirements: one single .html file; all CSS in the one <style> block in <head>; zero <script> tags; zero requests to external resources (no CDN links, no web fonts, no remote images, no analytics). The only URLs allowed in the file are the ones rendered as text links in the links section. The file must render correctly when opened from disk with no network connection.
6. **Save and report the location.** Save the file as dashboard-<project>-YYYY-MM-DD.html (today's date) in /Documents/Cowork/projects/<project>/. If a file with that exact name already exists, do not overwrite it: save as dashboard-<project>-YYYY-MM-DD-v2.html (then -v3 and so on). After saving, state the full OneDrive path of the file you actually wrote. If the platform placed the file in a session folder instead of the requested path, say so explicitly, give the actual location, and offer to copy the file into the project folder.
7. **Offer one follow-up.** Offer to create an Outlook draft via the Email built-in with a short cover note and the dashboard file attached, addressed to recipients the user names. Create the draft only; never send. Also tell the user they can pin the file's OneDrive link to a Teams channel tab themselves; do not post to Teams on their behalf.

## OUTPUT ARTIFACTS

| Artifact | Filename | Save location |
|---|---|---|
| Project dashboard (primary) | dashboard-<project>-YYYY-MM-DD.html | /Documents/Cowork/projects/<project>/ |
| Collision-safe variant | dashboard-<project>-YYYY-MM-DD-v2.html (v3, v4 ...) | /Documents/Cowork/projects/<project>/ |
| Reviewed final (only after the user approves the content, per SAFETY RULES) | dashboard-<project>-YYYY-MM-DD-final.html | /Documents/Cowork/projects/<project>/ |
| Optional share email | Outlook draft (never sent) | Outlook Drafts folder |

Always report the exact path of every artifact written, in the conversation, immediately after writing it.

## FALLBACKS AND EDGE CASES

- **No project folder or no tracker files.** Say plainly that no tracker was found at /Documents/Cowork/projects/<project>/. Offer two options: (a) the user runs the project-status-tracker skill first, or (b) pasted-summary mode: the user pastes a status summary into the chat, you parse it into the same five sections, and any section the summary does not cover is rendered with "No data provided". In pasted-summary mode, ask where to save; default to creating /Documents/Cowork/projects/<project>/ with the user's approval.
- **Some files missing.** Build the dashboard anyway. Render each missing section with the placeholder text "No data in tracker" rather than omitting the section, so the layout stays consistent between snapshots.
- **A file exists but cannot be read.** Name the file, continue with the rest, and mark the affected section "Source file unreadable: <filename>".
- **More than 10 risks or 10 decisions.** Show the top 10 (risks by severity, decisions by recency) and add a count line such as "Showing 10 of 14 risks; full list in risks.md".
- **No status colour anywhere.** Propose Amber or Green per references/content-mapping.md and ask. Do not generate until the user confirms a colour.
- **Output landed in a session folder.** Known platform behaviour. Report the real location, then copy the file to /Documents/Cowork/projects/<project>/ with the user's approval and confirm the final path.
- **Skill not triggering.** Skills are discovered only when a new conversation starts. If the user installed this folder mid-conversation, tell them to start a new Cowork conversation and ask again.

## SAFETY RULES

- Never delete or overwrite any file without explicit user approval in this conversation. On filename collision, write a new versioned file instead.
- Never modify the tracker files. This skill reads them only.
- Include the DRAFT ribbon (see template) in every generated dashboard. Only produce a version without the ribbon after the user has reviewed the dashboard and confirmed the content is accurate; save that as a new file with -final appended before the extension.
- Email: create Drafts only. Never send, and never add recipients the user did not name.
- Include only content that appears in the tracker files or was stated by the user. No invented numbers, dates, names or links.
- No external calls from the HTML: no scripts, no CDN assets, no tracking pixels, no remote fonts or images.

## QUALITY SELF-CHECK

Before reporting the dashboard as done, confirm every box:

- [ ] Output is one single .html file whose content contains no external URLs, no CDN references and no script tags, so it renders offline
- [ ] All CSS lives in the one <style> block; the file contains zero <script> tags and zero external resource URLs
- [ ] All five sections are present: status banner, milestones, risks heat list, decisions log, links; empty ones say "No data in tracker" or "No data provided"
- [ ] Every milestone, risk, decision and link traces to a tracker file or the user's pasted summary
- [ ] Status colour was taken from the tracker or confirmed by the user, never guessed as Red
- [ ] Risks are sorted High, Medium, Low and capped at 10 with a count line if truncated
- [ ] Filename matches dashboard-<project>-YYYY-MM-DD.html (or a -v2 style variant) and the full save path was reported to the user
- [ ] The DRAFT ribbon is visible in the footer
- [ ] No tracker file was modified and nothing was overwritten or deleted
- [ ] Any email produced is sitting in Drafts, unsent

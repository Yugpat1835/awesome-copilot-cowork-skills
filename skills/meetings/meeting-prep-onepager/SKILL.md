---
name: meeting-prep-onepager
description: Builds a one-page meeting prep brief and saves it as a Word document in OneDrive. Gathers the calendar invite, recent email threads with attendees, Teams messages and shared files, then distils them into purpose, attendee positions, open threads, key files, talking points and risks. Use when the user asks to prepare for a meeting, wants a briefing before a call, or asks what they need to know before their next or a named meeting.
---

# Meeting Prep One-Pager

## PURPOSE

Produce a one-page meeting prep brief as a Word document so the user walks into a meeting already knowing the meeting purpose, who wants what, which threads are still open, which files matter, what to say and where the tension is. The brief replaces the manual digging through email, Teams and files that normally precedes an important meeting. The output is a single .docx, hard-capped at one page, saved to a named OneDrive path that you report back exactly.

## WHEN TO RUN

Run when the user asks to prepare for a meeting, asks for a briefing or one-pager before a call, or asks what they need to know before a meeting. If the user does not name a meeting, default to their next upcoming calendar meeting that has at least one other attendee. Do not run for all-day events, appointments with no other attendees, or focus blocks unless the user explicitly names one.

## INPUTS YOU GATHER

From the user (ask only if missing or ambiguous):

- Target meeting: a meeting name or date, otherwise default to the next upcoming meeting with at least one other attendee.
- Optional focus: anything the user wants emphasised, for example a decision they need to land or a person they want to read carefully.

From Microsoft 365 (gather without asking):

- The calendar invite: attendee list, organiser, invite body, agenda items, attached or linked files, recurrence pattern.
- Email threads from the last 14 days involving any attendee, or whose subject matches the meeting title or agenda keywords.
- Teams messages from the last 14 days in chats or channels involving the attendees that touch the meeting topic.
- Files referenced in the invite or in those threads, plus files shared or modified by attendees in the last 30 days that match agenda keywords.
- For recurring meetings: the most recent recap or summary from the previous occurrence, including carried-over action items.

## WORKFLOW

1. Identify the target meeting (built-in: Calendar Management). If the user named a meeting, search the next 14 days of their calendar for the best title match. Otherwise select the next upcoming meeting with at least one other attendee, skipping all-day events and focus blocks. If two or more meetings plausibly match, list up to 3 with dates and times and ask the user which one. Once selected, state the meeting title, date, time and attendee count in the conversation, then proceed.
2. Extract the invite details (built-in: Calendar Management): full attendee list with the organiser flagged, the invite body, any agenda items, any attached or linked files, and whether the meeting is part of a recurring series. For a recurring series, target the next occurrence.
3. Gather email context (built-in: Email, read-only). Search the user's mailbox for threads from the last 14 days that involve any attendee, plus threads whose subject matches the meeting title or agenda keywords. From each relevant thread, note in your own words: the topic, the latest position of each participant, and any question addressed to the user that has not been answered.
4. Gather Teams and file context (built-in: Enterprise Search). Find Teams messages from the last 14 days in chats or channels involving the attendees that mention the meeting topic. Then find files: anything referenced in the invite or the threads from step 3, plus files shared or modified by attendees in the last 30 days that match agenda keywords. For each candidate file capture the filename, owner, last-modified date and a one-line summary of what it contains.
5. For recurring meetings only (built-in: Meetings): pull the most recent recap or transcript summary from the previous occurrence and extract decisions made and action items that are still open.
6. Draft the brief. If references/onepager-template.md and references/example-brief.md are present (they ship with the full skill folder), follow the structure and word budgets there; if they are not, the section list and rules in this step are sufficient on their own. The six sections, in order: meeting purpose; attendees and what each likely wants; open threads and unresolved questions; relevant files; suggested talking points; risks or tensions to be aware of. Rules while drafting:
   - Hard cap: 450 words of body text total, so the document fits one page. If over, trim in this order: files beyond the top 3, talking points beyond the top 3, attendee lines for the least relevant attendees (keep the organiser), then open threads beyond the top 3.
   - Every line must trace back to something you gathered in steps 2 to 5. Base each "likely wants" line on a specific signal (a thread, a message, their role on the invite). If you have no signal for an attendee, write "No recent signal" rather than inventing a position.
   - If a section has no findings, write exactly "Nothing found in the last 14 days." Do not pad.
   - Summarise threads and messages in your own words. Never quote more than one line verbatim.
7. Create the Word document (built-in: Word). Document title on the first line: "DRAFT meeting prep: <meeting title>, <meeting date>". Use compact bullets, no cover page, no table of contents.
8. Save the file to OneDrive at /Documents/Cowork/output/meeting-prep-YYYY-MM-DD-<short-meeting-name>.docx where YYYY-MM-DD is the meeting date (not today's date) and <short-meeting-name> is the meeting title lowercased, kebab-case, letters and digits only, maximum 4 words. Example: meeting-prep-2026-06-12-q3-vendor-renewal.docx. If the output folder does not exist, create it. If a file with that name already exists, do not overwrite it: append -v2 (then -v3, and so on) before the extension.
9. Verify and report. Confirm the file exists at the path you named, not in a temporary session folder; if it landed in a session folder, save it again explicitly to the named path. Then report in the conversation: the exact full OneDrive path of the saved file, the body word count, which sections (if any) came back empty, and which meeting the brief covers.

## OUTPUT ARTIFACTS

- meeting-prep-YYYY-MM-DD-<short-meeting-name>.docx, saved to OneDrive /Documents/Cowork/output/. One page, six sections, body capped at 450 words, title prefixed DRAFT. This is the only artifact; the skill writes nothing else.

## FALLBACKS AND EDGE CASES

- No upcoming meeting with other attendees in the next 7 days: say so and ask the user to name a meeting or date. Do not produce an empty brief.
- Multiple meetings match a named meeting: list up to 3 candidates with date and time and ask the user to pick. Do not guess.
- The meeting starts within 15 minutes: offer a shortened brief first (purpose, top 3 talking points, top 2 risks) and produce the full one-pager only if the user still wants it.
- Output lands in a session folder instead of /Documents/Cowork/output/: save it again to the named path, verify, and report the final path actually used. Always report the real location, never the intended one.
- The output folder cannot be created: save to OneDrive /Documents/Cowork/ instead and state clearly in the conversation that the fallback location was used.
- Sparse data (new colleagues, external attendees, quiet inboxes): keep the brief honest. Mark empty sections "Nothing found in the last 14 days." and note in the report that external attendees have limited visible history.
- More than 8 attendees: profile the organiser plus the 7 attendees most active in the gathered threads, then add one line: "+N others not profiled."
- Recurring meeting with no previous recap available: skip step 5 silently and note "No recap available from the previous occurrence" in the open threads section only if that section is otherwise empty.

## SAFETY RULES

- Never delete or overwrite any file without explicit user approval in the conversation. When a filename collides, write a new versioned file instead.
- This skill is read-only on email, calendar, Teams and files. It never creates, modifies or sends email, never edits the invite, and never posts to Teams.
- The only write it performs is the new .docx in /Documents/Cowork/output/ (or the documented fallback location).
- The document title is prefixed DRAFT and stays that way until a human reviews it. Tell the user the brief is a draft based on automated gathering and should be skimmed before the meeting.
- Summarise people's messages in your own words; never include more than one verbatim line from any email or Teams message in the brief.

## QUALITY SELF-CHECK

Before reporting done, confirm every box:

- [ ] The selected meeting (title, date, time, attendee count) was stated to the user before gathering.
- [ ] All six sections are present in order; empty sections say "Nothing found in the last 14 days." rather than filler.
- [ ] Body text is 450 words or fewer and the document fits one page.
- [ ] Every "likely wants" line is grounded in a named signal or marked "No recent signal".
- [ ] Every listed file has a filename, owner, last-modified date and one-line summary.
- [ ] The filename matches meeting-prep-YYYY-MM-DD-<short-meeting-name>.docx and uses the meeting date, not today's date.
- [ ] The document title starts with DRAFT.
- [ ] No verbatim quote longer than one line appears anywhere in the brief.
- [ ] The exact full OneDrive path of the saved file was verified and reported in the conversation.

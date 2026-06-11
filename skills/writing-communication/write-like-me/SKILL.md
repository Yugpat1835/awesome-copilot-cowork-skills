---
name: write-like-me
description: Builds a personal voice profile from roughly 90 days of the user's sent email and meeting transcripts, then drafts emails and documents that match how the user actually writes. Use when the user asks to write like me, match my voice or tone, build or refresh my voice profile, or wants an email or document drafted in their own style.
---

# Write Like Me

Two modes in one skill. BUILD analyses the user's own sent mail and meeting transcripts and writes a reusable voice profile. DRAFT loads that profile and applies it to any requested email or document. Compose the built-in Email, Meetings, Enterprise Search, PDF and Word skills; never duplicate them.

## PURPOSE

Produce email and document drafts that read like the user wrote them, not like generic AI output. The voice profile is a Markdown file recording the user's greetings, sign-offs, sentence length, formality, vocabulary, structure habits, and dos and donts, built once from evidence and reused on every draft.

## WHEN TO RUN

- BUILD mode: the user asks to build, refresh or update their voice profile, or DRAFT mode finds no profile anywhere.
- DRAFT mode: the user asks for an email or document "in my voice", "like me", "the way I write", or similar.
- Mode selection: if references/voice-profile.md exists in this skill folder, default to DRAFT. If it does not exist, tell the user and offer BUILD. If the user explicitly asks to rebuild or refresh, run BUILD even when a profile exists.

## INPUTS YOU GATHER

BUILD mode:

1. Scope confirmation: default is sent mail and meeting transcripts from the last 90 days. The user may narrow it (one mailbox folder, work topics only, one language).
2. Whether to include meeting transcripts. Default to excluding transcripts of meetings with external participants; include them only if the user explicitly opts in. Some users prefer mail only; respect that.

DRAFT mode:

1. What to produce: an email or a document.
2. Audience and purpose: who reads it and what should happen after they read it.
3. Key points to cover, plus any source files in OneDrive or SharePoint to draw from.
4. Target length, if the user has one. Otherwise use the typical length recorded in the profile.

## WORKFLOW

### BUILD mode

1. Use the Email built-in skill to retrieve the user's sent messages from the last 90 days. Exclude automatic replies, calendar responses, forwards with no added text, and messages under 15 words. Aim for at least 30 usable messages. If more than 100 qualify, sample evenly across the 90 days rather than taking only the most recent.
2. If the user agreed to transcripts, use the Meetings built-in skill to retrieve meeting transcripts from the last 90 days where the user spoke. Exclude transcripts of meetings with external participants unless the user explicitly opted in. Use up to 10 transcripts and keep only the user's own speech turns. Discard every other participant's words entirely.
3. Open references/voice-profile-template.md from this skill folder and fill every section: greetings, sign-offs, sentence and paragraph length, formality and tone, signature vocabulary, never-uses list, structure habits, punctuation and formatting, spoken versus written differences, dos and donts. Quote at most three excerpts per section, each under 25 words, and only from the user's own words.
4. Complete the metadata block at the top of the profile: build date, number of messages analysed, number of transcripts analysed, dominant language, confidence (High if 30 or more messages, Low otherwise).
5. Save the completed profile as /Documents/Cowork/output/voice-profile.md in the user's OneDrive. Report the exact saved path in the conversation.
6. Tell the user, in these terms: "Move voice-profile.md from /Documents/Cowork/output/ into /Documents/Cowork/skills/write-like-me/references/. Skills can only load companion files from inside their own folder, and Cowork does not write into the skills folder itself, so this move is a manual step. Then start a new conversation before your first draft request."
7. Also tell the user: the profile is a standing file derived from roughly 90 days of their correspondence, they can delete it at any time, and a stale profile should be rebuilt rather than edited.

### DRAFT mode

1. Read references/voice-profile.md from this skill folder. If it is missing, follow step 1 of FALLBACKS AND EDGE CASES.
2. Gather the DRAFT inputs listed above. Use the Enterprise Search built-in skill to locate any source file the user named but did not link. If a source file is a PDF, read it with the PDF built-in skill.
3. Write the draft applying the profile: open with a greeting from the profile matched to the audience's formality, close with the user's usual sign-off, keep average sentence length within the profile's recorded range, use the signature vocabulary where it fits naturally, never use anything on the never-uses list, and follow the structure habits (bullets versus paragraphs, opener style, how actions are handed off).
4. Check the draft against QUALITY SELF-CHECK below and revise once before producing the artifact.
5. Produce the artifact:
   - Email: use the Email built-in skill to create the message in the user's Outlook Drafts folder. Never send it. Report that it is sitting in Drafts awaiting review.
   - Document: use the Word built-in skill to create DRAFT-<topic>-YYYY-MM-DD.docx, put the word DRAFT on the title line inside the document, and save it to /Documents/Cowork/output/ in the user's OneDrive.
6. End by reporting three things: what was created, exactly where it is, and the build date of the voice profile used. If that build date is more than 90 days old, suggest a rebuild.

## OUTPUT ARTIFACTS

- BUILD: /Documents/Cowork/output/voice-profile.md (Markdown, structured per references/voice-profile-template.md, with a metadata block recording build date, evidence counts and confidence).
- DRAFT, email: a message in the user's Outlook Drafts folder. Never sent.
- DRAFT, document: /Documents/Cowork/output/DRAFT-<topic>-YYYY-MM-DD.docx with DRAFT on the title line.
- Always state the exact location of every artifact in the conversation. If a file landed in a session folder instead of the named path, say so explicitly and give the session path.

## FALLBACKS AND EDGE CASES

1. Profile missing in DRAFT mode: check /Documents/Cowork/output/voice-profile.md. If it is there, use it for this draft and remind the user to move it into /Documents/Cowork/skills/write-like-me/references/. If it is nowhere, offer to run BUILD mode now.
2. Fewer than 30 usable sent messages: build anyway, set confidence to Low in the metadata, and tell the user which sections rest on thin evidence.
3. No transcripts accessible, or the user declined them: build from mail only and record "Transcripts analysed: 0" in the metadata.
4. Sent mail in more than one language: profile the dominant language, record the split in the metadata, and ask which language to use whenever a DRAFT request is ambiguous.
5. Saving to /Documents/Cowork/output/ fails or the file lands in a session folder: report the actual location and offer to retry the save to the named path.
6. The user asks for a register the profile has no evidence for (for example a formal complaint when every sampled message is casual): say so, draft using the nearest match in the profile, and flag the gap in your final report.
7. The user asks to update only one part of the profile (for example new sign-off): do not edit references/voice-profile.md in place. Run a fresh BUILD or write the amended profile to /Documents/Cowork/output/voice-profile.md and let the user replace the copy in references/ themselves.

## SAFETY RULES

- Never send email. Email output exists only as an Outlook Draft until the user sends it themselves.
- Never delete or overwrite any file without explicit user approval in the conversation. A rebuild writes a fresh voice-profile.md to /Documents/Cowork/output/; replacing the copy in references/ is the user's manual step, never yours.
- Label every generated document DRAFT in both the filename and the title line until a human has reviewed it.
- The voice profile records stylistic features only: greetings, sign-offs, sentence patterns, vocabulary, structure habits. It must never contain third-party names, client or customer identifiers, deal terms, project codenames or message subjects, even paraphrased. Excerpts come only from the user's own words (their sent messages and their own speech turns in transcripts), never other participants' content or the bodies of messages the user received.
- The profile is a standing data asset built from roughly 90 days of correspondence. After every BUILD, tell the user where it is stored, that they can delete it at any time, and that a stale profile should be rebuilt. Transcripts of meetings with external participants are excluded unless the user explicitly opted in.
- Work only in the user's OneDrive and SharePoint. Never claim to have read local device files.

## QUALITY SELF-CHECK

Confirm every applicable box before reporting completion:

- [ ] BUILD: every template section is filled or explicitly marked "insufficient data".
- [ ] BUILD: metadata records build date, message count, transcript count, dominant language and confidence.
- [ ] BUILD: every excerpt is the user's own words and under 25 words.
- [ ] BUILD: the profile contains no third-party names, client identifiers, deal terms, project codenames or message subjects.
- [ ] BUILD: the move instruction (output folder to references/, then a new conversation) was given verbatim.
- [ ] DRAFT: greeting and sign-off come from the profile and match the audience.
- [ ] DRAFT: nothing from the never-uses list appears in the draft.
- [ ] DRAFT: average sentence length sits within the profile's recorded range.
- [ ] DRAFT: email exists only in Outlook Drafts, or the document filename starts with DRAFT- and the title line says DRAFT.
- [ ] The exact save location of every artifact was reported to the user.

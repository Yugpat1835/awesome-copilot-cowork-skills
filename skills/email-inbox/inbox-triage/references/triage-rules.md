# Inbox triage rules

The inbox-triage skill reads this file at the start of every run.
Until you edit it, the skill runs in report-only mode: it categorises mail and
creates reply drafts, but it never moves or archives anything.

To enable rules:

1. Change the answer under "Rules enabled" below from no to yes.
2. Remove the comment markers around the example rules, or write your own, one per line.
3. Start a NEW Cowork conversation. Skill files are picked up at conversation start.

Matcher reference: "from:" matches when the value appears anywhere in the sender
address (so "from:@bigclient.com" matches the whole domain); "subject-contains:"
is a case-insensitive subject match. A message must match the whole rule to be
acted on.

## Rules enabled

no

## Archive rules

One rule per line, each starting with "- archive:". Matched messages are
archived, never deleted.

<!-- Examples, remove this comment block to activate:
- archive: from:newsletter@
- archive: from:notifications@github.com
- archive: subject-contains:status page update
-->

## Move rules

One rule per line: "- move: <matcher> -> folder:<folder name>". The target
folder must already exist in your mailbox; the skill skips the rule and reports
it if the folder is missing. It never creates mail folders on its own.

<!-- Examples, remove this comment block to activate:
- move: from:alerts@yourmonitoring.com -> folder:Automated Alerts
- move: subject-contains:out of office -> folder:OOO
-->

## Priority senders (optional)

Mail matching these rules is always categorised needs-reply-today. Priority
rules work even in report-only mode because they only affect categorisation.

<!-- Examples, remove this comment block to activate:
- priority: from:ceo@yourcompany.com
- priority: from:@biggestclient.com
-->

## What the skill will never do, regardless of this file

- Delete any message.
- Send any email.
- Act on a message that matches no rule here.

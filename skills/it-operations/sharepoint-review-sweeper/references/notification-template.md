# Owner notification template

Use this template for every owner notification. Create each one as an email Draft only, never send. Replace every angle-bracket field with run values.

## Subject

Document review overdue: <N> document(s) in <Library name>

## Body

Hello <Owner first name>,

The following document(s) in <Library name> (<Site URL>) are past their scheduled review date as of <today's date>:

| Document | Review date | Days overdue | Link |
|---|---|---|---|
| <Document name> | <Review date> | <Days overdue> | <Link> |

Please review and update each document, or correct its review date in the library if a review has already taken place.

The full sweep results are in <workbook path>.

This reminder was prepared automatically by a document review sweep. Reply to <user name> with any questions.

## Rules

- One email per owner, regardless of how many documents they own.
- Sort rows by days overdue, largest first. List at most <maximum per email> documents; if the owner has more, add the line: "Plus <N> more, see the full list in the sweep workbook."
- Address only the single resolved owner. No CC, no BCC, no other recipients.
- Plain professional tone. No urgency theatrics, no exclamation marks.
- Do not promise consequences or deadlines the user has not stated; if the user gave a review-by date in conversation, include it, otherwise leave deadlines out.

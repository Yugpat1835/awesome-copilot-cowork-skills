# Sweep configuration

The skill reads this file at the start of every sweep. Replace each angle-bracket placeholder with your value. Required values that are missing or still in angle brackets are asked for in conversation; everything else falls back to the defaults shown.

## Target library (required)

- Site URL: `<https://yourtenant.sharepoint.com/sites/YourSite>`
- Library name: `<Policies>`

## Metadata columns (required)

- Review-date column: `<Review Date>` (the date column holding each document's next scheduled review)
- Owner column: `<Document Owner>` (the person or text column identifying who must review the document)

## Thresholds

- Grace days: `0` (days past the review date before a document counts as overdue)
- Due-soon window: `14` (documents due within this many days appear on the Due soon sheet)
- Maximum documents listed per owner email: `20` (the workbook always carries the full list)

## Output

- Output folder: `/Documents/Cowork/output/sharepoint-review-sweeper/` (OneDrive path; created if it does not exist)
- Workbook filename pattern: `review-sweep-YYYY-MM-DD.xlsx` (fixed; same-day re-runs get `-v2`, `-v3` suffixes, nothing is overwritten)

## Scope (optional)

- Folder within library: (leave blank to sweep the whole library)
- Exclude file types: (for example `.aspx`, `.url`)
- Exclude owners: (for example former employees whose documents should land under Unassigned)

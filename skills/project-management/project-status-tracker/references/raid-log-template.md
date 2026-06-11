# RAID Log Template for risks.md

Use everything below the line as the initial content of risks.md when scaffolding a new project. Replace `<Project name>` and the date placeholder; leave the example rows in place as TBC stubs only if the user has given no risks yet, otherwise replace them with real entries.

Conventions:

- RAID = Risks (might happen), Assumptions (taken as true but unverified), Issues (happening now), Dependencies (we rely on someone outside the team).
- IDs are sequential per table: R-001, R-002 for risks; A-001 for assumptions; I-001 for issues; D-001 for dependencies. Continue the sequence on every update, never reuse an ID.
- Likelihood and Impact use H (high), M (medium), L (low). Do not invent scores: if a source does not indicate severity, set M and note "score TBC" in the description.
- Status values: Open, Mitigating, Closed, Superseded. Closed and Superseded rows stay in the table with the date of the change; never delete a row.
- Every Open risk needs an Owner and a Review by date. If none is stated in any source, set Owner to TBC; the skill carries Owner TBC risks into the Asks section of the weekly status document.

---

# Risks log: <Project name>

## Changes

- YYYY-MM-DD: File created.

## Risks (might happen)

| ID | Raised | Description | Likelihood | Impact | Owner | Mitigation / next step | Review by | Status |
|----|--------|-------------|------------|--------|-------|------------------------|-----------|--------|
| R-001 | YYYY-MM-DD | TBC | M | M | TBC | TBC | YYYY-MM-DD | Open |

## Assumptions (taken as true, not yet verified)

| ID | Raised | Assumption | Impact if wrong | Owner | Validate by | Status |
|----|--------|------------|-----------------|-------|-------------|--------|
| A-001 | YYYY-MM-DD | TBC | TBC | TBC | YYYY-MM-DD | Open |

## Issues (happening now)

| ID | Raised | Description | Impact | Owner | Next step | Status |
|----|--------|-------------|--------|-------|-----------|--------|
| I-001 | YYYY-MM-DD | TBC | M | TBC | TBC | Open |

## Dependencies (we rely on someone else)

| ID | Raised | Dependency | Needed by | Owner | Counterparty | Status |
|----|--------|------------|-----------|-------|--------------|--------|
| D-001 | YYYY-MM-DD | TBC | YYYY-MM-DD | TBC | TBC | Open |

---
name: Cowork behaviour report
about: Report how a skill behaved in a real tenant
labels: tenant-report
---

> These reports are how skills earn their tested-in-Cowork status. Cowork is a Frontier preview and its documentation is prerelease, so behaviour drift is expected and worth reporting, including things that worked.

## Skill name and version

The skill folder name and the version from its Changelog (for example `transcript-to-actions`, 1.0).

## What you asked

The trigger phrase or request you gave Cowork, as close to verbatim as you can share.

## What happened

What Cowork actually did, including anything that diverged from the SKILL.md. Of particular interest:

- Silent Planner or To Do failures (the skill claimed a task was created but it does not exist)
- Files saved to the session folder instead of the stated OneDrive location
- Discovery issues (the skill was not picked up at the start of a new conversation)
- Steps skipped, reordered, or invented

## Tenant surface

Where you ran it: Cowork on the web, the desktop app, or Teams.

## Date

When you ran it (Cowork behaviour changes between preview updates, so the date matters).

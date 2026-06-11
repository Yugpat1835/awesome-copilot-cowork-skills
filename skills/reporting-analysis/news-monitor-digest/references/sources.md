# Sources and relevance criteria

This file is the configuration for the news-monitor-digest skill. Edit it once and every future digest follows it. Keep the three parts below: the Role line, the Relevance criteria list, and the Sources table. The worked example is real and runnable; replace it with your own role and sources.

## How to edit

- **Role:** one line describing the job the digest serves. Every so-what line in the digest is written against this role.
- **Relevance criteria:** 4 to 7 bullet points. An item must match at least one to be considered, and items matching more criteria rank higher.
- **Sources table:** one row per source. Use the site's top-level news or blog URL. 6 to 15 sources is the practical range; past that, tighten the criteria instead of adding rows.
- **Exclusions:** things the digest must never include, even from listed sources.

---

## Worked example: Microsoft 365 administrator

**Role:** IT administrator responsible for a Microsoft 365 tenant, including Copilot licensing, tenant settings and rollout communications.

### Relevance criteria

An item qualifies if it involves at least one of:

- Licensing or pricing changes for Microsoft 365, Copilot or related add-ons
- A feature reaching general availability or public preview that changes tenant settings or admin centre options
- Security, compliance or data-residency changes affecting tenant configuration
- A deprecation, retirement or enforced migration with a date
- An admin action required before a deadline
- Agent governance, identity or management capabilities (Copilot agents, autonomous agents)

### Sources

| Source | URL | What to look for |
|---|---|---|
| Microsoft 365 blog | https://www.microsoft.com/en-us/microsoft-365/blog/ | Product announcements, licensing news |
| Official Microsoft Blog | https://blogs.microsoft.com/ | Strategy and major launches |
| Microsoft Tech Community | https://techcommunity.microsoft.com/ | Admin-level feature posts, GA and preview notices |
| Microsoft 365 Roadmap | https://www.microsoft.com/en-us/microsoft-365/roadmap | Dated rollout entries matching the criteria |
| Microsoft Learn (what's new pages) | https://learn.microsoft.com/ | Documentation changes that signal shipped behaviour |
| The Verge, Microsoft section | https://www.theverge.com/microsoft | Independent coverage and context on Microsoft news |
| Windows Central | https://www.windowscentral.com/ | Early reporting on Microsoft 365 and Copilot changes |

### Exclusions

- Rumours and unconfirmed leaks, unless explicitly labelled "(unverified)" and clearly consequential
- Sponsored content and press-release rewrites with no admin-relevant detail
- Consumer-only features with no tenant or licensing impact
- Anything without a publication date on the page

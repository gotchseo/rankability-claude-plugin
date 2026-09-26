---
name: technical-triage
description: Crawl a client site with Rankability Site Auditor and turn the findings into a short, prioritized fix list. Use when the user asks for a site audit, technical SEO check, indexability or crawl problems, broken links, Core Web Vitals issues, or "what should we fix first" on a website.
---

# Run a technical triage

Outcome: the five fixes that matter most, each with evidence, affected URLs and who can do it, not a dump of every finding.

## 1. Reuse a recent audit when one exists

1. Resolve the client with the Rankability connector's `resolve_client`, or take the domain the user gave.
2. Call `site_audit_list` with the `client_id`. If a completed audit is recent enough for the user's purpose (ask if unsure), use it and skip to section 3.

## 2. Run a new audit with approval

1. Agree a page ceiling: the site's size if known, otherwise 500. The maximum is 1,000.
2. Call `site_audit_estimate` with that `max_pages` and `get_usage_and_limits`, show the impact level and remaining usage window, and ask for approval. Do not convert usage into money.
3. After approval, call `site_audit_run` with the domain, `client_id`, `max_pages`, `confirm_usage: true` and a stable `idempotency_key`.
4. Poll `site_audit_get` with `view: "status"` until it reaches a terminal state. If it errors or is cancelled, report that and stop.

## 3. Prioritize the findings

1. Call `site_audit_get` with `view: "summary"` for bounded findings and totals.
2. For the largest issue groups, call `site_audit_get` with `view: "full"`, small `issue_limit` and `page_limit` values, and `page_fields` that include `gsc_clicks` and `gsc_impressions`, so fixes on pages that earn traffic rank first.
3. Open individual pages with `site_audit_get_page` only when you need body evidence for a specific fix.
4. Cluster related findings into themes (for example: pages blocked from indexing, redirect chains, orphan pages, duplicate titles, slow templates). Rank themes by impact on pages with search demand, then by effort.

## Output

- **Top five fixes:** for each, the theme, why it matters, affected URL count with two or three examples, the evidence, and whether a developer, a content editor or the CMS settings can fix it.
- **Watch list:** lower-priority themes in one line each.
- **Not checked:** anything the crawl could not reach, such as pages beyond the ceiling or blocked sections.

Offer to turn fixes that need new or rewritten content into Copywriter briefs, and offer a follow-up crawl after fixes ship.

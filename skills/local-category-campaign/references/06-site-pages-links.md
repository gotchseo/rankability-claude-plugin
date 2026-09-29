# Phase 6: Site, page and backlink audits

Goal: a short, ranked fix list for the market's money pages. Raw findings are not the deliverable; what matters for the campaign goal is.

## Site audit

1. Check for an existing audit (`site_audit_list`). If none is recent, `site_audit_estimate` then `site_audit_run` with usage approval (for a small local business site: up to 500 pages, no external links).
2. Read results with `site_audit_get` and `site_audit_get_page` for the market's pages.
3. Rank for the goal: internal links into the category's market pages, thin or template-copied city pages, duplicate content between city hubs, sitemap entries that redirect or leave out live pages, orphan and dead campaign pages, schema phone or address that doesn't match the market profile. Say explicitly what to ignore.

## Page audits

Run `page_audit_run` (usage approval) on the category's market page, the market hub page, the homepage and the 2 or 3 highest-value service pages, each with its target search query, the market location, and the intent set explicitly (transactional or local service for money pages). Recheck any live defect the audit reports with `scrape_page` before listing it. Report patterns across pages first, then page-specific fixes, then what to ignore.

## Backlinks

1. `get_backlink_profile` for the client (summary, history, anchors, top pages, domain quality). If a section is stale, offer `backlink_profile_refresh` with approval.
2. Report real linking sites, not the raw total: most raw referring domains for local service sites are niche-wide spam that competitors carry too. Use the domain quality classification.
3. Check where links land: do old or redirected URLs send authority to the wrong page (for example a market's legacy URL redirecting to a different city)? Those redirect fixes are often the highest-leverage link work.
4. Lost links worth reclaiming, a paid or guest-post pattern (policy risk, zero local value), links pointing to competitors but not the client, and local link opportunities (chamber, sponsorships, local press, manufacturer dealer locators).
5. Don't recommend disavowing niche-wide spam. Suggest confirming there is no manual action in Search Console (handoff).

## Output

Site, page and backlink sections in [templates.md](templates.md), each ending in a ranked action list with owner and status "pending approval". Attach and log.

---
name: monthly-client-report
description: Assemble a client-ready monthly or quarterly SEO and AI search report from Rankability data. Use when the user asks for a client report, monthly update, QBR, results summary, "what did we do this month", or a recap to send a client, for one client or several.
---

# Assemble the monthly report

Outcome: a report an agency can send under its own name, built only from measured data, with the work shipped and the plan for next month.

## Gather the evidence (read-only, no usage)

1. Resolve the client with the Rankability connector's `resolve_client`; ask if several match. Confirm the reporting period (default: the last complete calendar month).
2. `get_client_overview` for integrations, Tracker portfolio and recent work.
3. AI and search visibility: `get_tracker_brand_summary`, then `get_tracker_trends` (up to 90 days) for the most important projects, and `get_tracker_matrix` only if the user wants query-level detail.
4. Google performance: if Search Console is connected, call `get_gsc_search_performance` twice with explicit `start_date` and `end_date`, once for the period and once for the previous period of equal length, with `mode: "pages"` and then `mode: "queries"` (`limit` 25). Empty data means no data, not zero demand.
5. Work shipped: `list_content_projects` with the `client_id` (completed in the period) and `site_audit_list` for audits run. Include publishing receipts from `publishing_list_deliveries` if the user wants them.
6. Optional strategy paragraph: `consult_serena` with a specific question such as "What should we prioritize next month for this client, given these results?"

Do not start scans or other usage-bearing work to fill gaps. If data is missing or stale, report that and offer a follow-up.

## Write the report

Use the agency's voice. Do not mention internal tool names, IDs or "data_state". Structure:

1. **Summary:** three sentences: the result, the reason, the next focus.
2. **AI search visibility:** mention and citation rates by platform with the change since last period where a comparison exists. Name the queries that improved and the ones competitors still own.
3. **Google performance:** clicks, impressions, average position and top pages versus the previous period.
4. **Work completed:** content published or drafted, audits and fixes, with links where the user has them.
5. **Next month:** three to five planned actions, each tied to a query, page or finding.
6. **Notes on the data:** anything not measured, not yet connected, or carried forward from an older run, with dates.

Rules that keep the report honest:

- A platform or query with no completed measurement is "not yet measured", never zero.
- State a trend only where an earlier comparable result exists.
- SPI is a 0 to 100 presence index, not traffic. Do not present it as visits or revenue.
- Separate what was measured from what is inferred, and do not promise AI recommendations.

Offer the report as a document or artifact the user can edit, and offer a shorter email version.

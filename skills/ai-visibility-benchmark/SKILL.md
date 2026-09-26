---
name: ai-visibility-benchmark
description: Benchmark a client's visibility in AI answers and Google for its money queries, or report where an existing benchmark stands. Use when the user asks how a client shows up in ChatGPT, Perplexity, Gemini, Claude, AI Overviews or AI Mode, wants an AI visibility baseline or share of voice, is onboarding a new client, or asks which clients in the portfolio need attention.
---

# Benchmark AI visibility

Outcome: a measured baseline (or an honest status of the existing one) that an agency can show a client, plus the next three actions.

## 1. Find the client and what already exists

1. Call the Rankability connector's `resolve_client` with the name or domain. If several candidates match, ask which one. For a portfolio question ("which clients need attention?"), skip this and call `get_tracker_summary` with no `client_id`, then rank clients by top movers.
2. Call `get_client_overview` for the resolved client. If Tracker projects exist, go to section 3. Report what exists before proposing anything new.

## 2. Set up a benchmark when none exists

1. If the client has no workspace, confirm the brand name, domain and market, then call `create_client`. Offer `create_client_connect_link` so the client can connect Google Search Console and Analytics; say that Rankability works without them.
2. Propose 3 to 5 money queries: the prompts a buyer would type, such as "best [service] in [city]" or "[category] for [audience]". Local and long-tail queries often show zero search volume in keyword tools. That is normal and is not a reason to drop them.
3. Call `tracker_capabilities` with the `client_id` to see which platforms the plan includes and whether YouTube, TikTok or Local Pack need identities first.
4. For each approved query, show the exact keyword, platforms, location and mode, then call `create_tracker_project` with `auto_track_enabled: false` (a one-time benchmark), `confirm_create: true` and a fresh `idempotency_key`. Recurring tracking is a separate choice the user makes explicitly.
5. Before any scan, follow **Usage approval** below with `operation: trigger_scan` and the new `project_id`, then call `trigger_scan`. Scans run asynchronously. Tell the user results appear in a few minutes and offer to report when they finish.

## 3. Report the benchmark

1. Call `get_tracker_brand_summary` for mention and citation rates by platform, and `get_tracker_matrix` for the keyword by platform detail (paginate only if needed, 100 rows maximum per call).
2. For direction over time, call `get_tracker_trends` on the two or three most important projects.
3. Apply **Reading measurements** below to every number.
4. Optional: for a strategic read grounded in the client's saved evidence and Rankability's methodology, call `consult_serena` with the `client_id` and a specific question.

Write the answer in this shape:

- **Headline:** one or two sentences on where the client stands and the single biggest gap.
- **Scorecard:** a table of platform, mention rate, citation rate, coverage (how many queries were measured) and freshness date.
- **Movers:** the largest gains and drops, only where a comparison exists.
- **Gaps:** queries where competitors are mentioned or cited and the client is not.
- **Next three actions:** each tied to a specific query, platform and page.
- **Not measured:** platforms or queries with no completed measurement, stated plainly.

## Reading measurements

- `data_state`: `measured` is a result. `not_ranked` means a completed scan where the target was absent. `no_scan` means no completed measurement yet. `not_tracked` means the platform was not selected. Never report `no_scan` or `not_tracked` as zero or as "not visible".
- `comparison_state`: `no_history` means there is no earlier comparable result, so do not describe a trend. `comparable` means a change can be stated.
- `carried_forward_from_latest_run` marks a valid result from an older run. Show its date.
- SPI is a 0 to 100 index of search presence. It is not traffic and not a forecast.
- AI answers vary between runs. Describe rates across queries and runs, not single answers, and never promise that a change will make an AI recommend the client.

## Usage approval

Before any scan, research, crawl, audit or content generation: call `get_usage_and_limits` and `estimate_usage_impact` for the exact operation, show the impact level and the remaining usage window in the terms the tools return, and ask for approval. Only then pass `confirm_usage: true` with a stable `idempotency_key`. Do not convert usage into money. If a limit is reached, report `retry_at` and stop.

---
name: competitor-citation-gap
description: Find where AI answers mention or cite competitors instead of the client, and brief the content that could earn that ground. Use when the user asks why a competitor shows up in ChatGPT, Perplexity, Gemini or AI Overviews and the client does not, wants AI share of voice versus competitors, or asks what content to create to get cited.
---

# Close a competitor citation gap

Outcome: a short list of queries where competitors win AI answers, the sources those answers rely on, and one content brief for the best opportunity.

## 1. Read the saved evidence first

1. Resolve the client with the Rankability connector's `resolve_client`; ask if several match.
2. Call `get_tracker_matrix` for the client. Look for queries where the client is `not_ranked` or has no mention while the answer is measured. Rows with `no_scan` or `not_tracked` are missing measurement, not gaps.
3. For the three most promising queries, call `get_tracker_results` with `view: "full"` to read the answer text, cited URLs, platform and run date. Note which competitors are named and which pages or third-party sources are cited.

## 2. Fill evidence gaps only with approval

If a query the user cares about has never been measured, propose a live check with `search_intelligence_run` across the relevant platforms, with `extract_brands` set to the client and named competitors and `extract_domains` set to their domains. Follow **Usage approval** first (`operation: search_intelligence_query`, `platform_count` equal to the platforms you will query), and pass a stable `idempotency_key`. Use `view: "summary"` first and fetch `search_intelligence_get` with `view: "full"` only for the runs you will quote.

## 3. Diagnose each gap

For each query, classify why the competitor wins, using only what the answer and citations show:

- **Owned content gap:** the competitor has a page that directly answers the query and is cited; the client has none.
- **Third-party source gap:** the answer cites directories, reviews, lists or publications that include the competitor and not the client.
- **Entity or fact gap:** the answer describes the client inaccurately or incompletely.

Label every causal explanation as an inference. A citation alone does not prove why an engine chose a source.

## 4. Brief the best opportunity

Pick one gap with the clearest evidence. For an owned content gap, offer to create a Copywriter brief: confirm the topic, `page_contract` (`article` or `commercial_service`), intent and location, then call `create_content_stepped` with the `client_id`. Request AI research platforms in `research_platforms` only when the user wants AI evidence in the brief. Review the brief with `get_content_artifacts` before any `approve_brief`, which needs **Usage approval**. For a third-party source gap, list the cited sources worth pursuing and offer to save them to a Prospector list (`prospector_create_list`, `prospector_add_item`, each with the user's approval of the exact list and URL).

## Output

A table of query, platform, competitor(s) named, cited sources, gap type and evidence date; then the chosen opportunity, the proposed page or outreach, and what future measurement would confirm it worked.

## Usage approval

Before any scan, research, crawl, audit or content generation: call `get_usage_and_limits` and `estimate_usage_impact` for the exact operation, show the impact level and remaining usage window in the terms the tools return, and ask for approval. Only then pass `confirm_usage: true` with a stable `idempotency_key`. Do not convert usage into money. If a limit is reached, report `retry_at` and stop.

---
name: refresh-decaying-page
description: Find a client page that is losing Google clicks or rankings and produce an updated, optimized draft to reclaim it. Use when the user asks which pages are declining, why traffic dropped on a page, wants to refresh or update old content, or asks to write or rewrite a page for a keyword with Rankability Copywriter.
---

# Refresh a decaying page

Outcome: one page chosen on evidence, a reviewed brief, and an updated draft with its content score, delivered as a draft and never published live.

## 1. Pick the page on evidence

1. Resolve the client with the Rankability connector's `resolve_client`.
2. If Search Console is connected, call `get_gsc_search_performance` with `mode: "pages"` for the last 28 days and for the 28 days before, and compare clicks, impressions and position. Rank pages by lost clicks. Empty data is missing data, not zero demand.
3. For the top candidate, call `get_gsc_search_performance` with `mode: "query_pages"` and `page_contains` set to its path to find the queries it is losing.
4. Present the top three candidates with the numbers and let the user choose. If the user already named a page or keyword, confirm it and skip ahead.

## 2. Create and review the brief

1. Confirm the target keyword, `page_contract` (`article` for editorial pages, `commercial_service` for service and conversion pages), intent, tone, location for local clients, and target word count.
2. Call `create_content_stepped` with the `client_id` so the draft inherits the client's brand voice, knowledge base and exclusions. Leave `research_platforms` at its default unless the user asks for AI answer research; AI sources run only when requested. Use a stable `idempotency_key`.
3. Poll `get_content_project` until the brief is ready, then read it with `get_content_artifacts` (`include: ["outline", "entities", "faqs", "seo_assets"]`).
4. Review the brief with the user. Flag FAQs that are off-topic for the page's intent and headings that duplicate other client pages, and apply agreed edits with `update_content_brief`.

## 3. Generate the draft with approval

1. Follow **Usage approval** with `operation: create_content_stepped`, then call `approve_brief` with `confirm_usage: true`.
2. Poll `get_content_project` until complete, then call `get_content_artifacts` with `include: ["draft", "quality_score"]` together. Check `freshness_state` so the score belongs to this exact draft.
3. Summarize what changed versus the live page: new sections, answered queries, entities covered, and the score.

## 4. Deliver as a draft

If the user wants it in their CMS or repository, call `publishing_list_connections`, then `publishing_prepare_artifact`, then `publishing_preflight`, show the result, and only after approval call `publishing_request_draft_delivery` with the same IDs and idempotency key. This creates a draft or pull request for human review. Live publishing is not available through this connector.

## Usage approval

Before any scan, research, crawl, audit or content generation: call `get_usage_and_limits` and `estimate_usage_impact` for the exact operation, show the impact level and remaining usage window in the terms the tools return, and ask for approval. Only then pass `confirm_usage: true` with a stable `idempotency_key`. Do not convert usage into money. If a limit is reached, report `retry_at` and stop.

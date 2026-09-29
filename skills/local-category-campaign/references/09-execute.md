# Phase 9: Execute changes

Goal: approved fixes actually ship, and each shipped change is logged with a date so later snapshots can be read against it.

## Choose the path by what the client has (from `get_client_overview` and `publishing_list_connections`)

- **GitHub connection (code-based site):** prepare the change and deliver it as a draft pull request through Rankability publishing: `publishing_prepare_artifact`, `publishing_preflight`, show the diff and get approval, then `publishing_request_draft_delivery` with the same ids and idempotency key. For site code changes outside Copywriter content (schema, internal links, redirects), use the `ai-visibility-to-website-pr` skill in Claude Code.
- **WordPress connection:** the same publishing flow delivers drafts to WordPress. Live publishing is not available through the connector; a person publishes.
- **No connection:** write a task for the client's web person with the exact change (page, current text or code, replacement, reason, evidence) and log it as a handoff.

## Typical changes from a local category campaign

- Money page rebuild for the market: market-specific proof, real reviews, license numbers, pricing transparency, FAQs matched to the prompt set, LocalBusiness schema with the market's canonical NAP and `sameAs`. Use Copywriter (`create_content_stepped` or `optimize_page`) with usage approval.
- Internal links into the market's category pages from the pages that already have authority.
- Redirect and sitemap fixes found in phase 6.
- One page per head term: resolve pages competing for the same query.
- Profile and directory fixes from phases 5 and 7 are done by whoever controls the listings (handoff), never by Claude.

## After each change

`append_campaign_log` with `kind: action`, the date shipped, the URL, and which prompts it should affect. That lets the weekly check-in connect movement to work.

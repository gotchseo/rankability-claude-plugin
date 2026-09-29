# Phase 7: Competitors and gaps

Goal: know who actually wins the category and every place they are named, listed or cited where the client is not.

## Pick the top 3 competitors by measured visibility

Use `get_visibility_summary` for the prompt set: rank competitors by AI mentions across all answers plus Maps top-3 appearances. National chains with local franchises count if they're named for the market. Don't pick competitors by guesswork or by who the client dislikes. Save the choice with `append_campaign_log` (`kind: decision`).

## Profile them

For each: Google profile category, rating and review count (confirm in a browser before quoting ratings to a client), website pages for the category and market, BBB accreditation, directories and "best of" lists they appear on, local press and links (`get_backlink_profile` is for the client only; use third-party data if the user has it), and how AI answers describe them.

## Where the client is missing

1. Call `get_client_visibility_gaps` with the `campaign_id` (or the prompt set's `project_ids`). In one call it returns every ranking or AI-cited page without the client across the prompt set, one row per page, with page type (directory listing, "best of" list, review platform, info page, community thread, competitor site, lead-gen doorway), market match, competitors present, platforms, prompt count, best position and priority. It also returns AI answers without the client and queries where the client is outside the organic top 10 or the Maps top 3. Paginate with `limit` and `offset`; filter with `page_types`. Doorway, wrong-city and off-topic pages are hidden unless you pass `include_excluded: true`.
   For one report's detail, use `get_tracker_sources` or `get_tracker_citation_analysis` with `client_missing_only: true`, `get_tracker_results` with `view: "summary"` (add `include_all_results: true` for full organic and Maps lists), and `get_tracker_competitors`.
2. Review the page types. Never target lead-gen doorway sites (out-of-state template domains). Pages marked unverified (login wall, check failed, not checked) are "could not verify", not "missing".
3. Verify absence before reporting it. A mention check can miss the client when it appears under its profile name or when a page blocks fetching. Recheck blocked or doubtful pages in a browser, and mark anything unverifiable as such.

## Output

The gap analysis and opportunity list templates in [templates.md](templates.md): gaps ranked by impact on winning the category, where the client already leads, the fastest openings, decisions needed. Optionally save placement targets to Prospector (`prospector_create_list`, `prospector_add_item`) with approval of the exact list. Attach and log.

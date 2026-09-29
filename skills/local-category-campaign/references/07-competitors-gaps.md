# Phase 7: Competitors and gaps

Goal: know who actually wins the category and every place they are named, listed or cited where the client is not.

## Pick the top 3 competitors by measured visibility

Use `get_visibility_summary` for the prompt set: rank competitors by AI mentions across all answers plus Maps top-3 appearances. National chains with local franchises count if they're named for the market. Don't pick competitors by guesswork or by who the client dislikes. Save the choice with `append_campaign_log` (`kind: decision`).

## Profile them

For each: Google profile category, rating and review count (confirm in a browser before quoting ratings to a client), website pages for the category and market, BBB accreditation, directories and "best of" lists they appear on, local press and links (`get_backlink_profile` is for the client only; use third-party data if the user has it), and how AI answers describe them.

## Where the client is missing

1. For each report in the prompt set, read the results with the client-missing filter (`get_tracker_results` with the filter that returns only sources, citations and results without the client). Collect:
   - **AI citations:** pages AI answers cite that name competitors but not the client (directories, "best of" lists, info pages on licensing and cost, community threads).
   - **Search results:** organic and Maps results for each query where the client isn't on page 1 or in the pack.
   - **Directory profile pages** where competitors hold the slot.
2. Classify each page: directory listing, "best of" list, info page, community thread, competitor site, lead-gen doorway (out-of-state template sites; list them but never target them).
3. Verify absence before reporting it. A mention check can miss the client when it appears under its profile name or when a page blocks fetching. Recheck blocked or doubtful pages in a browser, and mark anything unverifiable as such.

## Output

The gap analysis and opportunity list templates in [templates.md](templates.md): gaps ranked by impact on winning the category, where the client already leads, the fastest openings, decisions needed. Optionally save placement targets to Prospector (`prospector_create_list`, `prospector_add_item`) with approval of the exact list. Attach and log.

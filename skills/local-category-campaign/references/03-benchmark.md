# Phase 3: Week 0 benchmark

Goal: a saved baseline everything later is compared against. Answer these seven questions:

1. GA4, last 3 months
2. Google Search Console, last 3 months
3. Bing Webmaster Tools, last 3 months
4. Visibility in AI answers for the category
5. Visibility in AI citations for the category
6. Visibility in classic search for the category
7. Visibility in local search (Maps) for the category

## Steps

1. **Scans.** Every report in the prompt set needs a completed scan. Check `jobs_status` with the `client_id`. Wait for scheduled scans when they are close, or run scans now with usage approval (`trigger_scan` per report). Re-run any that failed. A platform that times out (often Google AI Overviews) is recorded as unmeasured, not as absent.
2. **First-party data.** `get_tracker_seo_performance` with `days: 90` gives GA4 and GSC totals versus the previous 90 days, top pages, top queries and landing pages. For the market's pages and queries, add `get_gsc_search_performance` (`mode: pages` with `page_contains: "<city>"`, and `mode: queries` with `query_contains: "<city>"`) for both periods.
3. **Visibility.** `get_visibility_summary` for the prompt set's report ids. It counts every brand name and returns per report and platform: mentioned, cited, position, Maps position, organic positions, top competitors and most-cited domains.
4. **Save it.** `save_campaign_snapshot` with `label: "Week 0"` and the GA4/GSC date range. The snapshot stores the numbers; don't retype them.
5. **Cross-check organic.** For the head terms, compare the Tracker's Google position with Search Console's average position. If the Tracker says not ranked where Search Console says 1 to 3, inspect the captured list (`get_tracker_results` with `include_all_results: true`); a mixed or off-topic list is a bad capture. Report Search Console for organic and note it.
6. **Bing and Google Business Profile insights** are not in Rankability. Mark question 3 as not measured and log a handoff for a Bing Webmaster Tools export. Profile insights (calls, direction requests, discovery searches) need owner access; log that too.

## Report

Use the benchmark template in [templates.md](templates.md): the seven-question checklist, headline KPIs with proposed Week 12 targets, a scorecard by prompt, what it means, competitors, sources the AI answers cite, and caveats. Attach it to the campaign.

What usually matters most in the read:
- Whether the client wins the generic "best" prompts or only the specific ones where it's genuinely different.
- Google's own AI surfaces (AI Overviews, AI Mode) versus the others; they lean on Maps data and reviews.
- Which client page ranks for the head term. If it's the wrong page, or two pages compete, flag it.
- Which third-party sites the AI answers cite. Those are phase 7's targets.

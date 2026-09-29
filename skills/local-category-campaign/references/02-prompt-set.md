# Phase 2: Prompt set

Goal: one Tracker report per distinct buyer intent, localized to the market on both fronts: the search query and the AI prompt.

## Gather evidence first

1. `get_gsc_search_performance` for the last 90 days, filtered to the city (`query_contains: "<city>"`) and to category terms (for example `plumb`, `drain`, `water heater`). Note queries with impressions, their positions and landing pages. Page-level and query-level numbers differ; don't mix them (see [data-rules.md](data-rules.md)).
2. Offer a Researcher keyword report (usage approval required): `researcher_run` with `client_id`, `include_gsc: true`, `location: "<City>, <State>, United States"`, 8 to 12 seed topics built as "<service> <city> <state abbr>", up to 6 competitor domains, and `content_goals` stating the category and market. Poll `researcher_get` with `view: status`, then read `view: full` once. Results include noise (other trades, other cities, city trivia). Keep only keywords that name the market and the category.
3. Local modifiers often show zero volume. That is normal and never a reason to drop an intent.

## Design the set

- **One intent per report.** If two prompts would get the same answer, keep one. A list is a maximum, not a quota.
- Cover these intents, adapting names to the category: hire now (head term), **best [category] in [city]** (the goal itself), best company with reasons (AI-native), emergency, 2 to 4 highest-value specific jobs (for plumbing: water heater, drain, sewer, leak, water treatment), price research, pricing or financing, independent reviews, licensed and verified, the client's genuine differentiator (for example "one company for plumbing, HVAC and electrical"), commercial buyers if relevant.
- **Search query:** short and typed, always with the city and state ("plumber athens al"), never the bare city if it's shared elsewhere.
- **AI prompt:** a full question naming the city and state ("Who is the best plumber in Athens, Alabama?").
- Drop phrasings that break the client's content rules (for example "cheap").

Show the table (intent, search query, AI prompt, why it earns a slot, what was cut and why) and get approval before creating anything.

## Create the reports

1. `tracker_capabilities` with the `client_id` to confirm platforms and the local market dependency.
2. Check the organization's report capacity before creating a batch. If the plan cap would be hit, stop and tell the user how many slots are needed.
3. For each approved intent, `upsert_tracker_project` (dry run first, then `confirm_upsert: true`) with: `topic`, `name` ("<Market> <Category> NN: <intent>"), `location: "<City>, <ST>, USA"`, `frequency: weekly`, `auto_track_enabled: true` (only if the user approved recurring tracking), `platform_policy: { all_supported: true, exclude: [youtube_search, google_video_pack, tiktok_search] }` unless video identities are connected, `channel_queries: { aiPrompt, traditionalQuery, localQuery }`, and a stable `idempotency_key` per report.
4. Set brand matching in the same `upsert_tracker_project` call for every report: `brand_aliases` (every name the client appears under: legal name, Google profile name, "<Brand> Plumbing", common short forms) and `gbp_location_name` (the market's Google profile name exactly). Without these, mentions and Maps positions under the profile name are missed.
5. Reuse existing reports where the intent matches: update their queries and schedule instead of creating duplicates. Retire reports whose intent is covered (rename to "Retired: ..." and turn off the schedule) rather than deleting history.
6. Creating a report may start its first scan immediately. Use `jobs_status` with the `client_id` to see running, failed (needs re-run) and never-scanned reports; re-run failed first scans only with usage approval.
7. Update the campaign's prompt set with `update_campaign`: `prompt_set: { tracker_project_ids: [...] }` (or `tracker_cluster_id` if the reports already form one Tracker cluster for this client). The campaign only references the reports; it never creates or scans them. Then `append_campaign_log` the change.

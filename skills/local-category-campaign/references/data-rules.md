# Reading the data

Apply these to every number in every phase.

## Tracker

- `data_state`: `measured` is a result. `not_ranked` means a completed check where the client was absent. `no_scan` means no completed measurement. `not_tracked` means the platform isn't selected. A failed or timed-out check is unmeasured. Never report `no_scan`, `not_tracked` or a failed check as zero or "not visible".
- An empty search results list is an unmeasured check, not "not ranked".
- `comparison_state: no_history` means there is nothing to compare; don't describe a trend.
- SPI is a 0 to 100 index, not traffic and not a forecast.
- Each AI answer is one capture. Describe rates across prompts and weeks, not single answers.
- Maps positions come from one point in the market; other neighborhoods can see a different order.
- Tracker organic positions come from one check in the market. Search Console positions are averages across all searchers. Both are valid; don't compare one against the other.
- Brand matching depends on the report's brand aliases and profile name. If the client appears under a name that isn't set, the tools can miss it; fix the settings (phase 2) rather than hand-counting.

## Search Console

- Page-level totals are higher than query-level totals because Google hides rare queries at query level. Compare page with page and query with query.
- A query missing from the results is missing evidence, not zero demand.
- The maximum range per request is 120 days. For "last 3 months versus the 3 before", make two requests.
- Keyword tools under-report local, city-modified searches. Zero volume is normal for them.

## Search results

- Out-of-state lead-gen doorway sites (template domains, `*.netlify.app`, city subdomains) often hold top organic spots for local queries. List them as they appear; never target them.
- Results past about position 10 include other cities and off-topic pages. Tag them.
- A bare city name that exists in several states returns the bigger city's results. Always include the state.

## Evidence

- Label claims [verified], [unverified], [assumption] or [decision].
- Verify competitor ratings in a browser before quoting them to a client.
- Pages that block fetching are "could not verify", never "absent".

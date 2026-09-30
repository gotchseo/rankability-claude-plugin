# Phase 1: Intake and context

Goal: a campaign record that any teammate, agent or Serena can read to understand the campaign in two minutes.

## Steps

1. **Pull what Rankability already knows.** Call `get_client_overview`. Note: brand name, domain, business profile, selling points, content rules (`do_not_use`, blocked topics), connected integrations (GSC, GA4, Google Business Profile, WordPress, GitHub), `tracker_identity` (brand aliases, profile name), existing Tracker reports, Copywriter projects and site audits. Then `list_client_sources` and read the sources that matter (`get_client_source`): an existing strategy, entity record or business profile often already states the goal. Reuse it rather than inventing a new one. Call `publishing_list_connections` too, so you know early whether fixes can ship as GitHub pull requests or WordPress drafts.
2. **Read the site.** Use your own web fetch (free) on the homepage and the page that targets the category in the market (for example `/plumber-athens-al/`). Record name, phone, address for the market, hours, licenses, services, guarantees, financing and reviews claims, plus the site platform (WordPress, Webflow, code-based) and whether a repository exists. Use `scrape_page` only when a fetch is blocked; it uses crawler usage.
3. **Confirm the four inputs with the user:** client, market (city and state), category (trade or service, including how buyers phrase it), and window (default 12 weeks: end date = start date + 83 days, so the record reads "Week 1 of 12"). Ask what "winning" means to them and the client, and what the business outcome is (booked calls, form leads, revenue). Default definition: top 3 in Google Maps for the head term from the market, page 1 organic for the head terms, and named by most AI platforms for the "best [category] in [city]" prompts. Check Search Console first: if organic is already won (positions 1 to 3), say so and aim the targets at Maps and AI.
4. **Check the market for traps.** Is the city name shared with a bigger city elsewhere (Athens GA vs Athens AL, Springfield, Portland)? If so, every query must carry the state. List every name the business appears under: legal name, brand, Google profile name, domain-style name (for example "St Louis SEO Consultant"), and founder or principal if customers use it. Is the brand name about a different trade (for example "Fuller HVAC" chasing plumbing)? Is there a near-identical competitor name? These become phase 2 aliases and phase 5 collision checks.
5. **Check location assets.** Does the client have a physical location or Google Business Profile in the market, or only a service area? Is that profile connected in Rankability? If the market's profile isn't connected, log a handoff to connect it. It is usually the single most important asset for Maps.
6. **Create the record** with `create_campaign` (show the exact fields first; it requires `confirm_create: true` and an `idempotency_key`): name (for example "Athens AL plumbing, Q4 2026"), goal (one sentence), market, category, start and end dates, and context:
   - `facts`: verified client facts relevant to the market, each labeled.
   - `rules`: the client's content rules plus campaign rules (no unverifiable superlatives, no response-time promises unless the client confirms them, and so on).
   - `open_questions`: who approves copy, who has website access, whether the market office is staffed, whether paid ads (LSA) run alongside, what "winning" means for reporting.
7. `append_campaign_log`: "Campaign created" with links to the pages read.

## Output

Report the campaign record back in the context template from [templates.md](templates.md), including open questions for the user and handoffs logged.

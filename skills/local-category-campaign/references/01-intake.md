# Phase 1: Intake and context

Goal: a campaign record that any teammate, agent or Serena can read to understand the campaign in two minutes.

## Steps

1. **Pull what Rankability already knows.** Call `get_client_overview`. Note: brand name, domain, business profile, selling points, content rules (`do_not_use`, blocked topics), connected integrations (GSC, GA4, Google Business Profile, WordPress, GitHub), existing Tracker reports, Copywriter projects and site audits.
2. **Read the site.** Use `scrape_page` on the homepage and the page that targets the category in the market (for example `/plumber-athens-al/`). Record name, phone, address for the market, hours, licenses, services, guarantees, financing and reviews claims.
3. **Confirm the four inputs with the user:** client, market (city and state), category (trade or service, including how buyers phrase it), and window (default 12 weeks from today). Ask what "winning" means to them and the client. Default definition: top 3 in Google Maps for the head term from the market, page 1 organic for the head terms, and named by most AI platforms for the "best [category] in [city]" prompts.
4. **Check the market for traps.** Is the city name shared with a bigger city elsewhere (Athens GA vs Athens AL, Springfield, Portland)? If so, every query must carry the state. Is the client's brand name about a different trade (for example "Fuller HVAC" chasing plumbing)? Note it as a risk; it shapes phases 2 and 5.
5. **Check location assets.** Does the client have a physical location or Google Business Profile in the market, or only a service area? Is that profile connected in Rankability? If the market's profile isn't connected, log a handoff to connect it. It is usually the single most important asset for Maps.
6. **Create the record** with `create_campaign`: name (for example "Athens AL plumbing, Q4 2026"), goal (one sentence), market, category, start and end dates, and context:
   - `facts`: verified client facts relevant to the market, each labeled.
   - `rules`: the client's content rules plus campaign rules (no unverifiable superlatives, no response-time promises unless the client confirms them, and so on).
   - `open_questions`: who approves copy, who has website access, whether the market office is staffed, whether paid ads (LSA) run alongside, what "winning" means for reporting.
7. `append_campaign_log`: "Campaign created" with links to the pages read.

## Output

Report the campaign record back in the context template from [templates.md](templates.md), including open questions for the user and handoffs logged.

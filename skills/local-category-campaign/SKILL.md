---
name: local-category-campaign
description: Run a multi-week local campaign to make a client the default answer for a category in one market, such as "best plumber in Athens, AL", across Google Maps, Google organic and AI answers (ChatGPT, Gemini, Claude, Perplexity, Copilot, AI Overviews, AI Mode). Use when the user wants to start, plan, benchmark, audit, run the weekly check-in for, or report on a local category or "best [service] in [city]" campaign for a client in Rankability, or asks what to do next on an existing campaign.
---

# Local category campaign

Outcome: the client becomes the business that search and AI answers name for one category in one market, with every step measured in Rankability, logged in the campaign record, and approved by the user before anything is spent, changed or published.

A campaign is one client, one market (city), one category (trade or service) and a fixed window (usually 12 weeks). It lives in Rankability as a **campaign record**: goal, market, prompt set, context, an action and decision log, saved benchmark snapshots and attached documents. The record is the source of truth. Claude, Serena and the agency team all read it, so write to it as you go and read it before you act.

## Start here every time

1. Resolve the client with `resolve_client`. If several match, ask.
2. Call `list_campaigns` for the client.
   - **A campaign exists:** call `get_campaign`. Report where it stands (week N of M, latest snapshot headline, open decisions, open handoffs) before proposing anything. Then continue at the phase the log shows is next, or run the weekly check-in if a week has passed since the last snapshot.
   - **No campaign:** start at phase 1.
3. If the user asks for one piece only (for example "just the benchmark" or "just the brand audit"), run that phase and log it. Phases can run on their own; the order below is the recommended path, not a gate.

## Phases

Read the reference file for a phase when you reach it. Each one lists the steps, the tools, where approval is needed and what to save.

| # | Phase | What it produces | Reference |
|---|---|---|---|
| 1 | Intake and context | Campaign record with goal, market, category, dates and context | [references/01-intake.md](references/01-intake.md) |
| 2 | Prompt set | One Tracker report per buyer intent, localized on both the search and AI side | [references/02-prompt-set.md](references/02-prompt-set.md) |
| 3 | Week 0 benchmark | Saved snapshot: AI mentions and citations, organic, Maps, GSC, GA4 | [references/03-benchmark.md](references/03-benchmark.md) |
| 4 | Measurement audit | Is tracking and attribution trustworthy? Funnel stress test | [references/04-measurement-audit.md](references/04-measurement-audit.md) |
| 5 | Brand and entity audit | Canonical name, address, phones, profiles, collisions, category association | [references/05-brand-entity.md](references/05-brand-entity.md) |
| 6 | Site, page and backlink audits | Ranked fixes for the market's money pages and link profile | [references/06-site-pages-links.md](references/06-site-pages-links.md) |
| 7 | Competitors and gaps | Top 3 competitors by measured visibility; where they are named or listed and the client is not | [references/07-competitors-gaps.md](references/07-competitors-gaps.md) |
| 8 | Knowledge and Serena | Verified facts in the client knowledge base; Serena checked against them | [references/08-knowledge-serena.md](references/08-knowledge-serena.md) |
| 9 | Execute changes | Approved fixes shipped as a GitHub pull request, a WordPress draft, or a task for the client's web person | [references/09-execute.md](references/09-execute.md) |
| 10 | Weekly check-in | New snapshot, comparison with Week 0 and last week, next actions | [references/10-weekly.md](references/10-weekly.md) |

Rules for reading every number are in [references/data-rules.md](references/data-rules.md). Output shapes for each document are in [references/templates.md](references/templates.md).

## Operating rules

### Approval gates (never skip)

Ask and wait for a clear yes before each of these. Show exactly what will happen.

- **Usage:** any scan, research, crawl, audit, content generation or backlink refresh. Call `get_usage_and_limits` and `estimate_usage_impact` for the exact operation, show the impact level and remaining window in the tools' own terms, then pass `confirm_usage: true` with a stable `idempotency_key`. Never convert usage into money. On a usage limit, report `retry_at` and stop.
- **Creating or changing Tracker reports**, including schedules and brand settings. Creating a report can start its first scan, so treat creation as usage.
- **Writing to the client knowledge base or client profile.**
- **Anything client-facing or public:** publishing, pull requests, directory submissions, emails, outreach, review requests.
- **Deleting anything.** Prefer retiring (rename and unschedule) over deleting, and never delete customer history without an explicit request.

Approval for one action does not carry over to the next.

### Handoffs to a person

Some steps need access Claude doesn't have. Don't guess around them. Log each one with `append_campaign_log` (`kind: handoff`, named owner) and keep going with the rest.

Common handoffs: Google Business Profile owner access (categories, insights), a logged-in GA4 or GTM admin view, license lookups behind a captcha, call tracking, Cloudflare or firewall settings, website or CMS access, Bing Webmaster Tools, and anything that needs the client's confirmation (office staffing, acquisitions, license holders).

### Evidence labels

Label every claim in a document: **[verified]** seen directly in data or on the page, **[unverified]** from snippets or inference, **[assumption]** a choice made to fill a gap, **[decision]** needs the user or client to decide. Causal explanations for why an AI engine or Google chose a source are always inferences.

### Logging

After each phase or meaningful action, call `append_campaign_log` with a one-line summary and links. Record decisions with `kind: decision` and `decision_status`. Save benchmarks with `save_campaign_snapshot`, never as prose alone. Attach finished documents with `attach_campaign_document` (mark internal notes `internal` so they stay out of client-facing output).

### Writing

Plain language. No em dashes. No emojis in anything client-facing. Outreach is sent by a real named person at the agency, never signed as someone else, and an AI-drafted message must be disclosed where the channel requires it. Never promise rankings, AI placements or time savings.

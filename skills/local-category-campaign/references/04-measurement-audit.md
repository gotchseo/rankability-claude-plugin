# Phase 4: Measurement audit

Goal: know whether the campaign's results will be measurable before spending weeks on work. Read-only: change nothing, submit nothing.

## Tracking checklist (score each Pass, Partial, Fail or Unverified)

1. **Are tracking scripts organized?** Fetch the homepage and the market page source. List hard-coded tags, tag manager containers and measurement IDs. Flag duplicate GA4 IDs, tags delayed or blocked by performance plugins, and tags firing on the wrong pages. If a public GTM container ID is present, its `gtm.js` can be read to list tags and triggers.
2. **Traffic, events and conversions?** Which key events exist, and do forms, calls and estimate tools each fire one?
3. **Google data?** GSC and GA4 connected in Rankability (`get_client_overview`), healthy, data current.
4. **Bing data?** Bing verification (DNS TXT, `BingSiteAuth.xml`, meta tag) and whether anyone reads Bing Webmaster Tools.
5. **User data?** Consent, retention, and whether personal data leaks into URLs or events.
6. **AI answers and citations?** Tracker reports exist and are scheduled (phase 2). AI referrers (chatgpt.com, perplexity.ai and similar) visible in GA4?
7. **Phone calls?** Call tracking present, numbers swapped on the site, calls attributed to source.
8. **Deals through a CRM?** Unverified unless the user can show it.
9. **Dashboard?** Is there one place the client sees results?

Items that need admin access (GA4 admin, GTM workspace, call tracking, CRM, Bing) become handoffs.

## Funnel stress test

In a browser, walk the main lead form and call paths without submitting real data:
- Does the conversion event fire only on a completed submission, or on every step and failed validation?
- Is there a confirmation page or only an inline message (affects conversion tracking)?
- What junk does validation let through (fake phone, fake email, out-of-area ZIP)?
- Does a firewall or bot rule block or freeze the form silently?
- Do `tel:` links dial the right number in the right format?
- Does the "how did you hear about us" field include AI assistants and search?

Stop before the final submit unless the user explicitly approves a clearly labeled test submission.

## Output

The measurement audit template in [templates.md](templates.md): scorecard, findings with evidence, a fix plan (proposed, nothing done), handoffs and open questions. Log it and attach it.

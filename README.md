# Rankability for Claude

Rankability is the AI search platform for agencies. This plugin connects Claude to your Rankability account and teaches Claude the workflows agencies use to win clients, do the work, and prove results: measuring how clients appear in Google and in AI answer engines (ChatGPT, Perplexity, Gemini, Claude, Google AI Overviews and AI Mode), creating and refreshing optimized content, triaging technical issues, and assembling client-ready reports.

## What's included

- **Rankability connector** (`https://app.rankability.com/mcp`): your clients, Tracker measurements, Copywriter, Site Auditor, Search Console data, Search Intelligence, Prospector, publishing drafts and Serena.
- **Skills**
  - `ai-visibility-benchmark`: set a baseline for a client's money queries across AI engines and Google, or report where it stands.
  - `competitor-citation-gap`: find where AI answers cite competitors instead of your client and brief the content to close the gap.
  - `refresh-decaying-page`: find a page losing clicks and produce an updated draft to reclaim it.
  - `technical-triage`: crawl a site and turn findings into a short, prioritized fix list.
  - `monthly-client-report`: assemble a client-ready monthly report from measured data.
  - `ai-visibility-to-website-pr`: turn one measured opportunity into a reviewed website pull request (Claude Code).

## Use it

1. Add the plugin, open its **Connectors** tab, and connect Rankability. You sign in with your Rankability account and approve the requested scopes.
2. Ask in plain language, for example: "How visible is Acme Plumbing in ChatGPT and AI Overviews?", "Build this month's report for Acme", or "Which of Acme's pages are losing traffic?"
3. Claude reads saved data first. Before anything that uses your Rankability usage allowance (scans, research, crawls, audits, content generation), Claude shows the usage impact and waits for your approval.

A Rankability account is required. Start at https://www.rankability.com.

### Install before the directory listing is live

- **Claude (web, desktop, Cowork):** Customize, Plugins, Add, Add marketplace, then enter `https://github.com/gotchseo/rankability-claude-plugin`.
- **Claude Code:** `/plugin marketplace add gotchseo/rankability-claude-plugin`, then `/plugin install rankability@rankability`.

## Data and privacy

This plugin contains only instructions and a reference to Rankability's hosted server. It runs no local code and sends data to no other destination. When you use it, Claude sends your requests and the parameters of each tool call (for example client names, domains, keywords and page URLs) to `app.rankability.com` under your Rankability account, and receives your Rankability data in return. Access is granted by OAuth and can be revoked in Rankability under Settings, Connected apps. Rankability's handling of this data is described in its [privacy policy](https://www.rankability.com/privacy/) and [terms](https://www.rankability.com/terms/).

## Support

Documentation: https://help.rankability.com/api/mcp-getting-started. Support: via https://help.rankability.com.

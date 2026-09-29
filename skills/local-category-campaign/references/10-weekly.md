# Phase 10: Weekly check-in

Goal: a short, honest weekly read: what moved, what caused it (where the log supports a link), and the next three actions.

## Steps

1. `get_campaign`. Note the week number, last snapshot, open decisions and handoffs.
2. `get_client_scan_status`: confirm this week's scheduled scans completed. Offer re-runs for failures (usage approval).
3. `save_campaign_snapshot` with `label: "Week N"`.
4. `compare_campaign_snapshots` against Week 0 and against last week.
5. Read the comparison with [data-rules.md](data-rules.md):
   - AI answers vary between runs. Call a change a trend only when it holds across several prompts or two or more weeks.
   - Unmeasured cells on either side are excluded, not counted as losses.
   - Maps position is from one point in the market.
6. Match movement to logged actions by date. Say "consistent with" rather than "caused by".
7. Check open handoffs and decisions; nudge the named owners in the report.

## Report

The weekly template in [templates.md](templates.md): headline (one or two sentences), KPI table (Week 0, last week, this week), wins, losses, what shipped this week, blockers and handoffs, next three actions. `append_campaign_log` the summary and attach the report if the user wants a client-facing version (mark it `client_facing`).

At the final week, write the campaign close-out: Week 0 versus final, what worked, what didn't, what to keep doing, and set the campaign status to completed.

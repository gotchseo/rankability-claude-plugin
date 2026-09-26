---
name: ai-visibility-to-website-pr
description: Turn a measured Rankability AI visibility opportunity into one evidence-backed website pull request. Use when the user has connected Rankability MCP and opened the website repository; stop for approval before usage-bearing or repository-changing work.
---

# AI visibility to website PR

Use this skill for one client, one measured opportunity, and one website repository. The repository must be the website's actual source, with a known review and deployment path. If the website repository is unavailable, produce a scoped recommendation and stop. Do not create a parallel Rankability project, report, audit, or brief.

## Establish the evidence

1. Confirm the active Rankability organization and account contract with `get_usage_and_limits`. Resolve the user's client name or domain with `resolve_client`; use `list_clients` only when they have not identified a client. If resolution returns several candidates, ask which one they mean before client-scoped work.
2. Read saved evidence first. For broad Tracker analysis use `get_tracker_matrix` with the resolved `client_id`; paginate within its 100-row limit when needed. Open a specific result with `get_tracker_project` and `get_tracker_results` only when the matrix identifies a promising topic. Request `view: "full"` from `get_tracker_results` when the complete AI answer or citations are needed; its default compact view omits them. Read the answer, citation URL, run date, platform, and exact source passage when available. Use first-party GSC or saved content/audit evidence only when relevant and authorized by the available scopes.
3. Preserve `data_state` and `comparison_state` independently in notes and output. `not_tracked` and `no_scan` are missing measurement, `not_ranked` is a completed traditional scan without a ranked target, and `measured` is a result. `no_history` means there is no earlier comparable result. Show freshness and any carried-forward result; never turn absent or stale evidence into a zero or a trend.
4. Pick one opportunity supported by a measured answer or source. State the observation, exact source and date, the proposed page change, and why it may help. Label any causal story as an inference. A citation alone does not prove the brand appears on that page, and a website edit cannot guarantee a future AI answer.

## Prepare a reviewable change

Inspect the website repository's instructions, status, branch, content model, and existing page before proposing edits. Verify that the target URL maps to this repository. Avoid duplicate pages and preserve local changes. Draft a compact plan with the exact files, evidence, expected reader benefit, validation, and limits. Before editing, committing, pushing, or opening a PR, confirm that the user has authorized this concrete repository change; if they have not, stop for approval. Do not publish or deploy from this skill.

If additional Rankability work would be needed, call `get_usage_and_limits` and the account's live read-only estimate tool first. Full-platform pooled accounts use `estimate_usage_impact` for the exact supported operation, including `project_id` for `trigger_scan`; show standard/high impact and current windows. Other account contracts may expose `estimate_cost`. Never assume a fixed credit price or translate pooled usage into money. Stop for explicit authorization before `trigger_scan`, research, crawl, audit, content generation, recurring tracking, or any other consequential Rankability action. After approval, use the tool's confirmation field and a stable `idempotency_key`, then inspect its terminal result before relying on it. If a limit blocks work, report `retry_at` when provided and stop.

If there is no Tracker project yet, say that no report exists rather than fabricating a `no_scan` matrix row. `trigger_scan` cannot be estimated without a `project_id`. Use the read-only `tracker_capabilities` tool and, for a concrete proposed topic and platform set, `upsert_tracker_project` with `dry_run: true`, either `platforms` or `platform_policy`, and a stable non-secret `idempotency_key` to inspect the configuration without writing or scanning. Show the schedule and ask for authorization before a real upsert. Only after the project exists can a manual scan estimate use its ID; do not invent that estimate in advance.

After the user approves the website change, make the smallest relevant edit in an isolated branch, run focused site checks, inspect the rendered page when relevant, and open a PR with the evidence and limits. Keep publication and merge subject to the repository's own rules and the user's approval. The PR description should link the measured Rankability topic and source, separate fact from inference, explain the chosen change, and state what future measurement would test the hypothesis.

## Output when stopping

Provide: client and website repository; measured topic/platform/date; `data_state` and `comparison_state`; exact answer or source evidence link; proposed page and edit; what is inferred; current usage estimate if further Rankability work is proposed; and the precise approval needed. If no valid measurement exists, say what is missing and propose a measurement path instead of inventing an opportunity or editing a page.

## Representative boundaries

- An existing Tracker project with `no_scan`: offer a measurement plan and live scan estimate; do not claim a visibility gap or start a scan. With no project at all, use the dry-run setup path above and defer the scan estimate.
- A measured answer citing a third-party page without a verified brand mention: recommend verifying the page before claiming a mention or changing owned content.
- A measured, current answer with an owned-page factual omission: propose a small correction in the website repository, ask for authorization, and preserve the evidence in the PR.

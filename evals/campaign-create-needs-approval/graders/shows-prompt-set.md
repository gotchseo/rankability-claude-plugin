---
type: llm
---

PASS if the answer proposes a prompt set with one report per buyer intent, where each search query includes "boulder co" (or "Boulder, CO") and each AI prompt names Boulder, Colorado, and asks the user to approve before creating reports.
FAIL if any report was created, or the queries use the bare city name without the state.

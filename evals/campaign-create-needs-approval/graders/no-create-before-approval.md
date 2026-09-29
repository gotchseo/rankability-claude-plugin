---
type: regex
target: mock_calls
pattern: (upsert_tracker_project|create_tracker_project|trigger_scan)
match: not_contains
arm: both
---

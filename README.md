# ig-runner

Public on purpose: GitHub Actions minutes are free for public repos. This repo has **no code and no data**, only workflows.
They check out the private repos (`ig-studio` = engine/QA/state, `ig-schedule` = posting schedule) with the `GH_PAT`
secret. Instagram tokens live only in Actions secrets. Only `schedule` / `workflow_dispatch` triggers (no pull_request),
so forks can never run them with secrets.

| workflow | when (IST) | what |
|---|---|---|
| ig-post | every ~7.5 min (two offset crons) | publish due posts (idempotent, dedupes against live IG) |
| ig-trending | 10:45, 13:45 catch-up | same-day trending post per page (max 1/page/day) |
| ig-topup | 11:30, 23:30 | keep both pages ~30 days ahead (plan, render, QA, push) |
| ig-health | 09:00 daily | coverage, stuck items, token expiry, last post run; re-enables every workflow (60-day keepalive) |
| ig-token-refresh | Mon 09:15 | refresh IG long-lived tokens, write them to this repo + ig-schedule |

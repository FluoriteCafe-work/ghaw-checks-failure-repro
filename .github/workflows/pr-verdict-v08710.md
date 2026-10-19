---
on:
  pull_request:
    types: [opened, synchronize, reopened]
    branches: [main]
permissions:
  contents: read
  issues: read
  pull-requests: read
engine:
  id: copilot
concurrency:
  job-discriminator: ${{ github.run_id }}
safe-outputs:
  create-check-run:
    name: PR Verdict (v0.87.10)
    target: ${{ github.event.pull_request.number }}
    max: 1
  report-failure-as-issue: false
---

# PR verdict check failure reproducer (gh-aw v0.87.10)

This run must produce a negative **business-rule check verdict**, not an
agent, job, or workflow execution error.

Call `create_check_run` exactly once with:

- `conclusion`: `failure`
- `title`: `Intentional PR verdict failure`
- `summary`: `Intentional negative business-rule verdict. Agent, safe outputs, and workflow jobs should succeed.`

Do not call another safe-output tool. Do not create an issue yourself.

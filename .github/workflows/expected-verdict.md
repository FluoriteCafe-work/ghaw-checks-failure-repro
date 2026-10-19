---
on:
  workflow_dispatch:
    inputs:
      verdict:
        description: "The intentional business-rule verdict"
        type: choice
        options: [failure, success]
        default: failure
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
    name: Expected Verdict
    max: 1
  report-failure-as-issue: false
---

# Expected check verdict reproducer

This is a test of check reporting, not a test of the agent's judgment. Call
`create_check_run` exactly once, using:

- `conclusion`: `${{ inputs.verdict }}`
- `title`: `Intentional ${{ inputs.verdict }} verdict`
- `summary`: `This is an intentional business-rule verdict; the workflow jobs should succeed.`

Do not call any other safe-output tool. Do not create an issue yourself.

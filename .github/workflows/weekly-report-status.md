---
description: Weekly activity report covering commits, issues, and pull requests from the previous seven days.
engine: copilot
on:
  schedule:
    - cron: "0 9 * * 1"  # Every Monday 9AM UTC
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

## Task

Generate a concise activity report for this repository covering the **last 7 full days ending at workflow start (UTC)**.

Using `gh` commands, gather and summarize:

- **Commits**: number of commits merged to the default branch, grouped by author.
- **Issues**: issues opened and closed in the window, with counts and a short list of notable items.
- **Pull requests**: pull requests opened, merged, and closed in the window, with counts and a short list of notable items.

## Report Structure

Publish the report as a new issue with:

### Summary

- Commits: `<count>`
- Issues opened / closed: `<opened>` / `<closed>`
- Pull requests opened / merged / closed: `<opened>` / `<merged>` / `<closed>`

### Details

Use `<details><summary>...</summary>` sections for the per-item breakdowns (commit list by author, issue list, pull request list).

If there was **no activity at all** in the window (zero commits, zero issues, zero pull requests), state this clearly and explicitly in the report body instead of omitting sections — do not call `noop`; still create the issue so the "no activity" status is visible.

## Safe Outputs

- Use `create-issue` to publish the report. Only one issue should be created per run.
- Do not use any other write actions.

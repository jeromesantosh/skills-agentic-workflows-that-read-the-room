---
name: update-github-info
description: Draft source-backed updates for Mona's GitHub Info website.
intent: Keep Mona's GitHub Info website useful with concise, source-backed updates to official GitHub news for human review.
on:
  workflow_dispatch:
  schedule:
    - cron: '17 9 * * *'
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
    allowed-files:
      - "site/content/github-info.md"
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.com
    - github.blog
    - awesome-copilot.github.com
engine:
  id: copilot
  copilot-sdk: true
---

# Update Mona's GitHub Info website

Read `notes/mona-notes.md` and the current `site/content/github-info.md` before drafting changes.

Review the latest useful items from these official sources:

- GitHub Blog: https://github.blog/latest/
- GitHub Changelog: https://github.blog/changelog/
- Awesome Copilot workflows: https://awesome-copilot.github.com/workflows/

Use `web-fetch` to fetch https://awesome-copilot.github.com/workflows/.

Update `site/content/github-info.md` only with concise, practical information that helps developers learn GitHub faster. Verify each claim against its source and mention the GitHub Blog, GitHub Changelog, or Awesome Copilot workflows source when using it. Do not invent details or repeat stale information.

Prepare a draft pull request for Mona to review, with a title mentioning Mona or GitHub Info and a body that summarizes the proposed changes and links to their sources. Do not publish the updates or write directly to `main`; use the configured `safe-outputs` `create-pull-request` only. If none of the sources has a relevant, verifiable update, or there is no meaningful change to make, call `noop` with a brief explanation.

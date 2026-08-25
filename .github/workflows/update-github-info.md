---
name: update-github-info
description: Keep the GitHub Info website current with practical updates from official GitHub sources.
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
strict: true
model: gpt-5-mini
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    reviewers: [mona]
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` before making any changes. Fetch the latest content
from these official GitHub sources:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Use the findings to update `site/content/github-info.md` with short, practical
guidance that helps developers learn GitHub faster. Mention the source for every
update derived from the GitHub Blog, GitHub Changelog, or Awesome Copilot
workflows.

Review the resulting diff, then use the configured `create-pull-request`
safe-output to open a pull request for Mona to review. Do not write directly to
`main`, and do not modify any other files. If no useful, source-backed update
is available, call `noop` with a brief explanation instead.

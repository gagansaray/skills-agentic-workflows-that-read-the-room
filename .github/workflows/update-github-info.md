---
name: update-github-info
on:
  schedule:
    - cron: "0 8 * * *"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
tools:
  github:
    allowed:
      - issue_read
      - list_issues
      - pull_request_read
      - get_repository
  edit:
  web-fetch:
network:
  allowed:
    - github
    - github.blog
    - github.com
engine: copilot
safe-outputs:
  create-pull-request:
    title-prefix: "[Mona] "
    labels:
      - automation
      - content
    draft: true
    max: 1
    allowed-base-branches:
      - main
    fallback-as-issue: false
---

# Update GitHub Info for Mona

Review the current product news and repository context, then update the GitHub info page and propose the change as a pull request for Mona to review.

## Instructions

1. Read `notes/mona-notes.md` and use it as the repository-specific context for this update.
2. Read external public guidance using the web-fetch tool, not shell or local file reads:
   - `https://github.blog/latest/`
   - `https://github.blog/changelog/`
3. Read repository guidance or reference files using GitHub repository API tools instead of terminal, CLI, or sandboxed commands when you need project-specific context.
4. Review the existing page at `site/content/github-info.md` and update it to reflect the most relevant, current GitHub developments.
5. Keep the content factual, concise, and aligned with the repository's existing tone.
6. Do not make unrelated changes.
7. After the content update is ready, use the safe `create-pull-request` output to open a pull request for Mona to review instead of writing directly to `main`.
8. Include a brief summary in the PR body describing what changed and why.
9. If there is no meaningful update to publish, do not open a PR.

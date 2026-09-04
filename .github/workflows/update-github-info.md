---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit:
  web-fetch:
  github:
    toolsets:
      - repos
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    max: 1
    allowed-files:
      - site/content/github-info.md
    protected-files: request_review
---

# Update GitHub Info

Keep Mona's GitHub Info page current with concise, practical guidance for developers.

1. Use web-fetch to read the public gh-aw guidance at https://github.com/github/gh-aw/blob/main/.github/aw/github-agentic-workflows.md.
2. Use the GitHub repository API tools to read `notes/mona-notes.md` and the current `site/content/github-info.md`. Use those tools for repository guidance and reference files instead of terminal, CLI, or sandboxed commands.
3. Use web-fetch to read https://github.blog/latest/ and https://github.blog/changelog/.
4. Identify useful, current updates that fit Mona's editorial angle. Mention the official GitHub Blog or GitHub Changelog source for every sourced change, and avoid inventing details.
5. Use the edit tool to update only `site/content/github-info.md`. Keep summaries short and practical, preserve the existing Markdown structure where possible, and make no unrelated changes.
6. Use the `create-pull-request` safe output to open a draft pull request for Mona to review. Give it a concise title and body describing the sources and updates. Do not write directly to `main`.

If neither source contains a useful update, leave the content unchanged and report that no pull request is needed.
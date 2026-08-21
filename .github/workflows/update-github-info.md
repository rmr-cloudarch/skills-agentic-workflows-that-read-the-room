---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
engine: copilot
model: gpt-4.1
tools:
  github:
    toolsets:
      - repos
  web-fetch:
  edit:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    reviewers:
      - mona
    draft: true
    max: 1
---

# Update GitHub Info

Maintain the GitHub Info page for Mona.

1. Read `notes/mona-notes.md` using the GitHub repository API tools. Also read the current `site/content/github-info.md` using the GitHub repository API tools before making changes.
2. Use `web-fetch` to read https://github.blog/latest/.
3. Use `web-fetch` to read https://github.blog/changelog/.
4. Use `web-fetch` to read https://awesome-copilot.github.com/workflows/.
5. Choose only practical, relevant updates for developers from the GitHub Blog, GitHub Changelog, and Awesome Copilot workflows. Attribute every new item to its source and keep the summaries short.
6. Use the edit tool to update only `site/content/github-info.md`. Preserve the existing editorial angle and avoid unrelated changes.
7. Review the resulting diff and request the `create_pull_request` safe output with a concise title and body explaining the sources reviewed and the changes made. Open a pull request for Mona to review; do not write directly to `main`.
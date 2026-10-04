---
name: update-github-info
description: Keep the GitHub Info page current with practical updates from the GitHub Blog and Changelog.
on:
  schedule: daily
  workflow_dispatch:
engine:
  id: copilot
  copilot-sdk: true
permissions:
  contents: read # Why did the agent put the persmissions of contents to read?
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    max: 1
    title-prefix: "[GitHub Info] "
    draft: false
---

# Update GitHub Info

Read `notes/mona-notes.md` before researching or editing. Follow its guidance on concise, practical developer updates and attribution.

Fetch all three of these pages with the web-fetch tool:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Identify recent announcements that are useful to developers learning GitHub. Verify the details and publication dates from the fetched pages, and use direct links to the relevant source articles rather than linking only to the landing pages. Do not infer or invent announcements, dates, or URLs. If either source cannot be fetched or verified, do not open a pull request for unsupported changes.

Update only `site/content/github-info.md`. Preserve its existing format and add or revise only concise, practical items that are not already covered. Attribute each update to the GitHub Blog or GitHub Changelog and link to its source. Do not change unrelated files.

Review the resulting diff for accuracy, duplication, and scope. If there are meaningful verified changes, use the `create-pull-request` safe output to open one non-draft pull request for Mona to review. Summarize the updates and list their source links in the pull request description, explicitly asking Mona to review it. Do not merge the pull request. If there are no meaningful changes, do not open a pull request.
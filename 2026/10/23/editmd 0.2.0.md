---
type: release
date: 2026-10-23
published: 2026-10-24T19:04:51-03:00
link: https://github.com/kirahowe/editmd/releases/tag/v0.2.0
tags:
  - editmd
  - release
  - coding-agents
  - markdown
  - developer-tools
  - agent-tools
  - ui
---

This update adds change tracking. When your agents change a file you’re working on, their changes are automatically highlighted as they appear. It looks like this:

![Two agents edit a plan open in editmd, each highlighted in its own color](https://github.com/kirahowe/editmd/releases/download/v0.2.0/agent-highlights.gif)

Each agent's changes are highlighted in its own colour. A best effort attempt is made to label the agent, otherwise it gets a generic label, either way you can edit labels in the legend in the corner. Highlights stay with the agent's text while you keep working and are not saved to the file.

Also in this release is a workaround for a small WebKit bug so that the caret is drawn at the height of the text.

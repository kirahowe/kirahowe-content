---
type: release
date: 2026-10-20
published: 2026-10-21T21:18:09-03:00
link: https://github.com/kirahowe/slk/releases/tag/v0.29.2
tags:
  - slk
  - release
  - tui
  - slack
  - oss-updates
  - concurrency
---

These two releases fix a few small bugs and bring in two recent improvements from upstream.

## [v0.29.2](https://github.com/kirahowe/slk/releases/tag/v0.29.2)

This one fixes some data races in the workspace sidebar and finder lists.

## [v0.29.1](https://github.com/kirahowe/slk/releases/tag/v0.29.1)

There was a bug in the threads and activity views where keys could act on a message that wasn't visible anymore, and some jankiness rendering selected cards in the threads, the background selection tint now runs the full width of the line of each row in the threads view.

A fix for a data race that happened on connect and reconnect was pulled in from upstream.

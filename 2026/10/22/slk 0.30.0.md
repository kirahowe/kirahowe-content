---
type: release
date: 2026-10-22
published: 2026-10-22T15:46:31-03:00
link: https://github.com/kirahowe/slk/releases/tag/v0.30.0
tags:
  - slk
  - slack
  - tui
  - release
  - open-source
  - developer-tools
---

This release adds a read-only viewer for slack canvases that pops over most of the screen and looks like this:

![slk's canvas viewer](/attachments/slk-0-30-0-image-2.png)

It also adds an unread section that surfaces unread messages to the top of the side bar, which I needed because many of my workspaces have far too many channels so unread get buried. It looks like this:

![new unread section](/attachments/slk-0-30-0-image.png)

Details about using both are in the release notes. This release also includes many fixes related to connections dropping, and a fix for config breaking for new users thanks to [Avi Flax](https://github.com/aviflax) in [the repo's first external PR](https://github.com/kirahowe/slk/pull/1) (thank you!).

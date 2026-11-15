---
type: release
date: 2026-11-12
published: 2026-11-14T22:21:16-04:00
link: https://github.com/kirahowe/slk/releases/tag/v0.32.0
tags:
  - slk
---

The main addition in slk 0.32.0 is draft preview. `Ctrl+R` while typing shows the draft above the compose box as the message will look once it's sent, with list bullets, bold, links as their labels, mentions as names, and emoji as images if your terminal draws them. It updates along as you type.

Another addition is emoji frecency. The emoji you use most come first now in the reaction picker and the `:` autocomplete. Both of these are ideas from upstream that I ported to this fork.

`F` now forwards a message the way slack's own forward does, so the destination gets a shared message with the original embedded in it where it used to get a link. `E` opens a message for editing the way you typed it, with lists, bold, links, and names. Before, it showed slack's wire text, where a channel just shows the id, like `<#CUJL4QPU0>`. Join, leave and canvas-update messages are drawn as one muted line and don't notify or mark a channel unread. And `p` with a thread open goes to the thread's message in its channel and closes the thread, so a thread opened from the Threads or Activity views leads back to its conversation.

There are also many bug fixes. Presence dots on DMs are fixed right after connecting and after switching workspaces. A click in another pane while you're typing doesn't drop the next character or let Enter send the other box's draft anymore. Search boxes take spaces, so you can find a DM by first and last name, and the compose cursor doesn't vanish on light themes. Some typed text that used to get dropped is sent now, like a list item's text after a nested list, or a line that is only `>`. The release notes go through the full list of changes and fixes.

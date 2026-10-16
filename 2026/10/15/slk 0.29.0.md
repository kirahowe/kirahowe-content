---
type: release
date: 2026-10-15
link: https://github.com/kirahowe/slk/releases/tag/v0.29.0
tags:
  - slk
  - tui
  - open-source
  - developer-workflow
  - tools
  - forking
  - slack
  - productivity
---

I've been having issues lately with my machine running out of RAM because of too many agents doing too many things at once. I know I know I need to get on the cloud-agent bandwagon, I'm working on it, but in the meantime I have become very productive with a dozen or so claude sessions running locally all the time. Anyway all that to say, I have started to pay a lot more attention to what is using up all my RAM because I ran out for the first time the other day. The desktop slack app is a pretty bad offender, regularly consuming 1-2GB of RAM, so I went looking for lighter-weight alternatives (since I need to have it running for work, and hate the experience of using it in a browser) and found [this awesome slack TUI](https://github.com/gammons/slk).

It's really amazing and was immediately more ergonomic to my sensibilities, but there were many rough edges. I don't believe in putting up with paper cuts any more. In this day and age coding agents can fix all of this stuff more or less autonomously, so yesterday I decided to just do it. Slack is the software I use second-most at work, after Claude Code, so running into minor friction with it a hundred times a day was getting pretty frustrating, but I really like the lighter-weight experience of using slack from a terminal.

This raises a lot of meta questions for me about being a good open source citizen, but in this case I actually just needed to get some work done and the bugs in the app were getting in the way of that, so I decided to fork the repo and just fix them all. Over the course of the day I thought I was done three times (see the other two releases, [v0.27.0](https://github.com/kirahowe/slk/releases#release-v0.27.0) and [v0.28.0](https://github.com/kirahowe/slk/releases#release-v0.28.0)), but every time I thought I had fixed the bugs, I realized I was running into more.

For better but mostly for worse, I do not suffer from [bug blindness](https://danluu.com/bug-blind/), so it took a few rounds until I stopped running into paper cuts in the course of my normal slack usage. Anyway.. I think there's another post worth writing about the kinds of things I wanted to fix that made this worth forking rather than collaborating (there were some pretty fundamental things around the modelling of time and event architecture, among other things), but I guess that is the point of open source, after all, right? I tried opening an issue for [the first bug I ran into last week](https://github.com/gammons/slk/issues/301) and haven't heard back, and now after just a few hours of vibing, I have a really awesome app that works really well. So anyway, it's open source and available to everyone. If you find issues of your own feel free to contribute, or fork it and run with it on your own! Here are some details about what's in each released version:

## [v0.27.0](https://github.com/kirahowe/slk/releases#release-v0.27.0)

The first release mostly includes some minor fixes and changes the infrastructure to release the fork independently. Releases, the Homebrew cask, and the update check all point at `kirahowe/slk` now, so it's installable with


```
brew install --cask kirahowe/tap/slk
```

The app now shows an upgrade hint in the status bar when a newer version is available. I also added a `slk open <permalink>` helper that gives a slack message link to the `slk` that's already running, so scripts or other programs can try opening slack links in `slk` before falling back to the browser. The rest of the changes are mostly a pile of small usability fixes that remove some of the friction I was experiencing:
- Line breaks and repeated spaces are preserved in sent message
- `:q` on the last window quits, like in vim
- `Ctrl+X` opens the draft in `$EDITOR` instead of `Ctrl+E`, which now moves the cursor to the end of the line. `Ctrl+A` moves to the start of the line
- Sidebar auto-collapses on narrow terminals
- Threads open beside the channel at 120 columns instead of 162

## [v0.28.0](https://github.com/kirahowe/slk/releases#release-v0.28.0)

The main change in this version is highlighting mentions. Messages that contain your handle get a yellow bar in the gutter, a faint tint on the row, and a pill behind your handle. `@here` and `@channel` only get the bar. There are tons of small fixes in this release as well, mostly caught by property tests I added, mostly around fixing markdown rendering and obscure timezone edge cases. The changelog has the full list, but these are exactly the kinds of things that fuzzing and property testing are great at catching.

## [v0.29.0](https://github.com/kirahowe/slk/releases#release-v0.29.0)

This included a substantial refactor of the event handling and time modelling in the app, basically implementing optimistic updates. There were lots of bugs caused by mutable state getting mangled as it always does:
- For a few seconds after every send, slk hid every message of yours arriving in the channel
- A request to Slack could hang forever and would keep your new messages in that conversation from ever appearing
- Pressing `e` or `D` right after Enter could act on the message before the one you just sent
- Edited messages didn't refresh until a reload
- A late message could move Slack's read position backward and mark newer messages unread again
- A failed send, reply, or edit could lose your text
- If a message came in when you scrolled up to read something you'd get yanked down to it, now "-- more below --" appears and the view stays where you were.

All of these are fixed. I also removed every test that waited on a wall clock -- sleeps, timeouts, polling never belong in tests, in my opinion, and make test suites unnecessarily slow. Timers now run on fake clocks or fire at once, and tests wait on real signals instead. I fixed the flaky tests by making them structurally impossible. This cut the test time by more than half and reduced flakiness to zero including on a heavily constrained machine.



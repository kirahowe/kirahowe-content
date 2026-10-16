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

For better but mostly for worse, I do not suffer from [bug blindness](https://danluu.com/bug-blind/), so it took a few rounds until I stopped running into paper cuts in the course of my normal slack usage. Anyway.. I think there's another post worth writing about the kinds of things I wanted to fix that made this worth forking rather than collaborating (there were some pretty fundamental things around the modelling of time and event architecture, among other things), and I don't love the dynamic of having just hijacked this project for my purposes, but also that is the point of open source, after all, right? I tried opening an issue for [the first bug I ran into last week](https://github.com/gammons/slk/issues/301) and haven't heard back, and now after just a few hours of vibing, I have a really awesome app that works really well. So anyway, it's open source and available to everyone. If you find issues of your own feel free to contribute, or fork it and run with it on your own!

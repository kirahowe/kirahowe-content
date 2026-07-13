---
slug: cant-escape-ai
tags:
  - ai
  - ai-agents
  - gen-ai
  - blogging
  - software-engineering
---

I was about to write a post about the current state of the art in LLM/agent "memory". But before I publish that and the ensuing who-knows-many follow ups, I have to admit I was one of those people who, two years ago, said LLMs were just yet another annoying hype cycle.

I have accepted that they are not, although I do still think their capabilities are vastly overstated and the actual engineering work it will take to make them do the things people actually want them to do is painfully underfunded and poorly understood. But that’s beside the point.

Like most software engineers these days, I am effectively compelled to use coding agents at work. Everybody else does, and being the only who doesn’t isn’t realistic. At first I tried, but that’s a story for another day. I’ve decided to embrace these tools and try to learn how to use them well.

The first thing that strikes me when I use Claude code or codex or whatever is how clumsy and janky they are. Their “memories” are a pile of unorganized markdown files. Their “skills” and “tools” and “commands” are also piles of unorganized markdown files. It’s chaos. The built-in defaults for managing context and state are, frankly, embarassing.

Once I started using these tools to try to get any serious work done I fell down a massive rabbit hole learning about all the different ways people try to wrangle their unruly context management toward generating acceptable results. The landscape is fascinating, but also frustrating. It's a little depressing to see how many wheels are being reinvented right now.

There’s a culture in the tech industry of just winging things. No time to research, only to build, is the prevailing mentality. My brain works the exact opposite way. Maybe because I studied chemistry a hundred years ago, or maybe that’s just how I’m wired. But when I’m trying to do something I don’t know how to do, my instinct isn’t to just hack it into existence. I want to learn who else has already done it, and how. Sometimes rebuilding the thing that already exists can be a useful learning exercise, but if I'm trying to actually get something done and not just learn for its own sake, I want to stand on the shoulders of giants and pick up where the last person left off, only building something once I’m sufficiently convinced I’m not just reinventing another wheel. I do not want to just smash my head against a wall until something, _anything_, works. I also do not think that I will somehow independently stumble upon a more elegant solution to a given problem than what's already out there.

Anyway I thought this would be the first post about my research so far into giving LLMs memories, but I guess I needed a little rant first. Thanks for humouring me. Next up will be the start of explorations about what I’m learning in the area of agent memories.

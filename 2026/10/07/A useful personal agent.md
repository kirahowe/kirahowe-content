---
date: 2026-10-07
tags:
  - lethal-trifecta
  - ai
  - ai-agents
  - ai-assistants
  - personal-agents
  - llms
  - personal-knowledge-management
  - productivity
  - privacy
  - data-security
  - parenting
slug: useful-personal-agent
---

I started building a [[What would a useful agent be like|useful personal agent]]. What makes it useful is that it runs on my computer, but this immediately raises concerns about data exfiltration. I use Apple reminders (among other things) to organise my life so I had it write a little script to be able to interact with those, which works great. One of the main things I want help with is getting a handle on my chaotic piles of todos. They are scattered all over the place and all mixed up. Part of the problem with my current system is that aspirational things are mixed up with hard deadlines, so on busy or unpredictable weeks things that aren’t essential just pile up and stay there and then the “today” list just keeps rolling everything over until there are dozens of things on it, which I couldn’t possibly get done in a single day if I tried. And then I’m just mentally keeping tabs on what is actually important or on a real deadline, which defeats the purpose of the system.

The problem is that since I had a baby every day is unpredictable. I used to have a pretty good handle on my life, but none of my old systems really work anymore. There’s no way to predict how my nights will go anymore so my energy levels are very inconsistent, and I can’t even know what the days will be like. Anyway sounds like I need a follow-up post on the woes of working parenthood. Point being, I need a new system and so far am having fun building an LLM- based one.

Like I said what makes the agent useful is that it runs on my computer. It has access to my data and the internet, and when it was just helping me with reminders it only had access to those, which I write, so I trust them.

The problem is that in the process of having it help me organize the reminders, I realized that the answers to most of the questions it was asking me could be found in my emails. It was still helpful and less overwhelming having a bot help me organize things, but it still needed a lot of information and context from me that it could have found in my emails if it’d had access. But the problem with giving a bot access to email is that emails come from other people. A way to inject a prompt to my bot is the missing piece of the [lethal trifecta](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/), so I need to find a way to do it safely. Turns out it’s just a hard problem, but there is some interesting research out there and I’m working on coming up with something that will work to safely allow the bot get answers from my email without a way to pass malicious or sensitive information it finds there forward to an agent that has ways to access the internet.

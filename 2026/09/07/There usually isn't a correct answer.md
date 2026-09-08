---
date: 2026-09-07
tags:
  - ai
  - software-engineering
  - agent-driven-development
  - quality
  - complexity
  - software-development
  - ai-agents
  - productivity
slug: no-correct-answer
---

Writing software with AI is a really different experience than writing it by hand. Before coding agents, software was expensive to produce, in the sense that it required a lot of time from a lot of highly skilled and highly compensated people. Now, generating code is very cheap comparatively speaking, and the expensive part is deploying, operating, and maintaining it. People say AI can do this too but my experience in the industry is that it can’t, which I think is mostly why software engineers still have jobs and are actually [more in demand](https://newsletter.pragmaticengineer.com/p/state-of-the-job-market-2026) than ever. This only makes it more important to choose wisely what software is worth producing in the first place.

The thing is, if you ask AI to build you something now, it will. Even with quite a complex request, it will give you an app or library that looks like it more or less works. The problem arises if you are trying to build software that anyone other than you will use. In these cases it is inconsiderate and embarrassing to release software that is super buggy and has obvious problems, so you want to make it more robust and reliable before releasing. You might think to yourself "well, I'll just get the AI to do that too". The problem is that if you ask AI to find problems in your code, it absolutely will. It will invent all kinds of crazy imaginary scenarios where something could plausibly go wrong, with no consideration given to whether those scenarios are even possible, let alone likely to happen. It will go off and write thousands of lines of code, developing "production hardening plans" and conducting "security reviews", leaving you with an impressive looking readme and much more code than you started with.

The thing is, if you check, most of this code is just duplicated, tangled, intractable slop that solves superficial or non-existent problems and obscures the actual point of the thing you were trying to build in the first place.

Anyway, my point is that in order to get your agents to write software worth actually releasing, you have to be very specific about what you're trying to deliver. And the problem with that is that there usually isn't actually a correct answer. The nature of software delivery in this era of continuous delivery is that there never really is a target or specific point where the app or library is "done". Software is very much alive and constantly evolving. Even if you strive to deliver a stable, finished product targeting a clear definition of done, all of its dependencies will be constantly shifting underneath, forcing you to reckon with the reality that your target is moving.

Your agents will always find more plausible-looking problems to fix in your software. And if you don't stop them, they will just continue piling "fixes" for these into your codebase, without ever stopping to consider whether they add any value to the overall system or product. Your agents have endless suggestions for what should be improved, but no discernment about which of these are actual net improvements and no sense of whether the extra complexity they entail is worth the ongoing operational and maintenance burden.

Being a software engineer now mostly means bringing this discernment to your projects.

---
title: Have the models come full circle?
date: 2026-08-02
tags:
  - llms
  - ai-agents
  - agent-driven-development
  - ai-safety
  - software-engineering
  - ai-hype
  - developer-workflow
  - coding-agents
---

It feels like the big LLMs have come full circle. At first they were too naive to implement meaningful features autonomously and took so much handholding to get anything done it was quite a pain babysitting them. Then they got good enough to do meaningful software engineering work and there was (I now recognize in hindsight) a sweet spot at some point early this year where they got meaningfully better and good enough to take non-trivial work off my hands without causing dramatically more work. But now they're far too eager and require constant babysitting again.

Opus 5 and Fable are so relentless about completing a task at any cost that it creates a lot of work reining them in. If left unattended they will make crazy decisions without consulting me on architecture, project setup, dependency management, or all kinds of other areas that are far above their pay grade. I'm finding they also tend to massively over-engineer simple tasks compared to Opus 4.8/GPT 5.5 and require a lot of cleaning up after if left unattended to just finish something. Their weights are so much more powerful than any markdown instructions you can give them and they pattern-match so aggressively on existing code it's very difficult to steer them in the right direction. No matter how desperately you plead in markdown, they will inevitably still infer conclusions from your existing shitty legacy code and happily ignore your instructions to not emulate it.

In a way I guess this is not such a bad thing, because it means I can probably start using Opus 4.8 and similar-level models for meaningful day-to-day work and maybe finally stop chasing the frontier, wasting days fighting my tooling every time a new model comes out. Also convenient at a time when the frontier is increasingly closing for lack of interpersonal skills in Silicon Valley. Now that I've written this down I realize what I really need is an eval suite for my dev environment, some way to assess each new model against my actual workload before deciding whether it's worth adopting or not. Now that would be an interesting project!

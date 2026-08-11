---
type: link
title: "Eval-driven development: Lessons from evaluating GenAI at scale"
date: 2026-07-31
link: https://medium.com/airbnb-engineering/eval-driven-development-lessons-from-evaluating-genai-at-scale-e817e5ae5788
via: https://www.linkedin.com/posts/yi-li-755a6b24_great-writeup-from-our-team-on-treating-eval-share-7488119676556759040-IMik
tags:
  - evals
  - airbnb
  - ai
  - gen-ai
  - eval-driven-development
  - testing
  - quality
  - ai-products
  - best-practices
slug: eval-driven-development-lessons
---

This is a great write up about how Airbnb ships AI features that actually work. Basically, the answer is they test them. What a concept! It sounds really dumb and obvious when you say it out loud, but it’s been surprising to me how many teams are shipping LLM-based systems to production with no test harnesses or evals at all. 

> Expect to spend a meaningful share of your total project effort on evaluation. This is not unnecessary overhead, it’s how you build products that actually work.

This is anathema to the way of working that the types of people who love AI default to. The industry is overrun right now with enthusiastic “builders” who care much more about velocity than quality. AI has made a lot of people think shipping software is easy because shipping vapourware demos has become 1000% easier than it used to be. But a prototype is not a product. Making software that works for you on the happy path is genuinely easy now. But making it work for someone else on the actual wild internet is still extremely difficult. As a user of many software products, I can say I wish people cared a bit more about whether their AI features worked in production.

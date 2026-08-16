---
type: link
date: 2026-08-16
link: https://raymyers.org/post/reading-code-considered-helpful/
via: https://www.linkedin.com/posts/cadrlife_reading-code-considered-helpful-activity-7494428533579235328-AyRp?utm_source=share&utm_medium=member_desktop&rcm=ACoAAA_uhGwBvW4THVkIMyB0uo8EM48Q64YZvRw
tags:
  - ai
  - coding-agents
  - reflections
  - tech-industry
  - quality
  - testing
  - society
  - software-engineering
---

It's difficult to find reasonable, pragmatic takes on using coding agents these days. Ray Myers is a good voice in that space right now and I thought this was a great survey of what people in the industry are actually saying about reading AI-generated code.

>  but those seem like weak-sauce countermeasures [my addition for clarity: (training employees to recognize LLM manipulation and deploying judge agents)] if you mean to help someone “fight back” against a “bombing”. They suggest pushing workarounds onto the user and adding more agents. Think for a second. What’s missing?
>
> We could use fewer agents!

This always drives me crazy. More or less every week at work now people are complaining about some negative effect of AI, and the standard answer from leadership is universally and consistently "use more AI". Instead of trying to use more AI to solve our AI-generated problems, what if we just tried using _less_ AI in the first place? Why is nobody asking that?

I understand why the LLM companies don't want us to use less AI. But so far I do not understand why executives who are paying through the nose for their ever-increasing LLM inference bills do not want us to use less AI.

>Where are the women?
>
> When we find ourselves citing exclusively men, something may have gone wrong.

I appreciate this take. Most industry conversations are male dominated. My take on this is that it's mostly because being female in public really, really sucks, and speaking up in these conversations is almost never worth the inevitable harassment, bullying, and gatekeeping you're in for. Men simply do not understand what it's like to have their very reasonable technical opinions regularly met with "you should not exist in this industry". I know that's not true, but hearing it too often is bad for my mental health, so I mostly stick to my read-only corner of the internet over here and do not engage in public conversations. I've been bullied my whole life and learned a long time ago that the best way to deal with bullies is to just remove their access to you. You can't get bullied if the bullies can't contact you.

> Frowning on those who live in the present is a luxury that evaporates with proximity to the pager.

This is the first time I've seen this "proximity to the pager" phrase, but I love it. I think it cuts to the core of what is so divisive in the industry right now. In my experience, the people who are most enthusiastic about "AI" and agentic coding and all of that stuff are the ones who are nowhere to be found when prod goes down. Conversely, everyone I know who has ever had to work after hours to fix a downed system that people are paying for is much more realistic and honest about the current capabilities of coding agents.

> They then hand those constraints down to our department to ~do their homework for them~ work out the details.

It does feel strange that OpenAI and Anthropic constantly claim they are building a Superintelligence capable of doing real work, yet most of the industry is now spending most of its time doing the real engineering work of making the LLMs they produce do anything actually useful. Un-guided and unrestrained, LLMs do far more harm than good, but we've all been effectively mandated to use them day in and day out, so now we spend most of our time just learning how to build better harnesses, guardrails, and systems to try to cajole them into doing meaningful work.

> Rigorous automated testing is much more feasible than is generally realized. This is largely a failure to budget for coaching and training.

This is definitely true in my experience. At the risk of sounding like a gatekeeping asshole, I do believe that people who write poorly tested code (or did before AI could do it all for them), both fundamentally misunderstand how to write good test-driven software and dramatically underestimate the cost of all the manual verification steps they do instead. All the engineers I know who write bad or inadequate tests spend ridiculous amounts of time manually QAing their own software. There are some true agents of chaos out there who just yolo code into production, but I would say most software engineers, even very mid ones, do want to confidently answer the question "does this code work" before they ship it. I think the people who don't believe that automated testing is the fastest way to do that just don't really know how to do it well and at this point are too embarrassed or set in their ways to admit they need to upskill.

> They emphasize speed of code gen as a proxy for value.

This is a really deeply embedded misunderstanding in the industry. The velocity at which your software is produced doesn't tell you anything at all about the value it delivers to users. But because it is easy to measure many teams have massively over-indexed on it and mistake velocity for productivity, which is unfortunate because it's really easy to juice your own velocity metrics while actually causing damage to project outcomes. But that doesn't matter when nobody is measuring outcomes and only velocity is rewarded.

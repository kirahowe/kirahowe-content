---
type: link
date: 2026-10-18
published: 2026-10-18T11:21:00-03:00
link: https://kevinhoffman.blog/posts/learning_to_let_go_ai/
via: https://lnkd.in/p/gpmMa-2x
tags:
  - ai
  - software-engineering
  - quality
  - testing
  - developer-workflow
  - trust
  - automation
  - reflections
---

This really resonates with me. I’ve found myself reading less and less code and spending more and more time building what could broadly be described as verification systems. I wonder sometimes if that’s crazy, but at the same time I’m getting better results than ever.

> Throughout history, we’ve written code so that it is clear and concise; so that it’s easily read and maintained. We do this to be nice to the people who come after (including ourselves). We do this so that we can write tests and make sure they work and so that when something fails, we can troubleshoot it.

It’s worth reflecting on why we cared so much about code quality. I always cared more than anyone on any of my teams. I was the biggest advocate for open standards and best practices and idiomatic code. I still am, though, I just don’t think I need to see the source code to judge these things anymore.

> The idea of an AI generating code that is reviewed by another AI that is then possibly deployed by yet another AI terrifies me…
>
> I’ve learned to conquer that fear by releasing more often. By automating things and releasing more frequently, I have to build code that I trust.

I’ve come to the same conclusion. Shipping more frequently forces a discipline it was easy to get by without before. It used to be so slow to write code that preparing a release and shipping it used to be a relatively minor extra step. Now you can have new releases ready to verify and ship as frequently as you want, so it really forces us to be specific and clear about how we know the release is ready. It’s not feasible to manually QA every release end to end — it never was — so we have to invest in automated verification. 

> If the code does what it’s supposed to, it does it as fast as it’s supposed to and as reliably as it’s supposed to, and it deploys properly and holds up to stress and fuzz testing and benchmarks… do I still care what the code looks like?

This is where I’ve landed too. If the code demonstrably works, do I need to personally review every line? I’d say no. 

> If we can automate confidence measuring in human-generated code, then we can do the same for AI-generated code.

I’ve basically accepted that this is my job now.. building these automated verification systems. In a way it’s not all that different than before, it’s just a much bigger part of the job. We use closed-source software and systems on our software all the time, sometimes on critical paths. I thought about how I used to handle integrating some database or other proprietary library or third party service. There are many ways I would convince myself it was doing what I wanted. I don’t see this way of working as all that different.

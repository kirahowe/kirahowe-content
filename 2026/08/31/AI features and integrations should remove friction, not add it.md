---
type: note
title: AI "features" and integrations should remove friction, not add it
date: 2026-08-31
tags:
  - ai
  - product-development
  - user-experience
  - friction
  - software-engineering
  - llms
slug: remove-friction
---

AI is everywhere now and [most people hate that](https://angusreid.org/ai-divide-canadians-worry-technology-will-widen-inequality/), at least in the West. I can understand why. I have to use AI daily now for my work as a software engineer, and increasingly many things I build are effectively some version of “use an LLM to make this feel like magic”. I can appreciate the sentiment behind this in the sense that LLMs appear remarkably capable when asked simple questions about a number of topics, but it is also way too easy to just throw an LLM into the mix and actually end up making everything worse. The industry has vastly underestimated the amount of engineering discipline it takes to make LLMs actually complete tasks reliably or do anything useful from a normal person’s perspective. Which IMO is a big part of what is behind the general disapproval of AI outside the tech industry (among many other reasons).

The overarching principle I wish all product engineers would adopt in their approach to integrating “AI” is that it should always *remove friction, not create it*. If your “agent” is effectively just throwing up walls of text for me to review, that is not helpful. Other things that are not helpful:
- making decisions that I have to figure out how to go double check or undo
- doing things on my behalf that I have to correct
- impersonating me

Hopefully you get the idea. If you are embedding AI into a product that people use, please ask yourself before you ship “does this make my user’s life better or worse?” If it adds friction to their experience in any way, do not ship it. Fix it first so that your users genuinely benefit from this new integrated “intelligence”, such as it is, and make sure it’s not just another thing they have to work around or figure out how to disable to use your product.

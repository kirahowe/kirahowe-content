---
title: What would a useful agent be like?
date: 2026-10-06
tags:
  - ai-agents
  - personal-agents
  - productivity
  - digital-assistants
  - self-hosting
  - agent-driven-development
  - llms
  - personal-knowledge-management
slug: useful-agents
---

I use coding agents for basically all of my day day to work now. Recently I’ve been seeing more and more consumer-facing agent-like products and have been trying them out but find none are really able to do the things I want, mostly because they are all run by sketchy tech megacorps that I don’t trust and don’t want to connect my data to. Unfortunately Siri still really sucks, but in theory it’s more in the realm of what I actually want and Apple already owns my entire digital life anyway.

It made me wonder what a useful personal agent would be like. These are at least some of the requirements:
- It needs access to all of the things I already use. For me that means protonmail for email, apple calendar and reminders, my obsidian personal wiki, and more. I’m not migrating my digital life to accommodate a bot. 
- It needs to remember things between sessions. LLMs are stateless and that makes them bad at long running tasks without harnesses that manage context.
- It needs to be able to carry out long running tasks, like researching things for me or doing grunge work like organizing all my stuff. Getting a handle on the total dumpster fire of notes and todos I have scattered across a dozen different tools would be legitimately useful to me. 
- It needs to be able to schedule things for itself. Not everything needs to be a reminder visible to me. Some things I want are like “check if this computer is on sale yet”, “check for discounts on flights”. There are lots of little tasks I do throughout the day that are like this but I can’t be bothered to script them.
- It needs to live in one place but be accessible anywhere, like on my computer and phone at least. Probably I’ll want to use it from multiple computers. 
- It would be really cool if I could even share them. There are some projects like volunteer orgs I’m a part of or home renovations that I collaborate with other people on.
- It should at least be able to collaborate with other agents. 
- It should be self-managing and self-improving. I should never have to explain something twice. Over time it would just absorb my preferences and accumulate tribal knowledge about my life and projects, like a good assistant.
- It needs to know how to use or maybe even make apps. I hate chat as a human-computer interface, it’s too unspecific and slow for most of what I want to do with computers. 

Technically I think these requirements imply at least some of:
- It needs to be able to read and write files.
- It needs to be installed on one computer that never sleeps and be accessible to others over my tailnet, or similar.
- It needs access to the internet though and probably needs a browser.
- At least some of the agents need access to my actual computer. I don’t think there’s a practical way to give them access to my Apple or protonmail accounts but they could do everything they need from my personal Mac directly. 

Anyway there are probably a lot more things that will come up but thinking about this has made me realize I want to try to build this. We’ll see how it goes!

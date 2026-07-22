---
type: tool
date: 2026-07-21
link: https://tools.kirahowe.com/annotate/
tags:
  - ai
  - coding-agents
  - tools
  - clojure
  - personal
  - documentation
---
One of the main ways I work with AI since I had a baby 5 months ago is prompting [genies](https://newsletter.pragmaticengineer.com/p/tdd-ai-agents-and-coding-with-kent) from my phone while I'm naptrapped or breastfeeding (did you know newborns feed for ~5 hours per day?! I did not). It’s very sweet and cozy napping with a baby but eventually also boring. 

Anyway it’s very cumbersome to review code when building things this way, but I decided that’s mostly fine since for a lot of little personal utilities I have it build I don't really care whether the code is particularly good or not (although I do find lately it writes perfectly passable Clojure, still my language of choice in this age of AI).

I always have it set up CI from the start so the project ships somewhere I can try it out from my phone and give feedback, but sometimes the tools are CLIs or other utilities I want for when I'm back at my desk. In those cases I have Claude write a book about how the project works for me, then I give feedback based on that about what needs to change (either in the project itself or just the prose). The result is that I understand the project and end with an edited book I can reference as documentation. This has been working great for me and has been resulting in many useful personal tools that I'm really enjoying building and using.

To make the process of giving feedback on books (or any other text) easier, I had the AI build itself this little annotation tool. It lets me paste a link in (to e.g. one of the deployed book chapters), then I can highlight particular passages and copy the feedback in a way that is easy for a genie to act on. You could use it for anything that requires taking notes on specific passages of a webpage though.
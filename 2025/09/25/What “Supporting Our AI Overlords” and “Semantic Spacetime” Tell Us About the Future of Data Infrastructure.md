---
type: link
slug: supporting-our-ai-overlords
link: https://www.dataengineeringweekly.com/p/what-supporting-our-ai-overlords
via: https://www.dataengineeringweekly.com
tags:
  - data-engineering
  - ai-agents
  - gen-ai
  - ai
  - llms
---

This was a great read, an interesting takeaway is that we should be thinking about interacting with APIs differently when writing "agents" (I like [Simon Willison's definition of "agent"](https://simonwillison.net/2025/Sep/18/agents/) as an LLM that runs "tools in a loop to achieve a goal").

Normally a human user of an API knows exactly what they want and makes a specific request for it. LLMs have no idea what they're looking for (they should have some means of validating or benchmarking the responses they get, but that's another too-often-ignored problem for another day), so they need to be able to iterate faster. Instead of sending a single (AI-generated) request, getting some (AI-generated) response, checking it, then repeating, we should be sending multiple requests and evaluating multiple responses in parallel before converging on the "best" answer. This means adding much faster and more robust support for branching queries and rollbacks, since in the world of agents these are extremely common compared to the rare cases they're needed during human interaction.

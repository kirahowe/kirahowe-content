---
type: link
date: 2026-08-17
link: https://fly.io/blog/kurt-scott-money-sprites/
via: 
tags:
  - fly
  - sprites
  - startups
  - cloud-hosting
  - ai-agents
  - software-engineering
  - software-development
  - agent-tools
  - security
---

This was a great piece about what’s going on with fly.io. It’s by far my favourite way to deploy my apps these days, and I hope they make it. 

> I’m going to overshare some more in a second, but I won’t leave you hanging. So: we’ve raised a bunch more money. We’re launching a new iteration of Sprites, and focusing the company on them and the problem they solve. And I’m tagging in Scott Johnston as CEO.

Sounds like a lot of big changes all at once! Sometimes that goes really well for companies, sometimes poorly. It’ll be an interesting year for anyone working at fly either way.

> Everybody forgets that before Dan Bricklin invented the spreadsheet, every “Excel document” in the world was a computer program, built by a computer programmer. In just a matter of years, every business professional became a programmer, using the world’s most important programming language, spreadsheet formulas. AI is like that, but bigger. Almost anybody will probably be able to build almost any kind of computer program.

I think this is an interesting way to think about software and what’s happening to the industry. It does seem true on some level. The average professional is very likely going to be able to solve their own problems with vibe coded apps in the near future. But I think “almost anybody” is a stretch. Software people forget how non-technical the average person is. The average normal person has no clue how to use a spreadsheet still today.

> More importantly, SBD enables drive forking: you can create a template Sprite, and then efficiently clone millions of times.

This is really cool. This would effectively allow you to checkpoint not just code but an agent's environment already set up along with a particular version of your code.. that could be really powerful.

> The other big new thing in Sprites is Connectors. Connectors build on work we did to secure our core platform: they let Sprites make authenticated requests to other systems, without giving agents anything useful to exfiltrate. Connectors have fun security properties, but are also much more pleasant to use than manually managing accounts and API keys.

This is also really cool! The other annoying thing with running agents on VPSs right now is auth.. it’s risky and a huge maintenance burden to have keys fanned out as prolifically as your agents. The desire to have fully functional throwaway environments is just fundamentally at odds with the need to sometimes have secrets on them. Issuing ad hoc secrets per env at agent scale just isn’t feasible. This seems like a potentially great solution.

> I could write this post without pissing anybody off, but I don’t know how to do that and still have it be worth reading.

I can appreciate the honesty. And this was a great read. 

> Five of the most dangerous words in startups are “¿Por qué no los dos?”. We do one thing or the other. We don’t limp in on both.

This is vague about what the future of fly’s now-legacy business looks like, and pretty explicit that they’re all in on sprites. I do think people will still need an easy way to deploy all their little vibe coded apps though. I hope they keep fly up and running too. We’ll see.

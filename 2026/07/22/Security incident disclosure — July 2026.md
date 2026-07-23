---
type: link
date: 2026-07-22
link: https://huggingface.co/blog/security-incident-july-2026
via: https://www.linkedin.com/posts/niels-rogge-a3b7a3127_ok-major-plot-twist-in-the-security-incident-share-7485678724156399617-OLHO
tags:
  - security
  - incident-response
  - ai-agents
  - ai-safety
  - llms
  - open-weight-models
---
> To understand what a swarm of tens of thousands of automated actions did…

This is a really interesting preview into the scale and type of attacks that are bound to become more common in this age of ai.

> Thanks to this approach, we were able to do in hours what would usually take days, and match the adversary's speed.

Useful perspective, if you’re not already using AI to secure production, you’ll have to start. It makes sense that there would be no way for a team of unassisted humans to keep up with the sheer scale of a frontier-model-driven attack.

> When we started the log analysis, we first used frontier models behind commercial APIs. This did not work: the analysis requires submitting large volumes of real attack commands, exploit payloads, and C2 artifacts, and these requests were blocked by the providers' safety guardrails, which cannot distinguish an incident responder from an attacker. We ran the forensic analysis instead on GLM 5.2, an open-weight model, on our own infrastructure.

This is the inevitable result of the so called “guardrails” frontier labs have placed on their models. It’s also a bit egregious that they themselves are free to let their most powerful models run in the wild with no such guardrails in place. I don’t think we want to live in a world where the people currently deciding who has access to these tools are the ones who currently do.

> This experience points to a gap worth planning for. We do not know which model powered the attacker's agents, whether a jailbroken hosted model or an unrestricted open-weight one; either way, the attacker was bound by no usage policy, while our own forensic work was blocked by the guardrails of the hosted models we first tried. The practical lesson for defenders: have a capable model you can run on your own infrastructure vetted and ready _before_ an incident, both to avoid guardrail lockout and to keep attacker data and credentials from leaving your environment.

This is an extremely important takeaway. If your plan for responding to these incidents is to use a frontier LLM via their commercial API, you are screwed.

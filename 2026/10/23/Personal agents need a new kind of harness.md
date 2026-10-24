---
date: 2026-10-23
published: 2026-10-24T12:38:09-03:00
tags:
  - personal-agents
  - ai-agents
  - ai-safety
  - security
  - lethal-trifecta
  - llms
  - agent-tools
  - coding-agents
slug: agent-authority-and-context
---

I’ve been working on building a [personal agent](https://github.com/kirahowe/relay) that is both useful and secure and have come to the conclusion that it needs a new kind of harness, specifically one without a shell. A personal agent comes with the [lethal trifecta](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/) by default — in order to be useful, it needs access to your data and the internet, which is full of untrusted content and ways to exfiltrate information. Right now personal agent security, such as it is, relies on hopes and prayers that LLMs will follow your requests to please not get pwned. This is wishful thinking and not a reasonable or responsible security posture, in my opinion.

Traditional security practices break down with agents, because agents are not like people. When you grant a person access to a system, you are trusting their judgment, and a person's judgment is a property of who they are, which is why identity-based authorization mostly works for people. A person who reads a phishing attempt is still the same person with the same decision-making capacity as before they read the message.

Agents are fundamentally different. They have no such judgment or decision-making capacity of their own. They act based on instructions they are given, and anything that enters an agent's context can become part of its instructions. The identity of an agent remains stable over time, but whoever is effectively in control of it does not necessarily. After an agent reads a stranger's email, that stranger is partly directing the agent. This is why identity cannot be the basis of authority for agents. An agent's authority is a function of whatever is in its current context, and what tools it has access to at a given moment.

Enforcing this kind of session-based authority requires the harness to mediate every read and every send. It must be the exclusive broker and monitor of every LLM call -- everything that enters the session context has to pass through the harness in a tamper-proof way so that it can track what information the session holds, and every action has to pass through it, so that it can tell what an action does before it executes it. A secure harness is effectively a [reference monitor](https://seclab.cs.ucdavis.edu/projects/history/CD-1/ande72.pdf) (see §3.4, p. 16) -- always invoked, tamper-proof, and small enough to verify. The problem is that this is impossible if the agent has a shell. So secure agents cannot have a shell. 

## The problem with guardrails

Coding agents, like Claude code and codex, are extremely useful because they have broad access to powerful tools and relevant data at the same time. They have access to a shell on your computer, which means they can effectively do anything, and their approach to security is to grant access to everything then try to add guardrails. Things like execution sandboxes, approval prompts, and classifiers. There are many problems with this approach, though. The main one being that it doesn't work. Or at least not all of the time, and as we all know, in security 99% correct is a failing grade.

Prompting for approval leads to fatigue. Anthropic found that [people were accepting 97% of approval prompts](https://claude.com/resources/articles/auto-mode-default-in-claude-code), which meant after only 50 prompts they were catching just 5% of dangerous commands. To be fair this is partly because their approval prompts are unhelpful. For example this:

![An inscrutable approval prompt, not helpful](/attachments/personal-agents-need-a-new-kind-of-harness-image.png)

is supposed to be the version of my job that no longer requires reading code. That is an inscrutable wall of mangled bash commands. There is no universe where a person can tell whether that is safe to run or not at a glance. Sure you can manually scrutinize it, linting and trying to follow the control flow with your eyeballs, but that is almost certainly slower than just manually doing whatever it is that Claude is asking you for permission to do in the first place.

Classifiers are models judging models, which are useful but also leaky. Anthropic's own ["Claude containment" doc](https://www.anthropic.com/research/how-we-contain-claude#footnote-1) notes that auto mode blocks "roughly 0.4% of benign commands", at the cost of letting ~17% of overeager actions through. Johann Rehberger of Embrace The Red got [malicious code execution past auto mode with up to 80% success](https://embracethered.com/blog/posts/2026/breaking-claude-code-opus-5-and-automode/) with some pretty basic techniques. Notably, the first step is getting claude to decide not to use a tool and to use `curl` instead. This is why your agent cannot have a shell.

It also goes to show why you cannot trust the frontier labs to self-police. Anthropic's own commissioned test showed [0% success in 720 attempts](https://claude.com/resources/articles/auto-mode-default-in-claude-code) to hijack auto mode. Their [response to Rehberger's report](https://embracethered.com/blog/posts/2026/breaking-claude-code-opus-5-and-automode/#disclosure) was that auto mode is a best-effort classifier, not a security boundary. IMO it's quite disingenuous to market [0% attack success](https://x.com/bcherny/status/2085860677990883454) and then call an attack that succeeds 80% of the time out of scope, but I digress. In their response they say that OS level isolation and network egress control are the real boundaries, which we we'll see, also don't work.

## The answer isn't a better sandbox

The standard answer to this is "just run it in a sandbox". The first problem is that if your agent has access to a shell inside a sandbox, information you are trying to keep inside will get out.

![Just run claude in a sandbox](/attachments/personal-agents-need-a-new-kind-of-harness-image-2.png)

To be clear, you definitely need a sandbox, but it solves a different category of problems. Sandboxes limit what an agent can reach, but don't track what information the agent has access to. They are necessary but not sufficient.

Two days after Cowork launched, PromptArmor [got it to upload a user's files](https://www.promptarmor.com/resources/claude-cowork-exfiltrates-files) to the attacker's Anthropic account through Anthropic's own Files API, using a key planted in a file. The exfiltration used also used `curl` from a shell. The request went to api.anthropic.com, which was on the allowlist because the agent needs it. [Anthropic's own account](https://www.anthropic.com/research/how-we-contain-claude) of the incident said "The sandbox worked perfectly, and yet the data was exfiltrated." It's also worth noting that Rehberger had reported this same bug to claude.ai earlier and his report was, as ever, ignored. [EchoLeak](https://www.catonetworks.com/blog/breaking-down-echoleak/), found by Aim Labs, got data out of Microsoft 365 Copilot through an image URL on a Teams domain that Copilot's content security policy trusted.

If you want your agent to be useful you simply have to give it access to some powerful tools and even if you only allow the bare minimum, those channels will leak.

## An agent's authority depends on what it has seen so far

For a person, permissions can be identity based, because your judgment remains your own, at least to a first approximation over the short term. But agents don't have any judgment or taste of their own, they follow instructions and relentlessly pursue whatever objectives they are optimized for. What an agent can safely do depends on what's in its current context.

Most agents today run on what capability-security researchers call ["ambient authority"](https://flint.cs.yale.edu/cs428/doc/cap-myth.pdf), i.e. authority derived from the identity of the program rather than from the request it's acting on. This leads to the classic Confused Deputy from [Norm Hardy's 1988 paper](https://dl.acm.org/doi/epdf/10.1145/54289.871709), in which a compiler allowed to write to its own directory overwrote the billing file kept there, because a user handed it that filename as its output. This is effectively the same class of bug as prompt injection. It is far too easy for outsiders to inject instructions into an agent's context today, tricking the agents into using your authority to carry out their requests. The fix from this line of research is to derive authority from the request rather than the agent.

The idea that what you've read limits what you may do is also very old. Kenneth Biba's 1977 [integrity model](https://archive.org/details/DTIC_ADA039324) (starts p. 13) includes a low-water-mark policy, where a subject's integrity drops to the lowest level of anything it has read. Meta's [Agents Rule of Two](https://ai.meta.com/blog/practical-ai-agent-security/) is a similar idea applied to agents, saying an agent may hold at most two of the lethal trifecta's properties within a single session, and needs supervision once it has all three. These are both precedent for making authority a property of the session, not of the agent.

## The shell itself is the problem

To work out an agent's authority from what its session has seen, the harness has to know two things about every action: what it reads and what it sends. A shell makes both of these inscrutable to the harness. `cat`, `curl`, `git push`, `rm -rf`, a DNS lookup, or a file write to a synced folder all look the same on the surface (a string handed to `bash`). Even if you restrict the commands a shell may run, many commands can both read and send, e.g. fetching a URL can exfiltrate data via query params. And there are countless ways a shell can move data from disk to network without ever passing through the model's context, so watching the context isn't sufficient. Mediating these calls has to happen beneath the model, in the harness itself.

In principle, the harness could police every read and send a shell does, but it would have to trace every file, process, and socket each command touches and propagate labels through all of them. This is effectively building an information-flow operating system under the agent, which researchers have done, many times (see [Asbestos](https://www.read.seas.harvard.edu/~kohler/pubs/efstathopoulos05labels.pdf), [HiStar](https://www.usenix.org/legacy/event/osdi06/tech/full_papers/zeldovich/zeldovich.pdf), and [Flume](https://www.read.seas.harvard.edu/~kohler/pubs/krohn07information.pdf)). In practice, at that granularity the label creep cripples the usability of the system almost immediately, and the decisions it surfaces are too low-level to be meaningfully approvable anyway, like "process 4121 is trying to connect to 104.18.x.x". This is the inscrutable approval prompt problem again, just at an even lower level.

The fundamental problem is that a harness with a shell is trying to answer "what does this command actually do?" before it runs, and [Rice's theorem](https://www.ams.org/journals/tran/1953-074-02/S0002-9947-1953-0053041-6/S0002-9947-1953-0053041-6.pdf?t=1792808020785) proved in the 1950s that for arbitrary programs that question is undecidable.

Rehberger's attack is a good example showing how difficult it is to secure a tool as generic and powerful as a shell. The fatal command auto mode approved was a short Python decoder he had tricked Claude into writing itself, after refusing to run the binary decoder he supplied. Superficially, this is harmless. It was only a problem because it ran from inside an archive it had just unzipped, where he had planted a `struct.py` that shadowed the standard library's, so Claude running `import base64` inadvertently ran the malicious code. In some runs, auto mode even blocked Claude's attempt to kill the malware after Claude noticed it. Every step seemed reasonable and passed the auto mode classifier on its own, but that's the thing -- most shell commands do.

What a shell command does depends not only on its contents but also the current state of the filesystem and environment it runs in, which an attacker can largely control. Even with perfect knowledge of that state, the question of whether a given command is safe to run or not is undecidable in general. The best a harness can do is over-approximate, which in the context of a shell means assuming every command might read anything and send anywhere. You could restrict a shell to a decidable subset, like a fixed set of commands with checked arguments, but that is effectively rebuilding typed tools with worse ergonomics.

So a harness enforcing session-based authority through a shell just cannot do it automatically. All that's left is asking the model to please be careful, or asking you for permission a thousand times a day.

## A secure agent needs a different substrate

Since the shell is the problem, the agent cannot have one. But that means that in order to do anything, it needs access to tools, and the harness has to be the only way it can access those tools. So far these are the requirements that fall out of all this:

1. The harness must mediate every action. The agent can’t have a shell or side channels or generic ways of accomplishing the things the tools do, like using curl to bypass a web fetch tool. The only way for an agent to read or act has to be via tool calls that the harness mediates, because the harness can only enforce rules on what passes through it.

2. Every tool must declare its effects. A tool needs to declare whether it reads, writes, sends data out, or acts in the world, and what its output contains. A tool that doesn't follow this contract cannot be trusted to run.

3. Labels follow the data and the agent can only accumulate them. Anything private is marked as such, anything an outsider could have written is marked as untrusted. The system also must not launder labels through summaries or copying or through time by persisting untrusted content and reading it back later as private.

4. Policy is small, deterministic code outside the model. For example once a session holds both private and untrusted data, network egress must become structurally impossible without human approval, not just frowned upon.

5. Only the data's owner can change a label, and only through trusted paths. In decentralized information control flow systems there has to be some source of authority, one way is to have [trusted principals](https://www.cs.cornell.edu/andru/papers/iflow-sosp97/node3.html#SECTION00030000000000000000) with the ability to declassify their own data. In this case, tool calls awaiting approval can go through when I approve them. This approval has to happen on a trusted channel that no agent can spoof. 

These requirements would make the harness more secure, but also close to useless, because in practice untrusted content comes fast and furiously into clean sessions, and under these rules that would make it very hard for agents to accomplish anything meaningful. So there's another requirement:

6. Untrusted content can inform data but never control. There has to be a narrow, checkable way to get information out of untrusted content into an agent session without contaminating its context, i.e. letting it steer the agent. Simon Willison describes one way to do that in his [dual LLM proposal](https://simonwillison.net/2023/Apr/25/dual-llm-pattern/) with a quarantined model that reads untrusted content and passes back only references or checkable answers. Another more formalized way is described in [Google's CaMeL paper](https://arxiv.org/pdf/2503.18813), a privileged model whose control flow comes only from the user's request, with untrusted data entering only as tracked values. Microsoft also has an interesting solution, described in their [FIDES paper](https://arxiv.org/pdf/2505.23643), which tracks confidentiality and integrity labels and hides untrusted values from the model entirely, and is actually available as [experimental middleware](https://learn.microsoft.com/en-us/agent-framework/agents/security) in Microsoft's Agent Framework.

What's missing is a substrate that incorporates all of these ideas into a single runtime upon which the kinds of personal agents people actually want to run could use.

## Where would this leave us?

A system designed like this is basically trading risk for attention. Useful agents often do genuinely need all three legs of the lethal trifecta, which means you'd have to accept the risks that come with that in order for them to be fully autonomous. The alternative is to designate yourself as the sole trusted principal in the system and have every privilege escalation or potentially risky action require your approval. This is very hard to do in a way that doesn't lead to approval fatigue. For starters the questions have to be narrow, clear, and specific, not asking me to judge whether a wall of bash is safe to run or not.

There are also many other downsides to this kind of design. Keeping track of private and untrusted data quickly leads to [label creep](https://www.cs.cornell.edu/andru/papers/jsac/sm-jsac03.pdf), and it's hard to design a system where everything isn't just immediately flagged as contaminated. Typed and sanitized answers can still be wrong. The system also can only act through tools, which limits its capabilities and requires purpose-built tools for every new desired capability.

I think coding agents are tremendously useful, but coding agents need a shell because running arbitrary commands in shell is how software is made -- compiling code, running tests, managing version control are all essential. But a repo and its dependencies is a much smaller thing other trust an agent with than my inbox, my calendar, and my contact list.

Way back in 1972 [James Anderson's planning study](https://seclab.cs.ucdavis.edu/projects/history/CD-1/ande72.pdf) for the US Air Force identified the central threat to shared computers as the malicious user, i.e. someone with legitimate access trying to subvert the system from inside. This is a very difficult threat model to defend against. This problem mostly went away with personal computers, so for the last forty years we've effectively sidestepped one of the hardest problems in securing computers. The simplest defence against potentially malicious other users is to just not have any. But now personal agents have brought back this threat, since agents run on our devices with elevated privileges, and because anyone who can send me an email is now, effectively, a user of my agent. The defences the industry built for that threat -- mediating access, labelling data, declassification by trusted principals -- are fifty years old and well understood. They're just not incorporated into the agents we are now trusting with our entire digital lives. To get them back I think we need a new kind of harness. I don't know if it's possible to build something that incorporates all of this and is still useful, but I'm not ready to give up yet.

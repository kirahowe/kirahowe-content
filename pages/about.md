---
title: About
---

I'm Kira Howe, a software engineer in Yarmouth, Nova Scotia. I've been writing
software since 2015.

I build full-stack web applications and developer tooling in Clojure, end to end
— system architecture, durable background jobs, server-rendered hypermedia UIs,
and the pipelines that deploy them. I like software that's simple, durable, and a
pleasure to operate. Clojure's data science ecosystem is a thread I keep pulling
on; I've written tutorials and tools for it and still contribute where I can,
though most of my recent energy goes into shipping deployed systems and the tools
that make building them easier.

I studied chemistry before I wrote software for a living, which is probably why my
instinct when I hit something I don't know how to do is to go find out who has
already done it, rather than smash my head against it until something works.

I currently work at [Seeq](https://www.seeq.com). If I could afford to work on
open source full time I would; for now it gets whatever free time I can give it.

## What I write about here

Mostly Clojure, data infrastructure, and lately what it actually takes to make
LLMs and coding agents do useful work. Other things turn up too — books, faith,
and whether this industry can be a force for good instead of evil. Everything is
organized by date and [tag](/tags), and there's [a feed](/feed.xml). Every tag has
one of its own.

## What I'm building

**Developer tools**

- **[clef](https://github.com/kirahowe/clef)** — An opinionated, Rails-inspired
  full-stack web framework for Clojure. One command (`clef new myapp`) scaffolds a
  complete, deployable app: HTTP routing with Reitit, component lifecycle with
  Integrant, layered per-environment EDN configuration, structured logging, and
  Docker + Fly.io + GitHub Actions CI/CD wired up out of the box. Distributed as a
  single self-contained Babashka script via Homebrew. Pre-alpha — public for
  development transparency, not usable yet.
- **[claimgraph](https://github.com/kirahowe/claimgraph)** — A bi-temporal,
  epistemically-typed knowledge graph for AI coding-agent memory, meant to replace
  the `CLAUDE.md`/`AGENTS.md` markdown pile with something owned, portable, and
  inspectable. Nothing is ever hard-deleted: contradictions close a validity
  interval, so the graph can answer both what we currently believe about something
  and what we believed in March, and why it changed.
- **[compositor](https://github.com/kirahowe/compositor)** — Manage many
  concurrent coding-agent sessions against one repo and composite all their
  in-flight work into a single live dev server, so you review by using the app
  rather than reading diffs. Jujutsu is the storage engine and stays invisible.

**Libraries**

- **[secrets](https://github.com/kirahowe/secrets)** — Manage application secrets
  as one version-controlled, age-encrypted EDN file instead of a sprawl of
  environment variables. One private key decrypts it; the structure, defaults, and
  ciphertext live in git alongside a value-free manifest that makes each change
  reviewable. Runs identically under JVM Clojure and babashka.
- **[clj-llm](https://github.com/kirahowe/clj-llm)** — A small, functional Clojure
  library for calling language models from any provider, including local ones,
  with evals built in from the ground up. Stateless and context-agnostic: every
  function takes a config map and returns data. The premise is that you can't
  build well with LLMs unless measuring what they do is as easy as calling them.

**Apps**

- **[reader](https://github.com/kirahowe/reader)** · live at
  [themiscellany.app](https://themiscellany.app) — A distraction-free reading
  queue that unifies articles, research papers, and newsletters into one place.
  Save a URL, paste an arXiv id or DOI, or forward a newsletter to a private
  inbound-email alias. Everything is auto-tagged and surfaced based on your own
  reading patterns.
- **[hosted-clay](https://github.com/kirahowe/hosted-clay)** — A hosted platform
  for [Clay](https://scicloj.github.io/clay/) notebooks, one of Scicloj's live
  programming libraries. Each notebook runs in its own isolated Fly.io Sprite with
  a browser-based IDE (code-server + Calva) beside live-rendered output, while a
  Clojure control plane handles authentication, a warm-VM pool, notebook
  lifecycle, and a WebSocket-relaying reverse proxy.
- **[finances](https://github.com/kirahowe/finances)** — A personal finance app
  that aggregates transactions across institutions via Plaid and Lunchflow, stored
  in an embedded Datalevin database. Uses Datastar for a server-authoritative
  hypermedia architecture, with small TypeScript islands for latency-sensitive
  interactions like keyboard grid navigation and undoable edits.

**On the web**

- **[tools](https://github.com/kirahowe/tools)** · live at
  [tools.kirahowe.com](https://tools.kirahowe.com) — A monorepo of small,
  self-contained web tools deployed together as a single Cloudflare Worker, each
  at its own path.
- **[this website](https://github.com/kirahowe/website)** — A folder of markdown
  files in an Obsidian vault, rendered by a few thousand lines of Clojure running
  under [babashka](https://babashka.org) with no external dependencies at all. I
  wanted authoring to be as easy as adding to my personal wiki, with the tooling
  handling frontmatter, `[[wikilinks]]`, pasted images, and organizing everything.
  The code and the content live in separate repositories.

A pattern you'll notice across most of these: Integrant-managed lifecycles,
layered EDN config instead of env-var sprawl, server-rendered hypermedia over
heavy SPAs, and real production concerns like migrations, health checks, and
CI/CD built in from the start.

## Selected talks

- **Clojure for Data Deep Dive** — London Clojurians, 2024
- **Clojure for Data Science in the Real World** — Clojure/conj, 2023
- **Using Clojure for More Than Software Development** — re:Clojure, 2022
- **Visualizing Data with Hanami** — re:Clojure, 2021

## Things I'm often brought in to help with

I'm not actively looking, but I take on the occasional consulting engagement when
it lines up with what I care about. Usually that means one of these:

- **Making sense of a large or tangled codebase**, and reorganizing it so people
  can work in it again.
- **Turning competing stakeholder requests into a plan**, and then into an actual
  shippable thing.
- **Getting answers out of piles of data.**
- **Levelling up early-career developers**, quickly.
- **Building a culture of open, community-driven development**, and reshaping
  development processes to support it.

I thrive around open-source innovation, community engagement, and hard problems
that deserve elegant, sustainable solutions.

## Elsewhere

You can find me on [GitHub](https://github.com/kirahowe). I love hearing from
people working on interesting problems.

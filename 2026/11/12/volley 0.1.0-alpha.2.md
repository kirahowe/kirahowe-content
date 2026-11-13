---
type: release
date: 2026-11-12
published: 2026-11-12T22:41:22-04:00
link: https://github.com/kirahowe/volley/releases/tag/v0.1.0-alpha.2
tags:
  - volley
---

[volley](https://github.com/kirahowe/volley) 0.1.0-alpha.2 is out. volley is my test runner for `clojure.test` on babashka and the JVM. It runs test namespaces in parallel worker processes and reads Kaocha's `tests.edn` and flags, so a project that runs Kaocha today can switch by changing one command.

The main change this release is an improvement for small JVM suites. A worker JVM has to start and load the project again, which for a suite of a few seconds or less took longer than it was worth, so once a project's recent runs have taken 10 seconds or less volley runs the tests in its own JVM. On a 70-test project of mine that came to 5.65s against Kaocha's 5.71s. With worker JVMs (the old implementation) it was 7.6s.

Tests also run in random order now, as under Kaocha's randomize plugin. Each namespace's tests are shuffled from a seed, and a failed run prints the seed so you can run that order again, and `--no-randomize` turns it off. If any of your tests depend on running in a particular order, this is a way to find out.

Watch mode also now follows changes to `tests.edn`, `deps.edn` and `bb.edn`, and failure reports show the output around each failure. The [release notes](https://github.com/kirahowe/volley/releases/tag/v0.1.0-alpha.2) have more details about the rest of the changes and bug fixes. It's on Clojars as `com.kirahowe/volley {:mvn/version "0.1.0-alpha.2"}`. It is still an alpha, and is for `clojure.test` only, with no ClojureScript and no coverage.

---
type: release
date: 2026-10-19
published: 2026-10-19T14:07:11-03:00
link: https://github.com/kirahowe/volley/releases/tag/v0.1.0-alpha.1
tags:
  - release
  - volley
  - clojure
  - testing
  - developer-tools
  - open-source
  - oss
  - babashka
  - performance
slug: introducing-volley
---

I made a test runner for Clojure! Clojure is still my language of choice and I've been writing most of my personal projects with it (or babashka) lately, and especially in the babashka projects have been wishing for a better test running experience. I use vitest at work, so it inspired a lot of the functionality of volley.

It's a runner for `clojure.test` tests and currently works on babashka and JVM Clojure. It runs test namespaces in parallel worker processes, shows each namespace as it finishes, and has a watch mode that reruns only the tests that change. It's compatible with kaocha, since that's what I was mostly using before, so switching is just changing one command. With AI generating more and more of my code these days, I find I'm running more and more tests, and was wanting a runner that could parallelize large test suites where that results in noticeable speedup.

This is what volley looks like running its own test suite:

![volley running its own test suite](https://github.com/kirahowe/volley/raw/main/doc/volley.gif)

## Try it out

`volley` is on Clojars as `com.kirahowe/volley`. For bb projects, add it to `bb.edn` with a task:

```clojure
{:paths ["src" "test"]
 :deps {com.kirahowe/volley {:mvn/version "0.1.0-alpha.1"}}
 :tasks {test {:doc "Run the tests"
               :requires ([volley.main])
               :task (apply volley.main/-main *command-line-args*)}}}
```

On JVM Clojure projects that already use kaocha, swap `lambdaisland/kaocha` for `com.kirahowe/volley` in `:extra-deps`, and change `kaocha.runner` to `volley.main` in `:main-opts`, and leave the rest alone. A `bin/kaocha` binstub that runs `clojure -M:test "$@"` should keep working.

## How it works

The parent process plans the run and hands namespaces to workers, which stay alive across runs. By default, it runs one worker per CPU, capped at 8 for bb and 4 on the JVM. `--workers N` overrides these, and `--isolate` gives every namespace a fresh worker. Workers run on whichever runtime the parent uses, or you can specify directly with `--runtime bb|jvm`. Timings are saved in `.volley/`, so later runs start the slowest namespaces first.

In a terminal, volley re-draws one line per running namespace. When `stdout` is piped, it prints plain lines instead. Failures show expected and actual values, a structural diff for `=` assertions, captured output, and the call stack without the bb interpreter's frames. A failed `defspec` property test shows its seed and shrunk input. The run ends with the slowest tests and prints a command that reruns just the failures. 

`--watch` polls test and source paths, works out from `ns` forms which test namespaces depend on the file you changed, and reruns only those. Keys let you rerun everything, rerun failures, or filter by namespace or test name. 

Most of kaocha's options and config are supported by default. Suite ids, `--focus` and `--skip` (and their `-meta` forms), `--fail-fast`, the reader tags in `tests.edn`, `:kaocha/bindings`, pending tests, the hooks plugin, JUnit XML, custom reporters, the `--print-*` flags, and kaocha's exit codes should all work as expected.

## Performance

So far I've only tested this on my busy 16-core M4 max MacBook Pro, but I have found huge improvements on big test suites. In one bb project with 507 tests runs went from ~150s to ~30s with 8 workers, on another JVM Clojure project I saw improvements from ~215s to 40s. So far small JVM Clojure test suites don't see much improvement in my experience. This is on my radar to improve, but for now if your tests run in under about 10s, you might not see any improvement with volley because the JVM startup overhead dominates the timing.

## Known limitations

- Only handles `clojure.test` for now. There's no ClojureScript and no coverage.
- Kaocha plugins such as the notifier, gc-profiling and cloverage are accepted but do nothing. volley prints one warning pointing this out.
- `--randomize` and `--seed` are accepted with a warning. This release doesn't randomize test order.
- volley departs from Kaocha on purpose in a few places: load errors, `System/exit` inside a test, fail-fast inside a test, load order, and the `--print-*` maps. There are more details in the ["Deliberate divergences from Kaocha" section here](https://github.com/kirahowe/volley/blob/v0.1.0-alpha.1/doc/design.md#deliberate-divergences-from-kaocha).

This is the very first alpha release so there are still many rough edges, but I'm using it all day every day on my own projects so figured it's ready "enough" to put out there. My goal is to keep improving it to fix all the paper cuts. If you try it and run into any, I would love to know about it. Please feel free to create issues in the repo or message me in any of the Clojure community places I lurk. Thanks for reading!

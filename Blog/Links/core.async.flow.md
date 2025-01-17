---
link: https://github.com/clojure/core.async/commit/03b97e0b3e0ec329629bcbf76106658dce4a5d61
via: https://bsky.app/profile/cgrand.net/post/3lfskho3u6s2l
tags:
  - clojure
  - core-async
  - rich-hickey
date: 2025-01-16
---
Rich Hickey just pushed a new namespace to the `core.async` library that looks really interesting. The [accompanying rationale](https://github.com/clojure/core.async/commit/8e18e17c8a6ad579bc40701b335c46f1fa29f608) explains what it's all about in simpler terms than the code, but it feels like a big step forward in making core.async more intuitive to use. Channels are a super useful abstraction, but as the rationale explains, they are still a relatively low-level construct that require expertise and good architectural decisions to use well. This new namespace provides some more abstractions on top of channels that handle, among other things, "all channel I/O, thread lifecycle and coordination with the flow graph". This seems very powerful.

These are very high-level abstractions over an entire system, but I often wonder if this is just the inevitable direction in which software is headed. As we come to understand software systems better and better, and as the tools for generating implementations of solutions to known problems become better and better, it seems like this shift toward ever higher-level abstractions is the natural outcome.

It reminds me a bit of what Hyperfiddle is doing with [electric Clojure](https://github.com/hyperfiddle/electric), abstracting over the entire network, not just the "front" or "back" end of a web app. It's a totally different domain, but similar in that it feels like an impossibly high level to develop at, yet it appears to work very well. I'm excited to out both of these.

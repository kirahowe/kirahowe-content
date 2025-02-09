---
link: https://www.counting-stuff.com/storage-is-cheap-storing-isnt-2/
via: https://www.counting-stuff.com
date: 2025-01-21
tags:
  - data-science
  - software-engineering
  - data-engineering
  - logging
  - storage
  - cost
---
I love [Randy Au](https://bsky.app/profile/randyau.com)'s newsletter in general, but this one makes a particularly useful point: Not thinking about why you're doing something ahead of time is expensive and wasteful.

Randy's discussion of how this issue manifests in software teams in particular is completely on point, in my experience. But it applies to all areas of life. Software engineers get asked all the time to just "log everything", with the assumption being that since we have "big data" tools now, we'll be able to make use of it all later. The reality is that extracting value from heaps of unorganized, unstructured raw data is actually very difficult and potentially expensive, and the time to think about what questions you want to answer is _before_ you start collecting data in the first place. It's also mostly true that once something is being collected or logged, it will go on forever. Another consequence of not thinking through your reporting and monitoring infrastructure ahead of time is that nobody really knows who is depending on what, and so things get left in place "just in case" it breaks something downstream. Of course this is madness, but it's how many organizations operate in reality.

It's true that storage is cheap now, but that doesn't mean accessing said storage is cheap, let alone doing something useful with the mess that's in there. Keeping terabytes of logs in S3 is like having a free warehouse in Labrador for all the tchotchkes you know you don't need but can't bring yourself to throw out. 

A lot of this data hoarding stems from organizations wanting to be "data-driven", without ever explaining what that means for their context or why it matters. Collecting data is easy and cheap but does not inherently add value, and the difficulty of extracting value from raw data is a function of its volume (among other things). It's worth spending at least a little bit of time up front thinking about what 
---
type: release
date: 2026-10-22
published: 2026-10-22T23:04:19-03:00
link: https://github.com/kirahowe/editmd/releases/tag/v0.1.0
tags:
  - editmd
  - release
  - markdown
  - macos
  - open-source
  - developer-tools
  - coding-agents
---

I made a markdown editor for MacOS! With Claude writing most of my code now I spend a lot more time than I used to editing docs. I prefer working in markdown, and wanted a really simple wysiwyg editor that works like a word processor but saves files as markdown.

I often work with agents on docs now, so I needed an editor that would not break my workflow if the file was edited while open. I will often be writing and have an agent go search for references, for example, or add links and references, or fill in quotes that I only vaguely remember, or add code examples to a spec, or any number of other things, so I wanted something that would let me keep working seamlessly while the file I had open was also being editing by agents at the same time.

Most editors either clobber one side or throw up a "the file changed on disk" dialog. editmd uses [Y.js](https://github.com/yjs/yjs) to merge your agents edits in real time, like you're collaborating on a google doc. If an agent edits the file while it's open, its changes just appear, your unsaved edits stay put, and Cmd-Z only undoes your own changes, never the agent's.

![Screenshot of editmd](https://kirahowe.github.io/editmd/images/notes-light.png)

## Try it out

It needs macOS 14 or later, and runs on both Apple silicon and Intel:

```sh
brew install --cask kirahowe/tap/editmd
open -a editmd notes.md
```

It's not signed with an Apple Developer ID (yet?), so the cask clears the quarantine flag for you. If you grab the zip from the release page directly, run `xattr -dr com.apple.quarantine editmd.app` before opening it. There's also a little website at [kirahowe.github.io/editmd](https://kirahowe.github.io/editmd/) with some elaboration of the features.

## How it works

It's a native AppKit document app with a WebKit view running a [Milkdown](https://milkdown.dev) editor (ProseMirror + remark), all bundled into the app so nothing loads from the network. The document in each window is a [Y.js](https://yjs.dev) CRDT. When the file changes on disk, editmd diffs the new text against the version it last saw, replays the difference as edits block by block, and lets Y.js merge them with whatever you've typed since. Edits to different paragraphs, list items or table rows combine cleanly.

Documents autosave one second after you stop typing (or every five seconds if you don't stop). A file you open and save without editing keeps its exact bytes. An edited one keeps its encoding (UTF-8, UTF-16 or Windows-1252), its line endings, its YAML or TOML front matter, reference-style links and tables. GitHub flavoured markdown works so tables, task lists, strikethrough, footnotes, and GitHub's heading anchors all render properly, so a table of contents written for GitHub works as expected. It also supports mermaid diagrams so fenced `mermaid` blocks render as diagrams with a live preview while you edit them. Clicking on a diagram shows the raw markdown, or pressing `Cmd-/` flips the entire doc to the raw markdown.

It's also safe to open external (i.e. untrusted) documents. `Cmd+click` on a link never launches anything -- text files open in editmd, and any other file, folder, or app is just shown in Finder. Remote images are blocked until you allow them, like in Mail, so a document can't leak any information via an image fetch.

## On using AI to ship software

I have found working with AI to build software increasingly fun. Obviously this was built with heavy assistance from Claude (I primarily use Opus 5.5 right now), but it is still very tailored to my taste and needs. I am also coming to appreciate how much better at coding Claude is than I ever was. It's kind of sad to admit defeat, but it's really just true that it catches things I don't now. Once I thought this was ready for release, I asked Claude to QA rigorously before putting up a release, and it found a bunch of stuff I definitely would have shipped:

- If WebKit's content process crashed, the window reloaded stale text, and the next autosave silently overwrote changes that had already been saved
- Cmd-clicking a link to an `.app` in a cloned repo would launch it, with no Gatekeeper prompt since cloned files aren't quarantined
- Opening a document fetched its remote images, i.e. tracking pixels
- Windows-1252 files got silently converted to UTF-8, and UTF-16 files opened as garbage
- Running 485 generated markdown cases through the serializer turned up real content loss: badges (`[![build](…)](…)`) lost their links, tables with ragged rows shifted their columns, and unused link definitions just disappeared

Normally these are the kinds of issues I would have never noticed until they screwed over a real user, but we don't have to accept these kinds of problems in our software anymore! I just told Claude to spin up a bunch of parallel agents to fix all these problems and it fixed seven different issues, each in its own git worktree, each one going through implementation → independent code review + adversarial QA → fix, until two reviewer agents signed off. It ran 30 sub agents and took about two and a half hours. I had a main agent doing integration, which still caught yet another real bug -- two of these workflows had each taken over the markdown serializer, and one of them had broken reference links. Every fix came with regression tests, and the test suite grew from 65 web tests to 762.

## Known limitations

There are still some known issues due to the fundamental complexities of merging concurrent edits to a single document:

- If you and another program edit the *same* paragraph at the same moment, the paragraph keeps both changes, which may need manual tidying.
- A save checks the file one last time before writing, but an outside write that lands in the few microseconds between that check and the write still gets overwritten. Nothing can realistically close that gap without the other program's cooperation.
- Links with custom schemes (`obsidian://`, `file://`) don't do anything on Cmd-click in the rendered view yet.
- Very large files (hundreds of KB) are fine to type in, but the first autosave after opening still serializes the whole document.

This is the very first release, so there are definitely still rough edges, but I'm already using this every day now. If you try it and run into anything, please open an issue on [the repo](https://github.com/kirahowe/editmd). Thanks for reading!

# The Inner World

A browser graphic-novel game built from Chapters One and Two of *The Inner World*, a novel in progress by Richard Garza. The chapter text is embedded in the game file.

You play as Glitch, a journalist in a sealed underground city who feels everything a room hands him and counts everything in it, at the same time, and can't stop doing either.

**Play it:** open `index.html` in any modern browser. No build step, no server, no dependencies beyond web fonts.

## What's in the repo

| Path | What it is |
|---|---|
| `index.html` | The whole game: HTML, CSS, script data, canvas scenes, and engine in one file |
| `docs/DESIGN.md` | Design notes: palette, type, scenes, mechanics, and why |
| `docs/BRANCHES.md` | Every choice point, where each branch goes, and which lines were added for the game |
| `docs/EDITING.md` | How to add beats, choices, countable figures, scenes, and chapters |
| `.claude/launch.json` | Local static-server config for previewing in Claude Code |

## How it plays

- **Read.** Narration and dialogue arrive in cream caption boxes over a drawn, animated scene. Click, tap, or press Space to advance. Clicking while text is still typing finishes the paragraph.
- **Count.** Every figure in the prose is underlined in slab blue. Tap it and it goes on Glitch's tally in the corner. The wrist-slate flickers each time, because upstairs reads as he breathes.
- **Choose.** Nine forks. A blue square marks the arithmetic choice, an amber dot marks the feeling choice. Most branches rejoin the book a beat later. The feeling meter never shows a number; it warms the edges of the screen instead.
- **Get pinged.** The editor's messages buzz onto the slate at the moments they land in the text. Mara's message arrives in her own voice.
- **Write it down.** At the end, the sheet of paper is filled in by hand with the three lines from the book, then a line describing the shape of your day built from your choices, then the figures you counted.

Progress saves in the browser. Number keys 1 to 3 pick choices. Reduced-motion settings are honored.

## Status

Chapters One and Two are playable. Chapter Three is not yet written.

## Rights

The manuscript and all text in this repository are © Richard Garza, all rights reserved. The game code exists to present that text and carries no separate license.

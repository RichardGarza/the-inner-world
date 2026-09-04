# Design notes

## The read

The city is sealed and underground. Nobody down here has seen daylight. So the page commits to a single dark world instead of offering light and dark themes: near-black ground with a cold blue bias, emergency amber as the only accent, and the recorder's dull slab blue reserved for anything the city reads or records.

## Palette

| Token | Hex | Used for |
|---|---|---|
| `--ground` | `#0a0c0f` | Page and stage ground |
| `--concrete` / `--concrete2` | `#1a1e24` / `#252a31` | Riveted plates, table, walls |
| `--amber` / `--amber2` | `#e39a35` / `#f3c26b` | Strip lighting, the feeling meter, chapter kickers, buttons |
| `--work` | `#dfe5ea` | Work-white light, plate lettering |
| `--slab` / `--slab2` | `#4f93bd` / `#8fc3e6` | The recorder, the wrist-slate, countable figures, the tally |
| `--paper` / `--paper2` | `#e8e2d3` / `#d6cfbd` | Caption boxes and choice buttons |
| `--ink` | `#15171a` | Caption text |

Feeling is not a number in this story, so it is never rendered as one. It's an amber vignette whose opacity is the `--feel` custom property, set from the feeling meter.

## Type

| Role | Face | Why |
|---|---|---|
| Plates and titles | Big Shoulders Display | Reads like a stamped municipal sign, which is what every heading in this city is |
| Narration | Spectral | A book face for a book, at 18px and 64 characters wide |
| Slate, tally, counts | IBM Plex Mono | Everything the city reads is monospaced and tabular |
| The sheet of paper | Caveat | The one thing in the world written by hand |

Fonts load from Google Fonts with real fallback stacks.

## Scenes

Every scene is drawn procedurally on a `<canvas>` each frame. There are no image files. Silhouettes are a circle and a rounded rect. A film-grain pattern is composited over every frame.

| Scene | What moves |
|---|---|
| `elevator` | The light bar flickers; 31 silhouettes in three rows; the occupancy plate |
| `bay` | Six ceiling lights switch between amber and cold white; four rows of the line sway; the recorder glows blue on a crate |
| `corridor` | Amber floor seams converge on a vanishing point; the pump glow pulses on the left wall |
| `water` | A drop falls every 2.4 seconds, rings spread, and the reflected figure breaks into slices and reassembles |
| `block` | Ceiling light warms from amber to white over 20 real seconds; Mara appears in the doorway when her flag is set |
| `concourse` | 41 panels across four levels cycle 11 warm messages; panel 6 stutters to a grey grid and panel 19 turns to dark water when their flags are set; the crowd walks |
| `newsroom` | Corrin's screen glows blue with the freeze-frame; a record light blinks |
| `archive` | Shelves of flats; an open flat with a black bar over the byline; the whole frame trembles with the presses |
| `paper` | A lamp cone over a table; the handwritten sheet is a DOM element on top |

## Mechanics

**Counting.** `n('thirty-one', 31)` in the script wraps a figure in a tappable `<b class="n">`. Tapping increments the tally, records the value, pops a `+31`, and flickers the slate. Each figure can only be counted once per beat. The first countable figure shows a one-time hint.

**Feeling and counting meters.** Beats and choices carry `c` and `f` increments. They accumulate independently and never cancel. The end card shows the count as digits and the feeling as a bar.

**Choices.** A beat with a `choice` array shows buttons after typing finishes. Each choice can carry `c`, `f`, a `go` target, and a `set` flag. Branch beats use `next` to rejoin the main line.

**Flags.** Story flags (`hard`, `corridors`, `recoff`, `waited`, and so on) are read at the end to write the "shape of the day" line on the paper. Scene flags (`mara`, `p6`, `p19`) change what the canvas draws.

**Pings.** A beat's `ping` array sends editor messages to the slate, staggered 1.6 seconds apart. `mara` sends one in her voice.

**Save.** State is written to `localStorage` after every beat. The title screen offers Continue when a save exists. "Read again" clears it.

## What is deliberately not here

- No light theme. The world has one look.
- No images. Everything is drawn so the file stays self-contained and the look stays consistent.
- No score. The tally is Glitch's habit, not a target.

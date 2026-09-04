# Editing the game

Everything lives in `index.html`. The story is a JavaScript array called `beats`, near the top of the `<script>` block. Edit it, save, reload.

## A beat

```js
{ t: `Narration or dialogue as HTML.` }
```

Optional fields:

| Field | Meaning |
|---|---|
| `id` | A label other beats can jump to |
| `who` | Speaker name shown above the text (`'Lena'`, `'Mara'`, `'Corrin'`, `'Glitch'`) |
| `scene` | Switch the canvas to this scene when the beat starts |
| `where` | Text for the location plate in the top-left |
| `flag` | Set a scene flag that changes what the canvas draws (`'mara'`, `'p6'`, `'p19'`, `'p6off'`, `'maragone'`) |
| `c` / `f` | Add to the count or feeling meter when this beat starts |
| `ping` | Array of editor messages sent to the wrist-slate, staggered |
| `mara` | One message from Mara sent to the slate |
| `fx: 'flicker'` | Flash the screen twice |
| `inner` | Dark caption box for Glitch's own thoughts |
| `sheet` | Show the handwritten sheet of paper over the scene |
| `next` | After this beat, jump to the beat with this `id` instead of the next one |
| `choice` | An array of choices; see below |
| `card` | Show a chapter card instead of text: `{k:'Chapter Three', t:'Title', s:'First line.'}` |
| `end` | The last beat; advancing shows the end card |

## A choice

```js
choice: [
  { l: 'Ask the hard one.', c: 2, go: 'hard1', set: 'hard' },
  { l: 'Leave it in your throat.', f: 1, go: 'hard2' }
]
```

`l` is the button label. `c` or `f` decides the marker and the meter. `go` names the beat `id` to jump to. `set` records a story flag. Branch beats usually end with `next:` pointing back to the main line.

## A countable figure

Wrap it with the `n()` helper inside the template string:

```js
t: `There were ${n('thirty-one', 31)} of us in it that morning.`
```

The first argument is the text as it appears, the second is the value that goes on the tally.

## Inline styles

- `<span class="plateq">IF THEY KNEW, THEY WOULD CARE</span>` renders as a stamped plate.
- `<span class="slabq">STOP COUNTING.</span>` renders as slate text.
- `<em>` is italic and is used for the inner voice.

## A new scene

Add a function to the `scenes` object. It receives `(t, f)` where `t` is seconds since the scene started and `f` is the scene-flag object. Draw with the canvas context `ctx`; `W` and `H` are the viewport size. Helpers: `ground(top, bottom)`, `glow(x, y, radius, color, alpha)`, `fig(x, y, height, alpha)` for a silhouette, `platetext(...)` for a riveted plate.

## The sheet at the end

`renderSheet()` builds the handwritten page from story flags. Add a line there for any new flag you introduce.

## A new chapter

1. Add a `card` beat with the chapter's kicker, title, and first line.
2. Add its beats after it.
3. Give the last beat `end: true` and remove `end` from the previous chapter's last beat.
4. Update the end card text in the HTML (`End of Chapter Two`, `Chapter Three is not yet written`).

## Previewing

Any browser can open `index.html` directly. In Claude Code, `.claude/launch.json` starts a static server on port 8765.

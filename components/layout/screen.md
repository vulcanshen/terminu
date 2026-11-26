# screen (the whole screen)

**Language**: English · [繁體中文](screen-zh_TW.md)

The skeleton of the whole screen. A panel's frame is in [`panel`](panel.md), the frame floating over it in
[`popup`](popup.md).

## screen.1 From top to bottom

1. **The top row**: in a multi-screen app, the screen chip row, with a full-width separator below it; a single-screen app
   may have a statusbar row (whether to, the app may decide for itself).
2. **The panel area**: the remaining height. Each screen numbers its own panels from `[1]`; `1`–`9` jump only to the
   panels of the current screen (Rules K1).
3. **The bottom row**: the footer.

## screen.2 Footer

One row, written like a hint (Rules M5); keys Blue, colon and description Overlay0 ([`color`](../color.md)). When too
narrow, whole pairs are dropped from the end (the hint in [`popup`](popup.md)). The content depends on the situation:

| Situation | Footer |
|---|---|
| Normal | `Space:menu ?:help !:log Tab\|1–N:panels q:quit` |
| A screen with only one panel | `Space:menu ?:help !:log q:quit` |
| In a mode (Rules K11) | `Space:menu ?:help`, the mode's own keys, and last `Esc:<verb for leaving>`; in an app's own mode, which keys stand between those is the app's call, a core key such as `q:quit` included (Rules K11); where the user has put one of its actions on `Space`, no `Space:menu`, and that action written `Space:<action>` first, where `Space:menu` was (half of a pair under one verb, the pair as Rules M5 writes it: `j|Space:move`; Rules K11). E.g. `Space:menu ?:help Enter:drop Esc:cancel` |
| Typing in a panel filter (input state) | `Enter\|Tab:list Esc:clear` |
| Typing in a panel filter, no results | `Tab:list Esc:clear` (`Enter` does nothing, as in the hint of [`input/finder`](../input/finder.md)) |
| Focus on a PTY in a panel | the exit key, plus the keys the app keeps (Rules K10); in an interactive terminal, then `Alt-v:select` and `PgUp:history` (dialog/terminal). E.g. `Alt-Esc:leave Alt-z:zoom Alt-v:select PgUp:history` |
| A popup is open | as for the screen underneath, dimmed with the whole screen (Rules F8); the popup's own keys are in its bottom-border hint |

**The reminder on `!`**: when the App Log ([`dialog/note`](../dialog/note.md)) holds errors not seen yet, `!:log`
becomes `!:2 errors` (the description in Red); with only warnings not seen yet, `!:1 warning` (Peach); once the App Log
has been opened, it is `!:log` again.

While a terminal popup is open, the footer is not drawn: the terminal covers the bottom row, and the bits left showing at
its two ends are blank, with none of the footer's words peeking out ([`dialog/terminal`](../dialog/terminal.md)).

**Why**: the footer is the entry point of Rules M1, so what it shows must be keys that can be pressed now. While
typing `Space` `?` `q` are characters, and in a PTY every key goes to the subprocess —
writing the usual footer there would teach the user to press the wrong keys. With a popup open the footer keeps its
words and is only dimmed: dimmed means "you are not here now" (Principle P6, the same thing as Rules F8); as popups open
and close, the bottom row only darkens and brightens instead of changing its words all the time; `?` is still on the
footer, and `?` on a popup opens that popup's key reference anyway (Rules M1).

## screen.3 Screen chip row

The top row of a multi-screen app: one capsule per screen, drawn as the capsule chain in [`panel`](panel.md), the chain's
colour being Blue (the selected screen filled with Blue, its text Base bold; the unselected ones filled with Mantle, their
text Blue, not bold). When it does not fit, it shrinks by the capsule chain's rules: first down to `[M] [F] [S]`, then the
unselected ones are folded away.

The statusbar's content goes on its right (see below). Below the chip row runs a full-width heavy line `━` in Overlay0; during
long work (a transfer, a download) it fills with Green from the left as a progress bar, and the status text beside it is
Green too. While a terminal popup is open, the chip row and this separator both stay
([`dialog/terminal`](../dialog/terminal.md)): the progress stays in sight from inside a shell.

**A single-screen app has no chip row**: the progress of long work is the app's content, written in the work's own
row, Green while it runs (e.g. the row in filu's `[3] Tasks` reads `3/10`, and the running glyph is Green). Work
running on the place a panel's location row names may be written in that row instead (e.g. a push of the repository
the row names; panel.10 in [`panel`](panel.md)). While a terminal popup is open, that row is covered and the progress
is out of sight; that is fine, and no extra row is opened for it.

## screen.4 Statusbar

Whether there is one, the app may decide for itself. A single-screen app puts it on the top row; a multi-screen app uses the right of
the chip row rather than a row of its own. It is not a surface; focus never rests on it.

- Written like a label (Rules M5): hotkeys, if any, are marked (e.g. kbu's `[C]ontext: prod  [N]amespace: default`).
- A group is written `label: value`, one space after the colon; two cells between groups, with no separator symbol
  ("Diagrams and spacing" in the [components](../README.md): the two-cell rule does not apply here).
- Ordinary text Overlay0; the "where you are now" values Lavender (user footprint); work in progress Green; the counts of
  errors and warnings Red and Peach.
- Fixed width (Rules L2): the last dynamic field is not padded, while the fields before it keep their fixed widths; when
  it does not fit it is truncated, never wrapped (L3).

## screen.5 Narrow widths

When not all panels fit, only the focused panel is drawn, at full width; `Tab` changes panels as usual, showing one at a
time. The threshold, the app may decide for itself from the minimum widths of its panels, but it may not be above 60 (Rules L1: 60
columns must work properly, every panel side by side). Narrow widths happen only at or above the app's minimum size; below it, see "Smaller than
the minimum size" below.

## screen.6 Zoom

Enlarging one panel is the app's own feature: whether there is one, and its key, the app may decide for itself (e.g. filu's `z`).
The spec gives the default: when zoomed, only the focused panel is drawn, filling the panel area, as with narrow widths;
`Tab` and the digit keys change panels as usual, the panel changed to is zoomed too, and only pressing the zoom key again
restores the layout. How a panel is enlarged, the app may decide for itself (e.g. filu sets the tabs of one panel side by side);
without a way of its own, the default holds.

**Why**: what each app wants to see enlarged differs, so the spec keeps only a default everyone understands; with the
default the same as narrow widths, what the user learns on a narrow screen works when zoomed too.

## screen.7 Smaller than the minimum size

When the screen is smaller than the app's minimum size (Rules L1: 60×32 by default; the app may lower it, but not above
60×32), the whole screen draws just three rows, centred both ways:

```
                kbu
needs a terminal of at least 60×20
   Press [Ctrl-C] twice to quit
```

- **The name**: the app's command name, Blue bold (as the splash's name, Rules S5).
- **The hint**: on the row below the name, `needs a terminal of at least <width>×<height>`, giving the app's minimum
  size; Overlay0.
- **How to quit**: on the row below the hint, `Press [Ctrl-C] twice to quit`, Overlay0; written as an empty state's
  hint, the key in brackets (screen.8, Rules M5).
- **When it does not fit**: the hint goes first, then the row on how to quit, and the name always stays (drawn as far
  as it fits when it is wider than the screen); the hint or the row on how to quit wider than the screen does not fit
  either. Nothing crashes, down to 1×1.
- **No key does anything**: none goes to the app, none to a PTY; `q` and a single `Ctrl-C` do nothing either. Only
  pressing `Ctrl-C` twice quits at once (the forced quit of Rules K9).
- **The state is kept**: once the window is back at or above the minimum size, the screen is as it was, nothing changed.

**Why**: drawn by force on a screen below the minimum size, the layout is bound to be broken, and the user sees a heap of
cut frames, unable to tell whether the app is broken or the window too small; saying the name and the size needed, the
user just enlarges the window. Meanwhile the user cannot see the app's state, so passing keys on as usual would be
working blindfolded — something might be deleted by mistake, and what is typed into a shell cannot be seen; so no key
does anything, and a double `Ctrl-C` is kept as the way out in an emergency. The quit flow may open a confirm to ask
something, which cannot be drawn then, so `q` and a single `Ctrl-C` do nothing either. The way out is written on the
screen: with no key doing anything, someone who doesn't know the rule takes the app for stuck; when the window can't be
made larger (a tmux pane split in half, say) it is the only way out, so it goes after the hint (reported by hostu,
2026-10-27).

## screen.8 Empty states

One centred fact, plus a hint naming the key, both in Overlay0; keys in the hint are in square brackets (Rules M5).
Example:

```
No hosts yet

Press [A] to add a host, or [Space] to see what you can do here
```

- **When too long**: it wraps between words ("Wrapping" in the [components](../README.md)), each row centred, still one
  cell from the frame on each side; it is never cut, nor does the sentence have to be shortened to fit.
- **An empty list**: the empty state takes the whole panel, the header included, its sentence centred in the panel (the
  ordinary list in [`panel`](panel.md)).

A panel's loading and errors use this look too ("Loading and errors" in [`panel`](panel.md)).

## screen.9 Resizing panels

On a screen with more than one panel, the user moves the lines between them from the panel that has the focus, and the
app keeps where they are left (the user, 2026-11-26, from gittu and ccodu):

| Key | Does |
|---|---|
| `>` | the focused panel wider, by 2 columns |
| `<` | narrower, by 2 columns |
| `+` | taller, by 1 row |
| `-` | shorter, by 1 row |
| `=` | every line of the current screen back to the default |

**A line is shared**: what moves is the line on the panel's edge, and every panel touching that line moves with it, the
panels on its other side growing or shrinking. A line runs as far as panels meet along it:

```
┌───┬───┐      ┌───┬───────┐
│ 1 │ 2 │      │ 1 │   2   │
├───┼───┤      ├───┴───────┤
│ 3 │ 4 │      │     3     │
└───┴───┘      └───────────┘
```

On the left, `>` on [1] makes [1] and [3] wider together and [2] and [4] narrower; `+` on [1] makes [1] and [2] taller
and [3] and [4] shorter. On the right, the upright line runs through the top row only: `>` on [1] makes [1] wider and
[2] narrower, and [3] does not move; `+` on [1] makes [1] and [2] taller and [3] shorter.

- **Which line**: a panel with a line on both sides (the middle of three columns, say) moves the one on its right for
  the width and the one below it for the height; a panel against the right or the bottom of the panel area moves the
  line on its other side, so that `>` always makes it wider and `+` taller.
- **The least size**: each panel has a least width and height, the app's own, small enough that at 60×32 every panel
  still fits side by side (Rules L1); a line stops as soon as any panel it moves is at its least.
- **When nothing moves**: the key never does nothing (Rules M6): an Info toast ([`dialog/toast`](../dialog/toast.md))
  says why, e.g. `[2] is already full width`, `[2] is already full height`, `[4] is at its minimum width` (naming the
  panel that stopped the line, the focused one first). Narrow widths (screen.5) and zoom (screen.6) show one panel, so
  it is full width and full height then. `=` with every line at its default says `The layout is already the default`.
- **Where that toast sits**: on the panel, at the edge that would have moved, inside its frame and over none of its
  borders: the right edge at its top right, the left edge at its top left, the bottom edge at its bottom centre, the top
  edge at its top centre; a panel already full width counts as its right edge, already full height as its bottom edge.
  It goes by the edge, not by the way the line goes: `>` and `<` on [1] above both bring it up at [1]'s top right. The
  rest is as for any toast: the same words make no new one (`INFO ×3`), and several stack, growing into the panel; one wider
  than the panel keeps to that side, over the panel beside it, never off the screen. `=`'s toast is at the usual place.
- **Kept**: once the user moves a line, where it is left is kept in the app's state (Rules E3), for each screen, the
  widths by the terminal's width and the heights by its height, and used whenever the terminal is that wide or that high
  again; a size with nothing kept takes the default, the app's own. Nothing is written before the user moves a line. `=`
  also takes out of the state what was kept on this screen for this width and this height.
- **In the menus**: `>` `<` `+` `-` act on the focused panel, so they are panel operations in every panel's Space menu;
  `=` acts on the whole screen, a global operation (Rules M2, M3; Principle P3):

| Row | Description |
|---|---|
| `[>] Wider` | `by 2 columns, kept for this width` |
| `[<] Narrower` | `by 2 columns, kept for this width` |
| `[+] Taller` | `by 1 row, kept for this height` |
| `[-] Shorter` | `by 1 row, kept for this height` |
| `[=] Default layout` | `this screen's lines back as they were` |

A row whose press would only bring the toast is disabled (M6), `[=]` while every line of the screen is at its default;
on a screen with only one panel the four rows are not shown, and the keys still answer with the toast.

- **The keys are kept**: on a panel, no app takes these five keys for anything else. Where keys go elsewhere (a popup,
  input state, a PTY, a mode), they are not resize keys there (Rules K8, K10, K11).

**Why**: where a line suits depends on what the panels hold and on the user's terminal (a long branch name, a wide
diff), so the user moves it, and the app keeps it for that size: a split set on a 200-column terminal means nothing at
80. The keys are vim's `Ctrl-W` `<` `>` `+` `-` `=`. A key acts on the focused panel ("this one wider") rather than
moving a line the way the arrow points, so it reads the same on every panel; a shared line keeps panels that line up
lined up. 2 columns and 1 row look about as long, a cell being about twice as tall as it is wide. A press that does
nothing reads as a broken key, and the user resizing is looking at the panel, so the toast comes at the edge they are
looking at, not at the bottom of the screen, where it would cover the panel being resized.

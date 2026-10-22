# screen (the whole screen)

**Language**: English · [繁體中文](screen-zh_TW.md)

The skeleton of the whole screen. A panel's frame is in [`panel`](panel.md), the frame floating over it in
[`popup`](popup.md).

## From top to bottom

1. **The top row**: in a multi-screen app, the screen chip row, with a full-width separator below it; a single-screen app
   may have a statusbar row (up to the app).
2. **The panel area**: the remaining height. Each screen numbers its own panels from `[1]`; `1`–`9` jump only to the
   panels of the current screen (Rules K1).
3. **The bottom row**: the footer.

## Footer

One row, written like a hint (Rules M5); keys Blue, colon and description Overlay0 ([`color`](../color.md)). When too
narrow, whole pairs are dropped from the end (the hint in [`popup`](popup.md)). The content depends on the situation:

| Situation | Footer |
|---|---|
| Normal | `Space:menu ?:help !:log Tab\|1–N:panels q:quit` |
| A screen with only one panel | `Space:menu ?:help !:log q:quit` |
| In a mode (Rules K11) | `Space:menu ?:help`, the mode's own keys, and last `Esc:<verb for leaving>`. E.g. `Space:menu ?:help Enter:drop Esc:cancel` |
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

## Screen chip row

The top row of a multi-screen app: one capsule per screen, drawn as the capsule chain in [`panel`](panel.md), the chain's
colour being Blue (the selected screen filled with Blue, its text Base bold; the unselected ones filled with Mantle, their
text Blue, not bold). When it does not fit, it shrinks by the capsule chain's rules: first down to `[M] [F] [S]`, then the
unselected ones are folded away.

The statusbar's content goes on its right (see below). Below the chip row runs a full-width heavy line `━` in Overlay0; during
long work (a transfer, a download) it fills with Green from the left as a progress bar, and the status text beside it is
Green too. While a terminal popup is open, the chip row and this separator both stay
([`dialog/terminal`](../dialog/terminal.md)): the progress stays in sight from inside a shell.

**A single-screen app has no chip row**: the progress of long work is the app's content, written in the work's own row,
Green while it runs (e.g. the row in filu's `[3] Tasks` reads `3/10`, and the running glyph is Green). While a terminal
popup is open, that row is covered and the progress is out of sight; that is fine, and no extra row is opened for it.

## Statusbar

Whether there is one is up to the app. A single-screen app puts it on the top row; a multi-screen app uses the right of
the chip row rather than a row of its own. It is not a surface; focus never rests on it.

- Written like a label (Rules M5): hotkeys, if any, are marked (e.g. kbu's `[C]ontext: prod  [N]amespace: default`).
- A group is written `label: value`, one space after the colon; two cells between groups, with no separator symbol
  ("Diagrams and spacing" in the [components](../README.md): the two-cell rule does not apply here).
- Ordinary text Overlay0; the "where you are now" values Lavender (user footprint); work in progress Green; the counts of
  errors and warnings Red and Peach.
- Fixed width (Rules L2): the last dynamic field is not padded, while the fields before it keep their fixed widths; when
  it does not fit it is truncated, never wrapped (L3).

## Narrow widths

When not all panels fit, only the focused panel is drawn, at full width; `Tab` changes panels as usual, showing one at a
time. The threshold is set by the app from the minimum widths of its panels, but may not be above 80 (Rules L1: 80
columns must work properly). Narrow widths happen only at or above the app's minimum size; below it, see "Smaller than
the minimum size" below.

## Zoom

Enlarging one panel is the app's own feature: whether there is one, and its key, are up to the app (e.g. filu's `z`).
The spec gives the default: when zoomed, only the focused panel is drawn, filling the panel area, as with narrow widths;
`Tab` and the digit keys change panels as usual, the panel changed to is zoomed too, and only pressing the zoom key again
restores the layout. How a panel is enlarged is up to the app (e.g. filu sets the tabs of one panel side by side); the
default needs no note, and a different one goes into the design decisions of the dev-remarks.

**Why**: what each app wants to see enlarged differs, so the spec keeps only a default everyone understands; with the
default the same as narrow widths, what the user learns on a narrow screen works when zoomed too.

## Smaller than the minimum size

When the screen is smaller than the app's minimum size (Rules L1: 80×40 by default; the app may lower it, but not above
80×40), the whole screen draws just two rows, centred both ways:

```
                kbu
needs a terminal of at least 60×20
```

- **The name**: the app's command name, Blue bold (as the splash's name, Rules S5).
- **The hint**: on the row below the name, `needs a terminal of at least <width>×<height>`, giving the app's minimum
  size; Overlay0.
- **When it does not fit**: the hint goes first, and the name always stays (drawn as far as it fits when it is wider
  than the screen); nothing crashes, down to 1×1.
- **No key does anything**: none goes to the app, none to a PTY; `q` and a single `Ctrl-C` do nothing either. Only
  pressing `Ctrl-C` twice quits at once (the forced quit of Rules K9).
- **The state is kept**: once the window is back at or above the minimum size, the screen is as it was, nothing changed.

**Why**: drawn by force on a screen below the minimum size, the layout is bound to be broken, and the user sees a heap of
cut frames, unable to tell whether the app is broken or the window too small; saying the name and the size needed, the
user just enlarges the window. Meanwhile the user cannot see the app's state, so passing keys on as usual would be
working blindfolded — something might be deleted by mistake, and what is typed into a shell cannot be seen; so no key
does anything, and a double `Ctrl-C` is kept as the way out in an emergency. The quit flow may open a confirm to ask
something, which cannot be drawn then, so `q` and a single `Ctrl-C` do nothing either.

## Empty states

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

A panel's loading and errors use this look too ([`panel`](panel.md)).

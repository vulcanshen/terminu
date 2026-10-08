# screen (the whole screen)

**Language**: English · [繁體中文](screen-zh_TW.md)

The skeleton of the whole screen. A panel's frame is in [`panel`](panel.md), the frame floating over it in
[`popup`](popup.md).

## From top to bottom

1. **The top row**: in a multi-screen app, the screen chip row, with a full-width separator below it; a single-screen app
   may have a statusbar row (up to the app).
2. **The panel area**: the remaining height.
3. **The bottom row**: the footer.

## Footer

One row, written like a hint (Rules M5); keys Blue, colon and description Overlay0 ([`color`](../color.md)). When too
narrow, whole pairs are dropped from the end (the hint in [`popup`](popup.md)). The content depends on the situation:

| Situation | Footer |
|---|---|
| Normal | `Space:menu ?:help Tab/1–N:panels q:quit` |
| An app with only one panel | `Space:menu ?:help q:quit` |
| In a mode (Rules K11) | `?:help`, the mode's own keys, and last `Esc:<verb for leaving>`. E.g. `?:help Enter:drop Esc:cancel` |
| Typing in a panel filter (input state) | `Enter/Tab:list Esc:clear` |
| Focus on a PTY in a panel | the exit key, plus the keys the app keeps (Rules K10). E.g. `Alt-Esc:leave Alt-z:zoom PgUp:history` |

While a terminal popup is open, it covers the footer ([`dialog/terminal`](../dialog/terminal.md)).

**Why**: the footer is the entry point of Rules M1, so what it shows must be keys that can be pressed now. In a mode
`Space` does nothing, while typing `Space` `?` `q` are characters, and in a PTY every key goes to the subprocess —
writing the usual footer there would teach the user to press the wrong keys.

## Screen chip row

The top row of a multi-screen app: one capsule per screen, drawn as the capsule chain in [`panel`](panel.md), the chain's
colour being Blue (the selected screen filled with Blue, its text Base bold; the unselected ones unfilled, their text
Blue). When it does not fit, it shrinks by the capsule chain's rules: first down to `[M] [F] [S]`, then the unselected
ones are folded away.

The statusbar's content goes on its right (see below). Below the chip row runs a full-width separator in Overlay0; during
long work (a transfer, a download) it fills with Green from the left as a progress bar, and the status text beside it is
Green too.

## Statusbar

Whether there is one is up to the app. A single-screen app puts it on the top row; a multi-screen app uses the right of
the chip row rather than a row of its own. It is not a surface; focus never rests on it.

- Written like a label (Rules M5): hotkeys, if any, are marked (e.g. kbu's `[C]ontext: prod  [N]amespace: default`).
- Ordinary text Overlay0; the "where you are now" values Lavender (user footprint); work in progress Green; the counts of
  errors and warnings Red and Peach.
- Fixed width (Rules L2); when it does not fit it is truncated, never wrapped (L3).

## Narrow widths

When not all panels fit, only the focused panel is drawn, at full width; `Tab` changes panels as usual, showing one at a
time. The threshold is set by the app from the minimum widths of its panels, but may not be above 80 (Rules L1: 80
columns must work properly).

## Empty states

One centred fact, plus a hint naming the key, both in Overlay0; keys in the hint are in square brackets (Rules M5).
Example:

```
No hosts yet

Press [A] to add a host, or [Space] to see what you can do here
```

A panel's loading and errors use this look too ([`panel`](panel.md)).

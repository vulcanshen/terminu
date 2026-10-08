# slider (a value in a range)

**Language**: English · [繁體中文](slider-zh_TW.md)

## Purpose

A value within a range, used where a position says more than a number (e.g. a ratio, a brightness). For typing an exact
number use [`number`](number.md).

## Look

In a form or a panel: a track and the number.

```
Red          ━━━━━━●━━━━━ 128
```

- The track is a heavy line `━`, with `●` where the value is. The track's width and colour are the app's choice (e.g.
  webu and locku use 12 cells; locku draws the track in its channel's colour).

**Why**: a thin `─` is too faint in many fonts to be seen as a track.

## Keys

- `Enter` opens a [`select`](select.md) whose options are the numbers from bottom to top, one per step: the cursor opens
  on the current value, `j`/`k` move, `Enter` chooses; typing a number filters (typing `20` leaves 20, 120, 200–209…).
- A slider has no keys of its own; in a one-value-per-row panel `h`/`l` move between items, so they cannot drag it in
  place.

## Value

- **Every slider must have three attributes, bottom, top and step**: without them the number list cannot know how many
  options it has. An unset step is `(top − bottom) / 10`. A step may be a fraction.

**Why**: ten steps by default keep the list short enough to take in at a glance while still telling sizes apart; a list
with many rows relies on filtering.

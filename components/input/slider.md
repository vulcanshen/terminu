# slider (a value in a range)

**Language**: English · [繁體中文](slider-zh_TW.md)

## Purpose

A value within a range, where a position says more than a number (e.g. a ratio, a brightness). It has three attributes: bottom, top and step.

## Look

Settled by the user, 2026-10-07.

```
Red          ━━━━━━●━━━━━ 128
```

- **In a form or a panel**: a track and the number. The track is a heavy line `━` (the user: the old `─` was too thin),
  with `●` where the value is. Its width and colour are the app's (webu and locku use 12 cells; locku draws the track in
  its channel's colour).
- **What `Enter` opens is a [`select`](select.md)** whose options are the numbers from bottom to top, one per step: a
  radio glyph before every row, the chosen one in Green (webu's and locku's `current` changes), the cursor opening on the
  current value, `j`/`k` to move, `Enter` to choose, and **`/` to filter by typing a number** (`20` leaves 20, 120,
  200–209…; the user: "do it"). A slider has no keys of its own; in a one-value-per-row panel `h`/`l` move between items,
  so they cannot drag it in place.

## Value

- **Every slider has three attributes, bottom, top and step** (the user, 2026-10-07): without them the number list cannot
  know how many options it has. An unset step is `(top − bottom) / 10`. A step may be a fraction (webu lists integers
  only today; noted as not done).
- webu's "multiply the step by 10 beyond 10000 rows" gives way to the step; a long list is narrowed with `/`.

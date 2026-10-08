# color-picker (colour)

**Language**: English · [繁體中文](color-picker-zh_TW.md)

An input popup for choosing a colour (colour fields on webu pages; locku's colour settings can use it). Settled by the user,
2026-10-07.

## Purpose

Choosing a colour.

## Look

```
╭─ Background ─────────────────────────────────╮
│                                              │
│  ████████  ████████                          │
│  ████████  ████████   ███   ███   ███        │   ← R/G/B: small swatches in their channel's colour (#2A0000, #002A00, #00003C)
│  old       new        R     G     B          │   ← the focused item's word is drawn as a cursor
│  #1E1E2E   #2A2A3C    2A    2A    3C         │   ← hex throughout
│                                              │
╰─ Enter:edit Esc:cancel ──────────────────────╯
```

- **One row, left to right**: old, new, R, G, B (the user). It stays small.
- **The old and new swatches are drawn large** (the user): old is the colour it opened with, never changing; new is the
  colour being adjusted, following R/G/B as they change. Under them `old`, `new` (words picked by me) and each hex. Side by
  side, they show how far the colour has moved.
- **R, G and B are small swatches**, not sliders (the user: sliders take too much room). Each is drawn in its channel's own
  colour (R is `#RR0000`, as locku draws its tracks today); under it its value, **always in hex** (the user).
- "Three sliders stacked" and "two swatches above, sliders below" were settled first; the user changed it to this row.

## Keys

- **new, R, G and B take the focus**, moved with `h`/`l` (one-dimensional: `j`/`k` back and on too); **old takes no
  focus** (the user: to change nothing, `Esc`). It opens on R. The focused item's word is drawn as a cursor (layer colour
  background, dark bold).
- **`Enter`** does the most direct thing to the focused item (K3):
  - R, G, B: opens a [`select`](select.md) of values (00–FF, step 1, the cursor on the current value), every row in hex
    with the decimal in brackets: `2A (42)` (the user: hex throughout, the decimal only noted in the select); `/` filters
    by typing, hex or decimal alike. On return new changes with it.
  - new: confirms, writes back and closes.
- **`Esc`** closes, changing nothing.
- **Hint**: on R/G/B `Enter:edit Esc:cancel`; on new `Enter:choose Esc:cancel`.
- No `Ctrl-S` and no new key: confirming is `Enter` on new.

## Value

- **In a form or a panel**: a small swatch and the hex (`███ #2A2A3C`); empty follows text's rule for empty values.
- Today: webu has users type `#RRGGBB`; it changes to this picker.

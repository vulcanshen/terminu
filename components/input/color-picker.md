# color-picker (colour)

**Language**: English · [繁體中文](color-picker-zh_TW.md)

## Purpose

Choosing a colour: colour fields on webu pages, locku's colour settings.

## Look

```
╭─ Background ─────────────────────────╮
│                                      │
│ ████████  ████████                   │
│ ████████  ████████   ███   ███   ███ │   ← R, G, B: small swatches, each in its channel's own colour
│ old       new        R     G     B   │   ← the focused item's word below is drawn as a cursor
│ #1E1E2E   #2A2A3C    2A    2A    3C  │   ← always in hex
│                                      │
╰─ Enter:edit Esc:cancel ──────────────╯
```

- **One row, left to right**: old, new, R, G, B. The layout is small and takes no large block.
- **The old and new swatches are drawn larger**: old is the colour it opened with, never changing; new is the colour
  being adjusted, following R, G and B as they change. Under them `old`, `new` and each one's hex. Compared side by
  side, they show how much has changed.
- **R, G and B are small swatches**, not sliders: each swatch is drawn in its channel's own colour (R is `#RR0000`);
  under it its value, **always in hex**.
- **Width**: the layout is fixed, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).

**Why**: three sliders take too much room; a row of small swatches with hex is read at a glance. Colours in the family
are all written in hex (`#2A2A3C`), and with the channels in hex too, they line up.

## Keys

- **The four items new, R, G and B take the focus**, moved with `h`/`l` left and right (one-dimensional: `j`/`k` go back
  and on too, Rules K12); **old takes no focus**: to change nothing, `Esc`. It opens with the focus on R. The focused
  item's word below is drawn as a cursor (layer colour background, Base bold).
- **`Enter`** does the most obvious thing to the focused item (Rules K3):
  - R, G, B: opens a [`select`](select.md) of numbers (00–FF, step 1, the cursor on the current value), every row in hex
    with the decimal in brackets: `2A (42)`; typing filters, by hex or decimal alike. Back from choosing, new changes
    with it and the focus stays on that channel.
  - new: confirms, writes back and closes.
- **`Esc`**: closes, changing nothing.
- **Hint**: on R, G, B `Enter:edit Esc:cancel`; on new `Enter:choose Esc:cancel`.

## Value

In a form or a panel: a small swatch and the hex (`███ #2A2A3C`); empty follows the rule for empty values in
[`input/README`](README.md).

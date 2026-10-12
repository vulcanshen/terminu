# color-picker (colour)

**Language**: English · [繁體中文](color-picker-zh_TW.md)

## Purpose

Choosing a colour: colour fields on webu pages, locku's colour settings.

## Look

```
┏━BACKGROUND━━━━━━━━━━━━━━━━━━━━━━┓
┃                                   ┃
┃ ████████  ████████                ┃
┃ ████████  ████████  ███  ███  ███ ┃   ← R, G, B: small swatches, each in its channel's own colour
┃ old       new       R▓▓  G    B   ┃   ← the focus on R: the name and hex rows below drawn as a cursor, as wide as the swatch
┃ #1E1E2E   #2A2A3C   2A▓  2A   3C  ┃   ← always in hex
┃                                   ┃
┃ ───────────────────────────────── ┃
┃                           Choose  ┃   ← the action row: the button `Choose`
┃                                   ┃
┗━ Enter:edit Esc:cancel ━━━━━━━━━━━┛
```

- **One row, left to right**: old, new, R, G, B, with two cells between the five items. The layout is small and takes no large block.
- **The old and new swatches are drawn larger** (8 cells wide, 2 rows tall): old is the colour it opened with, never changing; new is the colour
  being adjusted, following R, G and B as they change. Under them `old`, `new` and each one's hex. Compared side by
  side, they show how much has changed.
- **R, G and B are small swatches** (3 cells wide, 1 row tall), not sliders: each swatch is drawn in its channel's own colour (R is `#RR0000`);
  under it its value, **always in hex**.
- **The action row**: a separator under the content and one button on the right, `Choose`, drawn as the button of
  [`dialog/form`](../dialog/form.md) (Surface1 background and Text unfocused; layer colour background and Base bold
  focused; on the right, one cell from the border). A colour picker cannot be invalid, so it has no error row.
- **Width**: the layout is fixed, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).

**Why**: three sliders take too much room; a row of small swatches with hex is read at a glance. Colours in the family
are all written in hex (`#2A2A3C`), and with the channels in hex too, they line up.

## Keys

- **The four items R, G, B and `Choose` take the focus**, in the order R → G → B → `Choose`, moved with `h|l` left and
  right (one-dimensional: `j|k` go back and on too; wrapping at the ends, Rules K12). **old and new take no focus**:
  to keep old, `Esc`; new is what R, G and B make, with nothing of its own to focus. It opens with the focus on R.
  With the focus on a channel, both rows under it, the name and the hex, are drawn as a cursor (layer colour
  background, Base bold), as wide as the swatch above (3 cells × 2 rows).
- **`Enter`** does the most obvious thing to the focused item (Rules K3):
  - R, G, B: opens a [`select`](select.md) of numbers (00–FF, step 1, the cursor on the current value), every row in hex
    with the decimal in brackets: `2A (42)`; typing filters, by hex or decimal alike. Back from choosing, new changes
    with it and the focus stays on that channel.
  - `Choose`: confirms, writes back and closes.
- **`Esc`**: closes, changing nothing.
- **Hint**: on R, G, B `Enter:edit Esc:cancel`; on `Choose` `Enter:choose Esc:cancel`.

**Why**: R, G and B change new, so new has nothing of its own to focus; confirming takes a button as in a form, still
with `Enter`, and the button can be seen — "fields change the value, the button submits", the same as a form. The
focus block covers both the name and the hex and is as wide as the swatch: a one-cell block is easily missed, and the
hex being changed lights up with it.

## Value

In a form or a panel: a small swatch and the hex (`███ #2A2A3C`); empty follows the rule for empty values in
[`input/README`](README.md).

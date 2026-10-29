# color-picker (colour)

**Language**: English · [繁體中文](color-picker-zh_TW.md)

## color-picker.1 Purpose

Choosing a colour: locku's colour settings.

## color-picker.2 Look

```
┏━BACKGROUND━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                      ┃
┃ ████████  ████████                   ┃
┃ ████████  ████████  ███  ███  ███    ┃   ← R, G, B: small swatches, each in its channel's own colour
┃ old       new       R▓▓  G    B      ┃   ← the focus on R: the name and hex rows below drawn as a cursor, as wide as the swatch
┃ #1E1E2E   #2A2A3C   2A▓  2A   3C     ┃   ← always in hex, upper case
┃                                      ┃
┃ ──────────────────────────────────── ┃
┃                              Choose  ┃   ← the action area: the button `Choose`; `Tab` goes between the channels and the button
┃                                      ┃
┗━ Enter:edit Tab:actions Esc:cancel ━━┛
```

- **One row, left to right**: old, new, R, G, B, with two cells between the five items. The layout is small and takes no large block.
- **The old and new swatches are drawn larger** (8 cells wide, 2 rows tall): old is the colour it opened with, never changing; new is the colour
  being adjusted, following R, G and B as they change. Under them `old`, `new` and each one's hex. Compared side by
  side, they show how much has changed.
- **R, G and B are small swatches** (3 cells wide, 1 row tall), not sliders: each swatch is drawn in its channel's own colour (R is `#RR0000`);
  under it its value, **always in hex**.
- **When there was no value** (e.g. ccdrawu's Drawer background left unset, using the theme's own): old has no swatch
  and always reads `none` (Overlay0) — the column is only 8 cells, too narrow for the app's text for an empty value; new
  starts from `#000000`.

  ```
  ┃           ████████                   ┃
  ┃           ████████  ███  ███  ███    ┃
  ┃ old       new       R▓▓  G    B      ┃
  ┃ none      #000000   00▓  00   00     ┃   ← old empty, reading none; new starting from black
  ```

- **The action area**: a separator under the content and one button on the right, `Choose`, drawn as the button of
  [`dialog/form`](../dialog/form.md) (Surface1 background and Text unfocused; layer colour background and Base bold
  focused; on the right, one cell from the border). A colour picker cannot be invalid, so it has no error row.
- **Width**: the layout is fixed, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).

**Why**: three sliders take too much room; a row of small swatches with hex is read at a glance. Colours in the family
are all written in hex (`#2A2A3C`), and with the channels in hex too, they line up.

## color-picker.3 Keys

- **The four items R, G, B and `Choose` take the focus**. hjkl move only among R, G and B: `h|l` left and right, `j|k`
  back and on too (one-dimensional), wrapping at the ends (Rules K12); `Choose` is reached only with `Tab`. **old and new
  take no focus**:
  to keep old, `Esc`; new is what R, G and B make, with nothing of its own to focus. It opens with the focus on R.
  With the focus on a channel, both rows under it, the name and the hex, are drawn as a cursor (layer colour
  background, Base bold), as wide as the swatch above (3 cells × 2 rows).
- **`Tab|Shift-Tab` go back and forth between the channels (R, G, B) and `Choose`**, coming back to the channel they
  left — the field area and the action area of a form: `Tab` changes the area, hjkl move within it (Rules K2, K12,
  [`input/README`](README.md)).
- **`Enter`** does the most obvious thing to the focused item (Rules K3):
  - R, G, B: opens a [`select`](select.md) of numbers (00–FF, step 1, the cursor on the current value), every row in hex
    with the decimal in brackets: `2A (42)`; typing filters, by hex or decimal alike. Back from choosing, new changes
    with it and the focus stays on that channel.
  - `Choose`: confirms, writes back and closes. When there was no value it always counts as a change (from unset to a
    colour), and is written back even when new is `#000000`.
- **`Esc`**: closes, changing nothing.
- **Hint**: on R, G, B `Enter:edit Tab:actions Esc:cancel`; on `Choose` `Enter:choose Tab:fields Esc:cancel`.

**Why**: R, G and B change new, so new has nothing of its own to focus; confirming takes a button as in a form, still
with `Enter`, and the button can be seen — "fields change the value, the button submits", the same as a form, and
`Tab` goes between the channels and the button as in a form, while hjkl move only among the channels. The focus block
covers both the name and the hex and is as wide as the swatch: a one-cell block is easily missed, and the hex being
changed lights up with it.

## color-picker.4 Value

In a form or a panel: a swatch 3 cells wide (`███`), a space, and the hex (`███ #2A2A3C`); empty follows the rule for
empty values in [`input/README`](README.md). With the cursor on the field, the swatch keeps its own colour and the hex
still turns Base (the cursor block in [`color`](../color.md)).

**Hex is always written in upper case** (`#F2B753`), however the file stores it (`#f2b753` in a config file too): in the
colour picker, on a form and on a panel alike.

**Why**: hex is how a colour is written, like the format of a number; its case does not change the colour, so this is not
changing the value (values unchanged, "Uppercase" in [components](../README.md)); written one way, the same colour looks
the same in the colour picker and on a panel.

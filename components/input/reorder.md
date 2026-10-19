# reorder (moving items by hand into an order)

**Language**: English · [繁體中文](reorder-zh_TW.md)

## Purpose

Moving a set of items one by one into the order wanted (e.g. the order ccdrawu's drawer shows its items in); the value
is the whole order, written back once `Enter` confirms it (an input, Rules F1). It is the panel's Drag mode put into a
popup: picking up, moving and dropping take the same keys and look the same ([`layout/panel`](../layout/panel.md)).

Not the menu's sort picker ([`dialog/menu`](../dialog/menu.md)): a sort picker chooses the column to sort by and only
decides how things are shown; in a reorder the user moves the items, changing the order itself.

No search: once filtered, the row above on screen is not always the real one above, and a move could not say what it
swaps with. So it is not a finder; what gets ordered is usually a few items already chosen, easy to reach with `j|k`,
`u|d` and `gg|G`.

## Look

Holding nothing:

```
┏━ORDER━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                 ┃
┃   Usage                         ┃   ← every row keeps one cell at its start for a glyph
┃▓▓▓Cost▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃   ← the cursor: a layer-colour background, Base bold
┃   Model                         ┃
┃   Context                       ┃
┃   Git                           ┃
┃                                 ┃
┗━ Enter:apply D:drag Esc:cancel ━┛
```

Holding Cost, after one `k` (Cost swapped with Usage):

```
┏━ORDER━━━━━━━━━━━━━━━━━━┫Drag┣━┓   ← the Drag mode: the frame and the mode name turn Yellow
┃                                 ┃
┃▓󰓢▓Cost▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃   ← the held item: a Yellow background, Base bold, `nf-md-swap_vertical` at its start
┃   Usage                         ┃
┃   Model                         ┃
┃   Context                       ┃
┃   Git                           ┃
┃                                 ┃
┗━ Enter:drop Esc:cancel ━━━━━━━━━┛
```

- **Each row**: one cell at the start for a glyph, a space, then the item (Text). Only the held item draws the glyph;
  the other rows leave it blank. The cell is always kept, so text never shifts when an item is picked up or dropped
  (Rules L2).
- **Cursor**: as in the menu — a layer-colour background, Base bold, from border to border, the right padding the arrow
  U+E0B0 ([`dialog/menu`](../dialog/menu.md)).
- **The held item** (the Drag mode, Rules K11): drawn as the cursor with the layer colour swapped for the mode colour —
  a Yellow background, Base bold, the arrow Yellow too; its first cell shows `nf-md-swap_vertical` (U+F04E2). The frame
  and the mode name turn Yellow, with `┫Drag┣` set in the top border on the right (the mode name in
  [`layout/panel`](../layout/panel.md)).
- **Title**: as in [`layout/popup`](../layout/popup.md), naming what is being ordered (e.g. `ORDER`).
- **Width**: known when it opens ("Content width known when it opens" in [`layout/popup`](../layout/popup.md)): the
  widest item plus the two cells at the start, + 4; at least enough for the hint `Enter:apply D:drag Esc:cancel`
  (29 + 6 = 35 cells).

**Why**: the held item in the mode colour with arrows up and down says "this one is picked up and can go up or down",
and Yellow means "in a mode" across the family. Every row keeps the glyph's cell: picking an item up changes only that
row's colour and adds one glyph, and nothing else moves by a cell.

## Keys

- It opens with the focus on the list.
- **Holding nothing**:
  - `j|l` move the cursor on, `h|k` back (a one-dimensional list, Rules K12), wrapping at the ends; `u|d` half a page,
    `gg|G` the top and the bottom.
  - **`D`**: picks up the cursor's item and enters the Drag mode. `D` is this popup's own hotkey; `Space` does nothing,
    as Rules K5 says.
  - **`Enter`**: writes the whole order back and closes the popup; only then does it take effect (opened from a form,
    as in [`input/README`](README.md)). The order as it was when opened: no change; it closes.
  - **`Esc`**: with the order unchanged, it closes. Changed, it first opens a confirm asking whether to discard it (e.g.
    `Discard changes to Order?`): `Enter` discards and closes the popup; `Esc` closes the confirm and returns to the
    list, the order still there (Rules F3, F6, K4; as "Cancel" in [`dialog/form`](../dialog/form.md)). "Changed": an
    item dropped somewhere other than where it was picked up, never cleared after that — moving one away and back still
    counts.
  - **Hint**: `Enter:apply D:drag Esc:cancel`.
- **Holding an item** (the Drag mode, Rules K11):
  - `j|l`, `h|k`: swap it with the next or the previous item, the cursor going with it. It wraps at the ends: the last item
    moved down goes to the top and every other item moves down one; the first moved up goes to the bottom (Rules K12).
  - **`Enter`**: drops it and leaves the Drag mode; the cursor stays on it.
  - **`Esc`**: puts it back where it was picked up and leaves the Drag mode (K11: back to the state before it; Rules K4,
    one layer at a time). Only the next `Esc` is the cancel above.
  - Other keys do nothing (K11): `Space` opens no menu; `D` is not an alias for dropping.
  - **Hint**: `Enter:drop Esc:cancel`.
- **`?`**: this popup's key reference (Rules K6); while holding, the Drag mode's keys (K11).

E.g. ccdrawu's order is Usage, Cost, Model. With the cursor on Cost, press `D`, `k`, `Enter`: Cost goes to the top and
is dropped; another `Enter` writes back the new order Cost, Usage, Model. `Esc` while holding Cost puts it back second;
`Esc` after dropping it first asks whether to discard.

**Why**: ordering by hand on a panel already has the Drag mode; the popup copies it, so learning it once covers both.
Picking up with `D`, not `Space`: `D` is the popup's own hotkey, and K5 needs no further exception. `Enter` does one
thing at a time: dropping while holding, confirming the whole order otherwise. `Esc` goes back one layer at a time:
first the held item goes back, then the whole popup is cancelled. Asking first once the order has changed: throwing
away an order after several moves costs as much to redo as a form.

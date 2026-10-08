# checkbox (on / off)

**Language**: English · [繁體中文](checkbox-zh_TW.md)

## Purpose

A switch, or ticking several from a group. A switch and a small group flip in the form or panel itself; a large group opens a popup.

## Look

The rows of a popup for choosing several values (kbu's namespace picker) use the same markers as [`select`](select.md):

**A marker at the start of every row** (settled by the user, 2026-10-07, after kbu's way):

| | Before every row | The chosen row |
|---|---|---|
| **Select (one)** | a radio glyph: chosen `󰐾`, not chosen `󰐽` | text in Green |
| **Checkbox group (several)** | a checkbox glyph: ticked, not ticked | text in Green |

- A marker on the left is found by running the eye down the list; every row's text lines up; the chosen row has a colour
  (Green in [`color`](../color.md) is "the chosen value"). On a chosen row under the cursor the background is the cursor
  row's and the text stays Green.
- One-of-many uses radio glyphs (as radio fields in a form do), several-of-many checkbox glyphs: the glyph tells which, in a
  form or in a popup alike.
- Today: kbu's namespace picker is the several-of-many way; kbu's context picker uses `* ` and webu's select a grey
  `current` on the right, and they change.

## Keys

**A popup for choosing several** (settled by the user, 2026-10-07, after kbu's namespace picker):

- **`Enter`** ticks or unticks the cursor row and **takes effect at once**; the popup stays. Opened from a form, it is
  written back to the field at once (the form notes "changed"); opened on its own, it applies at once (kbu: panel 2
  refetches).
- **`Esc`** closes it. A tick is itself the confirmation, so there is nothing to cancel — the same as a switch in a form
  flipping at once on `Enter`.
- Hint: `Enter:toggle Esc:close`. With many options `/` filters, as in [`select`](select.md).
- No `Ctrl-S` (the user: kbu's way is more direct). I had proposed "ticks held until `Ctrl-S`, `Esc` discards", carrying
  over the form round's "`Esc` in an input popup leaves the field as it was" — which was set for input popups that are
  typed into and confirmed with `Enter`, not for ticking.

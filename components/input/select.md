# select (choose from a list)

**Language**: English · [繁體中文](select-zh_TW.md)

## Purpose

Choosing **one** value from a list. With few options that fit in a form, use [`radio`](radio.md); for several values, [`checkbox`](checkbox.md).

## Look

An input popup for choosing **one** value from a list (a `<select>` on a webu page, kbu's context picker; it is what `Enter`
opens on a form field with more options than fit). Choosing several belongs to [`checkbox`](checkbox.md). Settled by the
user, 2026-10-07.

- The look follows [`dialog/menu`](../dialog/menu.md): the cursor row and the way hotkeys are written. It opens with the
  cursor on the current value.

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

- `j`/`k` move (wrapping). **`Enter` chooses**: the value is written back and the popup closes; opened from a form, the
  focus moves on to the next field by the form's rules.
- **With many options, `/` filters**: the filter row follows the panel search row (`↑`/`↓` move while typing, `Enter`
  focuses the item, a second `Enter` chooses it); only `Esc` differs — in a popup it closes the whole popup (F1: a phase
  is not a layer; the finder and kbu do so today).
- Options may have hotkeys (webu's digits), written as in a menu; whether to have them is the app's.
- Today: kbu's context picker switches and closes on `Enter` while typing; it changes to focusing the item first.

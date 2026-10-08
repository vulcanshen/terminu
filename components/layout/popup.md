# popup: The floating frame

**Language**: English · [繁體中文](popup-zh_TW.md)

A popup is a frame floating over the screen. This file sets only the look of the frame itself, not what goes in it: that
depends on the kind — one that takes a value is an input ([`input/`](../README.md#input)), any other is a dialog
([`dialog/`](../README.md#dialog)). The popup's class, width, fixed height when it opens, the reserved error row and
dimming when stacked are in rules F1–F8 and not repeated here.

## Frame

- **Title**: says what this popup is for (`Rename`, `New host`, `Add bookmark`), glyph + text, on the top border.
- **Hint**: on the bottom border. When it does not fit, whole items are dropped from the end (like the footer in [`screen`](screen.md)),
  never cut mid-item. **Keys that move between items are left out** (`j/k`, `↑/↓`, a form's `Tab` between fields); only
  actions and leaving are written: users find movement out by using it (the user, 2026-10-07). A key that switches
  phase is not movement and is written (e.g. a finder's `Tab:list`).
- **Padding**: one blank row above and below the content, one cell from the border on the left and right.

(The title, hint, padding and dropping hint items moved here from defaults D3 on 2026-10-07.)

## Opening and closing animation

Rules F2: opening and closing are both animated. The length is the same across the family: 8 frames × 16 ms ≈ 128 ms,
symmetric for opening and closing (moved here from defaults D3 on 2026-10-07, made the same for all by the user). The form
of the animation is up to the app.

## Loading

Rules F7: while a popup is loading, a spinning loading icon always sits after its title. The spec (moved here from defaults
D3 on 2026-10-07; taken from the icon webu shows while loading a URL):

- Glyphs: Nerd Font `nf-md-circle_slice_1` to `_8` (U+F0A9E–U+F0AA5), eight frames, a circle filling slice by slice, then
  starting over.
- Speed: 90 ms a frame, 720 ms a turn.
- The frame comes from the clock, `frames[(now / 90ms) % 8]`, not a counter; the tick is only rescheduled while something
  is loading.
- Width: one cell, the same as the static glyph it replaces, so nothing shifts (braille dots were tried; their shape and
  width don't fit).
- Colour: the same as the text beside it; after a popup title, that layer's colour (bold).

## Cancelling and completing

Cancelling returns to the source; completing an action clears the whole stack (the usual answer to T1). (Moved here from
defaults D3 on 2026-10-07.)

## When the content does not fit

F7: the height is fixed when it opens and capped at the screen height; beyond that the content scrolls inside the frame.

- Only the content area scrolls; the padding, the error row and the borders stay put.
- It scrolls with the focus, by as little as needed for the unit holding the focus to be fully visible. The focus is not
  pinned to the middle.
- While the content does not fit, the right end of the bottom border reads `N of M`: N is the position of the unit holding
  the focus, M the number of units, in the layer colour. Nothing is shown when everything fits. When the bottom border
  runs out of room, hint items are dropped whole from the end as usual, and `N of M` stays.
- The unit depends on the kind (e.g. a form counts fields: the label and value rows of a stacked field, or the options of
  a radio field, make one field).

```
╭─ Title ────────────────────────────────────────╮
│                                                │   ← padding
│ content                                        │   ← content area: the only part that scrolls
│ content                                        │
│ content                                        │
│                                                │
│ error                                          │   ← error row (reserved, F7): stays put
│                                                │
╰─ hint ──────────────────────────────── 4 of 12 ╯
```

## Error row

Settled by the user, 2026-10-07.

- **Where**: the last row of the content area, with a blank row between it and the content; it never scrolls. A kind may
  add fixed rows below it (e.g. a form's separator and action row).
- **Reserved only in popups that can fail** (F7): blank when there is no error, the height unchanged.
- **Look**: Red text, sharing the content's left edge (centred when the content is centred). The frame and the title keep
  the layer colour: the layer colour tells which layer this is ([`color`](../color.md), F8), and Red would wipe that out; the error already
  has the Red error row (and, in a form, Red labels).
- **Input errors only** (the user, 2026-10-07): the error row says a value breaks a rule — format, range, a required
  field, a duplicate name — in a short message written by the app. When the popup's action itself fails (a submit error:
  the file system refusing a rename, a write failing, the remote refusing, the file changed underneath), it is **not**
  written in the error row: an **error popup** opens over the current popup — a note (F1) with its frame and text in Red,
  giving the whole message; closing it returns to the popup underneath with every value still there (F4, F5). Details
  are in the error popup of [`dialog/note`](../dialog/note.md).
- **Too long**: it keeps to one row, cut at the end with `…`. In a form, while it holds an error, the error row is an item
  that can take the focus, and `Enter` on it opens the same note as an error popup with the whole message (the user; for
  how to get there see [`dialog/form`](../dialog/form.md)). In an input popup the error row never takes the focus: keys
  there are for typing (K8), and the error row only holds the app's short messages.
- **When it changes**: it follows the check (the user) — it changes only when a check runs: an error found writes this
  error, none found clears it; between two checks it stays, even when the value changes. A form checks on submit, an
  input popup on `Enter`.

## Implementation notes

Moved here from Family defaults D3 on 2026-10-07: pitfalls met while getting F3 and F8 right, for apps written in Go with
Bubble Tea.

- One popup, one file, one animator.
- `Esc` is handled in one place only (`closeTop`).
- The quit confirm is a popup of its own, on top of the whole stack: `Ctrl-C` may come while another confirm is open, and borrowing that one would overwrite the question the user is answering.
- "On top" means three places at once: key routing, `closeTop`, and drawing order.
- When the `?` key reference sits on another popup, it is on top in key routing and in drawing alike; boxes such as confirm and options take keys before the menu under them.
- Whether a layer is "still there" is judged by opening-or-open (`owns()`), never by an `isActive()` that includes closing (Rules F3).

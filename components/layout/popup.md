# popup (the frame floating over the screen)

**Language**: English · [繁體中文](popup-zh_TW.md)

A popup is a frame floating over the screen. This file sets only the frame itself, not what goes in it: one that enters
or chooses a value is an input ([`input/`](../README.md#input)), any other is a dialog ([`dialog/`](../README.md#dialog)).
The popup's classes, size and dimming when stacked are in Rules F1–F8.

## Frame

```
╭─ Title ─────────────────────────────────────╮
│                                             │   ← padding
│ content                                     │
│ content                                     │
│                                             │   ← padding
╰─ Enter:run Esc:close ────────────── 4 of 12 ╯
```

- **Line style**: rounded `╭─╮`, in the layer colour ([`color`](../color.md)). Popups are always rounded: the top popup
  has the focus, and that is told by lit and dimmed (Rules F8, Principle P6), not by line style — on a popup, rounded
  does not mean unfocused.
- **Title**: glyph + text, after `╭─ ` on the top border, in the layer colour, bold. The text says what this popup is for
  (`Rename`, `New host`, `Add bookmark`); when too long it is cut at the end with `…`. Glyphs:

  | popup | glyph |
  |---|---|
  | menu | `nf-fa-bars` (U+F0C9) |
  | key reference | `nf-fa-question_circle` (U+F059) |
  | confirm | `nf-md-shield_alert` (U+F0ECC) |
  | toast | by kind, see [`dialog/toast`](../dialog/toast.md) |
  | terminal | `nf-md-console` (U+F018D) |
  | input, form, note | chosen by the app: the thing it edits or shows (e.g. a pen for Rename); avoid outline glyphs that are too thin |

- **Hint**: after `╰─ ` on the bottom border, written as Rules M5 says.
  - **Order**: `Enter` first → this popup's own keys → the `Tab:…` that switches parts → `Esc` last. The terminal is the
    exception: its exit key comes first ([`dialog/terminal`](../dialog/terminal.md)).
  - **Keys that move between items are left out** (`j/k`, `↑/↓`, a form's `Tab` between fields); only actions and
    leaving are written: users find movement out by using it. A key that switches parts is not movement and is written
    (e.g. a finder's `Tab:list`).
  - **When it does not fit, whole items are dropped from the end**, never cut mid-item; the scroll position at the right
    of the bottom border stays.
  - **A popup with only a typing row** (text, password, number): `?` is a character there, so the hint must list every
    operation, and fit in 80 columns (Rules M3).
- **Right of the bottom border**: the scroll position when the content does not fit (see "When the content does not fit"
  below).
- **Padding**: one blank row above and below the content, one cell from the border on the left and right. Every kind of
  popup has it, viewers too; only the terminal is the exception ([`dialog/terminal`](../dialog/terminal.md)).
- **Separators**: a separator inside a popup does not join the frame — a horizontal one leaves one blank cell at each
  end, a vertical one is not drawn into the top and bottom padding. Colour Overlay0.

**Why**: with the title, hint and padding in fixed places, the moment any popup opens the user's eyes know where to find
"what this is" and "what can be pressed". Separators do not join the frame: a line joined to the frame looks like it cuts
one frame into two, when it only divides the content into sections.

## Width

The two widths of Rules F7, set when the popup opens and unchanged while it is open:

| | Width | Examples |
|---|---|---|
| **Content width known when it opens** | the widest row + 4 (one cell of border and one of padding on each side), at least enough for the title and hint, at most `min(terminal width − 2, 120)` | input with a length limit (a PIN of at most 12 digits: 12 + 11 spaces + 4 = 27 cells), confirm, menu, key reference, toast, error popup, datetime picker, color picker |
| **Content width not known** | `min(terminal width − 2, 120)` | free-typed text, URLs, streaming content, search results, forms |

"Known" means that how wide it can get is known the moment it opens, not how many characters are typed now: at the first
digit of a PIN the frame is already 27 cells, and it does not grow with the typing.

Narrow content is aligned left, one cell from the border (e.g. confirm, datetime picker, color picker); a toast's text
and a password's unlock mask are centred.

## Opening and closing animation

Rules F2: opening and closing are both animated. The length is the same across the family: 8 frames × 16ms ≈ 128ms,
symmetric for opening and closing. The form of the animation is up to the app.

**Why**: at 128ms the frame can be seen stacking on and backing off, yet it is short enough that opening or closing
several layers in a row means no waiting.

## Loading

Rules F7: while a popup is loading, a spinning loading icon always sits after its title. While a panel is loading, it
sits after the capsule ([`panel`](panel.md)). The spec:

- Glyphs: `nf-md-circle_slice_1` to `nf-md-circle_slice_8` (U+F0A9E–U+F0AA5), eight frames, a circle filling slice by
  slice, then starting over once full.
- Speed: 90ms a frame, 720ms a turn.
- The frame comes from the clock, `frames[(now / 90ms) % 8]`, not a counter; the tick is only rescheduled while something
  is loading.
- Width: one cell, the same as the static glyph it replaces, so swapping it in and out shifts nothing. Braille dots do not
  fit in shape or width and are not used.
- Colour: the same as the text beside it; after a popup title, that layer's layer colour (bold).

## Cancelling and completing

Cancelling returns to the source (Rules F4); whether the source stays after completing follows Rules T1.

## When the content does not fit

Rules F7: the height is fixed when it opens, at most the screen height − 2; beyond that the content scrolls inside the
frame.

- Only the content area scrolls; the top and bottom padding, the error row and the top and bottom borders stay put.
- It scrolls with the focus, by as little as needed for the unit holding the focus to be fully visible. The focus is not
  pinned to the middle.
- While it does not fit, the right of the bottom border shows the scroll position, in the layer colour: with a cursor,
  `N of M` (the position of the unit holding the focus, and the total); without a cursor (a note), the visible lines,
  `N-M of T`. Nothing is shown when everything fits.
- The unit depends on the kind (e.g. a form counts fields: the label and value rows of a stacked field, or the options of
  a radio, make one field).

```
╭─ Title ────────────────────────────────────────╮
│                                                │   ← padding
│ content                                        │   ← content area: the only part that scrolls
│ content                                        │
│ content                                        │
│                                                │
│ error                                          │   ← error row: stays put
│                                                │
╰─ hint ──────────────────────────────── 4 of 12 ╯
```

## Error row

- **Where**: a fixed row below the content area that never scrolls, with a blank row between it and the content. A kind
  may add fixed rows below it (e.g. a form's separator and action row).
- **Reserved only in popups whose values can be invalid** (Rules F7): blank when there is no error, the height unchanged.
- **Value errors only**: a value breaks a rule — format, range, a required field, a duplicate name; the message is
  written by the app and is short.
- **Look**: Red text, sharing the content's left edge (centred when the content is centred). The frame and title do not
  change colour and keep the layer colour: the layer colour says "which layer", and turning it Red would lose that;
  besides, the popup itself is not an error, only one value in it is invalid (and a form also has Red labels).
- **Too long**: it keeps to one row, cut at the end with `…`. In a form, while it holds an error, the error row is an item
  that can take the focus, and `Enter` opens the whole message ([`dialog/form`](../dialog/form.md)). In an input popup
  the error row never takes the focus: that is where typing happens (Rules K8).
- **When it changes**: it follows the check — it changes only when a check runs: an error found writes this error, none
  found clears it; between two checks it stays, even when the value changes. A form checks on submit, an input popup on
  `Enter`.

**When the action itself fails** (a write failing, the remote refusing, the file changed underneath), it is not written
in the error row: an error popup opens straight over the current popup ([`dialog/note`](../dialog/note.md)); closing it
returns to the original popup with every value still there (Rules F4, F5).

**Why**: a value error belongs to one field, so it is written in the frame, where the user keeps seeing it while fixing
it. An action failure belongs to no field; its message must be shown whole, since only after reading it can the user
decide what to do next — retry, change a value, or give up.

> **Implementation reference (not a requirement)**: pitfalls met while getting Rules F3 and F8 right, for apps written in
> Go with Bubble Tea.
>
> - One popup, one file, one animator.
> - `Esc` is handled in one place only (`closeTop`).
> - The quit confirm is a popup of its own, on top of the whole stack: `Ctrl-C` may come while another confirm is open,
>   and borrowing that one would overwrite the question the user is answering.
> - "On top" means three places at once: key routing, `closeTop`, and drawing order.
> - When the `?` key reference sits on another popup, it is on top in key routing and in drawing alike; boxes such as
>   confirm and options take keys before the menu under them.
> - Whether a layer is "still there" is judged by opening-or-open (`owns()`), never by an `isActive()` that includes
>   closing (Rules F3).

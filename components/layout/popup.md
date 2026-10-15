# popup (the frame floating over the screen)

**Language**: English · [繁體中文](popup-zh_TW.md)

A popup is a frame floating over the screen. This file sets only the frame itself, not what goes in it: one that enters
or chooses a value is an input ([`input/`](../README.md#input)), any other is a dialog ([`dialog/`](../README.md#dialog)).
The popup's classes, size and dimming when stacked are in Rules F1–F8.

## Frame

```
┏━TITLE━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                             ┃   ← padding
┃ content                                     ┃
┃ content                                     ┃
┃                                             ┃   ← padding
┗━ Enter:run Esc:close ━━━━━━━━━━━━━ 4 of 12 ━┛
```

- **Line style**: heavy `┏━┓`, in the layer colour ([`color`](../color.md)). Popups are always heavy: the top popup
  has the focus, and that is told by lit and dimmed (Rules F8, Principle P6), not by line style — on a popup, heavy
  does not mean focused; a popup underneath, dimmed, is still heavy.
- **Title**: glyph + text, made into a capsule after `┏━` on the top border: rounded ends, U+E0B6
  (`nf-ple-left_half_circle_thick`) on the left and U+E0B4 (`nf-ple-right_half_circle_thick`) on the right; filled with
  the layer colour, text Base bold and uppercase ("Uppercase" in the [components](../README.md)). The text says what
  this popup is for (`RENAME`, `NEW HOST`, `ADD BOOKMARK`); names and paths in it are content and keep their case. When
  it names what the popup acts on, the name follows after `: ` (`EDIT: filu`, `ALTERM: myhost`); viewers and the
  file-picker keep their own form (`YAML — pod/nginx` in [`dialog/note`](../dialog/note.md), `IDENTITY FILE · ~/.ssh` in
  [`input/file-picker`](../input/file-picker.md)). When too long it is cut at the end with `…`. Tabs after the title follow
  the capsule chain of [`panel`](panel.md), one line segment away from the title (e.g. `┏━TITLE━CONSOLENETWORK━┓`). Glyphs:

  | popup | glyph |
  |---|---|
  | menu | `nf-fa-bars` (U+F0C9) |
  | key reference | `nf-fa-question_circle` (U+F059) |
  | confirm | `nf-md-shield_alert` (U+F0ECC) |
  | toast | by kind, see [`dialog/toast`](../dialog/toast.md) |
  | terminal | `nf-md-console` (U+F018D) |
  | input, form, note | chosen by the app: the thing it edits or shows (e.g. a pen for Rename); avoid outline glyphs that are too thin |

- **Hint**: after `┗━ ` on the bottom border, written as Rules M5 says.
  - **Order**: `Enter` first → this popup's own keys → the `Tab:…` that switches parts → `Esc` last. The terminal is the
    exception: its exit key comes first ([`dialog/terminal`](../dialog/terminal.md)).
  - **Keys that move between items are left out** (`j|k`, `↑|↓`); only actions and leaving are written: users find
    movement out by using it. A key that switches parts is not movement and is written (e.g. a finder's `Tab:list`, a
    form's `Tab:actions`).
  - **When it still does not fit at the widest frame, whole pairs are dropped from the end**, never cut mid-pair; the
    scroll position at the right of the bottom border stays. The frame's width already counts the hint and the scroll
    position ("Width" below), so pairs are dropped only on a terminal too narrow.
  - **A popup with only a typing row** (text, password, number): `?` is a character there, so the hint must list every
    operation, and fit in 80 columns (Rules M3).
- **Right of the bottom border**: the scroll position when the content does not fit (see "When the content does not fit"
  below).
- **Text on the frame always keeps one line segment away from the corner**: the title `┏━TITLE`, the hint
  `┗━ Enter:run`, the scroll position `4 of 12 ━┛` (the same on a panel, where only the capsule sits right after the
  corner, [`panel`](panel.md)).
- **Padding**: one blank row above and below the content, one cell from the border on the left and right (with a cursor
  across a whole row, the right padding is as wide as the arrow, see the next item). Every kind of popup has it, viewers
  too; only the terminal is the exception: no padding on any side
  ([`dialog/terminal`](../dialog/terminal.md)).
- **A cursor block covers the padding**: a list's cursor runs from frame to frame, covering the left and right padding,
  and the text on it stays one cell from the frame ([`dialog/menu`](../dialog/menu.md), [`input/finder`](../input/finder.md));
  a form's focus block runs from the value all the way to the frame, covering the right padding
  ([`dialog/form`](../dialog/form.md)). Its right padding holds U+E0B0 (`nf-pl-left_hard_divider`) in the block's
  colour, an arrow pointing at the row (the ordinary list in [`panel`](panel.md)). In a popup with a cursor across a whole
  row, the right padding is as wide as the arrow (the powerline symbol width of Rules E5: one cell as a rule; on a
  terminal where it takes two, every row keeps two on the right), so the arrow fits. Only a cursor across a whole row has
  the arrow; one-cell cursors such as the days, hours and minutes of the datetime picker do not.
- **Separators**: a separator inside a popup does not join the frame — a horizontal one leaves one blank cell at each
  end, a vertical one is not drawn into the top and bottom padding. Colour Overlay0.

**Why**: with the title, hint and padding in fixed places, the moment any popup opens the user's eyes know where to find
"what this is" and "what can be pressed". Separators do not join the frame: a line joined to the frame looks like it cuts
one frame into two, when it only divides the content into sections. A cursor block covers the padding: the same cursor
looks the same in every list (Principle P4), and the widest block is the easiest to spot (Rules L5); with the right
padding as wide as the arrow, every row is the same width, and the arrow neither covers text nor pushes the frame out.
Tabs after the title keep a line segment away, like any other text on the frame: the title and the tabs read as two
things, and the rounded and slanted capsules do not stick together. The title is a
rounded capsule and a panel's is slanted: the ends tell a frame floating above from a panel on the screen.

## Width

The two widths of Rules F7, set when the popup opens and unchanged while it is open:

| | Width | Examples |
|---|---|---|
| **Content width known when it opens** | the widest row + 4 (one cell of border and one of padding on each side; where the right padding is as wide as the arrow, its real width), at least enough for the title and hint (the hint's width + 6: `┗━ ` and ` ━┛`), and when it scrolls also for the scroll position (the hint's width + the scroll position's widest width + 9: `┗━ `, at least ` ━ ` between the two, and ` ━┛`), at most `min(terminal width − 2, 120)` | input with a length limit (a PIN of at most 12 digits: the content is 12 + 11 spaces + 4 = 27 cells, the hint `Enter:save Backspace:clear Esc:cancel` 37 + 6 = 43 cells, so the frame is 43 cells), confirm, menu, key reference, toast, error popup, datetime picker, color picker, reorder |
| **Content width not known** | `min(terminal width − 2, 120)` | free-typed text, URLs, streaming content, search results, forms |

"Known" means that how wide it can get is known the moment it opens, not how many characters are typed now: at the first
digit of a PIN the frame is already 43 cells, and it does not grow with the typing. The scroll position is counted at
its widest too (`20 of 20` for a 20-row menu, `T-T of T` for `N-M of T`), so the frame does not change width while it
scrolls; and the hint is always whole — its last pair is usually `Esc`, and how to close a popup must always be in sight.

Narrow content is aligned left, one cell from the border (e.g. confirm, datetime picker, color picker); a toast's text
and a password's unlock mask are centred.

## Opening and closing animation

Rules F2: opening and closing are both animated, in one form and one length across the family. Opening has three
parts:

1. **The line** (4 frames): on the popup's middle row, a heavy `━` line in the layer colour grows from the centre to
   both sides until it is as wide as the popup.
2. **The hold** (1 frame): the full line stays for one frame.
3. **The opening** (4 frames): the popup opens up and down from its middle row; each frame shows the rows at the very
   middle of the popup, the last frame the whole popup.

- **Closing**: the same 9 frames backwards — pressed into a line at the middle, then the line shrinks to its centre.
- **Length**: 32ms a frame; 9 frames each way, about 288ms.
- **Dimming**: from the first opening frame, what lies beneath is dimmed; once closing starts, it lights up again at
  once (Rules F8: a popup on its way out is no longer the top).
- **Keys**: a popup takes no keys until its opening animation ends; a closing one takes none either (Rules F3).
- Every kind of popup animates this way, toasts and terminals included.

**Why**: a line first and then the opening shows where the frame stacks on from and where it backs off to; with the
line held for a frame, "something is coming" is seen first. 288ms is enough to see the three parts without feeling
like a wait. One form for the family: the rhythm and the look stay the same from one app to the next. No keys while
it plays: on a frame not yet drawn, users cannot see what their key landed on.

## Loading

Rules F7: while a popup is loading, a spinning loading icon always sits after its title; when tabs follow the title (the
capsule chain in [`panel`](panel.md)), after the whole row of tabs. While a panel is loading, it sits after the whole
capsule chain ([`panel`](panel.md)). One space on each side. The spec:

- Glyphs: `nf-md-circle_slice_1` to `nf-md-circle_slice_8` (U+F0A9E–U+F0AA5), eight frames, a circle filling slice by
  slice, then starting over once full.
- Speed: 90ms a frame, 720ms a turn.
- The frame comes from the clock, `frames[(now / 90ms) % 8]`, not a counter; the tick is only rescheduled while something
  is loading.
- Width: one cell, the same as the static glyph it replaces, so swapping it in and out shifts nothing. Braille dots do not
  fit in shape or width and are not used.
- Colour: the same as the text beside it; after a popup title, that layer's layer colour (bold); on a panel's top border,
  the border colour (Blue with focus, Surface2 without, dimmed along with the frame) — the frame's colour either way.

## Cancelling and completing

Cancelling returns to the source (Rules F4); whether the source stays after completing follows Rules T1.

## When the content does not fit

Rules F7: the height is fixed when it opens, at most the screen height − 2; beyond that the content scrolls inside the
frame.

- Only the content area scrolls; the top and bottom padding, the error row and the top and bottom borders stay put.
- It scrolls with the focus, by as little as needed for the unit holding the focus to be fully visible. The focus is not
  pinned to the middle.
- While it does not fit, the right of the bottom border shows the scroll position, in the layer colour: with a cursor,
  `N of M` (the position of the unit holding the focus, and the total); without one (a note, a viewer outside the
  selection mode), the visible lines, `N-M of T`. Nothing is shown when everything fits, nor while the focus is outside
  the scrolling area (a form's error row or button).
- The unit:
  - A form counts fields: the label and value rows of a stacked field, or the options of a radio, make one field; M
    counts fields only, not the error row or the button.
  - A cursor in a stretch of text (a textarea, a viewer in the selection mode) counts lines: the cursor's line and the
    number of lines, the same numbers as the line numbers, not rows as drawn.
  - A wrapping viewer (outside the selection mode) scrolls a row as drawn at a time; in `N-M of T`, N and M are the
    lines of the top and bottom rows ([`dialog/note`](../dialog/note.md)).

```
┏━TITLE━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                ┃   ← padding
┃ content                                        ┃   ← content area: the only part that scrolls
┃ content                                        ┃
┃ content                                        ┃
┃                                                ┃
┃ error                                          ┃   ← error row: stays put
┃                                                ┃
┗━ hint ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4 of 12 ━┛
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

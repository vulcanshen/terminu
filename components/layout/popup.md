# popup (the frame floating over the screen)

**Language**: English · [繁體中文](popup-zh_TW.md)

A popup is a frame floating over the screen. This file sets only the frame itself, not what goes in it: one that enters
or chooses a value is an input ([`input/`](../README.md#components12-input)), any other is a dialog ([`dialog/`](../README.md#components11-dialog)).
The popup's classes, size and dimming when stacked are in Rules F1–F8.

## popup.1 Frame

```
┏━TITLE━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                             ┃   ← padding
┃ content                                     ┃
┃ content                                     ┃
┃                                             ┃   ← padding
┗━ Enter:run Esc:close ━━━━━━━━━━━━━ 4 of 12 ━┛
```

- **Line style**: heavy `┏━┓`, in the layer colour ([`color`](../color.md)); the error popup is the exception, its
  frame and title capsule both Red ([`dialog/note`](../dialog/note.md)). Popups are always heavy: the top popup
  has the focus, and that is told by lit and dimmed (Rules F8, Principle P6), not by line style — on a popup, heavy
  does not mean focused; a popup underneath, dimmed, is still heavy.
- **Title**: glyph + text, made into a capsule after `┏━` on the top border: rounded ends, U+E0B6
  (`nf-ple-left_half_circle_thick`) on the left and U+E0B4 (`nf-ple-right_half_circle_thick`) on the right; filled with
  the layer colour (Red for the error popup), text Base bold and uppercase ("Uppercase" in the
  [components](../README.md)). The text says what this popup is for (`RENAME`, `NEW HOST`, `ADD BOOKMARK`); names and
  paths in it are content and keep their case. When
  it names what the popup acts on, the name follows after `: ` (`EDIT: filu`, `ALTERM: myhost`); viewers and the
  file-picker keep their own form (`YAML — pod/nginx` in [`dialog/note`](../dialog/note.md), `IDENTITY FILE · ~/.ssh` in
  [`input/file-picker`](../input/file-picker.md)). When too long it is cut at the end with `…`. Tabs after the title follow
  the capsule chain of [`panel`](panel.md), one line segment away from the title (e.g. `┏━TITLE━CONSOLENETWORK━┓`). Glyphs:

  | popup | glyph |
  |---|---|
  | menu | `nf-fa-bars` (U+F0C9) |
  | key reference | `nf-fa-question_circle` (U+F059) |
  | confirm | `nf-md-shield_alert` (U+F0ECC) |
  | toast | by kind, see [`dialog/toast`](../dialog/toast.md) |
  | terminal | `nf-md-console` (U+F018D) |
  | compare | `nf-md-compare` (U+F018A) |
  | input, form, note, an app's own popup | the app may decide for itself: the thing it edits or shows (e.g. a pen for Rename); avoid outline glyphs that are too thin |

- **Hint**: after `┗━ ` on the bottom border, written as Rules M5 says.
  - **Order**: `Enter` first → the `h|l:tab` that switches tabs → this popup's own keys → the `Tab:…` that switches parts → `Esc` last. The terminal is the
    exception: its exit key comes first ([`dialog/terminal`](../dialog/terminal.md)).
  - **Keys that move between items are left out** (`j|k`, `↑|↓`); only actions and leaving are written: users find
    movement out by using it. A key that switches parts is not movement and is written (e.g. a finder's `Tab:list`, a
    form's `Tab:actions`). The `h|l` that switches tabs is written too, as `h|l:tab`: there `h|l` changes the whole page,
    not the item (e.g. the comparison's `UNIFIED` and `SPLIT`, a viewer with several pages); not when there is only one
    tab, or while `h|l` does not switch tabs (e.g. in the selection mode).
  - **When it still does not fit at the widest frame, whole pairs are dropped from the end, but the last `Esc` always
    stays**: starting from the pair before `Esc`, pairs are dropped one by one towards the front, never cut mid-pair; the
    scroll position at the right of the bottom border stays. The frame's width already counts the hint and the scroll
    position ("Width" below), so pairs are dropped only on a terminal too narrow. E.g.
    `Enter:install Tab:actions Esc:cancel` that does not fit becomes `Enter:install Esc:cancel`, and then `Esc:cancel`.
  - **A popup with only a typing row** (text, password, number): `?` is a character there, so the hint must list every
    operation, and fit in 60 columns (Rules M3, L1).
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
  terminal where it takes two, every row keeps two on the right), so the arrow fits. A form counts too: its focus block
  runs to the frame and ends in the arrow, so its right padding is as wide as the arrow as well. Only a block across a
  whole row has the arrow; one-cell cursors such as the days, hours and minutes of the datetime picker do not.
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

## popup.2 Width

The two widths of Rules F7, set when the popup opens and unchanged while it is open:

| | Width | Examples |
|---|---|---|
| **Content width known when it opens** | the widest row + 4 (one cell of border and one of padding on each side; where the right padding is as wide as the arrow, its real width), at least enough for the title and hint (the hint's width + 6: `┗━ ` and ` ━┛`), and when it scrolls also for the scroll position (the hint's width + the scroll position's widest width + 9: `┗━ `, at least ` ━ ` between the two, and ` ━┛`), at most `min(terminal width − 2, 120)` | input with a length limit (a PIN of at most 12 digits: the content is 12 + 11 spaces + 4 = 27 cells, the hint `Enter:save Backspace:clear Esc:cancel` 37 + 6 = 43 cells, so the frame is 43 cells), confirm, menu, key reference, toast, error popup, datetime picker, color picker, reorder |
| **Content width not known** | `min(terminal width − 2, 120)` | free-typed text, URLs, streaming content, search results, forms |

"Known" means that how wide it can get is known the moment it opens, not how many characters are typed now: at the first
digit of a PIN the frame is already 43 cells, and it does not grow with the typing. The scroll position is counted at
its widest too (`20 of 20` for a 20-row menu, `T-T of T` for `N-M of T`), so the frame does not change width while it
scrolls; and the hint is always whole — its last pair is usually `Esc`, and how to close a popup must always be in sight.
Pairs are dropped only when the frame is at `terminal width − 2` and still too narrow, and even then `Esc` stays (the
hint above).

When a number has a unit ([`input/number`](../input/number.md)), the unit row under the typing row counts as a row of
content: the widest row is the wider of the most digits and the unit.

Narrow content is aligned left, one cell from the border (e.g. confirm, datetime picker, color picker); a toast's text
and a password's unlock mask are centred.

## popup.3 Opening and closing animation

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
- **Closing one while opening another** (when Rules T1 clears the source): the source closes and the target opens at
  the same time, without waiting for the source. The closing source is not a layer: the target takes the layer colour
  of the layer it ends up on from its first frame ([`color`](../color.md), the layer colours), and the half-closed
  source lies under the target, dimmed as F8 says.
- **Several layers closing together** (e.g. one action closing the whole stack, Rules T1 clearing a source of two or
  more layers): every layer closes at the same time, each at its own size and in its own layer colour, all pressed into a
  line at the middle and shrinking away together, still 9 frames, about 288ms in all; not only the top one playing while
  the ones beneath simply vanish, nor one layer after another.
- **Keys**: a popup takes no keys until its opening animation ends; a closing one takes none either (Rules F3).
- Every kind of popup animates this way, toasts and terminals included.

**Why**: a line first and then the opening shows where the frame stacks on from and where it backs off to; with the
line held for a frame, "something is coming" is seen first. 288ms is enough to see the three parts without feeling
like a wait. One form for the family: the rhythm and the look stay the same from one app to the next. No keys while
it plays: on a frame not yet drawn, users cannot see what their key landed on. Several layers closing together play
together, the same idea as T1's "play together, don't wait": each layer is seen backing away, and three layers do not
make the user wait three times as long.

## popup.4 Loading

Rules F7: while a popup is loading, a spinning loading icon always sits after its title; when tabs follow the title (the
capsule chain in [`panel`](panel.md)), after the whole row of tabs. While a form's button is running (an action that
keeps the form open, or a submit that takes a while), the loading icon sits after the title too
([`dialog/form`](../dialog/form.md)). While a panel is loading, it sits after the whole capsule chain
([`panel`](panel.md)). One space on each side. The spec:

- Glyphs: `nf-md-circle_slice_1` to `nf-md-circle_slice_8` (U+F0A9E–U+F0AA5), eight frames, a circle filling slice by
  slice, then starting over once full.
- Speed: 90ms a frame, 720ms a turn.
- The frame comes from the clock, `frames[(now / 90ms) % 8]`, not a counter; the tick is only rescheduled while something
  is loading.
- Width: one cell, the same as the static glyph it replaces, so swapping it in and out shifts nothing. Braille dots do not
  fit in shape or width and are not used.
- Colour: the same as the text beside it; after a popup title, that layer's layer colour (bold); on a panel's top border,
  the border colour, not bold (Blue with focus, Surface2 without, dimmed along with the frame) — the frame's colour
  either way.

## popup.5 Cancelling and completing

Cancelling returns to the source (Rules F4); whether the source stays after completing follows Rules T1.

## popup.6 When the content does not fit

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
    counts fields only, not the error row or the button. A panel with one value per row counts the same way
    ([`panel`](panel.md)).
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

## popup.7 Error row

- **Where**: a fixed row below the content area that never scrolls, with a blank row between it and the content. A kind
  may add fixed rows below it (e.g. a form's separator and action area).
- **Reserved only in popups whose values can be invalid** (Rules F7): blank when there is no error, the height unchanged.
- **Value errors only**: a value breaks a rule — format, range, a required field, a duplicate name; what the message
  says, the app may decide for itself, and it is short.
- **When too many wrong values pause the input** (e.g. locku's cooldown after several wrong PINs), the countdown goes in
  the error row too: Red, updated every second (`try again in 27 s`), cleared when it ends. While paused, every key but
  `Esc` is swallowed and never reaches the typing row.
- **Look**: Red text, sharing the content's left edge (centred when the content is centred). The frame and title do not
  change colour and keep the layer colour: the layer colour says "which layer", and turning it Red would lose that;
  besides, the popup itself is not an error, only one value in it is invalid (and a form also has Red labels).
- **Too long**: it keeps to one row, cut at the end with `…`. In a form, while it holds an error, the error row is an item
  that can take the focus, and `Enter` opens the whole message ([`dialog/form`](../dialog/form.md)). In an input popup
  the error row never takes the focus: that is where typing happens (Rules K8).
- **When it changes**: it follows the check — it changes only when a check runs: an error found writes this error, none
  found clears it; between two checks it stays, even when the value changes. A form checks on submit, an input popup on
  `Enter`. A pause's countdown is the exception: it updates every second.

**When the action itself fails** (a write failing, the remote refusing, the file changed underneath), it is not written
in the error row: an error popup opens straight over the current popup ([`dialog/note`](../dialog/note.md)); closing it
returns to the original popup with every value still there (Rules F4, F5).

**Why**: a value error belongs to one field, so it is written in the frame, where the user keeps seeing it while fixing
it. An action failure belongs to no field; its message must be shown whole, since only after reading it can the user
decide what to do next — retry, change a value, or give up. A pause's countdown comes from too many wrong values, so the
error row is where it reads right; a toast leaves after a few seconds, but the countdown has to stay in sight until
typing is possible again.

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

## popup.8 An app's own popup

Content the seven classes cannot hold (Rules F1, e.g. kamonu's popup for drawing cells) goes in an app's own popup.

- **The same as any popup**: the frame, the title (its glyph from the table above), how the hint is written and ordered,
  the width, the opening and closing animation, loading, content that does not fit, the layer colours and the dimming,
  as on this page and in [`color`](../color.md).
- **With values to submit, it works like a form** ([`dialog/form`](../dialog/form.md)): the action area sits below the
  content as on a form, and `Tab` switches between the content and the action area; a button submits; `q` does
  nothing; once something changed, `Esc` first opens a confirm asking whether to discard it. How an invalid value is
  reported (where the error row goes, whether it takes the focus), the app may decide for itself; the error is still
  visible (Rules F5).
- **How the content is drawn and the keys on it, the app may decide for itself.** Inside that scope:
  - the core keys keep their meaning (Rules K1); when the focused cell has several values to cycle through, `Space` moves
    it to the next value (Rules K5);
  - movement follows Rules K12 (hjkl are the arrow keys);
  - hotkeys on the content are disclosed in this popup's `?` (Rules K6, M5), and the hint follows "hint" above;
  - where the focus is stays visible (Rules L5).

**Why**: content the seven classes cannot hold, forced into one of them, makes that class's keys lie. An app's own popup
keeps fixed what can be fixed — the frame, the layers, submitting, leaving — so when users open one, everything but the
content itself is the same as any popup in the family (the user, 2026-10-25, kamonu). The error row is left to the app:
the content is the app's own drawing, so only the app knows where in it an error points and whether the user should
move there to see it (the user, 2026-10-26, terminu-go's G101).

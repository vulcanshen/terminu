# textarea (multi-line text)

**Language**: English · [繁體中文](textarea-zh_TW.md)

## textarea.1 Purpose

Entering several lines of text: a comment or a description in a web form. Content where a line is a line, such as code
and config files, goes to the user's `$EDITOR` (e.g. sshu's File transfer), not to a textarea.

## textarea.2 Look

**Long lines wrap, with line numbers on the left**:

```
┃  1 Thanks for the quick reply. The new   ┃
┃    build fixes the crash on start.       ┃   ← the same line wrapped: the number column is blank
┃  2                                       ┃
┃  3 One more thing: the export button█    ┃   ← the cursor's line
```

- A line wider than the box continues on the next row, never scrolling sideways. Wrapping is only on screen; no line
  break is added to the value. Width is display width.
- **Wrapping breaks at spaces**: a word (e.g. an English word) is never split in two but moves whole to the next row;
  only a word longer than a row on its own (e.g. a long URL) is cut by cells into pieces ([the components'
  "Wrapping"](../README.md)). A textarea holds prose such as comments and descriptions, and a word cut in half is hard
  to read.
- **Line numbers**: the first row of each line carries its number, right-aligned, followed by a space; wrapped rows leave
  the number column blank — so the rows of one line are seen as one. Numbers in Overlay0, the cursor's line number in
  Text. The number column is **at least two digits**: max(2, the digits of the largest number). Lines 1–99 never shift;
  at line 100, line 1000 and so on it widens by one digit each time and the content moves one cell right — the user
  typed those lines, so the reason is plain. There is no limit on the number of lines.
- **Size**: the width and the height both take the maximum of Rules F7 (`min(terminal width − 2, 120)`, the screen
  height − 2): the content grows with typing, so its size cannot be known when it opens. Content taller than the box
  scrolls inside it, the cursor always in view; when it does not fit, the right of the bottom border shows the cursor's
  line `N of M` (counted in lines, the same numbers as on the left, not rows as drawn).
- **The cursor**: in Write one cell of Lavender background with Base text (as [`input/README`](README.md)); in Move one
  cell of the layer colour background with Base text. The value's text is Lavender in both. In either state, the cursor
  resting on a control character draws the whole control character with a Red background and Base text (as "Pasted
  control characters" in [`input/README`](README.md)).
- **`\t`**: a `\t` in the value is drawn as `input_tab_width` spaces (see `Tab` below), not aligned to any column.

## textarea.3 Keys

**Two states**:

| State | What | Hint |
|---|---|---|
| **Write** | typing (the input state). `Enter` breaks the line, `Tab` inserts spaces (Rules K8). It opens here | `Esc:move` |
| **Move** | entered with `Esc` from Write. Moves the cursor; `i`, `a`, `o` return to Write; **`Enter` confirms** | `Enter:save i:write Esc:cancel` |

- **Confirming is `Enter` in Move.**
- **On opening**: in Write, with the old value already in and the cursor at its end; no grey suggestion (the grey
  suggestion in [`input/README`](README.md) is for single-line inputs only).
- `Esc`: from Write into Move (the hint turns to `Enter:save`, which tells how to save); from Move it closes. When the
  content has changed, a confirm first asks whether to discard it ("Cancel" in [`dialog/form`](../dialog/form.md)).
- **Editing keys in Write**: the set in [`input/README`](README.md), plus what several lines need — `↑|↓` to the row
  above or below (rows as drawn, a wrapped row counting as one); `←|→` at the start or end of a line cross to the
  previous or next line; `Backspace` at the start of a line joins it to the line above. `Home` and `End` go to the start
  and the end of the whole text (as on one line: the very start and end of the value); the start and end of a line are
  `0|$` in Move.
- **A pasted line break is a real line break**: `\n`, `\r\n`, and a lone `\r` (many terminals send a pasted line break
  as `\r`).
- **Other pasted control characters**: as in "Pasted control characters" in [`input/README`](README.md), kept in the
  value and drawn in red (`\x1b`); `Backspace` deletes one whole. While the value holds one, confirming (`Enter` in Move)
  is held back — nothing is saved — and the error row names the value as a single-line input's does (e.g. `Notes can't have control characters`); it saves once they are
  deleted. Line breaks and `\t` do not count.
- **`Tab`**: inserts spaces, as many as the setting `input_tab_width` (4 by default, in each app's config file, Rules
  E3). The value holds those spaces; `Backspace` removes one at a time. A pasted `\t` is kept as it is — what the user
  pasted is not quietly changed — and drawn as `input_tab_width` spaces.
- **Keys in Move**: movement follows Rules K12 — `h|j|k|l`, `w|b|e`, `0|$`, `u|d`, `gg|G`. `i` starts writing before the
  cursor, `a` after the cursor, `o` opens a new line below and writes there (as in vim).
- Move is not a mode, nor the input state: core keys follow Rules K1 (`?` opens the key reference).

**Why**: the old value is in on opening: a change to several lines of text is mostly a sentence added or a few words
changed, ready to make at once; in Write `Tab` indents and could not take a suggestion. Replacing the whole text means
deleting it in Write, which is rare. With several lines, `Enter` is needed to break lines, so confirming takes either another key or another state;
with two states, `hjkl` in Move can move and `Enter` can confirm, with no extra submit key. The two states' cursors
differ in colour: the same letter types in Write and moves in Move, which must be told apart without reading the hint;
the layer colour already means "the cursor rests here" in the family. `Tab` inserts spaces rather than aligning: a
terminal cannot line things up with tabs, and pressing `Tab` means "some spaces"; how many is the user's setting. The
box always opens at the maximum: the same reason as the width ("content not known, take the maximum"), and a short old
value does not start scrolling after a few lines.

## textarea.4 Value

In a form or a panel: the first line, with `…` when more follows ([`input/README`](README.md)).

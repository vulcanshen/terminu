# textarea (multi-line text)

**Language**: English · [繁體中文](textarea-zh_TW.md)

## Purpose

Entering several lines of text: a comment or a description in a web form. Content where a line is a line, such as code
and config files, goes to the user's `$EDITOR` (e.g. sshu's File transfer), not to a textarea.

## Look

**Long lines wrap, with line numbers on the left**:

```
│  1 Thanks for the quick reply. The new   │
│    build fixes the crash on start.       │   ← the same line wrapped: the number column is blank
│  2                                       │
│  3 One more thing: the export button█    │   ← the cursor's line
```

- A line wider than the box continues on the next row, never scrolling sideways. Wrapping is only on screen; no line
  break is added to the value. Width is display width, and a character is never split in two.
- **Line numbers**: the first row of each line carries its number, right-aligned to the digits of the largest number,
  followed by a space; wrapped rows leave the number column blank — so the rows of one line are seen as one. Numbers in
  Overlay0, the cursor's line number in Text.
- **Width**: the content is not known, so it takes the maximum of Rules F7.

## Keys

**Two states**:

| State | What | Hint |
|---|---|---|
| **Write** | typing (the input state). `Enter` breaks the line, `Tab` indents (Rules K8). It opens here | `Esc:move` |
| **Move** | entered with `Esc` from Write. Moves the cursor; `i`, `a`, `o` return to Write; **`Enter` confirms** | `Enter:save i:write Esc:cancel` |

- **Confirming is `Enter` in Move.**
- `Esc`: from Write into Move (the hint turns to `Enter:save`, which tells how to save); from Move it closes. When the
  content has changed, a confirm first asks whether to discard it ("Cancel" in [`dialog/form`](../dialog/form.md)).
- **Editing keys in Write**: the set in [`input/README`](README.md), plus what several lines need — `↑`/`↓` to the row
  above or below (rows as drawn, a wrapped row counting as one); `←`/`→` at the start or end of a line cross to the
  previous or next line; `Backspace` at the start of a line joins it to the line above. A pasted line break is a real
  line break.
- **Keys in Move**: movement follows Rules K12 — `h/j/k/l`, `w/b/e`, `0/$`, `u/d`, `gg/G`. `i` starts writing before the
  cursor, `a` after the cursor, `o` opens a new line below and writes there (as in vim).
- Move is not a mode, nor the input state: core keys follow Rules K1 (`?` opens the key reference).

**Why**: with several lines, `Enter` is needed to break lines, so confirming takes either another key or another state;
with two states, `hjkl` in Move can move and `Enter` can confirm, with no extra submit key.

## Value

In a form or a panel: the first line, with `…` when more follows ([`input/README`](README.md)).

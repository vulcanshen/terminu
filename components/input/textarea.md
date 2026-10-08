# textarea (multi-line text)

**Language**: English · [繁體中文](textarea-zh_TW.md)

## Purpose

Entering several lines of text: a comment or a description in a web form. Content where a line is a line (code, config files) goes to the user's `$EDITOR`.

## Look

**Long lines wrap, with line numbers on the left** (settled by the user, 2026-10-07):

```
│  1 Thanks for the quick reply. The new   │
│    build fixes the crash on start.       │   ← the same line wrapped: the number column is blank
│  2                                       │
│  3 One more thing: the export button█    │   ← the cursor's line
```

- A line wider than the box continues on the next row, never scrolling sideways. Wrapping is only on screen; no line
  break is added to the value. Width is display width, and a character is never split.
- **Line numbers**: the first row of each line carries its number, right-aligned to the width of the largest number,
  followed by a space; wrapped rows leave the number column blank — so rows of one line are seen as one (the user). Numbers
  in Overlay0, the cursor's line number in Text (added by me).
- Content where a line is a line (code, config files) goes to the user's `$EDITOR` (as sshu's File transfer does); the
  components add no sideways-scrolling textarea.
- Today: webu scrolls only the cursor's line sideways, cuts the other lines at the edge and measures width in characters;
  it changes.

## Keys

**Two states and submitting** (settled by the user, 2026-10-07):

| State | What | Hint |
|---|---|---|
| **Write** | typing. `Enter` breaks the line, `Tab` indents (K8). It opens here | `Esc:move` |
| **Move** | entered with `Esc` from Write. `h`/`j`/`k`/`l` move the cursor, `i`, `a`, `o` return to Write; **`Enter` saves** | `Enter:save i:write Esc:cancel` |

- **Submitting is `Enter` in Move; there is no `Ctrl-S`** (changed by the user, 2026-10-07: the textarea has its two
  states already, so `Ctrl-S` is one too many; first settled as `Ctrl-S` submitting from either state). `Ctrl-S` stays in
  forms only, where `Enter` opens a field and another key is needed to submit.
- `Esc`: from Write into Move (the hint turns to `Enter:save`, which tells how to save); from Move it closes (with a
  confirm first when the content changed, see the next point).
- The two states are webu's way today, and rules K3 and K8 say so; they stay because the user wants hjkl (as in forms).

**Editing keys in Write** (following from what is settled): text's set, plus what several lines need — `↑`/`↓` to the row
above or below (rows as drawn, a wrapped row counting as one); `←`/`→` at the start or end of a line cross to the previous
or next line; `Backspace` at the start of a line joins it to the one above. A pasted line break is a real line break (the
paste rule leaves the textarea out; webu puts pasted line breaks inside one line today and changes).

- When the content has changed, `Esc` first opens a confirm asking whether to discard, as a form does (see "Cancel" in
  [`dialog/form`](../dialog/form.md); the user, 2026-10-07).

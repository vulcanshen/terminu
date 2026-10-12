# note (read-only content)

**Language**: English · [繁體中文](note-zh_TW.md)

## Purpose

Read-only content that scrolls and may have hotkeys and modes of its own (Rules F1): the key reference, viewers (a YAML
view, the App Log, a file's content), the error popup, the typing explanation on a form ([`dialog/form`](form.md)). With
a list of options to run with `Enter`, it is a menu, not a note.

## Look

- The frame follows [`layout/popup`](../layout/popup.md): the padding above and below is always there, in a viewer too.
- **Title**: a glyph plus what is shown, drawn as the title capsule (e.g. `YAML — pod/nginx`: `YAML` in uppercase,
  `pod/nginx` is content and stays as it is). The glyph is the app's choice; the glyphs of the key
  reference and the error popup are below.
- **Scroll position**: when the content does not fit, the right end of the bottom border shows the visible lines,
  `N-M of T`; in a viewer's selection mode, the cursor's line `N of M` (see "Selection mode" below).
- **Width**: notes whose content is known when they open (the key reference, the error popup, explanations) follow the
  content; a viewer's content width is not known, so it takes the Rules F7 cap.

## Keys

- Scrolling: `j|k`, `u|d`, `gg|G` (Rules K12). A viewer's selection mode is below.
- **Closed with `Esc` only**. `Enter` does not close it; nor does `Space` (Rules K5).
- **The exception**: the error popup (whether it popped up by itself or was opened with `Enter` on a form's error row)
  and the typing explanation on a form close on `Enter` too.
- **Hint**: the note's own hotkeys first, `Esc:close` last. E.g. `y:copy /:search v:visual Esc:close`.

**Why**: for a note the user opened, `Esc` after reading is the most natural; `Space` pages down in readers such as
`less` and `man`, and someone used to them presses `Space` on a note to page down, only to have the note close. When an
error popup or the typing explanation pops up by itself, the user's hands are typing or about to submit, and `Enter` is
a reflex; with `Enter` closing them too, that press is not lost, and nothing else on them would be set off by `Enter`.
The error popup opened from a form's error row looks exactly the same, so it takes the same keys: nothing on screen
tells how it was opened, and a form can be worked through with `Enter` all the way (`Enter` on the error row to read
the message, `Enter` back, `e` to the field, `Enter` to change it).

## Selection mode (viewers only)

A viewer (a YAML view, the App Log, a file's content) can select a stretch of text to copy; the key reference, the error
popup and a form's typing explanation have no such mode, and `j|k` only scroll there.

- **No cursor by default**: `j|k`, `u|d`, `gg|G` scroll; with tabs, `h|l` switch tabs (Rules K12).
- **The first `v`**: enters the selection mode (a mode, Rules K11: the frame and the mode name turn the mode colour
  Yellow). The cursor appears at the start of the first visible line, with nothing selected yet. `h|j|k|l`, `w|b|e`,
  `0|$`, `u|d`, `gg|G` move it, and the view scrolls when it reaches the edge. Hint `v:select Esc:cancel`.
- **The second `v`**: starts the selection where the cursor is; moving the cursor then stretches it. The selection runs
  by characters (vim's `v`): from the start to the cursor, the cursor's character included; for whole lines, move the
  cursor to the start of the line first. Hint `y:copy Esc:cancel`. Once selecting, `v` does nothing.
- **`y`**: copies the selection and leaves the mode; the selection and the cursor disappear.
- **`Esc`**: leaves the whole mode at either step without copying; the selection and the cursor disappear (K11: back
  to the state before it was entered). `v` is not taken as an alias for leaving (K12).
- **Colours**: the cursor is one cell of the layer colour background with Base text (the same as Move in
  [`input/textarea`](../input/textarea.md)); the selection has a Yellow background with Base text, the cursor's cell
  keeping the layer colour; an empty line inside the selection shows one cell.
- **Scroll position**: in the selection mode, the cursor's line `N of M` (counted in lines); back to `N-M of T` after it.

**Why**: move to the start first, then select — where the cursor appears is not always where the selection should
start, and with selection starting on the first `v`, the start would always be the first visible line. With no cursor
by default, `j|k` still scroll and `h|l` still switch tabs, and a note read and closed carries no cursor it never uses.
By characters: what is copied out of a note is often a word, a command or a URL. Copying usually finishes the job, so it
takes no extra `Esc`.

## Key reference

The "what keys work here" opened with `?` (Rules K6, M4).

```
┏━[2] HOSTS KEYS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                               ┃
┃ 󰋘 ITEM OPERATION                              ┃  ← section title
┃  Enter     Connect — what it is, then in      ┃
┃  E         Edit — change this host            ┃
┃  X         Delete — remove from hosts.yaml    ┃
┃ 󰋘 PANEL OPERATION                             ┃
┃  A         Add — a new host                   ┃
┃  /         Search — name, user, host, port, … ┃
┃ 󰋘 MOVE                                        ┃
┃  j|k       down, up                           ┃
┃  u|d       half a page up, down               ┃
┃  gg|G      to the top, the bottom             ┃
┃ 󰋘 CORE KEYS                                   ┃
┃  Space     what you can do here               ┃
┃  ?         this list                          ┃
┃  Tab       next panel                         ┃
┃  1–N       jump to panel N                    ┃
┃  q|Ctrl-C  quit                               ┃
┃ 󰋘 APP-WIDE                                    ┃
┃  M         Manage — hosts, credentials, …     ┃
┃                                               ┃
┗━ ?|Esc:close ━━━━━━━━━━━━━━━━━━━━ 1-20 of 23 ━┛
```

- **Title**: `nf-fa-question_circle` (U+F059) plus `<surface> keys`, e.g. `[2] HOSTS KEYS`, `SPACE MENU KEYS`.
- **One key per row**: indented two cells, the key padded to the width of the widest key, two blank cells, then the
  description. A description too long is cut at the end with `…`, never wrapped. Keys are written as in Rules M5 (no
  brackets, no colon).
- **Rows from a menu**: the description reads `label — description`; the label loses its hotkey marks and keeps its case
  (a menu's `[E]dit` becomes `Edit — change this host`).
- **Sections**: section titles as in a menu (`nf-md-hexagon`, uppercase, Overlay0, indented one cell, not bold). On a panel they are, in order:
  - `item operation`, `panel operation`: as in the Space menu.
  - `move`: the movement keys that work here (Rules K12), only those that really do (e.g. `h|l` only with tabs).
  - `core keys`: the core keys that work on this panel — `Space`, `?`, `Tab`, `1–N` (with several panels, Rules K1),
    `q|Ctrl-C`; `Esc` only where it does something here (e.g. a filter to clear); `Enter` is not repeated, since
    `item operation` already says what it does here.
  - `app-wide`: the global hotkeys.
- **On a popup** only that popup's own keys are listed (Rules K6): its hotkeys, `Enter`, `Esc`, the movement keys.
- **Colours**: keys in Blue, not bold; descriptions in Text. A key that cannot be pressed right now has both key and
  description in Surface2 (Rules M6).
- **Keys**: scrolling as above; `?` or `Esc` closes it, `Enter` does nothing. Hint `?|Esc:close`.

**Why**: the key reference is the only place that lists every key — the hint leaves out movement and the Space menu
lists only actions — so without the movement keys, `u|d` and `gg|G` would have nowhere to be learned (Principle P1).
Labels are not lowercased: that would break abbreviations such as `SSH config` and `YAML`, and the hotkey is already in
the key column on the left.

## Error popup

The note laid over a popup whose action failed (see the error row in [`layout/popup`](../layout/popup.md)). The whole
message opened with `Enter` on a form's error row is one too.

```
┏━SAVE FAILED━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                 ┃
┃ hosts.yaml changed on disk since it was opened. ┃
┃                                                 ┃
┗━ Enter|Esc:close ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **Look**: frame and text in Red; the title capsule is filled Red with Base bold text (the capsule as in
  [`layout/popup`](../layout/popup.md)). The title glyph is `nf-md-fire` (U+F0238), the same as the Error toast. The
  message wraps inside the frame; when too long it scrolls with `j|k`.
- **Title**: what failed (`RENAME FAILED`, `SAVE FAILED`). Opened from a form's error row, it is the field's name
  (`PORT`).
- **Closing**: both `Enter` and `Esc` close it, hint `Enter|Esc:close`.
- **After closing**: back to the popup underneath, the focus where it was, every value still there (Rules F4). Pressing
  `Enter` repeatedly, the first press closes it and the next is one more press where the focus was — on a form's button,
  a retry. The failed action changed nothing, so a retry at worst shows the error once more.

**Why**: an error popup is an error through and through, so its frame and text are Red; it is always on top and closes
with one key, so without the layer colour nobody is left wondering which layer it is. A popup with an error row is not
itself an error — only one value in it fails a rule — so its frame keeps the layer colour.

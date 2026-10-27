# note (read-only content)

**Language**: English · [繁體中文](note-zh_TW.md)

## note.1 Purpose

Read-only content that scrolls and may have hotkeys and modes of its own (Rules F1): the key reference, viewers (a YAML
view, the App Log, a file's content), the error popup, the typing explanation on a form ([`dialog/form`](form.md)). A
viewer always has a selection mode (see "Selection mode" below). With a list of options to run with `Enter`, it is a
menu, not a note.

## note.2 Look

- The frame follows [`layout/popup`](../layout/popup.md): the padding above and below is always there, in a viewer too.
- **Title**: a glyph plus what is shown, drawn as the title capsule: the kind in uppercase; to say which one is shown,
  ` — ` and then the name, the name as it is (e.g. `YAML — pod/nginx`). The glyph, the app may decide for itself; the glyphs of
  the key reference and the error popup are below.
- **Scroll position**: when the content does not fit, the right end of the bottom border shows the visible lines,
  `N-M of T`; in a viewer's selection mode, the cursor's line `N of M` (see "Selection mode" below). When a viewer
  wraps, N is the line of the top row, M the line of the bottom row and T the number of lines (e.g. the top row is a
  wrapped row of line 6 and the bottom row is line 10: `6-10 of 42`).
- **Width**: notes whose content is known when they open (the key reference, the error popup, explanations) follow the
  content; a viewer's content width is not known, so it takes the Rules F7 cap.
- **Wrapping when too long**: a note that is a piece of prose, such as the error popup or a form's typing explanation,
  wraps when it does not fit, as in [the components' "Wrapping"](../README.md), and is never cut. The key reference's
  descriptions are the exception, below.
- **A viewer's wrapping**: wrapping by default — a line wider than the frame continues on the next row, as in [the
  components' "Wrapping"](../README.md): breaking between words, and only a word wider than a row on its own is cut by
  cells. For content that must stay aligned (side by side, a table), the app may turn wrapping off: what is wider than
  the frame is cut, with `…` at the end of the line. Unwrapped, when the selection cursor walks into the cut part, the
  view scrolls sideways just enough to show it (as vim's nowrap does), with `…` at the start of lines cut on the left;
  the cut text can still be selected and copied. Leaving the selection mode returns the view to the left edge.
- **A viewer's line numbers**: whether a viewer draws line numbers on the left, the app may decide for itself: content where a line
  is a line, such as file content, a YAML view or the App Log, usually has them; a table the app lays out itself (e.g.
  filu's file info) gains nothing from them and may go without. When drawn they follow
  [`input/textarea`](../input/textarea.md): the first row of each line carries its number, right-aligned, with a space
  after it; a wrapped row leaves the gutter blank. Numbers are Overlay0; in the selection mode the cursor's line has its
  number in Text. Copying leaves the numbers out. The gutter is **at least three digits**: where the line count is known
  on opening (YAML view, file content) it is max(3, the digits of the line count) and stays so; a streaming App Log
  starts at three digits and widens only past 999 lines.
  **A viewer with tabs** (e.g. DevTools' Console and Network): the gutter follows the widest of the pages seen so far,
  and only ever widens — set by the page it opens on; wider on a page with more lines; kept, not narrowed, on going back
  to a page with fewer. A streaming page likewise only widens.
- **A viewer's syntax colours**: content with a fixed format (YAML, JSON, TOML, HTML, XML, Markdown…) is coloured as a
  text file in [`input/file-picker`](../input/file-picker.md)'s preview table (chroma's catppuccin-mocha, foreground
  only). The app gives the language (a YAML view is YAML; a DevTools Network response goes by its content type); file
  content goes by the file name, as in the preview. Whether content with no fixed format (e.g. App Log), or whose
  language cannot be told, is coloured, the app may decide for itself: uncoloured, it is plain text in Text; an app knows its content
  and may colour it as its situation needs (e.g. the ERROR and WARN lines of a log). The lib adds no syntax colours but
  keeps the colours the app gives. Line numbers stay Overlay0; the selection mode's
  range stays Yellow with Base text, with no syntax colours inside it.
- **Tabs and control characters in a viewer** (as in the [`input/file-picker`](../input/file-picker.md) preview; the
  rule for the whole family is "Control characters" in [components](../README.md)): drawn as a terminal would draw
  them. A Tab is drawn as `input_tab_width` spaces (the same setting as [`input/textarea`](../input/textarea.md)), not
  aligned to tab stops; `\n` is a line break, and in content the app hands over line by line, a `\n` inside one line
  splits it in two too; a `\r` before a line break (CRLF) is not drawn, being part of the line break; colour codes
  (SGR) colour the text; a `\r` within a line (a progress bar) keeps only the last state; any other control character,
  and any sequence that is not a colour code, is drawn by name in Red (`\x07`; `\x1b[2J`, which clears the screen, as a
  red `\x1b` followed by `[2J`, as in "Pasted control characters" in [`input/README`](../input/README.md)). Copying
  takes the original characters, not the spaces or names drawn. A viewer is for reading: a program's output is meant to
  look that way in a terminal; a red `\r` on every line of a CRLF file is only noise; and Red is what tells a control
  character from the four characters `\x07` written in a file.
- **A viewer's search** (where it has `/`): every hit is underlined, keeping its own colour; the current one is drawn as
  the cursor block (layer colour background, bold Base, the cursor in [`color`](../color.md)), saying "you are here". No
  colour is added: the mode colour Yellow is kept for the selection mode's range.

```
┃   1 apiVersion: v1                            ┃   ← a three-digit gutter (this YAML has 42 lines); numbers in Overlay0
┃   2 kind: Pod                                 ┃   ← the content in YAML's syntax colours
┃   3 metadata:                                 ┃
┃   4   name: nginx                             ┃
┃   5   annotations:                            ┃
┃   6     note: restarted by the deploy job     ┃
┃     after the config change                   ┃   ← the same line wrapped: the gutter is blank
┃   7 spec:                                     ┃
┃   8   containers:                             ┃
┃   9   - name: nginx                           ┃
┃  10     image: nginx:1.27                     ┃
```

**Why**: a viewer knows how many lines it holds when it opens (a streaming one aside), so its gutter is set once and the
screen does not jump; a textarea's lines are the user's own typing, so a wider gutter has a visible reason, and it
starts at two digits. Three digits: content within 999 lines never jumps. With tabs it does not narrow on going back:
the width seen is kept, so switching tabs back and forth does not keep jumping. The syntax colours are the preview's, so
a file looks the same in the preview and in a viewer.

## note.3 Keys

- Scrolling: `j|k`, `u|d`, `gg|G` (Rules K12). A viewer's selection mode is below.
- **A wrapping viewer scrolls by rows as drawn** (as `less` does): `j|k` one row at a time, `u|d` half a page counted
  in rows. A line taller than the frame (e.g. minified JSON) can be read to its end; this matches
  [`input/textarea`](../input/textarea.md)'s `↑|↓`, which follow the rows as drawn.
- **Closed with `Esc` only**. `Enter` does not close it; nor does `Space` (Rules K5).
- **The exceptions**: the error popup (whether it popped up by itself or was opened with `Enter` on a form's error row)
  and the typing explanation on a form close on `Enter` too; the key reference also closes on a second `?` (Rules K6).
- **A form's typing explanation takes only `Enter` and `Esc`**: every other typeable character (`q` and `?` included)
  does nothing — no quitting, no key reference (typing on a field in [`dialog/form`](form.md)).
- **Hint**: the note's own hotkeys first, `Esc:close` last; with tabs, `h|l:tab` comes first (the hint in
  [`layout/popup`](../layout/popup.md)). E.g. `y:copy /:search v:visual Esc:close`.

**Why**: for a note the user opened, `Esc` after reading is the most natural; `Space` pages down in readers such as
`less` and `man`, and someone used to them presses `Space` on a note to page down, only to have the note close. When an
error popup or the typing explanation pops up by itself, the user's hands are typing or about to submit, and `Enter` is
a reflex; with `Enter` closing them too, that press is not lost, and nothing else on them would be set off by `Enter`.
The error popup opened from a form's error row looks exactly the same, so it takes the same keys: nothing on screen
tells how it was opened, and a form can be worked through with `Enter` all the way (`Enter` on the error row to read
the message, `Enter` back, `e` to the field, `Enter` to change it).

## note.4 Selection mode (viewers only)

Every viewer (a YAML view, the App Log, a file's content…) has a selection mode, to select a stretch of text and copy
it; the key reference, the error popup and a form's typing explanation have no such mode, and `j|k` only scroll there.

- **No cursor by default**: `j|k`, `u|d`, `gg|G` scroll; with tabs, `h|l` switch tabs (Rules K12).
- **The first `v`**: enters the selection mode (a mode, Rules K11: the frame and the mode name turn the mode colour
  Yellow). The cursor appears at the start of the first visible line, with nothing selected yet. `h|j|k|l`, `w|b|e`,
  `0|$`, `u|d`, `gg|G` move it, and the view scrolls when it reaches the edge. Hint `v:select Esc:cancel`.
- **The second `v`**: starts the selection where the cursor is; moving the cursor then stretches it. The selection runs
  by characters (vim's `v`): from the start to the cursor, the cursor's character included; for whole lines, move the
  cursor to the start of the line first. The mode name becomes `Visual>select` (the mode name in
  [`layout/panel`](../layout/panel.md)). Hint `y:copy Esc:unselect`. Once selecting, `v` does nothing.
- **`y`**: copies the selection and leaves the mode; the selection and the cursor disappear, and a Success toast says
  it is copied ([`dialog/toast`](toast.md)).
- **`Esc`**: goes back one layer at a time (Rules K4, K11): once selecting, the selection disappears and it is back to
  `Visual`, the cursor where it is; before selecting, it leaves the whole mode and the cursor disappears. Neither copies.
  `v` is not taken as an alias for going back (K12).
- **Colours**: the cursor is one cell of the layer colour background with Base text (the same as Move in
  [`input/textarea`](../input/textarea.md)); the selection has a Yellow background with Base text, the cursor's cell
  keeping the layer colour; an empty line inside the selection shows one cell.
- **Scroll position**: in the selection mode, the cursor's line `N of M` (counted in lines, the same numbers as the
  gutter); back to `N-M of T` after it.

**Why**: move to the start first, then select — where the cursor appears is not always where the selection should
start, and with selection starting on the first `v`, the start would always be the first visible line. With no cursor
by default, `j|k` still scroll and `h|l` still switch tabs, and a note read and closed carries no cursor it never uses.
By characters: what is copied out of a note is often a word, a command or a URL. Copying usually finishes the job, so it
takes no extra `Esc`. `Esc` goes back one layer as everywhere else: one layer back from `Visual>select` is `Visual`,
so a start picked wrong is put right by going back, moving and selecting again (the user, 2026-10-24). Every viewer has it: nobody has to remember which viewers can select and which cannot, and any
stretch of text you can see in the family can be copied.

## note.5 Key reference

The "what keys work here" opened with `?` (Rules K6, M4).

```
┏━ [2] HOSTS KEYS━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                               ┃
┃ 󰋘 ITEM OPERATION                              ┃  ← section title
┃  Enter     Connect — what it is, then in      ┃
┃  E         Edit — change this host            ┃
┃  X         Delete — remove from hosts.yaml    ┃
┃ 󰋘 PANEL OPERATION                             ┃
┃  A         Add — a new host                   ┃
┃  /         Search — name, user, host, port, … ┃  ← description too long (with the frame already at its widest)
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
  description. A description too long is cut at the end with `…`, never wrapped (except in the "Each row" section, see below).
  Keys are written as in Rules M5 (no
  brackets, no colon).
- **Rows from a menu**: the description reads `label — description`; the label loses its hotkey marks and keeps its case
  (a menu's `[E]dit` becomes `Edit — change this host`).
- **Sections**: section titles as in a menu (`nf-md-hexagon`, uppercase, Overlay0, indented one cell, not bold). On a panel they are, in order:
  - `what each row is` (optional, only on a panel of one value per row): see "Each row" below.
  - `item operation`, `panel operation`: as in the Space menu.
  - `move`: the movement keys that work here (Rules K12), only those that really do (e.g. `h|l` to switch tabs only
    with tabs). A one-dimensional list (a form, a one-value-per-row panel without tabs, a menu) shows `h|k` going back
    and `j|l` going on. Nothing is listed when there is nothing to act on (Rules M6): no movement keys on an empty list,
    no scrolling keys when the content fits.
  - `core keys`: the core keys that work on this panel — `Space`, `?`, `Tab`, `1–N` (with several panels, Rules K1),
    `q|Ctrl-C`; `Esc` only where it does something here (e.g. a filter to clear); `Enter` is not repeated, since
    `item operation` already says what it does here.
  - `app-wide`: the global hotkeys. Quitting's `q` is already listed in `core keys` and is not repeated here (as with
    `Enter`).
  - A section about **another surface** (Rules M6; e.g. the keys inside a PTY in the panel, titled `terminal`): last,
    after `app-wide`. The sections before it come in the same order on every panel, so `core keys` and `app-wide` stay
    where they are with or without it; users read "what can be pressed here" first, then "once inside".
- **Each row** (a panel of one value per row, optional): the key reference may start with a section saying what each
  row of the panel means. The left column is the setting's name in the plain text colour (Text, not the keys' Blue: it
  is not a key), the right column the explanation; the sections of keys come after it. Whether to have it, the app may
  decide for itself. A long explanation wraps in the right column ([the components' "Wrapping"](../README.md); the name column stays,
  the following rows start where the explanation starts) instead of being cut: the section is sentences to read, not a
  table to look up, and the key reference scrolls, so a long one can still be read in full.
- **On a popup** only that popup's own keys are listed (Rules K6): its hotkeys, `Enter`, `Esc`, the movement keys.
- **Colours**: keys in Blue, not bold; descriptions in Text. A key that cannot be pressed right now has both key and
  description in Surface2 (Rules M6).
- **Keys**: scrolling as above; `?` or `Esc` closes it, `Enter` does nothing. Hint `?|Esc:close`.

**Why**: the key reference is the only place that lists every key — the hint leaves out movement and the Space menu
lists only actions — so without the movement keys, `u|d` and `gg|G` would have nowhere to be learned (Principle P1).
Labels are not lowercased: that would break abbreviations such as `SSH config` and `YAML`, and the hotkey is already in
the key column on the left.

## note.6 Error popup

The note laid over a popup whose action failed (see the error row in [`layout/popup`](../layout/popup.md)). The whole
message opened with `Enter` on a form's error row is one too.

```
┏━󰈸 SAVE FAILED━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                 ┃
┃ hosts.yaml changed on disk since it was opened. ┃
┃                                                 ┃
┗━ Enter|Esc:close ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **Look**: frame and text in Red; the title capsule is filled Red with Base bold text (the capsule as in
  [`layout/popup`](../layout/popup.md)). The title glyph is `nf-md-fire` (U+F0238), the same as the Error toast. The
  message may have several rows, given by the app a row at a time ("Control characters" in
  [components](../README.md)), with no blank row between them; each wraps inside the frame (as in [the components'
  "Wrapping"](../README.md)); when too long it scrolls with `j|k`.
- **Title**: what failed (`RENAME FAILED`, `SAVE FAILED`). Opened from a form's error row, it is the field's name
  (`PORT`).
- **Closing**: both `Enter` and `Esc` close it, hint `Enter|Esc:close`.
- **After closing**: back to the popup underneath, the focus where it was, every value still there (Rules F4). Pressing
  `Enter` repeatedly, the first press closes it and the next is one more press where the focus was — on a form's button,
  a retry. The failed action changed nothing, so a retry at worst shows the error once more.

**Why**: an error popup is an error through and through, so its frame and text are Red; it is always on top and closes
with one key, so without the layer colour nobody is left wondering which layer it is. A popup with an error row is not
itself an error — only one value in it fails a rule — so its frame keeps the layer colour.

## note.7 App Log

Every app has an App Log (Rules F5): what the app has done and what went wrong, newest last. `!` on a panel opens it
(Rules K1); it is a viewer (the viewer's rules and its selection mode above apply), and while it is open new entries
keep arriving, as in streaming content.

```
14:02:11 INFO Switched to Pods
14:02:40 OK   Scaled deployment.apps/nginx
14:03:02 WARN CRD discovery: the server is currently unable to handle the request
14:03:30 ERR  Namespace fetch failed: Forbidden
```

- **What goes in**: what the user did and how it ended; every toast (the same words); what the app did on its own in
  the background (e.g. a move under Rules E3, a default made at start, the details of something outside the app that
  could not be read).
- **What the user did**: an item, panel or global operation of Rules P3, run from a menu, by a letter hotkey or by
  `Enter`; one that only looks without changing anything counts too (opening a viewer, switching screens: `Switched to
  Pods`). Moving the cursor, moving the focus (`Tab`, the number keys), opening the Space menu, `?` or `!` are not
  operations and go unrecorded; what is done inside a popup is not recorded on its own: the result of the operation it
  belongs to is. The panel filter ([`layout/panel`](../layout/panel.md)) goes unrecorded too: filtering only changes
  what is in view, like moving the cursor, and a record of it means nothing (the user, 2026-10-27, G103). An operation
  is done once it is accepted: cancelled with `Esc` at the confirm before it, or at the form or input popup that takes
  its values, it was not done and has no result, and goes unrecorded (a confirm is only a door, Rules T1; SS46).
- **Each entry**: the time `HH:MM:SS` (Overlay0), a level, and what happened, capitalised as in [`dialog/toast`](toast.md). The level
  follows the toast's kinds and colours: `INFO` Text, `OK` Green, `WARN` Peach, `ERR` Red, in a level column four cells
  wide, left-aligned.
- **Kept in memory only**: it is emptied when the app quits; the number of entries has a limit, and when it is full the
  oldest goes.
- **Errors and warnings not seen yet**: shown on the footer's `!` (the footer in [`layout/screen`](../layout/screen.md));
  opening the App Log counts as seeing them.

**Why**: a toast is gone in seconds, and someone who missed it never learns an error happened; the App Log keeps it.
Errors alone do not show what was done before them, and the entries just before are often the cause — so is what was
being looked at, so an operation that only looks is recorded too; what counts is drawn by the three kinds of operation
of Rules P3, the same set the menus list, so every app records the same range (demou DM41); what the app does
in the background can only be seen here. `!`, like `?` and `Space`, works in every app of the family. Memory only: what
matters is what happened while the app was open this time, with no further kind of thing to store and clean up.

## note.8 Compare

The popup the compare mode of a panel opens ([`layout/panel`](../layout/panel.md)): a viewer (the viewer's rules and its
selection mode above apply). The title glyph is `nf-md-compare` (U+F018A), the title `DIFF — <anchor> ↔ <the other>`;
two tabs follow it, `UNIFIED` and `SPLIT`, switched with `h|l` (Rules K12).

- **Only the parts that differ**, each with 3 unchanged lines before and after; a separator between parts (Overlay0, as
  the separators in a popup).
- **The anchor is the base**: the anchor is the removed side, the other the added side.
- **UNIFIED**: a removed line starts with `-`, in Red; an added line with `+`, in Green; an unchanged line with a space,
  in Text. Two line-number columns, the anchor's and the other's, the other column blank on a line found on one side
  only; line numbers in Overlay0.
- **SPLIT**: the anchor on the left, the other on the right, half each, each with its own line numbers; removed lines on
  the left in Red, added lines on the right in Green, a blank row where the other side has no counterpart. Not wrapped:
  what is wider than its half is cut with `…` at the end (the viewer's unwrapped content).
- **The choice is remembered** (state, Rules E3). On a terminal narrower than 96 it is always UNIFIED and `SPLIT` is
  disabled (Rules M6), whichever was remembered.

**Why**: text only, because a binary or an image has no line-by-line difference to look at. Only the parts that differ,
so a long content changed in one or two places shows them at once, with 3 lines around to tell where they are (`git
diff`'s default). Green for added and Red for removed is the common diff convention, and `+` and `-` keep it from
reading as an error. The two layouts are tabs: no extra key, and the title shows which one is on; side by side needs 96,
the same threshold as the finder. Identical ones only get a toast: the result fits in one sentence, with no extra `Esc`
to press.

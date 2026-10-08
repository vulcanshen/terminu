# note (read-only content)

**Language**: English · [繁體中文](note-zh_TW.md)

## Purpose

Read-only content that scrolls and may have hotkeys and modes of its own (Rules F1): the key reference, viewers (a YAML
view, the App Log, a file's content), the error popup, the typing explanation on a form ([`dialog/form`](form.md)). With
a list of options to run with `Enter`, it is a menu, not a note.

## Look

- The frame follows [`layout/popup`](../layout/popup.md): the padding above and below is always there, in a viewer too.
- **Title**: a glyph plus what is shown (e.g. `YAML — pod/nginx`). The glyph is the app's choice; the glyphs of the key
  reference and the error popup are below.
- **Scroll position**: when the content does not fit, the right end of the bottom border shows the visible lines,
  `N-M of T`.
- **Width**: notes whose content is known when they open (the key reference, the error popup, explanations) follow the
  content; a viewer's content width is not known, so it takes the Rules F7 cap.

## Keys

- Scrolling: `j/k`, `u/d`, `gg/G` (Rules K12); in a text selection mode, `w/b/e` and `0/$` as well.
- **Closed with `Esc` only**. `Enter` does not close it; nor does `Space` (Rules K5).
- **The exception: the ones that pop up by themselves** — the error popup and the typing explanation on a form — close
  on `Enter` too.
- **Hint**: the note's own hotkeys first, `Esc:close` last. E.g. `y:copy /:search v:visual Esc:close`.

**Why**: for a note the user opened, `Esc` after reading is the most natural; `Space` pages down in readers such as
`less` and `man`, and someone used to them presses `Space` on a note to page down, only to have the note close. When the
two that pop up by themselves appear, the user's hands are typing or about to submit, and `Enter` is a reflex; with
`Enter` closing them too, that press is not lost, and nothing else on them would be set off by `Enter`.

## Key reference

The "what keys work here" opened with `?` (Rules K6, M4).

```
╭─ [2] Hosts keys ──────────────────────────────╮
│                                               │
│ item operation                                │  ← section title
│  Enter    connect — what it is, then in       │
│  E        edit — change this host             │
│  X        delete — remove from hosts.yaml     │
│ panel operation                               │
│  A        add — a new host                    │
│  /        search — name, user, host, port, …  │
│ core keys                                     │
│  Space    what you can do here                │
│  ?        this list                           │
│ app-wide                                      │
│  M        manage — hosts, credentials, …      │
│                                               │
╰─ ?/Esc:close ──────────────────── 1-12 of 20 ─╯
```

- **Title**: `nf-fa-question_circle` (U+F059) plus `<surface> keys`, e.g. `[2] Hosts keys`, `Space menu keys`.
- **One key per row**: indented two cells, the key padded to the width of the widest key, two blank cells, then the
  description. A description too long is cut at the end with `…`, never wrapped. Keys are written as in Rules M5 (no
  brackets, no colon).
- **Rows from a menu**: the description reads `label — description`.
- **Sections**: section titles as in a menu (Overlay0, indented one cell, not bold). On a panel they are, in order,
  `item operation`, `panel operation` (as in the Space menu), `core keys`, `app-wide` (global hotkeys); on a popup only
  that popup's own keys are listed (Rules K6).
- **Colours**: keys in Blue, not bold; descriptions in Text. A key that cannot be pressed right now has both key and
  description in Surface2 (Rules M6).
- **Keys**: scrolling as above; `?` or `Esc` closes it, `Enter` does nothing. Hint `?/Esc:close`.

## Error popup

The note laid over a popup whose action failed (see the error row in [`layout/popup`](../layout/popup.md)). The whole
message opened with `Enter` on a form's error row is one too.

```
╭─ Save failed ───────────────────────────────────╮
│                                                 │
│ hosts.yaml changed on disk since it was opened. │
│                                                 │
╰─ Enter/Esc:close ───────────────────────────────╯
```

- **Look**: frame, title and text in Red. The title glyph is `nf-md-fire` (U+F0238), the same as the Error toast. The
  message wraps inside the frame; when too long it scrolls with `j`/`k`.
- **Title**: what failed (`Rename failed`, `Save failed`). Opened from a form's error row, it is the field's name
  (`Port`).
- **Closing**: both `Enter` and `Esc` close it, hint `Enter/Esc:close`.
- **After closing**: back to the popup underneath, the focus where it was, every value still there (Rules F4). Pressing
  `Enter` repeatedly, the first press closes it and the next is one more press where the focus was — on a form's button,
  a retry. The failed action changed nothing, so a retry at worst shows the error once more.

**Why**: an error popup is an error through and through, so its frame and text are Red; it is always on top and closes
with one key, so without the layer colour nobody is left wondering which layer it is. A popup with an error row is not
itself an error — only one value in it fails a rule — so its frame keeps the layer colour.

# finder (a list with search)

**Language**: English · [繁體中文](finder-zh_TW.md)

## Purpose

A popup of a list with search: typing on top filters, the list below is chosen from. A plain finder means "go there"
(filu's Search, Find and Goto, webu's `/`).

These are all kinds of finder, each writing only what differs from here:

| Kind | What |
|---|---|
| [`select`](select.md) | choose one value (a slider's list of numbers and a color picker's 00–FF too) |
| the popup of [`checkbox`](checkbox.md) | choose several values |
| [`file-picker`](file-picker.md) | choose a file |

A list without search is a menu ([`dialog/menu`](../dialog/menu.md)). Filtering by typing straight into a panel is the
panel filter ([`layout/panel`](../layout/panel.md)), whose typing row has the same keys as here.

## Look

Terminal width 96 or more (e.g. 96×24):

```
┏━SEARCH━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ ┏━README.md━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                            ┃ ┃                                             ┃
┃  read                                3/41 ┃ ┃  1 # terminu                                ┃
┃ ────────────────────────────────────────── ┃ ┃  2                                          ┃
┃▓README.md▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃ ┃  3 The terminal UI you can use without      ┃
┃ README-zh_TW.md                            ┃ ┃  4 reading a manual first.                  ┃
┃ docs/readme-notes.md                       ┃ ┃  5                                          ┃
┃                                            ┃ ┃  6 ## Principle                             ┃
┃                                            ┃ ┃  7                                          ┃
┃                                            ┃ ┃  8 Every action can be found from the menu. ┃
┃                                            ┃ ┃  9                                          ┃
┃                                            ┃ ┃ 10 ## Components                            ┃
┃                                            ┃ ┃ 11                                          ┃
┃                                            ┃ ┃ 12 Frames, popups, inputs and dialogs.      ┃
┃                                            ┃ ┃ 13                                          ┃
┃                                            ┃ ┃ ─────────────────────────────────────────── ┃
┃                                            ┃ ┃ TYPE      text                              ┃
┃                                            ┃ ┃ SIZE      4.2 KB                            ┃
┃                                            ┃ ┃ MODIFIED  2026-10-10 09:12                  ┃
┃                                            ┃ ┃ MODE      -rw-r--r--                        ┃
┃                                            ┃ ┃                                             ┃
┗━ Enter|Tab:list Esc:cancel ━━━━━━━━━━━━━━━━┛ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

Terminal width under 96 (e.g. 80×24):

```
┏━SEARCH━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ ┏━INFO━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                    ┃ ┃                                     ┃
┃  read                        3/41 ┃ ┃ TYPE      text                      ┃
┃ ────────────────────────────────── ┃ ┃ SIZE      4.2 KB                    ┃
┃▓README.md▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃ ┃ MODIFIED  2026-10-10 09:12          ┃
┃ README-zh_TW.md                    ┃ ┃ MODE      -rw-r--r--                ┃
┃ docs/readme-notes.md               ┃ ┃                                     ┃
┃                                    ┃ ┃                                     ┃
┃                                    ┃ ┃                                     ┃
┃                                    ┃ ┃                                     ┃
┗━ Enter|Tab:list Esc:cancel ━━━━━━━━┛ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
┏━README.md━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                                            ┃
┃  1 # terminu                                                               ┃
┃  2                                                                         ┃
┃  3 The terminal UI you can use without                                     ┃
┃  4 reading a manual first.                                                 ┃
┃  5                                                                         ┃
┃  6 ## Principle                                                            ┃
┃  7                                                                         ┃
┃                                                                            ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **Two areas**: the typing row on top, the list below, a separator between them (not joining the border,
  [`layout/popup`](../layout/popup.md)).
  - The typing row starts with `nf-fa-angle_right` (U+F105), one cell from the border, then one space before the typed
    text (its width as the icon width of Rules E5): it says at a glance that this row is where typing filters, and the
    row is not a blank strip when the finder opens on the list with nothing typed. It is a glyph, not a placeholder
    ([`input/README`](README.md)). Its colour follows the row: Overlay0 like the whole row with the focus on the list,
    the layer colour with the focus on the typing row.
  - The filtered count `matches/total` (`3/41`) sits on the right of the typing row, in Overlay0: it is supporting
    information and does not compete with the typed text; with the focus on the list the whole row is Overlay0
    anyway, so the number never changes colour.
- **The preview**: a plain finder always has one (a select and a checkbox popup do not: a value has no content to
  preview). The chosen entry is previewed alongside.
  - **When it previews a file or a directory** (e.g. filu's Search, Find and Goto), it follows the preview of
    [`file-picker`](file-picker.md): the content, the four metadata rows and `hide_secrets_in_preview` all the same. Any
    other preview (e.g. a stretch of a page) is given by the app and has no metadata.
  - **Layout**: the list and the preview together take one popup's width (the maximum of Rules F7).
    - Terminal width 96 or more: side by side, half each. With metadata, the right box is "preview / separator /
      metadata".
    - Under 96, with metadata: the top row is the list box and the metadata box, half each (as wide as side by side);
      below them the preview box takes the full width; top and bottom take half the height each. The metadata has a
      box of its own, titled `INFO`. At 80×24 the list shows 5 entries and the preview 7 rows.
    - Under 96, without metadata: stacked, the list on top and the preview below, half each.
  - The preview box's title is the chosen entry's name (or where it is); the preview takes no focus.
  - The preview box's border and title capsule are in the layer colour (like the list box); its content is not
    dimmed (the preview is there to be read, and dimmed it is hard to read); its bottom border carries no text (no hint, no scroll position).
- **Listed while searching**: results are listed as they arrive, with a loading icon after the title; while none has
  arrived it reads `(indexing…)`.
- **Size**: a finder with a preview always takes the maximum height of Rules F7 (the screen height − 2): each entry's
  preview has a different length, so the height cannot be known when it opens; at the maximum the frame never jumps
  from entry to entry and the preview gets the most room; a short list leaves space below. A finder without a preview
  (a select, a checkbox popup) has its height fixed when it opens (F7). The width is not known, so it takes the
  maximum of F7.

### Markers in the list

Every row of a select and of a checkbox popup starts with a marker:

| | Before every row | The current value |
|---|---|---|
| **select (one)** | a radio glyph: chosen `nf-md-radiobox_marked` (U+F043E), not chosen `nf-md-radiobox_blank` (U+F043D) | text in Green |
| **checkbox popup (several)** | a checkbox glyph: ticked `nf-md-checkbox_marked` (U+F0132), not ticked `nf-md-checkbox_blank_outline` (U+F0131) | text in Green |

- A marker on the left is found by running the eye down the list; every row's text lines up; the current value has a
  colour (Green in [`color`](../color.md) is "in effect"). With the cursor on the current value, the background is the
  cursor's and the text the cursor's Base.
- **Green follows the tick and the dot on screen**: in a checkbox popup a row turns Green as soon as `Space` ticks it,
  and stops being Green when unticked, before `Enter` as well. In a popup, Green reads "this is the value `Enter`
  gives": the tick and the colour always agree, so there are never two signals to read; `Esc` goes back to the old
  value.
- One-of-many uses radio glyphs, several-of-many checkbox glyphs: the glyph tells which, whether drawn in a form or in a
  popup.

## States

Only the area holding the focus is lit (Principle P6, Rules F1). This means the two areas the focus can rest on (the
typing row and the list); the preview never takes the focus, is not one of them, and is always drawn as "The
preview" above says:

| Focus on | Typing row | The list's cursor |
|---|---|---|
| Typing row | drawn as an input's typing row: the value Lavender, with a cursor; the icon before it in the layer colour | the layer colour cursor, dimmed once more |
| List | the whole row drawn in grey (Overlay0), the icon and the count included, no cursor | layer colour background, Base bold, the arrow in its right padding (like a menu's cursor) |

## Keys

### Typing row

The panel filter uses this table too.

| Key | Does |
|---|---|
| Characters | typed in, the list filtering at once (the input state, Rules K8; editing keys as in [`input/README`](README.md)) |
| `↑\|↓` | move the cursor between results, wrapping at the ends (arrow keys type no characters, so there is no clash) |
| `Enter` | moves the focus to the item under the cursor without running it; with no results it does nothing |
| `Tab` | moves the focus to the list |
| `Esc` | closes the whole finder (Rules F1: a phase is not a layer); in the panel filter it clears the filter |

### Matching

How what is typed on the typing row filters. The same for a plain finder, a select, a checkbox popup, plain text typed in
a file-picker, and the panel filter:

- **Contains**: case-insensitive, and what is typed must appear unbroken in the item. E.g. `prod` matches `Prod-Web-01`;
  `db-replica-tokyo-ap-northeast-1`, which only holds p, r, o, d in that order, does not.
- **Several words**: each word separated by spaces must appear, in any order. E.g. `prod 22` finds `prod-web-01` on
  port 22 (across columns in a panel).
- **Order**: the results keep the list's own order and are not reordered. Numbers sort by value (`9` before `10`), text
  as text (the header in [`layout/panel`](../layout/panel.md)).

**Why**: only an unbroken match filters; a match that counts letters merely appearing in order leaves heaps of unrelated
items, which then need reordering by score to push the wanted one to the front. Keeping the list's order keeps its
sorting (a panel header's sort marker) true; numbers and text take the same matching: `20` leaves 20, 120, 200–209,
in order of size ([`slider`](slider.md)).

### List

| Key | Does |
|---|---|
| `j\|k` and the like | move (Rules K12: stepping wraps at the ends) |
| `Enter` | goes there (a select chooses, a checkbox popup applies, a file-picker chooses the file or goes into the directory) |
| `Tab\|/` | back to the typing row, typing on after the old text |
| `Esc` | closes the whole finder |

### Hint

| Focus on | Hint |
|---|---|
| Typing row | `Enter\|Tab:list Esc:cancel` |
| List | `Enter:<the verb for going there> Tab\|/:filter Esc:cancel` (e.g. `Enter:open`) |

**Why**: `Enter` on the typing row first focuses the item, and only a second press runs it: going from the typing row
back to the list never opens anything by the way. The cost is one more `Enter`; the fzf / VS Code quick-open way, "`Enter`
while typing goes straight there", is not taken — a finder's typing row and the panel filter are the same kind of typing
row, and one key needing a different number of presses in each is not remembered.

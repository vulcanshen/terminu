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

```
╭─ Search ────────────────────────────╮ ╭─ README.md ───────────────────────╮
│                                     │ │                                   │
│  read                          3/41 │ │ # terminu                         │
│ ─────────────────────────────────── │ │                                   │
│ ▓README.md▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ │ │ The terminal UI you can use…      │
│  README-zh_TW.md                    │ │                                   │
│  docs/readme-notes.md               │ │                                   │
│                                     │ │                                   │
╰─ Enter/Tab:list Esc:cancel ─────────╯ ╰───────────────────────────────────╯
```

- **Two areas**: the typing row on top, with the filtered count `matches/total` on its right (`3/41`); a separator (not
  joining the border, [`layout/popup`](../layout/popup.md)); the list below.
- **The preview**: a plain finder always has one (a select and a checkbox popup do not: a value has no content to
  preview). The chosen entry is previewed alongside.
  - The list box and the preview box together take one popup's width (the maximum of Rules F7). With a terminal width
    of 96 or more they sit side by side, half each; otherwise they stack, the preview below.
  - The preview box's title is the chosen entry's name (or where it is); the preview takes no focus. What the preview
    shows is the app's choice (a file's content, a directory tree, a stretch of a page).
- **Listed while searching**: results are listed as they arrive, with a loading icon after the title; while none has
  arrived it reads `(indexing…)`.
- **Size**: the height is fixed when it opens (Rules F7); the width is not known, so it takes the maximum of F7.

### Markers in the list

Every row of a select and of a checkbox popup starts with a marker:

| | Before every row | The current value |
|---|---|---|
| **select (one)** | a radio glyph: chosen `nf-md-radiobox_marked` (U+F043E), not chosen `nf-md-radiobox_blank` (U+F043D) | text in Green |
| **checkbox popup (several)** | a checkbox glyph: ticked `nf-md-checkbox_marked` (U+F0132), not ticked `nf-md-checkbox_blank_outline` (U+F0131) | text in Green |

- A marker on the left is found by running the eye down the list; every row's text lines up; the current value has a
  colour (Green in [`color`](../color.md) is "in effect"). With the cursor on the current value, the background is the
  cursor's and the text the cursor's Base.
- One-of-many uses radio glyphs, several-of-many checkbox glyphs: the glyph tells which, whether drawn in a form or in a
  popup.

## States

Only the area holding the focus is lit (Principle P6, Rules F1):

| Focus on | Typing row | The list's cursor |
|---|---|---|
| Typing row | drawn as an input's typing row: the value Lavender, with a cursor | the layer colour cursor, dimmed once more |
| List | the whole row drawn in grey (Overlay0), no cursor | layer colour background, Base bold (like a menu's cursor) |

## Keys

### Typing row

The panel filter uses this table too.

| Key | Does |
|---|---|
| Characters | typed in, the list filtering at once (the input state, Rules K8; editing keys as in [`input/README`](README.md)) |
| `↑`/`↓` | move the cursor between results (arrow keys type no characters, so there is no clash) |
| `Enter` | moves the focus to the item under the cursor without running it; with no results it does nothing |
| `Tab` | moves the focus to the list |
| `Esc` | closes the whole finder (Rules F1: a phase is not a layer); in the panel filter it clears the filter |

### List

| Key | Does |
|---|---|
| `j`/`k` and the like | move (Rules K12) |
| `Enter` | goes there (a select chooses, a checkbox popup applies, a file-picker chooses the file or goes into the directory) |
| `Tab` | back to the typing row |
| `/` | back to the typing row, typing on after the old text |
| `Esc` | closes the whole finder |

### Hint

| Focus on | Hint |
|---|---|
| Typing row | `Enter/Tab:list Esc:cancel` |
| List | `Enter:<the verb for going there> Tab:filter Esc:cancel` (e.g. `Enter:open`) |

**Why**: `Enter` on the typing row first focuses the item, and only a second press runs it: going from the typing row
back to the list never opens anything by the way. The cost is one more `Enter`; the fzf / VS Code quick-open way, "`Enter`
while typing goes straight there", is not taken — a finder's typing row and the panel filter are the same kind of typing
row, and one key needing a different number of presses in each is not remembered.

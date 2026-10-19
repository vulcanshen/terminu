# terminu components

**Language**: English · [繁體中文](README-zh_TW.md)

terminu components are the component specs under [tdp](../principle/README.md): the colour scheme, the screen, panels,
the frame floating over the screen, and each kind of content in that frame — what each looks like and how it is operated.
The principle gives the principles and rules; the components give the concrete parts. Versions and the CHANGELOG are
shared with tdp.

## What is a requirement

Everything written here is a requirement. Only four things are not: the parts stated as "up to the app", examples
(however they are introduced: "e.g.", "for example", "Example:", "such as", an "Examples" column), the "Why", and
paragraphs marked "Implementation reference (not a requirement)".

All of the components are in the fixed zone (["Departure" at the start of the Rules](../principle/rules.md)): what an app
cannot follow goes into the "偏離 tdp" (departures from tdp) section of its dev-remarks with the reason, and is reported
as a gap in tdp at the same time.

## Diagrams and spacing

- **A diagram's structure is a requirement; the data in it are examples**: frames, where glyphs go, spacing, alignment
  and the colours noted beside it are as drawn; names, values and descriptions are examples.
- **Where the text and a diagram disagree, the text wins**; two diagrams that disagree with each other are a bug in the
  spec, to be reported and fixed when found.
- **Numbers that cannot be counted, or are hard to count, are written in the text** (e.g. the minimum gap between a menu
  label and its description, which decides the popup's width).
- **"Indented N cells" means N cells in from the frame**: counted inward from the frame line, the line itself not
  counted (e.g. the key reference's "each row is indented two cells": the text starts on the third cell inside the frame
  line).
- **Nerd Font glyphs in a diagram are drawn with their real code points** (capsule ends, the arrow at the end of a
  cursor, the hexagon of a section title, the loading icon and so on), and every one of them is named by its code point
  in the text; where there is no Nerd Font they show as boxes. Backgrounds cannot be drawn: `▓` stands for a cursor
  block, and a capsule's fill is in the text. In a popup whose title glyph is chosen by the app (the glyph table in
  [`layout/popup`](layout/popup.md)), the diagram draws no glyph; in fact the glyph goes before the title text, with one
  space.
- **Two general rules**, which hold wherever the text says nothing else:
  - **Two cells between columns**: a label and its value, a label and its description, the columns of a table, items
    side by side.
  - **One cell between a glyph and the text after it** (e.g. `󰈔 id_ed25519`, a radio's `󰐾 password`).
- **The statusbar's `label: value` does not follow the two-cell rule**: it is written like a sentence, one space after
  the colon (`[C]ontext: prod  [N]amespace: default`); two cells between groups, with no separator symbol (the statusbar in
  [`layout/screen`](layout/screen.md)).

**Why**: spacing is something users see; left to the implementation, the same thing ends up a cell or two off across the
family, and the spec is no longer the one source to go by. Two general rules are easy to remember and carry over to new
components: two cells keep two columns apart (a label and its value are in different colours anyway); a glyph with only
one cell after it reads as one unit with its text. The statusbar's `label: value` is a phrase: the colon already parts the
label from the value, and two cells there would break it in two; two cells between groups are enough to keep them apart
without drawing a symbol as well.

## Wrapping

Wherever text wraps — a textarea, a viewer, a confirm, a note (e.g. a form's typing note), a toast, an error popup, an
empty state's sentence, the Rules S5 splash when too narrow — it wraps the same way, and what does not fit wraps rather
than being cut:

- **Break between words**: when the next word does not fit on the row, the whole word goes to the next row (e.g. an
  English word moves whole).
- **A break may fall between any two wide characters** (two cells, e.g. Chinese, Japanese): the place between a wide
  character and the character before or after it counts as a break too, so such text fills a row before going on.
- **Only a word wider than a row on its own** (e.g. a long URL) is cut by cells; when the row already has text before
  it, it starts a new row first and is cut there, not cut on after that text.
- **A wide character is never cut in half**: when cutting by cells leaves one cell on a row, that wide character goes
  whole to the next row.
- **The space at a break**: in a textarea and a viewer every character is drawn (the text cursor and the selection
  mode stop on it), so when a word fills a row exactly and a space follows, that space is drawn in the next row's first
  cell; text that is only shown (a confirm, a note, a toast, an error popup, an empty state, the splash) does not draw
  the space it breaks at.

```
see                     ← a row of 20 cells: the URL does not fit, so it starts a new row
https://example.com/    ← cut by cells from the start of the new row
very/long/path/abc
```

**Why**: text broken in the middle of a word can't be read; the splash already breaks this way (Rules S5). With one
rule, text wraps the same wherever it wraps in the family. A long word starting a new row before it is cut is the same
idea as "a word that does not fit moves whole to the next row": the URL begins a row of its own, easy to recognise and
to copy, not half of it hanging after the words before it.

## Uppercase

- **In uppercase**: a panel's capsules (`[N] label` and tabs), screen chips, popup titles, table headers, group titles
  in lists, the labels of a panel with one value per row, and the section titles of menus and the key reference.
- **Unchanged**: values, menu labels and descriptions, the descriptions in hints and the footer, key names, mode names,
  and the app's own content (the statusbar, the data in lists).
- **The letters in a hotkey marker stay as written**: what is printed in the brackets is the key to press, and case
  counts (Rules M5) — `[M]anage` becomes `[M]ANAGE`, `[m]anage` becomes `[m]ANAGE`.
- **Names and paths are content and keep their case, in a title and in a hint**: the titles `EDIT: filu`,
  `ALTERM: myhost`, `IDENTITY FILE · ~/.ssh` (what goes before the name: "Title" in [`layout/popup`](layout/popup.md));
  a form button's hint lowers only its verb, `Overwrite KBU.svg` → `Enter:overwrite KBU.svg` (the hint in
  [`dialog/form`](dialog/form.md)).
- **A panel's title too**: the label is split into "what this is" (uppercase) and a name (as it is), joined the way a
  popup title joins them — `[2] PODS: nginx-7d4f`; a label that is all name stays as it is — `[1] prod-web-01` (the
  capsule chain in [`layout/panel`](layout/panel.md)).

**Why**: what is in uppercase says "what this is" — names, titles, column names — and stands apart at a glance from
the content there is to read or change. Key names and hotkey markers stay: `q` and `Q` are different keys; content
stays: users recognise it as it is.

## Choosing among the options

Fields differ in nature — long or short values, few or many options — and so does the look that suits them. So the
components do not fix everything to one form; they list **a few options**, and the app picks by the nature of the field.
The choice is limited to the listed options: when none of them fits, that is a gap in tdp — report it and an option is
added, rather than inventing one inside the app.

## How to read

Read in order: **color → layout (screen, panel, popup) → dialog → input**. color and layout are the common base: every
component uses the colour scheme, and is drawn on the screen, in a panel or in a frame; dialog and input are what goes in
the frame.

## Three nouns

| Noun | What | File |
|---|---|---|
| **popup** | a frame floating over the screen: where the title, hint, padding, content area, scrolling and error row go. It sets only the look of the frame, not what goes in it | `layout/popup` |
| **input** | a kind of popup: enters or chooses one value and, once confirmed, writes it back. One file per kind of value | `input/` |
| **dialog** | a kind of popup that is not entering one value but the app talking to the user — a form, a list, a confirmation, read-only content, a message, a subprocess | `dialog/` |

- The seven classes of rules F1: the input class maps to `input/`, the other six to `dialog/`, one file each.
- Nothing is typed into a form (`dialog/form`): a field that takes typing or has more options than fit opens its value's
  input popup on `Enter`; a radio or checkbox with few options has them drawn in the form and is chosen in place.
- A list with search is a finder: a plain finder, a select, a checkbox popup and a file-picker are all kinds of finder
  (`input/finder`). A list without search is a menu (`dialog/menu`), except the
  reorder that puts items in order (`input/reorder`).
- Dialog rather than modal: modal names a behaviour — blocking what is underneath while open — and every popup but the
  toast does that, so it would not tell inputs from dialogs; dialog names the content — the app talking to you.

## color

| File | What |
|---|---|
| [`color`](color.md) | The colour scheme: presentation rules, calculation, colour codes |

## layout

| File | What |
|---|---|
| [`screen`](layout/screen.md) | The whole screen: footer, screen chip row, statusbar, narrow widths, zoom, smaller than the minimum size, empty states |
| [`panel`](layout/panel.md) | Panels: frame, lists, the location row, one value per row, panel filter |
| [`popup`](layout/popup.md) | The frame floating over the screen |

## dialog

| File | What |
|---|---|
| [`form`](dialog/form.md) | a form: several values filled in and submitted together |
| [`menu`](dialog/menu.md) | choose a row from a list and run it |
| [`confirm`](dialog/confirm.md) | one question, `Enter` accepts, `Esc` cancels |
| [`note`](dialog/note.md) | read-only content: the key reference, viewers, the error popup |
| [`toast`](dialog/toast.md) | a short message popping up from the bottom |
| [`terminal`](dialog/terminal.md) | a subprocess running in a frame |

## input

Each is a popup that enters or chooses that kind of value.

| File | What |
|---|---|
| [`README`](input/README.md) | rules shared by every input |
| [`text`](input/text.md) | single-line text |
| [`password`](input/password.md) | masked input |
| [`number`](input/number.md) | number |
| [`textarea`](input/textarea.md) | multi-line text |
| [`finder`](input/finder.md) | a list with search; select, the checkbox popup and file-picker are kinds of it |
| [`select`](input/select.md) | choose one value from a list |
| [`radio`](input/radio.md) | one of a few, drawn in a form |
| [`checkbox`](input/checkbox.md) | a switch, or ticking several |
| [`slider`](input/slider.md) | a value in a range |
| [`datetime-picker`](input/datetime-picker.md) | date and time |
| [`color-picker`](input/color-picker.md) | colour |
| [`file-picker`](input/file-picker.md) | choosing a file; it also comes in a kind for choosing a directory |
| [`reorder`](input/reorder.md) | moving items by hand into an order |

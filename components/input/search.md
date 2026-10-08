# search (search and filter)

**Language**: English · [繁體中文](search-zh_TW.md)

## Purpose

Two forms: the **finder** (a popup: a typing row, a result list and a preview; filu's Search, Find and Goto, webu's `/`)
and **the search row typed into a panel** (see [`layout/panel`](../layout/panel.md)). [`file-picker`](file-picker.md) is a
kind of finder.

## Look

**The finder's skeleton** (settled by the user, 2026-10-07; shared by file-picker):

- **Two areas**: the typing row on top (the result count on its right), a separator, the result list below. `Tab`
  switches between them.
- **The preview is required** (the user): the chosen result is previewed alongside. At a width of 96 or more the list and
  the preview sit side by side, stacked otherwise; the preview's title is the chosen result's name (or where it is), and
  the preview takes no focus. What it shows is the app's (a file's content, a directory tree, a stretch of a page). Today:
  the finders of filu and webu already work this way.
- **Results listed as they come**: arriving results are listed at once, with a loading icon after the title; while
  nothing has arrived it reads `(indexing…)` (filu).
- The height is fixed when it opens (F7).

## States

- **Finder focus** (Rules F1; moved here from defaults D3 on 2026-10-07): while typing, the filter row is lit and the
  list's cursor row is a faint highlight; after `Tab` to the list, the filter row is drawn all in grey (Overlay0, [`color`](../color.md)'s dim
  text) rather than F8's fade, with no highlight or cursor, and the list's cursor row turns to the popup's layer colour
  behind dark bold text (like a menu's cursor row). Only the side holding the keys is lit, the same language as F8's
  "only the top is lit" (kbu `40a0573`).

## Keys

**The finder** (settled by the user, 2026-10-07):

- **`Enter` while typing** moves the focus to the highlighted result in the list, without running it; with no results it
  does nothing.
- **`Enter` on the list** goes there (a file-picker chooses the file, see its file).
- `Tab` switches between the areas; `Esc` closes the whole finder (F1: a phase is not a layer).
- Why: the same principle as the panel search row (the user: "`Enter` first focuses the item; to run it, press again") —
  a finder's typing row and a panel's search row are the same kind of input, and one key needing a different number of
  presses in each is not remembered. The cost is one more `Enter`; the fzf / VS Code quick-open way, "`Enter` while typing
  goes straight there", is not taken.
- Today: webu works this way; filu goes straight there on `Enter` while typing, and changes. filu's way was the user's
  ruling of 2026-09-28 (from "`Enter` hands over to the list" to "picks at once"; rules F1 said "`Enter` submits the
  chosen one"); when I raised the clash, the user confirmed going back to "`Enter` enters the list" — filu's way is not
  good. F1 is changed.
- The search row typed into a panel is in [`layout/panel`](../layout/panel.md).

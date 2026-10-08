# menu (choose a row from a list)

**Language**: English · [繁體中文](menu-zh_TW.md)

Look and keys moved here from defaults D4 on 2026-10-07 (from a default to a requirement).

## Purpose

Choosing a row from a list and running it (F1): the Space menu, the global operation popup, option lists, task lists (`Enter` opening a row's full text).

## Look

- Menu rows: ` [k]label` left-aligned, description right-aligned and dim.
- If the hotkey is the label's first letter, bracket it in place (`[r]ename`); if it is inside the word, bracket it there
  (`UR[L]`); otherwise put it in front (`[n] New`). Core keys are written into the label: `[Enter] Edit`.
- A label that already shows its key (`[/] Search`) is not bracketed again.
- The cursor row: the popup's layer colour as background, dark bold text (defaults D3's finder paragraph says "like a
  menu's cursor row").
- The menu title is the focused panel's `[N] label`.
- Popup width follows Rules F7 throughout; a description too long for it wraps or is cut inside the box, never widening
  the box.

## Keys

- `j/k` move (wrapping), `Enter` runs, hotkeys run directly; bottom hint `Enter:run Esc:close` (no movement keys, see the hint in
  [`layout/popup`](../layout/popup.md); D4 had `j/k:move Enter:run Esc:close`).

# menu (choose a row to run)

**Language**: English · [繁體中文](menu-zh_TW.md)

## Purpose

A list without search, choosing a row to run it (Rules F1): the Space menu, the global operation popup, a sort picker, a
jobs list (`Enter` opening the row's full text). A list that needs search is a finder
([`input/finder`](../input/finder.md)); choosing a value to be written back is a select
([`input/select`](../input/select.md)).

## Look

```
╭─ ≡ [2] Hosts ─────────────────────────────────╮
│                                               │
│ item operation                                │  ← section title
│▓[Enter] Connect▓▓▓▓▓▓▓▓▓▓▓what it is, then in▓│  ← cursor
│ [E]dit                       change this host │
│ [X] Delete             remove from hosts.yaml │
│ ───────────────────────────────────────────── │  ← separator
│ panel operation                               │
│ [A]dd                              a new host │
│ [/] Search          name, user, host, port, … │  ← description too long
│ ───────────────────────────────────────────── │
│ Global operation    actions for the whole app │
│                                               │
╰─ Enter:run Esc:close ─────────────────────────╯
```

(`≡` stands for `nf-fa-bars`.)

- **Each row**: the label in Text, `[x]` in the label's colour; how hotkeys are marked is in Rules M5. The description in
  Overlay0, right-aligned, one cell from the right border; when too long it is cut at the end with `…` (M5: one line).
- **Section titles**: Overlay0, indented one cell, not bold; the cursor skips them.
- **Separators**: drawn like the separator in [`layout/popup`](../layout/popup.md) (not joined to the border, Overlay0);
  the cursor skips them.
- **The cursor**: the layer colour as background, bold Base text, filling the whole inner width; the whole row is in
  Base.
- **Disabled rows**: the whole row in Surface2; the cursor skips them, and their hotkeys do nothing (Rules M6).
- **Title**: `nf-fa-bars` plus text. The Space menu shows the focused panel's `[N] label` (what it lists is what that
  panel can do); any other menu says what it does (`Global operation`, `Sort by`).
- **The `Global operation` row** (Rules M2): no hotkey, and the description is always `actions for the whole app`.
- **Width**: every row is known when it opens, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).

**Why**: with descriptions right-aligned, names and descriptions form two columns, and the eye running down the names is
not interrupted by the descriptions. The cursor takes the layer colour as background: in a family popup, the block on the
layer colour is where `Enter` acts (in a form too).

## Keys

- `j/k` move, wrapping at both ends; `u/d` half a page, `gg/G` to the top and the bottom (Rules K12).
- `Enter` runs the cursor row; a hotkey runs its row directly.
- `Esc` closes it (the global operation popup returns to the Space menu, Rules F4); the Space menu also closes on another
  `Space` (Rules K5).
- **Hint**: `Enter:run Esc:close` (no movement keys, see the hint in [`layout/popup`](../layout/popup.md)).

# menu (choose a row to run)

**Language**: English · [繁體中文](menu-zh_TW.md)

## Purpose

A list without search, choosing a row to run it (Rules F1): the Space menu, the global operation popup, a sort picker, a
jobs list (see "Jobs list" below). A list that needs search is a finder
([`input/finder`](../input/finder.md)); choosing a value to be written back is a select
([`input/select`](../input/select.md)); moving items by hand into an order is a reorder
([`input/reorder`](../input/reorder.md)).

## Look

```
┏━ [2] HOSTS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                               ┃
┃ 󰋘 ITEM OPERATION                              ┃  ← section title
┃▓[Enter] Connect▓▓▓▓▓▓▓▓▓▓▓what it is, then in┃  ← cursor
┃ [E]dit                       change this host ┃
┃ [X] Delete             remove from hosts.yaml ┃
┃ ╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌ ┃  ← separator
┃ 󰋘 PANEL OPERATION                             ┃
┃ [A]dd                              a new host ┃
┃ [/] Search          name, user, host, port, … ┃  ← description too long (with the frame already at its widest)
┃ ╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌ ┃
┃ Global operation    actions for the whole app ┃
┃                                               ┃
┗━ Enter:run Esc:close ━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

(The glyph before a section title is `nf-md-hexagon`.)

- **Each row**: the label in Text, `[x]` in the label's colour; how hotkeys are marked is in Rules M5. The description in
  Overlay0, right-aligned, against the right padding (normally one cell from the right border); when too long it is cut at the end with `…` (M5: one line). At least two cells between the label and the description:
  this decides the widest row, and so the popup's width.
- **Section titles**: an `nf-md-hexagon` (U+F02D8), one space, then the title in uppercase ("Uppercase" in the
  [components](../README.md)). Overlay0, indented one cell (one cell from the frame, in the same column as the rows'
  text), not bold; the cursor skips them.
- **Separators**: between sections, the double dash `╌` (U+254C); otherwise drawn like the separator in
  [`layout/popup`](../layout/popup.md) (not joined to the border, Overlay0); the cursor skips them.
- **The cursor**: the layer colour as background, bold Base text, running from frame to frame (covering the left and
  right padding) with the text still one cell from the frame; the whole row is in Base. Its right padding is the
  arrow U+E0B0 in the layer colour (the cursor block in [`layout/popup`](../layout/popup.md)).
- **Disabled rows**: the whole row in Surface2; the cursor skips them, and their hotkeys do nothing (Rules M6).
- **Title**: `nf-fa-bars` plus text, drawn as the title capsule ([`layout/popup`](../layout/popup.md)). The Space menu
  shows the focused panel's `[N] label` (what it lists is what that panel can do); any other menu says what it does
  (`GLOBAL OPERATION`, `SORT BY`).
- **The `Global operation` row** (Rules M2): no hotkey, and the description is always `actions for the whole app`.
- **Width**: every row is known when it opens, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).
- **A jobs list's rows follow the jobs**: when a job's progress or state changes, its row changes while the menu is
  open, with no need to close and reopen it.

**Why**: with descriptions right-aligned, names and descriptions form two columns, and the eye running down the names is
not interrupted by the descriptions. The cursor takes the layer colour as background: in a family popup, the block on the
layer colour is where `Enter` acts (in a form too). With the hexagon and uppercase, section titles stand apart from the
rows that run at a glance; dashes between sections are lighter than a solid line, dividing the list without looking
like another frame.

## Keys

- A menu is a one-dimensional list: `j|l|↓|→` go on, `h|k|↑|←` go back, wrapping at both ends; `u|d` half a page
  (stopping at the ends), `gg|G` to the top and the bottom (Rules K12).
- `Enter` runs the cursor row; a hotkey runs its row directly.
- **After running**: whether the menu stays follows the table in Rules T1, by what happens once it is confirmed (opening
  something to look at, writing a value back, or editing that item in an editor keeps it; making the item go away,
  opening a shell, switching screens or drilling down clears it). Cancelling the confirm asked before an action with
  `Esc` always returns to the menu (Rules F4).
- `Esc` closes it (the global operation popup returns to the Space menu, Rules F4); the Space menu also closes on another
  `Space` (Rules K5).
- **Hint**: `Enter:run Esc:close` (no movement keys, see the hint in [`layout/popup`](../layout/popup.md)). A jobs
  list's hint is below.

## Inside a mode

The Space menu that `Space` opens inside a mode (Rules K11) lists only what can be done in the mode:

- **Title**: where the mode lives, as usual — the focused panel's `[N] label` on a panel, that popup's title in a popup.
- **`ITEM OPERATION`**: what can be done now to the item under the cursor (or the selected range); rows run as usual,
  picking one being the same as pressing its key (e.g. `[C]ompare` in the Compare mode, described `with <anchor>`;
  `[v] Select` before a selection starts and `[y] Copy` after). What cannot be done now is disabled by M6 (e.g. with the
  cursor on the anchor).
- **`<mode name> MODE`** (e.g. `COMPARE MODE`; with layers the whole name, e.g. `VISUAL>SELECT MODE`): the mode's own keys. The movement keys are only shown — the key in the
  label's place, in Blue (as in the key reference, "a key that can be pressed now"), the description in Overlay0; the
  cursor skips them and `Enter` does nothing there. What really does something runs like any other row: leaving the
  mode, named with the verb `Esc` has in the mode's hint (`[Esc] Leave` in the Compare mode, `[Esc] Cancel` where the
  hint says `Esc:cancel`).
- Panel, item and global actions and the `Global operation` row are never listed.
- `Esc` in the menu still closes the menu (K4), back to the mode; the `[Esc]` of the leaving row is the key pressed in
  the mode, as with `[Enter] Connect`.

**Why**: "when in doubt, hit `Space`" must answer inside a mode too. What applies to the thing at hand runs straight from
the menu, as in any Space menu; running a movement key from a list makes no sense, so those rows only tell what can be
pressed: the cursor skips them and the keys are Blue.

## Jobs list

Lists the jobs the app is running or has run (e.g. sshu's Jobs).

- **Its rows follow the jobs** (see "Look").
- **`Enter` acts on the cursor row**:
  - A row something can be done to (e.g. a transfer in progress can be cancelled): `Enter` opens a confirm whose
    content is the row's full text and whose question asks whether to do it ([`dialog/confirm`](confirm.md)). The hint
    names the action: `Enter:cancel Esc:close`.
  - A row with nothing to do: `Enter` opens the row's full text (Rules F1), hint `Enter:detail Esc:close`. That `Enter`
    runs nothing.
  - The hint changes with the cursor row and says what pressing does (Rules M5).

**Why**: a jobs list is for watching how far the jobs have got; rows that do not move would mean closing and reopening
it again and again. `Enter` always means "this row": where something can be done, you read the full text and confirm
first, so one press never cancels a half-finished transfer.

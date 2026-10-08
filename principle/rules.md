# tdp Rules

**Language**: English · [繁體中文](rules-zh_TW.md)

Every rule here **must hold**. Each carries a "why", which is its origin UX
([Principle P0](README.md#p0-rules-serve-the-ux-not-the-other-way-round)).

**What is a requirement**: everything stated in the rules and in [components](../components/README.md) is a requirement.
Only four kinds of text are not: parts that say "up to the app", examples marked "e.g.", the "why", and passages marked
"Implementation reference (not a requirement)".

**Zones**: each rule heading is tagged `fixed` or `concept` ([Principle P5](README.md#p5-fixed-zone-and-concept-zone)).
In a `concept` rule the semantics are still fixed; only the implementation is left to the app.
A fixed rule may mark the parts left to the app with "(concept)", and a concept rule may mark the parts set in stone with
"(fixed)".

**Departure**: the fixed parts are followed as a rule. When an app's nature makes a rule inapplicable, the app must write
down **which rule, where, and why** in the "偏離 tdp" (departures from tdp) section of its `docs/dev-remarks.md`. With a
written reason it is a **departure**; without one it is a **violation**, listed in `docs/<app>-terminu-fix.md`. The
components all count as the fixed zone: a departure from the components, besides its written reason, is also reported as
a gap in tdp — when a component's solution doesn't fit, tdp is missing a solution.

**Citing**: `tdp` plus the ID, e.g. `tdp K4`, `tdp M2`. Once published, IDs are never renumbered;
a retired rule keeps its ID and is marked retired.

| Chapter | Scope |
|---|---|
| [K](#k-core-keys) | Core keys |
| [M](#m-menus-and-disclosure) | Menus and disclosure |
| [L](#l-layout) | Layout |
| [F](#f-popups) | Popups |
| [X](#x-mouse) | Mouse |
| [T](#t-time-axis) | Time axis |
| [S](#s-splash) | Splash (the family easter egg) |
| [E](#e-app-and-environment) | App and environment: command line, environment variables, requirements, releases, documents |

---

## K Core keys

### K1 Core keys mean the same thing everywhere in the app `fixed`

| Key | Meaning | Rule |
|---|---|---|
| `Tab` | Move focus to the next object on the same level | K2 |
| `Enter` | Do the most intuitive action to what has focus; with focus on a value, confirm that value | K3 |
| `Esc` | Cancel / close the top layer | K4 |
| `Space` | On a panel, open / close the Space menu (what can be done here) | K5, M2 |
| `?` | Open / close the key reference: what keys work on the frontmost surface (read-only) | K6, M4 |
| `q` | Quit the app | K9 |

These keys carry this meaning on **every surface**; the only exceptions are input state (K8), PTY (K10), modes (K11) and
`q` on a form (K9). An app need not use all of them (a single-panel app has no use for `Tab`), and may designate core
keys of its own; once designated, those also keep their meaning on every surface. **No letter hotkey may take over a key
in this table.**

**Why**: what users learn is a **role** ("cancel", "move focus", "what can I do now"), not a key. With the roles fixed,
one lesson holds on every surface of every app in the family. A single surface where `Space` does something else adds a
rule to learn: "except here".

### K2 `Tab` switches focus between objects on the same level `fixed`

`Tab` moves focus to **the next object on the same level within the current surface**, wrapping from the last to the
first:

| Focus is on | `Tab` switches between |
|---|---|
| a screen | panels |
| a form ([components/dialog/form](../components/dialog/form.md)) | fields; the error row (while it holds an error) and the action row are each a stop too (the options inside a field move with hjkl, K12) |
| a popup with several areas (a finder, a datetime picker) | areas |

- `Tab` does not cross screens or leave the current popup.
- With focus in a PTY, `Tab` belongs to the subprocess (K10).
- **On a typing row** (the typing row of a finder or a select, a panel filter): `Tab` goes to its list
  ([components/input/finder](../components/input/finder.md)).
- **An input popup with a single area**: with a greyed-out suggestion (the old value), `Tab` accepts the suggestion; with
  no suggestion it does nothing.
- In the writing state of multi-line text, `Tab` is an indent character, not a field switch (K8).
- Cycling backwards (e.g. `Shift-Tab`) is a hotkey, and whether to offer it is up to the app; a form always has
  `Shift-Tab`.

**Why**: users press `Tab` expecting "the next one" — the next panel on a screen, the next field in a form. It is the
same role at different levels. Switching screens is a global operation (P3).

### K3 `Enter` does the most intuitive thing to what has focus `concept`

`Enter` does **the most intuitive action** to the focused item — enter a directory, connect, open, flip a setting.
What exactly is up to the app, but the same kind of item always gets the same action within an app.
When the panel itself is a content area with no "item" to pick (e.g. a preview, a log), `Enter` does the most intuitive
action to the whole panel, as the app decides (e.g. open a scrollable view).

**`Enter` does not move the focus** (fixed): after `Enter`, the focus stays where it was — once a field's input popup on
a form is confirmed, the focus is back on the same field; choosing a radio option or flipping a checkbox in place does
not move it either. Only `Tab` and the movement keys change position (K2, K12).

**In an input popup** (fixed), `Enter` acts on the area that has focus:

- **Focus on the value**: confirm the value — it is written back and the popup closes. If the value is invalid, it is
  **not written back**: the error goes in the reserved error row (F7) and the popup stays open.
  If the value is the same as when the popup opened, nothing is written back and the popup just closes.
- **Multi-line text**: in the writing state `Enter` is a newline; only `Enter` after leaving the writing state confirms.
- **A typing row** (the typing row of a finder or a select, a panel filter): `Enter` moves the focus to the item under
  the cursor in the list, without running it; a second `Enter` on the list runs or picks it. With no results it does
  nothing.
- **Other parts** (e.g. a datetime picker's month, a color picker's R): do the most intuitive thing (e.g. move to the
  calendar, open a list to pick the value from).

**A form** ([components/dialog/form](../components/dialog/form.md)) is not an input popup: in a form, `Enter` acts on the
focused item — opening that field's input popup, choosing a radio option, flipping a checkbox, pressing the button. Only
the button submits: it then checks **every** field, submits nothing if any is invalid, and moves the focus to the first
field with a problem.

In other popups (menu, confirm), `Enter` runs the row under the cursor / accepts.

**Why**: a literal definition such as "confirm / enter" does not survive real apps; what users expect from `Enter` is
"do the natural thing to this". In an input popup, that thing is confirming the value — and confirming an invalid value,
or failing to confirm without saying why, both leave the user stuck. `Enter` does not move the focus: pressing `Enter`
again and again only opens and closes things in the same place, and the user need not guess where a press will leave
them.

### K4 `Esc` closes one layer at a time and never leaves the app `fixed`

`Esc` cancels the current operation or closes the top layer: a popup if there is one (toasts included, F3); otherwise it
leaves the current mode (selection, dragging) or goes up one level (e.g. clearing a panel filter) — what "up one level"
means is defined by the app. **One layer per press**, and **`Esc` never leaves the app** — at the top it does nothing.

When a popup opens another (e.g. Space menu → global operation popup → confirm), `Esc` **closes only the topmost one**;
the popups underneath stay and are shown exactly as they were; the next press closes the next layer (F4).

**Why**: a lost user presses `Esc` repeatedly to get back somewhere safe. If the end of that sequence is the app closing,
`Esc` becomes a dangerous key, users stop pressing it, and the safe way out that "cancel" provides is gone. Quitting has
its own key (K9).

### K5 `Space` opens and closes the Space menu on a panel `fixed`

- With focus on a panel, `Space` opens the Space menu (M2); while the Space menu is open, `Space` closes it again.
  `Esc` closes it too.
- **`Space` closes only the Space menu it opened itself.** On any other popup (a confirm, input,
  note… opened by `Enter` or a hotkey), `Space` **does nothing**; those are closed by `Esc` or by their own flow. The one
  exception: on a checkbox popup's list, `Space` checks or unchecks
  ([components/input/checkbox](../components/input/checkbox.md)).
- A popup's own operations run by hotkey, disclosed in the hint on the popup's bottom border and in
  that popup's `?` help (K6); no Space menu is stacked on top of a popup.

**Why**: an entry key that opens but cannot close is a trap — users reach for the same key to get out and nothing
happens. But if `Space` could also close a confirm, it would double as `Esc`'s "cancel" (P4); and if it could stack a
menu on a popup, boxes on boxes would have no end. The family's flow is always: `Space` on a panel opens the menu,
`Enter` on a row, and only then does the next popup open. The checkbox popup is the exception: for checking items on a
list, `Space` is the key everyone knows, and `Enter` there is kept for confirming the whole set (P0).

### K6 `?` opens and closes the key reference from anywhere `fixed`

`?` responds on any surface; `?` again closes it, and so does `Esc`. It opens **the key reference of the frontmost
surface**: read-only and scrollable, with no cursor and nothing to run (M4; how it looks:
[components/dialog/note](../components/dialog/note.md)).

| Focus is on | The key reference lists |
|---|---|
| a panel | the keys that work on this panel, plus the core keys and the global hotkeys |
| a popup (the Space menu and the global operation popup included) | **only this popup's** keys |

Input state, PTY and modes follow K8, K10 and K11.

**Why**: whoever presses `?` wants to **read** "what can I press here". Putting reading and doing in one box leaves the
user standing on a list with a cursor where every row can be pressed — and afraid to move (F1: a popup belongs to
exactly one class). What can be done is under `Space`; what can be pressed is under `?`.

### K7 Aliases are complete `fixed`

When a role is bound to several keys, every alias must work **on every surface**. If that is not possible, don't alias.

**Why**: a partial alias (a key that cancels on the main screen but not in popups) is worse than none — it looks like a
convenience, but adds a rule to learn: "where it works and where it doesn't".

### K8 Input state: hotkeys are all off `fixed`

The **input state** is when the content is text being typed: focus is on a typing row — an input popup's value, a
textarea's writing state, the typing row of a finder or a select, a panel filter. The list of a select or a picker, a
textarea's moving state and a form itself are not the input state.

In the input state, **every key that produces a character is a character** and triggers nothing:

| Key | In input state |
|---|---|
| letter hotkeys, `Space`, `?`, `q` | typed as characters |
| `Esc` | cancels the input (K4) |
| `Enter` | see K3 |
| `Tab` | accepts a grey suggestion; on a typing row, goes to the list (K2); in the writing state of multi-line text, a character (indent) |
| `Ctrl-C` | starts the quit flow (K9) |

Normal behaviour returns the moment focus leaves the input surface.

**The writing state of multi-line text**: `Tab` is a character (an indent), just as `Enter` is a newline (K3); to
confirm, leave the writing state first (`Esc`), then press `Enter`. Whether the indent inserts `\t` or spaces is up to
the app.

**Why**: `Space`, `?` and `q` are all printable. Without this, users could never type a file name with a space or a
password with a question mark. `Esc` and `Enter` stay, because they do not compete with characters, and without them the
input box is a trap with no exit.

### K9 `q` and `Ctrl-C` quit the app `fixed`

- `q` and `Ctrl-C` do **the same thing**: start the app's quit flow. `q` is a character in the input state (K8) and does
  nothing on a form ([components/dialog/form](../components/dialog/form.md)); `Ctrl-C` still works in the input state and
  on a form. With focus in a PTY both belong to the subprocess (K10).
- **The quit flow is up to the app** (concept): quit at once, confirm first, or let the user choose how to quit.
  E.g. sshu asks whether to close open sessions first; filu lets the user choose whether to switch the shell to the last
  directory.
- **Pressing `Ctrl-C` again during the quit flow quits at once**, with no further questions.
- Quitting is listed in the global operation popup (M4).

**Why**: `Ctrl-C` is in every terminal user's muscle memory, and `q` is the TUI convention; if the two behaved
differently, users would have to remember which one asks and which one doesn't. Pressing `Ctrl-C` twice to force quit
means users can never be trapped by their own confirm box. `q` on a form is the exception: a form looks like a place to
type, and a user who thinks they are typing, hits `q` and leaves the app pays too high a price.

### K10 PTY: keys belong to the subprocess, with at least one exit key `fixed`

With focus in a PTY (a shell, editor or remote session running inside the app), **keys go to the subprocess**: core keys
and the app's hotkeys stop working — vim needs `Esc`, the shell needs `Tab` and `Ctrl-C`, a remote program may want any
chord.

- The app designates **at least** one exit key that moves focus out of the PTY (a combination the subprocess almost never
  uses; the family uses `Alt-Esc`), and discloses it permanently while focus is in the PTY (how it looks:
  [components/dialog/terminal](../components/dialog/terminal.md) and the footer in
  [components/layout/screen](../components/layout/screen.md)).
- **`Alt-Esc` always confirms first**: whenever pressing it would move focus out of the PTY or end the subprocess, whether
  or not the subprocess stays alive, a confirm comes first (`Enter` leaves, `Esc` returns to the PTY); what it does inside
  the PTY (e.g. stepping zoom down one level) needs no confirm. The reason: terminals send an Alt chord as "`Esc` plus the
  key", so `Alt-Esc` is byte for byte two `Esc`s; when the app is busy the reading end stalls, and two `Esc` presses pile
  up and are read as `Alt-Esc`. Pressing `Esc` repeatedly is common in vim; the confirm lets whoever misfired press `Esc`
  to go back to the PTY.
- **Other Alt-chord exit keys** (e.g. kbu's `Alt-t` hiding Alterm, `Alt-Enter` on a locked cell in sshu) can likewise be
  spelled by "`Esc` then that key"; whether they confirm is up to the app.
- Whether the app keeps other chords of its own inside the PTY besides the exit key (e.g. sshu's zoom, cell switching and
  history scrolling inside a cell) is up to the app. Any it keeps are disclosed permanently, like the exit key (M1).
- Where focus lands after the exit key is up to the app.
- While the subprocess is not ready for keys yet (e.g. the remote end is still connecting), the app may hold ordinary
  keys back (so they don't land on the remote end minutes later); but **`Ctrl-C` is still forwarded to the
  subprocess**, and the exit key still works and is still disclosed. With focus in a PTY the user takes every key as
  pressed inside the PTY; the only exceptions are the explicitly disclosed exit key and the chords the app keeps.

> **Implementation reference (not a requirement)**: measured with bubbletea v1.3.10, with keys already queued, two `Esc`s
> 150 ms apart still merged.

**Why**: with focus in a PTY, nearly everything the user does is the PTY's business; the more keys the app intercepts,
the likelier it breaks the subprocess, and the more "who owns this key right now" becomes something to remember. But a
PTY with no way out is a trap, so there must be at least one exit key, and it must be visible; whether to intercept the
rest depends on how the app's PTY is used — a single shell and a whole grid of live remote sessions have different
answers.

### K11 Core keys inside a mode `fixed`

With focus inside a mode (the term "mode"), the core keys act like this:

| Key | Inside a mode |
|---|---|
| `Space` | **opens no menu**; does nothing |
| `?` | the mode's key reference (read-only, K6): which keys work in the mode and what they do |
| `Esc` | leaves the mode (K4), back to where it was entered |
| `q`, `Ctrl-C` | run the quit flow, as K9 |
| `Tab` | a mode may suspend `Tab`, but pressing it must respond, saying to leave the mode with `Esc` first (e.g. a toast); while the toast is up, the first `Esc` closes it (K4) |

- A mode has no Space menu, and no list of keys to run either. The mode's own keys (move, select, drag) are pressed
  directly; they are disclosed in the `?` key reference and in the footer / bottom-border hint (how the footer looks
  inside a mode: [components/layout/screen](../components/layout/screen.md)).
- **A mode shows itself**: the mode name appears at the right of the top border of the frame the mode lives in (panel or
  popup), and the frame turns the mode colour; leaving the mode restores both. The mode name is a word, not colour
  alone: a focused panel in a mode still shows that it has focus (L5). How it looks:
  [components/layout/panel](../components/layout/panel.md).

**Why**: a mode is always a special case; its keys are movement and selection, pressed directly and in runs, not actions
on an item, and there is no item / panel / global to split them by. Turning them into a list you pick and run from (even
`h j k l` run from a list) only adds a detour; all the user needs is "what can I press here", which is exactly `?`'s job.

### K12 Navigation letters are kept for movement; hjkl are the arrow keys `fixed`

Where nothing is typed, `j k u d g G h l` are kept for movement, and no action takes them. `h`/`j`/`k`/`l` are
`←`/`↓`/`↑`/`→`, meaning what the layout makes them mean:

- **With a left-right structure** (tabs within one surface, two sides, a grid): up, down, left and right. `j`/`k` move up
  and down a list, `h`/`l` go left and right — switching tabs, crossing to the other side, the day before or after in a
  calendar.
- **In a plain one-dimensional list with no left-right structure** (a form, a one-value-per-row panel without tabs, a
  menu): `h`/`k` (`←`/`↑`) go back, `j`/`l` (`↓`/`→`) go on, whether the options run across or down.
- A one-dimensional list in a panel with tabs: `h`/`l` go to the tabs, `j`/`k` still move in the list.
- **`u`/`d` move half a page, `gg`/`G` to the top and the bottom.** `g` is only the start of a two-key chord: `gg` goes to
  the top, and other chords starting with `g` may be hotkeys (e.g. filu's and webu's `[go]to`); a single `g` does
  nothing. `Ctrl-U`/`Ctrl-D` are not taken as aliases.
- **Moving within a piece of text** (a note's selection, a textarea's moving state): add `w`/`b`/`e` (next word start,
  previous word start, word end) and `0`/`$` (line start, line end), as in vim.

**Why**: in the family hjkl are the arrow keys — forms, panels and lists all move with them; an app binding one to an
action has users trigger an action while they think they are moving. With a left-right structure, left and right are
left and right (filu's, kbu's and webu's `h`/`l` switch tabs, sshu's `h`/`l` cross to the other side); without one, the
left and right keys are idle and get "back" and "on", so users need not wonder whether options run across or down.
`Ctrl-U`/`Ctrl-D` are not taken: one set of keys per action is one set fewer to remember; and in shells and many input
boxes `Ctrl-U` means "clear this line", so the same chord would turn pages in one place in the family and delete text in
another — too high a price for a slip.

---

## M Menus and disclosure

### M1 The entry points are visible `fixed`

Every screen outside the input state must **permanently show** `?`, and `Space` (inside a mode `Space` does nothing and
need not be shown, K11), so a first-time user who has read no documentation can see them. How it looks: the footer in
[components/layout/screen](../components/layout/screen.md).

**Why**: users cannot press a key they do not know exists. An undisclosed entry point might as well not exist, however
complete the disclosure behind it (Principle P2).

### M2 Space menu: item → panel → global, three regions `fixed`

The Space menu lists **everything the current panel can do**, split by what it acts on (Principle P3), in a fixed order:

| Order | Region header | Contents |
|---|---|---|
| 1 | `item operation` | what can be done to the one item under the cursor |
| 2 | `panel operation` | what can be done to the current panel (or its tab) as a whole |
| 3 | (no header) | **always a single row**, `Global operation` (no hotkey): `Enter` opens the global operation popup (M4); the same even when the app has only one global action |

- **The header strings are fixed**: the app and the whole family use the English words in the table above, word for
  word.
- **The global row carries no region header**: its label `Global operation` already says what it is, and a `global operation` header above it only repeats it; a divider still separates it from the regions above.
- **No target, no region**: an empty list has no item, so item operation disappears, header and all.
- **On a panel's Space menu, the item and panel regions always carry their headers** (even when only one of them is left): the global row is always there, so the menu never holds just one kind of thing. Only the global row, and other ungrouped menus (M8), go without headers.
- Regions are separated by a divider line. How it looks: [components/dialog/menu](../components/dialog/menu.md).

**Why**: users read top down, so they see "what can I do to the thing I picked" first, then "to this whole panel", and
global last. Fixed header strings let users recognise "this is the same kind of menu" at a glance — a menu worded
differently reads as a different **kind** of menu. Putting global last, as a single row, means remembering the one key
`Space` is enough to find everything, without the global actions outgrowing the panel's own; and every app in the family
has a Space menu of the same shape.

### M3 Every action can be found in a menu `fixed`

- Every item operation and panel operation of every panel is in that panel's Space menu.
- Every global operation is in the global operation popup (opened from the Space menu's global row).
- A popup's own operations are all in that popup's bottom-border hint and `?` key reference (K5, K6).
- **A popup with only a typing row** (text, password, number): `?` is a character there (K8), so its hint lists every
  operation, and fits in 80 columns (the hint in [components/layout/popup](../components/layout/popup.md)).
- **A letter hotkey is a shortcut to a row in some list, not an extra feature.** An action triggered only by hotkey and
  found nowhere else is a violation.

Which region an action belongs to depends only on **what it acts on**, never on how important it is (Principle P3).

**Why**: a new user who has never seen a hotkey must be able to do everything, anywhere, with `Space` and `?` alone.
Each action that has to be learned in advance is a hole in "usable without the docs".

### M4 The global operation popup and the key reference `fixed`

**The global operation popup** (doing)

- Opened with `Enter` on the Space menu's global row (M2), over the Space menu; it is a menu (F1) listing **all** of the
  app's global actions — `j/k` to pick, `Enter` or the hotkey to run. Quitting the app must be here (K9).
- `Esc` goes back to the Space menu (F4); an action that closes the whole stack once run follows T1.
- The row that switches to the current screen is disabled as M6 says (e.g. `[M]anage` while on `[M]anage`).
- **Global hotkeys**: with no popup open, the hotkeys in the global operation popup can also be pressed directly on a
  panel. When one clashes with a panel's own hotkey, the panel's wins, and that panel's key reference does not list the
  global key it overrides. `q` follows K9.

**The key reference** (reading)

- Opened with `?` (K6). Read-only and scrollable, with no cursor and nothing to run — not a menu.
- What it lists: see K6; how it looks: [components/dialog/note](../components/dialog/note.md).

**Why**: a read-only help page cannot replace a list you can run (Principle P2) — what can be done is under `Space` and
in the global operation popup, one step from running; `?` is a permanent cheatsheet to glance at alongside. Reading and
doing live in two boxes, each of one class (F1). With the global actions gathered in one popup, no Space menu has to list
them again; users who know them press the global hotkeys directly on a panel, without opening two layers of menu every
time.

### M5 Each row = name + description, hotkeys marked with `[]` `fixed`

Each menu row has the **action name** on the left and a **one-line description** on the right:

```
 item operation
 [o]pen                        open it with the OS default app
 [r]ename                                    this item, in place
  ───────────────────────────────────────────────────────────
 panel operation
 [/] Search                                everything under here
  ───────────────────────────────────────────────────────────
 Global operation                      actions for the whole app
```

How keys are written is one rule for the whole app (menus, footer, panel hints, popup hints, the key reference, and the
README). Marking inside a label:

| Case | Form |
|---|---|
| A single letter, the first letter of the label | brackets in place: `[r]ename`, `[D]elete` |
| A single letter, inside the label | wrapped in place: `UR[L]` |
| A letter not in the label | in front: `[n] New` |
| With a modifier | `[Alt-t]erm` |
| Several characters | `[go]to` |
| Digits | always in front: `[3] Favorites`, never inside the word |
| A core key | in front: `[Enter] Edit` — it marks that pressing this key on the panel is this action; in a menu `Enter` still runs the row under the cursor |
| No hotkey | no brackets |

- **What is in the brackets is exactly the key to press, case included**: `[A]dd` is `Shift-A`.
- A row whose label already spells out the key (`[/] Search`) is not bracketed again.
- Colour or a glyph alone must not be the hint that "this is a hotkey"; mark it explicitly.
- What the description says is up to the app, but it must fit on one line.

**Key names** (the same everywhere on screen and in the README):

- The name printed on the key cap, UpperCamelCase, no abbreviations of our own: `Esc`, `Tab`, `Enter`, `Space`,
  `Backspace`, `Delete`, `Home`, `End`, `PgUp`, `PgDn`; arrows `↑` `↓` `←` `→`.
- Letters in the case actually pressed: `q`, `A` (that is `Shift-A`), `Alt-z`. The letter after `Ctrl` is always upper
  case (`Ctrl-C`, `Ctrl-U`): terminals can't tell the case of a `Ctrl` chord.
- Modifiers are joined with `-`: `Alt-t`, `Ctrl-C`, `Shift-Tab`, `Alt-Esc`.
- Several keys doing one thing are joined with `/`: `j/k`, `h/l`; a range uses `–`: `1–9`.

**By place**:

| Place | Form | Example |
|---|---|---|
| Label (menu rows, statusbar chips, panel titles) | the bracket marking above | `[r]ename`, `[Alt-t]erm` |
| Sentence (empty states, toasts, error messages, and keys mentioned in the description column of a menu or the key reference) | every key in square brackets | `Press [A] or [Space]`, `see App Log [!]`, `next tab [h]/[l]` |
| Hint, footer | `key:description`, no space around the colon, one space between items | `Enter:delete Esc:cancel` |
| Key reference | two columns, key and description; no brackets, no colon on the key | key column `Esc`, description column `close this popup` |

- In hints and the footer the key and its description are told apart by colour: the key in one colour, the colon and
  description in another (see [components/color](../components/color.md)). A description may run to several words; the
  key's colour still shows where each item starts.
- **README**: keys in the prose are Markdown code (`` `Enter` ``, `` `Ctrl-C` ``), not square brackets; names and
  notation as above. A label quoted from the screen is written as on screen (`[A]dd`).
- **Another tool's own keys** (e.g. tmux's `prefix l`, `C-a x`) are written the way that tool writes them: the user types
  them into that tool's config or reads them in its docs.

**Why**: the name answers "what action is this", the description answers "what does it do to what" — the same verb can
mean different things on different panels (delete the file, or remove the bookmark?). A description that won't fit on
one line usually means the action is badly named. Digits stay out of words because `432hz` would render as `4[3]2hz`.

### M6 Actions that can't run right now: disabled `fixed`

- **No target**: the row (or region) is not shown (M2).
- **A target, but the action can't run right now**: the row is still shown, in the disabled colour
  ([components/color](../components/color.md)), keeping its usual description with no reason added; the cursor skips it,
  and its hotkey does nothing.
- **The `?` key reference follows the same rule**: a key whose target exists but can't be pressed now is still listed,
  in the disabled colour; with no target it is not listed. The bottom-border hint and the footer, short on room and
  always on screen, may list only the keys that work now; that is up to the app.
- A section of the key reference with a title of its own describing **another surface** (e.g. `ssh grid` in the `?` of
  sshu's list, since a cell shows no key reference) is not this surface's keys and is shown as usual.

**Why**: users take a hidden action to mean the app doesn't support it; disabling tells them "this exists, just not
now". No reason is added because the reasons vary endlessly, and squeezing them into a one-line description would let
every row's length run out of control (M5). The cursor skips the row because landing on it would only lead to a key that
does nothing.

### M7 Entry points on a panel always respond `fixed`

With focus on a panel, `Space` and `?` must both respond when pressed: `Space` opens the Space menu (the global row is
always there, so the menu is never empty, M2), and `?` opens the key reference. On a popup, the key that always responds
is `?` (K6).

**Why**: when a key does nothing, users think the key is broken, not that there is nothing to do here.

### M8 Other grouped menus: cursor-related first `concept`

Any menu other than the Space menu (e.g. a sort picker, an open-with list) that groups its rows puts the actions related
to the current cursor first, then gives each following group a header naming its kind. A menu that needs no grouping is
listed directly.

**Why**: when users open a menu, what they look for most often is what they can do "to the thing I picked" — the same
reason the Space menu puts the item region first (M2). Every grouped menu follows this order, so users need not search
anew in each menu.

### M9 When one key has two indicators, mark which one fires `fixed`

When a hotkey does different things on different panels and both indicators are **on screen at the same time**, the user
must be able to see at a glance **which one fires when pressed on the current focus**: the one that fires is bright, the
one that doesn't is dim ([components/color](../components/color.md)).

**Why**: with two identical keys on screen at once, the user has no way to tell which thing pressing it will do. What is
bright is what has focus (Principle P6).

---

## L Layout

### L1 Minimum supported size: 80 columns × 40 rows `fixed`

At **80 columns × 40 rows**, the app must be able to complete all its core tasks. That is roughly a terminal window on
half of a 16:9 screen (8:9). How the panels split is up to the app; how to draw when not every panel fits: narrow widths
in [components/layout/screen](../components/layout/screen.md).

**Why**: a terminal often takes only half the screen — the other half is an editor, a browser or another terminal. A TUI
that only works full screen is unusable in the everyday split window.

### L2 Width does not follow content `fixed`

Dynamic text in titles, statusbars, chips and the like uses fixed-width slots or padding; its width never changes with
the length of the content.

**Why**: once widths float, the main view shifts sideways with them, and the whole screen shakes as popups open and
close.

### L3 Chrome has a fixed number of rows `fixed`

The number of rows for footer, statusbar, tab row and other permanent chrome is **the app's choice, and once chosen it is
locked**; it does not change with the amount of content. What doesn't fit is truncated or dropped from the end, never
wrapped.

**Why**: one more chrome row is one less main row, and the whole layout shifts in a chain. Stability always beats saving
space.

### L4 Every line is exactly the terminal width `fixed`

Every line on screen is exactly as wide as the terminal, no more, no less.

**Why**: one cell too many and the terminal wraps, knocking the whole screen out of place; one too few and stale cells
linger on screen. Misjudged CJK and icon widths are the usual cause.

### L5 Focus is visible, and moving it moves nothing else `fixed`

The focused surface must be recognisable at a glance, and moving focus **must not shift any content**.

- **Focus is not told by colour alone**: something besides colour must differ (e.g. the line style). A mode turns its
  frame the mode colour (K11); with colour alone, focus vanishes the moment a mode starts. How it looks:
  [components/layout/panel](../components/layout/panel.md).

**Why**: users need to know where their keys will go; and if the screen jumps every time focus moves, the eye has to find
its place again.

---

## F Popups

### F1 Popups come in seven classes, one class at a time `fixed`

The family's popups come in these seven classes only, each with fixed key meanings:

| Class | What the user can do | E.g. |
|---|---|---|
| **menu** | a list with no search: `j/k` moves the cursor, `Enter` or a hotkey runs the row | Space menu, global operation popup, a sort picker, a jobs list (`Enter` opens the row in full) |
| **confirm** | read a reminder or warning; `Enter` accepts, `Esc` cancels (F6); what to read first sits above, the question last | confirm before delete, the quit confirm, "Connect to X?" carrying the details |
| **input** | enter or pick one value, written back once confirmed; one value per popup. On the typing row it is the input state (K8); other parts follow K1 | rename, address bar, select, datetime picker |
| **form** | one value per row; `Tab` jumps a field at a time, hjkl move item by item (K12), `Enter` acts on the focused item (opening that field's input popup, choosing a radio option, flipping a checkbox, pressing the button), the button submits ([components/dialog/form](../components/dialog/form.md)) | sshu's Host form, webu's Sign in and Add bookmark |
| **note** | read-only, scrollable (K12); no list of options to run with `Enter` | key reference, YAML viewer, App Log, error popup |
| **toast** | a short message popping up from the bottom, gone on `Esc` or on its timer; every key but `Esc` passes through it | "Copied", an operation failed |
| **terminal** | a subprocess running in the box; every key is its, only the exit key and the chords the app keeps are the app's (K10) | kbu's Alterm, filu's shell |

- **A note may have hotkeys and modes of its own**: e.g. the YAML viewer's `/` search, `y` copy, `v` select (a mode,
  K11). Its hotkeys are disclosed in the bottom-border hint and in `?`; but once it has a list of options to run with
  `Enter`, it is a menu, not a note.
- **A menu's `Enter` may open the row in full**: in a list with a cursor and no other action of its own (e.g. a jobs
  list), `Enter` opens a note showing the row's whole content; it is still a menu.
- **A confirm may carry content to read before answering**: the question is why a confirm exists, and above it may sit
  the information to look at before answering (e.g. the details of X above "Connect to X?"), scrolled with `j/k` when
  long; it is still just a confirm, not a note plus a confirm, and need not be split into two popups.
- **A popup may change class by phase, but belongs to one class at a time.** E.g. a finder is an input while typing and a
  menu while its result list has focus; `Tab` switches focus between typing and the list, and `Esc` closes the whole
  finder (K4: a phase is not a layer). A preview beside it takes no focus and is not another surface.
  **Which side has focus must show**: only the side with focus is bright (Principle P6; how it looks:
  [components/input/finder](../components/input/finder.md)).
- **A list plus search is a finder**: the plain finder, select, the checkbox popup and file-picker are all kinds of
  finder — the typing row is the input state, the list is for picking; for the typing row's keys see
  [components/input/finder](../components/input/finder.md). They are still inputs, not two classes at once. A list with
  no search is a menu.
- **A toast is not a layer**: it triggers no dimming (F8) and does not count toward the layer colours' levels; but `Esc`
  closes it first (K4).
- **Each step of a multi-step flow is its own popup**: e.g. sorting by picking a column, then a direction, is two stacked
  popups (F4 keeps the source), not one box changing its content — each step has its own UX, and its own size fixed at
  opening (F7).
- Not in these seven: the splash (chapter S), and panel content an app draws as a box (e.g. webu's page dialogs, webu's
  departure).

**Why**: the class is the user's expectation of "what keys do inside this box". With only seven classes in the family,
each of fixed meaning, nothing is relearned from one app to the next; a popup mixing two classes at once gives the same
keys two possible meanings inside one box.

### F2 Opening and closing are both animated `fixed`

Popups **must animate** both when opening and when closing. The length is the same across the family (see
[components/layout/popup](../components/layout/popup.md)); the form of the animation is up to the app.

**Why**: without animation, a popup "suddenly appears, suddenly vanishes", and users don't feel the change of layer as it
stacks on and steps back. The same length: the same action takes as long in every app of the family, so the rhythm stays
the same from one app to the next.

### F3 `Esc` closes any popup at once `fixed`

Any visible popup — auto-dismissing toasts included — starts closing **immediately** on `Esc`, without waiting for a
toast's countdown. Closing is animated as usual (F2); a popup already running its closing animation ignores `Esc` and
takes no other keys either.

**Exceptions**:

- With focus in a PTY, `Esc` belongs to the subprocess (K10); a terminal is left with the exit key. A toast can then only
  wait for its timer to go.
- In a textarea's writing state, `Esc` leaves the writing state for the moving state (K8).
- In a form or a textarea whose content changed, `Esc` first opens a confirm asking whether to discard it
  ([components/dialog/form](../components/dialog/form.md)).

**Why**: users are not obliged to wait out a countdown. If a popup that is already closing takes another `Esc`, or still
eats other keys, the user's next key goes to the wrong place. In a PTY and a textarea, `Esc` is already needed by the
subprocess and for writing; throwing changed content away in one go costs a lot, so it asks once more.

### F4 The source stays by default `fixed`

When popup A opens popup B, A stays underneath by default; cancelling B returns to A. The same holds at any depth: `Esc`
closes only the topmost, and the stack underneath is shown as it was (K4).

**Why**: the user did not dismiss A, they just did one interaction in B. If cancelling B also removes A, they have to
walk the whole way again. (Whether A stays after B completes is T1.)

### F5 Errors show at once, without blocking the app `concept`

Errors must appear immediately (toast or popup), close on `Esc`, and **must not block the app**. Whether there is an
error history to look back at is up to the app.

**Why**: an error you can't see never happened; an error that blocks the app keeps the user from dealing with the error
itself.

### F6 Confirm: `Enter` accepts, `Esc` cancels, and it says what will happen `fixed`

- **Which actions need a confirm is up to the app**, regardless of whether they are reversible. Once an action is set to
  be confirmed, it is confirmed every time. The exception: a choice made explicitly in a picker may count as the
  confirmation (e.g. picking the default app from an "open with" list), as the app decides.
- `Enter` accepts, `Esc` cancels (K3, K4). A confirm may have hotkeys of its own (e.g. `y` / `n`), listed in the
  confirm's `?` help (K6).
- The prompt says **what accepting will do** (verb and object), not an abstract OK.
- A confirm cannot be completed by accident (e.g. a mouse click must not accept it).
- How it looks: [components/dialog/confirm](../components/dialog/confirm.md).

**Why**: users must know the consequence before pressing `Enter`. Whether to stop and confirm depends on how much the
action weighs for the user — launching an external program, cutting a session, deleting a file: the app knows the weight
best, and no rule such as "reversible means no need to ask" can judge it.

### F7 Popup size and position `fixed`

- **Width**, fixed when the popup opens and unchanged while it is open:
  - **The content's width is known at opening** (e.g. an input with a length limit, a confirm, a menu, the key reference,
    a toast, an error popup, a datetime picker, a color picker): the widest row + 4 (one cell of border and one blank
    cell on each side), at least wide enough for the title and the hint, and at most `min(terminal width − 2, 120)`.
  - **The content's width is not known** (e.g. free-typed text, a URL, streamed content, search results, a form):
    `min(terminal width − 2, 120)`.
  - Centred horizontally.
- **Height**: follows the content, **fixed when the popup opens** and not resized with the content afterwards; at most
  the screen height − 2 (the top row and the footer always stay in view), scrolling inside the box beyond that. Only two
  cases may change the height while the popup is open:
  - **Loading**: a popup whose content is not known when it opens (streaming, loading) may change height while loading.
    When loading ends, the height is fixed.
  - **A change the user made**: when the user's own action in this popup changes its row count (removing a row, a choice
    that adds a row, filtering candidates as they type), the height **may** follow — the user expects that change; the
    app may also keep the height. The principle is that what is disclosed is correct.
- **Loading is always disclosed**: while a popup is loading, a spinning loading icon **always** sits after its title
  (spec in [components/layout/popup](../components/layout/popup.md)), whether or not its height changes; the icon goes
  when loading ends. Loading here means the content of the **whole popup** has not arrived (e.g. the list's items are not
  all loaded). If just **one item** is itself a continuous stream of data (e.g. a connection that keeps sending), it is
  that item that is loading, not the popup — how to disclose it is up to the app.
- **Position**: centred vertically. The toast is the exception: centred at the bottom of the screen, its bottom border
  sitting just above the panel's bottom border ([components/dialog/toast](../components/dialog/toast.md)).
- **A popup whose value can be invalid reserves an error row** (an input popup, a form): it opens with one error row in
  its height, blank while there is no error; an invalid value has its error written in this row (K3), and the box keeps
  its height. One whose value cannot be invalid (e.g. a multi-line editor) need not reserve one. When the action itself
  fails (writing a file fails, the remote end refuses), nothing goes in the error row; an error popup opens
  ([components/layout/popup](../components/layout/popup.md)).
- **The terminal class is the exception**: its width is `terminal width − 2`, with no 120-column cap; above it the
  statusbar or the screen's chip row stays, and below it runs down to the last row of the screen, covering the footer —
  the subprocess needs the room, and inside a PTY the outside footer is not needed
  ([components/dialog/terminal](../components/dialog/terminal.md)).

**Why**: when every popup keeps sizing itself by its content, nobody can tell what it will look like before it opens,
and the box jumps whenever the content changes (L2). With only two ways to work out the width, both fixed at opening,
every box is predictable; a popup whose content is known need not stretch to full width, so it is neither empty on a
wide screen nor cramped on a narrow one; the 120-column cap keeps a menu's names and descriptions from drifting too far
apart on a wide screen. The error row is reserved inside the box rather than opening another popup: the error stays in
view while the user fixes it, with no extra key to dismiss it first.

### F8 With popups stacked, everything below the top one is dimmed `fixed`

While a popup is open, **everything but the topmost popup** — the popups beneath it and the whole base screen — is
dimmed. The same holds when popups open in a row or one opens inside another: only the topmost is ever bright (Principle
P6).

- Streaming content underneath (logs, remote sessions) and warning colours are dimmed too: T2 is about losing focus, not
  about being covered.
- **How to dim: fade every colour — foreground and background alike — toward the base, leaving shapes and layout
  untouched.** Never strip the colours and redraw, never drop backgrounds, never turn every foreground into one dim
  colour: that breaks whatever is drawn with a background (the body of a powerline capsule, a cursor bar, a selection).
  Layer colours, warning colours and streaming content go through the same fade and so become dimmed versions of
  themselves. The calculation is in [components/color](../components/color.md).
- **The drawn screen is dimmed once**: an unfocused panel is already dimmed (T2), and under a popup it gets a little
  darker again — so it shows where the focus was before the popup opened.
- **A toast does not trigger dimming**: it takes no key but `Esc` (F1) and is not a layer.
- **Borders are dimmed too, but keep their layer colour**: the borders of the popups below are drawn in a dimmed version
  of their own layer colour (components/color), not one common dim colour — dark, yet still showing which layer each is.

**Why**: popups are not always the same width, and an upper one may still cover the edges of the one below, so the boxes
do not always show the layers; brightness is the main cue for telling them apart, and it is exactly what P6 means: only
the layer being worked on is bright.

---

## X Mouse

### X1 The mouse is optional `fixed`

The app must be fully usable without a mouse.

**Why**: the mouse is not a first-class terminal input, and many environments (tmux, SSH, screen readers) don't have one
at all.

### X2 The mouse only maps to the keyboard `fixed`

If the mouse is supported, every mouse action maps to a keyboard action; **nothing can be done by mouse alone**.

**Why**: the mouse should be another way to press the keyboard, not another thing to learn.

---

## T Time axis

The rules in this chapter can't be seen in a screenshot; they exist only in the flow of use — they surface once an app is
complete enough, and more will be added as implementation continues.

### T1 After the target completes, does the source still mean anything? `concept`

The source stays by default (F4). The target clears the source before it enters only when it is clearly judged, by
function, that "once the user completes the target, the source has lost its meaning":

| Target | Clear the source? | Reasoning |
|---|---|---|
| A short confirm / message | keep | the user may want to go back to the menu and continue or cancel |
| Picking a value (an input popup, a select) written back to a form or a picker | keep | once the value is written back, the user carries on in the source |
| A long session (shell, editor) | clear | coming out of the session their attention has moved on; an old menu floating there is disorienting |
| A big context switch (drill-down, page change) | clear | the view underneath has changed; the old menu's target is gone |

**Why**: keeping is the safe default, and clearing needs a reason — otherwise users who finish something can't find their
way back. And "whether to clear" can't be written as a general rule: in code both cases look the same, and a screenshot
can't show it either; only reasoning about "once done with the target, does the user still want to see the source?"
answers it.

### T2 Unfocused panels are dimmed, streaming content excepted `fixed`

An unfocused panel **has its content dimmed with the same fade as F8** (its border being components/color's unfocused
border); **streaming content (logs, live output, remote sessions) is not dimmed on blur**. The exception is a popup on
top: attention is on the popup then, and everything below is dimmed as F8 says.

**Why**: dimming says "focus is elsewhere, look later" — what is bright is what has focus (Principle P6). Streaming
content has no later — information is passing by, and dimming it cuts off the glance from the corner of the eye. This is
also the textbook case of "rules serve the UX" (Principle P0): the origin UX of "dim on blur" is "don't compete for
focus", while streaming's UX is "catch updates from the corner of the eye" — two goals that happen to land on the same
panel, so the rule is extended rather than streaming sacrificed.

---

## S Splash

The splash is the terminu family's shared easter egg, and the **only thing in tdp that is deliberately not disclosed**.
The disclosure rules (M1, M3, M4) and the core-key rule (K1) do not apply to it; it is not a popup either, so chapter F
does not apply. The splash is documented only in tdp — never in an app's README, menus or help.

### S1 Every app has a splash, opened with `V` `fixed`

Every terminu app has a splash, opened with **`V`** on a panel. `V` is reserved for it:

- When a panel operation of some panel genuinely needs `V`, **that panel** may give `V` to the app; the splash cannot be
  summoned on that panel.
- But **at least one panel** in the app keeps `V` for the splash.

**Why**: an easter egg belongs to the family only if every member has it; and some apps' domains really do need `V`
(e.g. a selection mode) — giving up one panel is better than the whole app losing the egg.

### S2 Not disclosed `fixed`

The splash does not appear in the Space menu, the global operation popup, the key reference, the footer or panel hints,
and is not written in the README.

**Why**: a listed easter egg is no longer an easter egg. It is the one and only exception to "disclosure is the only
mechanism" (Principle P2) — which is why it is written here and in no app.

### S3 Any key only closes the splash `fixed`

While the splash is showing, **any key only closes it** — `q`, `Ctrl-C`, `Esc`, `Space` and `?` included; the key does
nothing else. A first `Ctrl-C` only closes the splash; it does not quit the app.

**Why**: faced with a screen they have never seen, users press any key to make it go away. If that key also did
something else (quit, open a menu), the egg would be a trap.

### S4 On a panel only, and only when asked for `fixed`

- It is not played at start-up.
- It can only be summoned with `V` on a panel; with a popup open, in input state or in a PTY, `V` does not summon it
  (in input state `V` is a character, K8; in a PTY it belongs to the subprocess, K10).

**Why**: a splash played at start-up is an intro everyone waits through every time, not an easter egg; and one that pops
up inside a popup, an input box or a PTY interrupts what the user is doing.

### S5 The content is the family icon `fixed`

The splash draws the app's `docs/icon.svg` — the terminu family mark — cell for cell, with a reveal animation. How the
animation runs is up to the app.

**Why**: the splash is the family's signature. Each member draws its own version of the family mark, so pressing `V`
tells you at once that this comes from the same family.

---

## E App and environment

What an app does off screen: the command line, environment variables, requirements, icon width, releases, documents.
This chapter is not on-screen UX; its reason is family consistency — the five apps do things the same way, so users who
have installed one can install the others, and know where to find config and data.

### E1 Command line: `version` and `help` `fixed`

Every app has:

- **`<app> version`**: prints the version. `--version` and `-v` may be aliases.
- **`<app> help`**: prints the command-line usage (unrelated to the `?` key reference inside the app). `-h` and `--help`
  may be aliases.

Other commands (e.g. `filu iconwidth`, `locku lock`, `webu <url>`) are up to the app.

**Why**: `help` and `version` are the first things anyone tries on a command-line tool. With the five apps using the
same pair, what can be asked of one app can be asked of every one.

### E2 Environment variable names `fixed`

`<APP IN CAPITALS>__<NAME>` — two underscores after the app name, the variable name in capitals with single underscores
between words (e.g. `FILU__ICON_WIDTH`, `KBU__ALTERM_LOGIN_SHELL`). Every variable the app itself reads (including ones
for tests and ones passed to its own subprocesses) is named this way. Shared names:

| Variable | Meaning |
|---|---|
| `<APP>__CONFIG` | the config **directory** (the config file lives in it) |
| `<APP>__STATE` | the state directory (when the app keeps state separately) |
| `<APP>__DATA` | the data directory |
| `<APP>__CACHE` | the cache directory |
| `<APP>__ICON_WIDTH` | manual override of how many cells an icon takes (E5) |
| `TERMINU__ICON_WIDTH` | shared by the family: an app with a PTY sets it for its subprocess, telling it how many cells an icon takes (E5) |

The exception: variables meant for another program follow that program's needs (e.g. the `LC_SSHU_COLORTERM` sshu
carries over ssh to the remote end — OpenSSH forwards only `LANG` and `LC_*` by default). Renamed variables do not keep
their old names.

**Why**: a variable shows at a glance which app it belongs to, and `TERMINU__` at once means the whole family. Two
underscores separate the app name from the variable name because the variable name itself has single underscores
(`ICON_WIDTH`); two underscores can't be mixed up with them.

### E3 Where config and data live `fixed`

| What | Default location | Override (E2) |
|---|---|---|
| Config | `$XDG_CONFIG_HOME/<app>` (falling back to `~/.config/<app>`) | `<APP>__CONFIG` |
| State (when the app keeps it separately) | in the config directory | `<APP>__STATE` |
| Data | under `~/.<app>/` | `<APP>__DATA` |
| Cache | the system's cache directory (macOS `~/Library/Caches/<app>`; Linux `$XDG_CACHE_HOME/<app>`, falling back to `~/.cache/<app>`) | `<APP>__CACHE` |

**Why**: with the five apps in the same places, users know where to look and what to back up. The cache goes in the
system's cache directory so that cache-cleaning tools can find it, and so it is not taken for data to back up.

### E4 Requirements: a Nerd Font and truecolor `fixed`

- Requires a Nerd Font; PUA glyphs are written as code points in the source.
- Requires a truecolor (24-bit) terminal: catppuccin's pale colours and components/color's layer gradient are indistinguishable in 256 colours, and dimming always outputs 24-bit (components/color). READMEs say so in their requirements, next to the Nerd Font.

**Why**: the family's icons, loading icon, and radio and checkbox glyphs are Nerd Font glyphs; the reason for truecolor is
given above.

### E5 The icons' real width `fixed`

With some fonts an icon takes two cells (the cursor moves two), while the width-measuring function measures one, and the
borders go crooked. What is measured is **how far the cursor actually moves**: a font whose icon looks wider than a cell
but moves the cursor one (the glyph spills into the next cell) counts as one.

- **Measured at run time**: the app probes at startup (CPR: print an icon, ask for the cursor position). Every width
  measurement (padding, clipping, centring, joining side by side, borders, overlaying popups) goes through one
  display-width function.
- **Overrides and order**: the icon width is taken from `<APP>__ICON_WIDTH`, then `TERMINU__ICON_WIDTH`, then the probe.
  The probe runs on unix only; Windows defaults to one cell, overridden by the environment variables.
- **Inside another app's PTY**: the probe is answered by the outer app's terminal emulator, which counts an icon as one
  cell, so the real width can't be measured. An app with a PTY therefore sets `TERMINU__ICON_WIDTH=<the cells it uses>`
  in its subprocess's environment when it starts one. Any family app running inside another's PTY then gets it right
  (filu in kbu's Alterm, kbu in filu's shell). Environment variables don't cross ssh; remote nesting relies on the app's
  own channel (sshu's nested command channel).
- **Overlaying a popup must not crash**: a popup may be wider or taller than the screen (the frame drawn during a resize
  still has the old size): start at 0 and clip what falls off the screen, and **never panic**; when it is larger in both
  directions it is clipped too, never handed back whole.
- **Tests**: the L4 screen tests also run once with "icons take two cells", opening each kind of popup once and measuring
  both the bare box and the whole screen with it overlaid; the edge cases include all three: the popup wider than the
  screen, taller than it, and larger both ways.

> **Implementation reference (not a requirement)**: filu `internal/ui/width.go` — `isWideIcon()`, `dispWidth()`,
> `dispClip()`, `padDisp()`, `dispCutLeft()`, `compositeDisp()` (replaces overlay's `Composite`, same interface),
> `centerDisp()` (replaces `lipgloss.Place`), `joinH()` / `joinV()` (replace `lipgloss.JoinHorizontal` /
> `JoinVertical`); detection is `DetectIconWidth()` in `iconwidth_unix.go`, called before `tea.NewProgram`; tests follow
> `d6_test.go` and `TestD6CompositeDispOversized`. Once done, it can be checked like this: apart from the width functions
> themselves, `internal/ui` has no calls to `lipgloss.Width`, `lipgloss.Size`, `lipgloss.Place`, `ansi.StringWidth` or
> `ansi.Truncate`.

**Why**: crooked borders make the whole screen unreadable, and the same font can move the cursor differently on different
terminals, so it can only be measured at run time.

### E6 Releases, tests and family assets `fixed`

- A single static binary built with goreleaser; `install.sh` / `uninstall.sh` (`curl | sh`, no sudo),
  also published to the Homebrew tap `vulcanshen/homebrew-tap`.
- Screen tests across sizes: at several terminal sizes, every line is exactly the terminal width (L4).
- `docs/icon.svg` is the family mark; the splash (chapter S) is drawn from it cell for cell, with a test keeping the two
  identical.
- Demo gifs are recorded with VHS, scripts in `.local/demos/` (how many go in the README: see E7).

**Why**: the five apps install, uninstall and release the same way; having installed one, users can install the others.
The screen tests guard L4; with the icon and splash test, the splash is not forgotten when the icon changes.

### E7 Documents `fixed`

**README**: `README.md` (English) and `README-zh_TW.md` (Traditional Chinese) stay in step, and cover only what users
need to know:

1. Title, badges, language switch (`English · 繁體中文`)
2. A one-line positioning plus a paragraph on what it can do
3. **One** representative demo gif
4. Features: what users get, not how it is done
5. Installation: prerequisites, how to install, what happens on first launch, removal
6. Quick start
7. Usage and keys
8. Configuration and where data is stored
9. Limitations (written in the user's language)
10. Related links: CHANGELOG, `docs/dev-remarks.md`
11. terminu family: follows terminu design, lists the other family members
12. License

No "status" section with a hard-coded version number — versions are left to the badge and the CHANGELOG.

Where the README talks about the icon width (usually the Nerd Font part of the prerequisites), it names both
`<APP>__ICON_WIDTH` and `TERMINU__ICON_WIDTH`, and says the latter is shared by the whole family: set it once and every
family app reads it; inside a family app's PTY the outer app sets it (E5). The form is free (a table or a sentence).
It names no font as "always two cells" — the same font may move the cursor differently on different terminals.

**`docs/dev-remarks.md`** (Traditional Chinese): what developers need to remind themselves of during development, and
decisions recorded while working with AI.

```
# <app> 開發者備忘
前言（一句話 + 遵循 terminu design principle）
## 運作方式
## 設計決定（決定 + 理由）
## 已否決，不要重提
## 已知的牆與未做
## 偏離 tdp（哪一條、在哪裡、為什麼）
## 設計文件導讀
## 建置與開發
## 發布（含踩過的坑）
```

The skeleton above is kept in Chinese because the file itself is written in Chinese. In order: title (`<app>` developer
notes), a preface (one sentence + follows the terminu design principle), how it works, design decisions (decision +
reason), rejected — do not raise again, known walls and not done, the "偏離 tdp" section (departures from tdp: which
rule, where, why), a guide to the design documents, building and development, releasing (including pitfalls hit).

**`docs/<app>-terminu-fix.md`**: where the app does not yet follow tdp, item by item, to fix (which rule is violated,
where, the current state, and how to fix it).

**Other design documents** (`ui.md`, `ux.md`, `function.md`…) are each app's own business — whether to have them and how
to split them is not tdp's concern; the "設計文件導讀" (a guide to the design documents) section of dev-remarks points
the way. There is no separate document mapping tdp clause by clause — what complies needs no record, departures go in
dev-remarks, violations in fix.md.

**Why**: a README introduces the tool, and what users want from it is "what is this, how do I install it, how do I use
it"; developer notes go elsewhere, so both are easy to find.

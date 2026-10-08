# tdp Rules

**Language**: English · [繁體中文](rules-zh_TW.md)

Every rule here **must hold**. Each carries a "why", which is its origin UX ([Principle P0](README.md#p0-rules-serve-the-ux-not-the-other-way-round)).

**Zones**: each rule heading is tagged `fixed` or `concept` ([Principle P5](README.md#p5-fixed-zone-and-concept-zone)). In a `concept` rule the semantics are still fixed; only the implementation is left to the app.

**Departure**: the fixed parts are followed as a rule. When an app's nature makes a rule
inapplicable, the app must write down **which rule, where, and why** in the "偏離 tdp"
(departures from tdp) section of its `docs/dev-remarks.md`. With a written reason it is a
**departure**; without one it is a **violation**, listed in `docs/<app>-terminu-fix.md`.

**Citing**: `tdp` plus the ID, e.g. `tdp K4`, `tdp M2`. Once published, IDs are never
renumbered; a retired rule keeps its ID and is marked retired.

| Chapter | Scope |
|---|---|
| [K](#k-core-keys) | Core keys |
| [M](#m-menus-and-disclosure) | Menus and disclosure |
| [L](#l-layout) | Layout |
| [F](#f-popups) | Popups |
| [X](#x-mouse) | Mouse |
| [T](#t-time-axis) | Time axis |
| [E](#e-app-and-environment) | App and environment: command line, environment variables, requirements, releases, documents |
| [S](#s-splash) | Splash (the family easter egg) |

---

## K Core keys

### K1 Core keys mean the same thing everywhere in the app `fixed`

| Key | Meaning | Rule |
|---|---|---|
| `Tab` | Move focus to the next object on the same level | K2 |
| `Enter` | Do the most obvious action to the focused item; in an input popup, submit | K3 |
| `Esc` | Cancel / close the top layer | K4 |
| `Space` | On a panel, open / close the Space menu (what can be done here) | K5, M2 |
| `?` | Open / close the key reference: what keys work on the frontmost surface (read-only) | K6, M4 |
| `q` | Quit the app | K9 |

These keys carry this meaning on **every surface**; the only exceptions are input state
(K8), PTY (K10) and modes (K11). An app need not use all of them (a single-panel app has no use for
`Tab`), and may designate core keys of its own; once designated, those also keep their
meaning on every surface. **No letter hotkey may take over a key in this table.**

**Why**: what users learn is a **role** ("cancel", "move focus", "what can I do now"),
not a key. With the roles fixed, one lesson holds on every surface of every app in the
family. A single surface where `Space` does something else adds a rule to learn: "except
here".

### K2 `Tab` switches focus between objects on the same level `fixed`

`Tab` moves focus to **the next object on the same level within the current surface**,
wrapping from the last to the first:

| Focus is on | `Tab` switches between |
|---|---|
| a screen | panels |
| a form ([components/dialog/form](../components/dialog/form.md)) | fields (one field at a time; the options inside a field move with hjkl, K12) |
| a popup with two areas (a finder, a datetime picker) | areas |

- `Tab` does not cross screens or leave the current popup.
- With focus in a PTY, `Tab` belongs to the subprocess (K10).
- **An input popup always has a single field** (several fields make a form, see the table): with a greyed-out
  suggestion, `Tab` **accepts the suggestion** (autocomplete), and does nothing else. (Since 2026-10-07; before, `Tab`
  switched fields in an input group and a suggestion there was accepted with a key the app chose, e.g. `→`.)
- In the writing state of multi-line text, `Tab` is an indent character, not a field switch (K8).
- Cycling backwards (e.g. `Shift-Tab`) is a hotkey; whether to offer it is up to the app; a form always has
  `Shift-Tab` (components dialog/form).

**Why**: users press `Tab` expecting "the next one" — the next panel on a screen, the
next field in a form. It is the same role at different levels. Switching screens is a
global operation (P3).

### K3 `Enter` does the most obvious action; in an input popup it submits `concept`

`Enter` does **the most obvious action** to the focused item — enter a directory,
connect, open, flip a setting. What exactly is up to the app, but the same kind of item
always gets the same action within an app.
When the panel itself is a content area with no "item" to pick (e.g. a preview, a log),
`Enter` does the most obvious action to the whole panel, as the app decides (e.g. open a
scrollable view).

**In an input popup, `Enter` submits** (fixed):

- **`Enter` always submits** the one value. If the value is invalid, **nothing is submitted**: the error goes in the
  reserved error row (F7) and the popup stays.
- In **multi-line text input**, `Enter` is a newline; submitting is triggered instead by
  `Enter` after leaving the writing state.
- **A typing row with a candidate list** (a finder, a select's filter): `Enter` moves the focus to the list, and a second
  `Enter` there submits (F1).

**A form** ([components/dialog/form](../components/dialog/form.md)) is not an input popup: in a form, `Enter` acts on the focused item — opening that field's input popup,
choosing a radio option, flipping a checkbox, pressing the button; submitting is the button or `Ctrl-S`, which checks
**every** field, submits nothing if any is invalid, and moves the focus to the first invalid field. Once an input popup is
confirmed, the form's focus moves on to the next field — the result of confirming a field, not `Enter` standing in for
`Tab`. (Since 2026-10-07; before, several fields shared one input popup, and `Enter` in any of them submitted the whole.)

In other popups (menu, confirm), `Enter` runs the row under the cursor / accepts.

**Why**: a literal definition such as "confirm / enter" does not survive real apps; what
users expect from `Enter` is "do the natural thing to this". In a form, that thing is
submitting — and submitting an invalid form, or failing to submit without saying why,
both leave the user stuck.

### K4 `Esc` closes one layer at a time and never leaves the app `fixed`

`Esc` cancels the current operation or closes the top layer: a popup if there is one
(toasts included, F3); otherwise it leaves the current mode (search, selection, dragging)
or goes up one level — what "up one level" means is defined by the app. **One layer per
press**, and **`Esc` never leaves the app** — at the top it does nothing.

When a popup opens another (e.g. Space menu → global operation popup → confirm), `Esc`
**closes only the topmost one**; the popups underneath stay exactly as they were and are
shown as before; the next press closes the next layer (F4).

**Why**: a lost user presses `Esc` repeatedly to get back somewhere safe. If the end of
that sequence is the app closing, `Esc` becomes a dangerous key, users stop pressing it,
and the safe way out that "cancel" provides is gone. Quitting has its own key (K9).

### K5 `Space` opens and closes the Space menu on a panel `fixed`

- With focus on a panel, `Space` opens the Space menu (M2); while the Space menu is open,
  `Space` closes it again. `Esc` closes it too.
- **`Space` closes only the Space menu it opened itself.** On any other popup (a confirm,
  input, viewport… opened by `Enter` or a hotkey), `Space` **does nothing**; those are
  closed by `Esc` or by their own flow.
- A popup's own operations (e.g. switching a viewport's layout) run by hotkey, disclosed
  in the hint on the popup's bottom border and in that popup's `?` help (K6); no Space
  menu is stacked on top of a popup.

**Why**: an entry key that opens but cannot close is a trap — users reach for the same
key to get out and nothing happens. But if `Space` could also close a confirm, it would
double as `Esc`'s "cancel" (P4); and if it could stack a menu on a popup, boxes on boxes
would have no end. The family's flow is always: `Space` on a panel opens the menu, `Enter`
on a row, and only then does the next popup open.

### K6 `?` opens and closes the key reference from anywhere `fixed`

`?` responds on any surface; `?` again closes it, and so does `Esc`. It opens **the key
reference of the frontmost surface**: read-only and scrollable, with no cursor and nothing
to run (M4).

| Focus is on | The key reference lists |
|---|---|
| a panel | the keys that work on this panel, and the core keys |
| a popup (the Space menu and the global operation popup included) | **only this popup's** keys |

Input state, PTY and modes follow K8, K10 and K11.

**Why**: whoever presses `?` wants to **read** "what can I press here". Putting reading
and doing in one box leaves the user standing on a list with a cursor where every row can
be pressed — and afraid to move (F1: a popup belongs to exactly one class). What can be
done is under `Space`; what can be pressed is under `?`.

### K7 Aliases are complete `fixed`

When a role is bound to several keys, every alias must work **on every surface**. If that
is not possible, don't alias.

**Why**: a partial alias (a key that cancels on the main screen but not in popups) is
worse than none — it looks like a convenience, but adds a rule to learn: "where it works
and where it doesn't".

### K8 Input state: hotkeys are all off `fixed`

While the user is typing (an input popup, a search row; a form itself is not in the input state, see components
dialog/form), **every key that produces a character is a character** and triggers nothing:

| Key | In input state |
|---|---|
| letter hotkeys, `Space`, `?`, `q` | typed as characters |
| `Esc` | cancels the input (K4) |
| `Enter` | submits (K3) |
| `Tab` | accepts a grey suggestion (K2); in a popup with two areas, moves to the other; in the writing state of multi-line text, a character (indent) |
| `Ctrl-C` | starts the quit flow (K9) |

Normal behaviour returns the moment focus leaves the input surface.

**In the writing state of multi-line text**, `Tab` is a character (an indent), just as
`Enter` is a newline (K3); to submit, leave the writing state first (`Esc`), then press `Enter`.
Whether the indent inserts `\t` or spaces is up to the app.

**Why**: `Space`, `?` and `q` are all printable. Without this, users could never type a
file name with a space or a password with a question mark. `Esc` and `Enter` stay,
because they do not compete with characters, and without them the input box is a trap
with no exit.

### K9 `q` and `Ctrl-C` quit the app `fixed`

- `q` and `Ctrl-C` do **the same thing**: start the app's quit flow. `q` is a character
  in input state (K8); `Ctrl-C` still works there. With focus in a PTY both belong to the
  subprocess (K10).
- **The quit flow is up to the app** (concept): quit at once, confirm first, or let the
  user choose how to quit. E.g. sshu asks whether to close open sessions first; filu lets
  the user choose whether to switch the shell to the last directory.
- **Pressing `Ctrl-C` again during the quit flow quits at once**, with no further
  questions.
- Quitting is listed in the global operation popup (M4).

**Why**: `Ctrl-C` is in every terminal user's muscle memory, and `q` is the TUI
convention; if the two behaved differently, users would have to remember which one asks
and which one doesn't. Pressing `Ctrl-C` twice to force quit means users can never be
trapped by their own confirm box.

### K10 PTY: keys belong to the subprocess, with at least one exit key `fixed`

With focus in a PTY (a shell, editor or remote session running inside the app), **keys go
to the subprocess**: core keys and the app's hotkeys stop working — vim needs `Esc`, the
shell needs `Tab` and `Ctrl-C`, a remote program may want any chord.

- The app designates **at least** one exit key that moves focus out of the PTY (a
  combination the subprocess almost never uses; the family uses `Alt-Esc`) and discloses it
  permanently while focus is in the PTY.
- **`Alt-Esc` always confirms first**: whenever it would move focus out of the PTY or end the
  subprocess, whether or not the subprocess stays alive, a confirm comes first (`Enter`
  leaves, `Esc` returns to the PTY); what it does inside the PTY (e.g. stepping zoom down
  one level) needs no confirm. Why: terminals send an Alt chord as "`Esc` plus the key", so
  `Alt-Esc` is byte for byte two `Esc`s. When the app is busy the reading end stalls, and two
  `Esc` presses pile up and are read as `Alt-Esc` (measured 2026-09-29 with bubbletea
  v1.3.10: with keys already queued, two `Esc`s 150 ms apart still merged). Pressing `Esc`
  twice is common in vim; the confirm lets whoever misfired press `Esc` to go back.
- **Other Alt-chord exit keys** (e.g. kbu's `Alt-t` hiding Alterm, sshu's `Alt-Enter` on a
  locked cell) can be spelled the same way by "`Esc` then that key"; whether they confirm is
  up to the app.
- Whether the app keeps other chords of its own inside the PTY besides the exit key (e.g.
  sshu's zoom, move to another cell and history scroll inside a cell) is up to the app.
  Any it keeps are disclosed permanently, like the exit key (M3).
- Where focus lands after the exit key is up to the app.
- While the subprocess is not ready for keys yet (e.g. the remote end is still connecting),
  the app may hold ordinary keys back (so they don't land minutes later), but **`Ctrl-C` is
  still forwarded to the subprocess**, and the exit key still works and is still disclosed.
  With focus in a PTY the user takes every key as pressed inside the PTY; the only
  exceptions are the disclosed exit key and the chords the app keeps.

**Why**: with focus in a PTY, nearly everything the user does is the PTY's business; the
more keys the app intercepts, the likelier it breaks the subprocess, and the more "who
owns this key right now" becomes something to remember. But a PTY with no way out is a
trap, so there must be at least one exit key, and it must be visible; whether to take
more depends on how the app's PTY is used — a single shell and a whole grid of live
remote sessions have different answers.

### K11 Core keys inside a mode `fixed`

With focus inside a mode (see the term), the core keys act like this:

| Key | Inside a mode |
|---|---|
| `Space` | **opens no menu**; does nothing |
| `?` | the mode's key reference (read-only, K6): which keys work in the mode and what they do |
| `Esc` | leaves the mode (K4), back to where it was entered |
| `q`, `Ctrl-C` | run the quit flow, as K9 |
| `Tab` | a mode may suspend `Tab`, but pressing it must respond, saying to leave the mode with `Esc` first (e.g. a toast); while the toast is up, the first `Esc` closes it (K4) |

- A mode has no Space menu and no list of keys to run. The mode's own keys (move, select,
  drag) are pressed directly; they are disclosed in the `?` key reference and in the footer
  / bottom-border hint (M3, as it applies inside a mode).
- The footer still shows `?` inside a mode (M1); `Space` does nothing there and need not
  be listed.
- **A mode shows itself**: its name always appears at the **right of the top border** of
  the frame it lives in (panel or popup), and the frame turns the mode colour (see
  [components/color](../components/color.md)); leaving the mode restores both. A focused panel keeps its focus line style
  (L5) in a mode; only the colour changes.
- **The mode name sits between two border junctions**, like a label set into the frame:
  `╔═[1] Kinds════╡Drag╞═╗`, `╭─ YAML ────┤Visual├─╮` (how the junctions are drawn is in
  [components/layout/panel](../components/layout/panel.md)).

**Why**: a mode is always a special case; its keys are movement and selection, pressed
directly and in runs, not actions on an item, and there is no item / panel / global to
split them by. Turning them into a list you pick and run from (even `h j k l` run from a
list) only adds a detour; all the user needs is "what can I press here", which is exactly
`?`'s job.

### K12 Navigation letters are kept for movement; hjkl are the arrow keys `fixed`

Where nothing is typed, `j k u d g G h l` are kept for movement, and no action takes them. `h`/`j`/`k`/`l` are
`←`/`↓`/`↑`/`→`, meaning what the layout makes them mean:

- **With a left-right structure** (tabs, two sides, a grid): up, down, left and right. `j`/`k` move up and down a list,
  `h`/`l` go left and right — to another tab, to the other side, to the day before or after in a calendar.
- **In a plain one-dimensional list with no left-right structure** (a form, a one-value-per-row panel without tabs, a
  menu): `h`/`k` (`←`/`↑`) go back, `j`/`l` (`↓`/`→`) go on, whether options run across or down.
- A one-dimensional list in a panel with tabs: `h`/`l` go to the tabs, `j`/`k` still move in the list.
- **`u`/`d` move half a page, `gg`/`G` to the top and the bottom.** `gg`, not a single `g`; `Ctrl-U`/`Ctrl-D` are
  not taken as aliases (the user, 2026-10-07).

**Why**: in the family hjkl are the arrow keys — forms, panels and lists all move with them; an app binding one to an
action has users trigger an action while they think they are moving. With a left-right structure, left and right are
left and right (filu's, kbu's and webu's `h`/`l` switch tabs, sshu's cross to the other side); without one, the left and
right keys are idle and get "back" and "on", so users need not wonder whether options run across or down. It used to be
a habit in Family defaults D5 ("`h` `l` switch tabs within a panel"); the user made it a rule on 2026-10-07.

---

## M Menus and disclosure

### M1 The entry points are visible `fixed`

Every screen outside input state must **permanently show** the two entry points, `Space`
and `?`, so a first-time user who has read no documentation can see them. The form is up
to the app (footer, sidebar, empty-state hint).

**Why**: users cannot press a key they do not know exists. An undisclosed entry point
might as well not exist, however complete the disclosure behind it (Principle P2).

### M2 Space menu: item → panel → global, three regions `fixed`

The Space menu lists **everything the current panel can do**, split by what it acts on
(Principle P3), in a fixed order:

| Order | Region header | Contents |
|---|---|---|
| 1 | `item operation` | what can be done to the one item under the cursor |
| 2 | `panel operation` | what can be done to the current panel (or its tab) as a whole |
| 3 | (no header) | **always a single row**, `Global operation`: `Enter` opens the global operation popup (M4) — even when the app has only one global action |

- **The header strings are fixed**, word for word as in the table above, across the app
  and the family.
- **The global row carries no region header**: its label `Global operation` already says what it is, and a `global operation` header above it only repeats it; a divider still separates it from the regions above.
- **No target, no region**: an empty list has no item, so item operation disappears,
  header and all.
- **On a panel's Space menu, the item and panel regions always carry their headers** (even when only one of them is left): the global row is always there, so the menu never holds just one kind of thing. Only the global row, and other ungrouped menus (M8), go without headers.
- Regions are separated by a divider line.

**Why**: users read top down, so they see "what can I do to the thing I picked" first,
then "to this whole panel", and global last. Fixed header strings let users recognise
"this is the same kind of menu" at a glance — a menu worded differently reads as a
different **kind** of menu. Putting global last, as a single row, means remembering the one key `Space` is enough to
find everything, without the global actions outgrowing the panel's own; and every app in
the family has a Space menu of the same shape.

### M3 Every action can be found in a menu `fixed`

- Every item operation and panel operation of every panel is in that panel's Space menu.
- Every global operation is in the global operation popup (opened from the Space menu's
  global row).
- A popup's own operations are all in that popup's bottom-border hint and `?` key
  reference (K5, K6).
- **A letter hotkey is a shortcut to a row in some list, not an extra feature.** An
  action triggered only by hotkey and found nowhere else is a violation.

Which region an action belongs to depends only on **what it acts on**, never on how
important it is (Principle P3).

**Why**: a new user who has never seen a hotkey must be able to do everything, anywhere,
with `Space` and `?` alone. Each action that has to be learned in advance is a hole in
"usable without the docs".

### M4 The global operation popup and the key reference `fixed`

**The global operation popup** (doing)

- Opened with `Enter` on the Space menu's global row (M2), over the Space menu; it is a
  menu (F1) listing **all** of the app's global actions — `j/k` to pick, `Enter` or the
  row's hotkey to run. Quitting the app must be here (K9).
- `Esc` goes back to the Space menu (F4); an action that closes the whole stack follows T1.
- The row that switches to the current screen is dimmed as M6 says (e.g. `[M]anage` while
  on `[M]anage`).

**The key reference** (reading)

- Opened with `?` (K6). Read-only and scrollable, with no cursor and nothing to run — not a
  menu.
- On a panel it lists at least the core keys and the keys that work on this panel; on a
  popup, the keys that work in that popup. Anything more is up to the app.

**Why**: a read-only help page cannot replace a list you can run (Principle P2) — what
can be done is under `Space` and in the global operation popup, one step from running;
`?` is a cheatsheet to glance at alongside. Reading and doing live in two boxes, each of
one class (F1). With the global actions gathered in one popup, no Space menu has to list
them again.

### M5 Each row = name + description, hotkeys marked with `[]` `fixed`

Each menu row has the **action name** on the left and a **one-line description** on the
right:

```
 item operation
 [o]pen                        open it with the OS default app
 [r]ename                                    this item, in place
 ─────────────────────────────────────────────────────────────
 panel operation
 [/] Search                                everything under here
 ─────────────────────────────────────────────────────────────
 global operation
 [q]uit                                            leave the app
```

How keys are written is one rule for the whole app (menus, footer, panel hints, popup
hints, the key reference, and the README). Marking inside a label:

| Case | Form |
|---|---|
| Single letter | `[r]ename`, `[D]elete` |
| With a modifier | `[Alt-t]erm` |
| Several characters | `[go]to` |
| Digits | always in front: `[3] Favorites`, never inside the word |
| No hotkey | no brackets |

- **What is in the brackets is exactly the key to press, case included**: `[A]dd` is
  `Shift-A`.
- Colour or a glyph alone must not be the hint that "this is a hotkey"; mark it
  explicitly.
- What the description says is up to the app, but it must fit on one line.

**Key names** (the same everywhere on screen and in the README):

- The name printed on the key cap, UpperCamelCase, no abbreviations of our own: `Esc`,
  `Tab`, `Enter`, `Space`, `Backspace`, `Delete`, `Home`, `End`, `PgUp`, `PgDn`; arrows
  `↑` `↓` `←` `→`.
- Letters in the case actually pressed: `q`, `A` (that is `Shift-A`), `Alt-z`. The letter
  after `Ctrl` is always upper case (`Ctrl-C`, `Ctrl-U`): terminals can't tell the case of a
  `Ctrl` chord.
- Modifiers are joined with `-`: `Alt-t`, `Ctrl-C`, `Shift-Tab`, `Alt-Esc`.
- Several keys doing one thing are joined with `/`: `j/k`, `h/l`; a range uses `–`: `1–9`.

**By place**:

| Place | Form | Example |
|---|---|---|
| Label (menu rows, statusbar chips, panel titles) | the bracket marking above | `[r]ename`, `[Alt-t]erm` |
| Sentence (empty states, toasts, error messages, and keys mentioned in the description column of a menu or the key reference) | every key in square brackets | `Press [A] or [Space]`, `see App Log [!]`, `next tab [h]/[l]` |
| Hint, footer | `key:description`, no space around the colon, one space between items | `Enter:delete Esc:cancel` |
| Key reference | two columns, key and description; no brackets, no colon on the key | key column `Esc`, description column `close this popup` |

- In hints and the footer the key and its description are told apart by colour: the key in
  one colour, the colon and description in another (see [components/color](../components/color.md)). A description
  may run to several words; the key's colour still shows where each item starts.
- **README**: keys in the prose are Markdown code (`` `Enter` ``, `` `Ctrl-C` ``), not
  square brackets; names and notation as above. A label quoted from the screen is written as
  on screen (`[A]dd`).
- **Another tool's own keys** (e.g. tmux's `prefix l`, `C-a x`) are written the way that tool
  writes them: the user types them into that tool's config or reads them in its docs.

**Why**: the name answers "what action is this", the description answers "what does it
do to what" — the same verb can mean different things on different panels (delete the
file, or remove the bookmark?). A description that won't fit on one line usually means
the action is badly named. Digits stay out of words because `432hz` would render as
`4[3]2hz`.

### M6 Actions that can't run right now: dimmed `fixed`

- **No target**: the row (or region) is not shown (M2).
- **A target, but the action can't run right now**: the row is still shown, **dimmed**,
  keeping its usual description with no reason added; the cursor can land on it, and
  neither `Enter` nor its hotkey does anything.
- **The `?` key reference follows the same rule**: a key whose target exists but can't run
  now is still listed, dimmed; with no target it is not listed. Hints and the footer, short
  on room and always on screen, may list only the keys that work now; that is up to the app.
- A separately titled section of the key reference describing **another surface** (e.g. the
  `ssh grid` section of sshu's list `?`, since a cell has no key reference of its own) is not
  this surface's keys and is shown at full brightness.

**Why**: users take a hidden action to mean the app doesn't support it; dimming tells
them "this exists, just not now". No reason is added because the reasons vary endlessly,
and squeezing them into a one-line description would let every row's length run out of
control (M5).

### M7 Entry points on a panel always respond `fixed`

With focus on a panel, `Space` and `?` must both open a menu when pressed, never nothing.
With no runnable action, the menu still opens and says there is nothing to do, and how to
close it. On a popup, the key that always responds is `?` (K6).

**Why**: when a key does nothing, users think the key is broken, not that there is
nothing to do here.

### M8 Other grouped menus: cursor-related first `concept`

Any menu other than the Space menu (e.g. a sort picker, an open-with list) that groups
its rows puts the actions related to the current cursor first, then gives each following
group a header naming its kind. A menu that needs no grouping is listed directly.

**Why**: as in M2 — users look first for "what I can do to the thing I picked".

### M9 When one key has two indicators, mark which one fires `concept`

When a hotkey does different things on different panels and both indicators are **on
screen at the same time**, the user must be able to see at a glance **which one fires on
the current focus**. How to mark it is up to the app; the family's way is that the one
that fires is bright, the other dim ([components/color](../components/color.md)).

**Why**: with two identical keys on screen at once, the user has no way to tell which
thing pressing it will do.

---

## L Layout

### L1 Minimum supported size: 80 columns × 40 rows `fixed`

At **80 columns × 40 rows**, the app must be able to complete all its core tasks. That is
roughly a terminal window on half of a 16:9 screen (8:9). How the panels split, what folds
away when narrow, and what happens below this size are up to the app.

**Why**: a terminal often takes only half the screen — the other half is an editor, a
browser or another terminal. A TUI that only works full screen is unusable in the everyday
split window.

### L2 Width does not follow content `fixed`

Dynamic text in titles, statusbars, chips and the like uses fixed-width slots or padding;
its width never changes with the length of the content.

**Why**: once widths float, the main view shifts sideways with them, and the whole screen
shakes as popups open and close.

### L3 Chrome has a fixed number of rows `fixed`

The number of rows for footer, statusbar, tab row and other permanent chrome is **the
app's choice, and once chosen it is locked**; it does not change with the amount of
content. What doesn't fit is truncated or dropped from the end, never wrapped.

**Why**: one more chrome row is one less main row, and the whole layout shifts in a chain.
Stability always beats saving space.

### L4 Every line is exactly the terminal width `fixed`

Every line on screen is exactly as wide as the terminal, no more, no less.

**Why**: one cell too many and the terminal wraps, knocking the whole screen out of
place; one too few and stale cells linger on screen. Misjudged CJK and icon widths are
the usual cause.

### L5 Focus is visible, and moving it moves nothing else `fixed`

The focused surface must be recognisable at a glance (how to mark it is up to the app),
and moving focus **must not shift any content**.

- **Focus is not told by colour alone**: something besides colour must differ (e.g. the
  line style). A mode turns its frame the mode colour (K11); with colour alone, focus
  vanishes the moment a mode starts. The family default is a double line `╔═╗` for focus
  and rounded `╭─╮` otherwise, the same width ([components/color](../components/color.md)).

**Why**: users need to know where their keys will go; and if the screen jumps every time
focus moves, the eye has to find its place again.

---

## F Popups

### F1 Popups come in seven classes, one class at a time `fixed`

The family's popups come in these seven classes only, each with fixed key meanings:

| Class | What the user can do | E.g. |
|---|---|---|
| **menu** | `j/k` moves the cursor, `Enter` or a hotkey runs the row | Space menu, global operation popup, option lists, a jobs list (`Enter` opens the row in full) |
| **confirm** | read a reminder or warning; `Enter` accepts, `Esc` cancels (F6) | confirm before delete, the quit confirm, "Connect to X?" under the host's details |
| **input** | type (input state, K8), `Enter` submits (K3), `Tab` accepts a suggestion (K2); one value per popup | rename, address bar |
| **form** | one value per row; `Tab` jumps a field at a time, hjkl move item by item (K12), `Enter` acts on the focused item (opening that field's input popup, choosing a radio option, flipping a checkbox, pressing the button), the button or `Ctrl-S` submits ([components/dialog/form](../components/dialog/form.md)) | sshu's Host form, webu's Sign in and Add bookmark |
| **note** | read-only, scroll with `j/k/u/d`; no list of rows to run with `Enter` | key reference, YAML viewer, app log |
| **toast** | a one-line message from the bottom, gone on `Esc` or on its timer; every key but `Esc` passes through it | "Copied", an operation failed |
| **terminal** | a subprocess running in the box; every key is its, only the exit key is the app's (K10) | kbu's Alterm, filu's shell |

- **A note may have hotkeys and modes of its own**: e.g. the YAML viewer's `/` search, `y`
  copy, `v` select (a mode, K11). Its hotkeys are disclosed in the bottom-border hint and
  in `?`; but once it has a list of rows to run with `Enter`, it is a menu, not a note.
- **A menu's `Enter` may open the row in full**: a list with a cursor and no other action
  of its own (e.g. a jobs list) may open a note with the row's whole content on `Enter`; it
  is still a menu.
- **A confirm may carry content to read before answering**: the question is why a confirm
  exists, and above it may sit what to look at before answering (e.g. the host's details
  above "Connect to X?"), scrolled with `j/k` when long; it is still just a confirm, not a
  note plus a confirm, and need not be split into two popups.
- **A popup may change class by phase, but belongs to one class at a time.** E.g. a finder
  is an input while typing and a menu while its result list has focus; `Tab` moves focus
  between typing and the list, and `Esc` closes the whole finder (K4: a phase is not a
  layer). A preview beside it takes no focus and is not another surface. **Which side has
  focus must show**: only the side holding the keys is lit (how it looks: [components/input/search](../components/input/search.md)).
- **An input may carry a candidate list** (a list filtered as you type): printable keys are
  always characters (`j` and `k` too, K8), only the arrow keys move among candidates, and
  `Enter` moves the focus to the chosen one in the list, where a second `Enter` submits it
  (the user, 2026-10-07; before, `Enter` while typing submitted at once — see
  [components/input/search](../components/input/search.md)). It is still an input, not two
  classes at once.
- **Each step of a multi-step flow is its own popup**: e.g. sorting by picking a column,
  then a direction, is two stacked popups (F4 keeps the source), not one box changing its
  content — each step has its own UX, and its own height fixed at opening (F7).
- **form is the seventh class, added 2026-10-07** (by the user): several fields used to share one input popup (the
  example read "host form"); once a form only shows values and opens an input popup per field, it is no input, and none
  of the other five classes either.
- Not in these seven: the splash (chapter S), and panel content an app draws as a box (e.g.
  webu's page dialogs, webu's departure).

**Why**: the class is the user's expectation of "what keys do inside this box". With seven
classes, each of fixed meaning, nothing is relearned from one app to the next; a popup of
two classes at once gives the same keys two possible meanings inside one box.

### F2 Opening and closing are both animated `fixed`

Popups **must animate** both when opening and when closing. The length is the same across
the family (see [components/layout/popup](../components/layout/popup.md)); the form of the
animation is up to the app.

**Why**: without animation, a popup "suddenly appears, suddenly vanishes", and users don't
feel the change of layer as it stacks on and steps back. The length used to be up to the
app; on 2026-10-07 the user made it the same across the family.

### F3 `Esc` closes any popup at once `fixed`

Any visible popup — auto-dismissing toasts included — starts closing **immediately** on
`Esc`, without waiting for a toast's countdown. Closing is animated as usual (F2); a popup
already running its closing animation ignores `Esc` and takes no other keys either.

**The exception**: a form or a textarea whose content changed first opens a confirm asking whether to discard it
(components dialog/form, input/textarea; since 2026-10-07).

**Why**: users are not obliged to wait out a countdown. If a popup that is already closing
takes another `Esc`, or still eats keys, the user's next key goes to the wrong place.

### F4 The source stays by default `fixed`

When popup A opens popup B, A stays underneath by default; cancelling B returns to A.
The same holds at any depth: `Esc` closes only the topmost, and the stack underneath is
shown as it was (K4).

**Why**: the user did not dismiss A, they just did one interaction in B. If cancelling B
also removes A, they have to walk the whole way again. (Whether A stays after B
completes is T1.)

### F5 Errors show at once, without blocking the app `concept`

Errors must appear immediately (toast or popup), close on `Esc`, and **must not block the
app**. Whether there is an error history to look back at is up to the app.

**Why**: an error you can't see never happened; an error that blocks the app keeps the
user from dealing with the error itself.

### F6 Confirm: `Enter` accepts, `Esc` cancels, and it says what will happen `fixed`

- **Which actions need a confirm is up to the app**, regardless of whether they are
  reversible. Once an action is set to be confirmed, it is confirmed every time. The
  exception: a choice made explicitly in a picker may count as the confirmation (e.g.
  picking the default app from an "open with" list), as the app decides.
- `Enter` accepts, `Esc` cancels (K3, K4). A confirm may have hotkeys of its own (e.g.
  `y` / `n`), listed in the confirm's `?` help (K6).
- The prompt says **what accepting will do** (verb and object), not an abstract OK.
- A confirm cannot be completed by accident (e.g. a mouse click must not accept it).

**Why**: users must know the consequence before pressing `Enter`. Whether to stop and
confirm depends on how much the action weighs for the user — launching an external
program, cutting a session, deleting a file: the app knows the weight best, and no rule
such as "reversible means no need to ask" can judge it.

### F7 Popup size and position `fixed`

- **Width**: `min(terminal width − 2, 120)` — one column spare on either side of the
  terminal, at most 120 columns; centred horizontally.
- **Height**: follows the content, **fixed when the popup opens** and not resized with the
  content afterwards; at most the screen height less top and bottom margins, scrolling
  inside the box beyond that. Only two cases may change the height while the popup is open:
  - **Loading**: a popup whose content is not known when it opens (streaming, loading)
    may change height while loading; when loading ends the height is fixed.
  - **A change the user made**: when the user's own action in this popup changes its row
    count (removing a row, a choice that adds a row, filtering candidates as they type),
    the height **may** follow — the user expects that change; the app may also keep the
    height. The principle is that what is disclosed is correct.
- **Loading is always disclosed**: while a popup is loading, a spinning loading icon
  **always** sits after its title (spec in [components/layout/popup](../components/layout/popup.md)), whether or not its height changes; the
  icon goes when loading ends. Loading here means the content of the **whole popup** has
  not arrived (e.g. the list's items are not all loaded). If just **one item** is itself a
  continuous stream of data (e.g. a connection that keeps sending), it is that item that is
  loading, not the popup — how to disclose it is up to the app.
- **Position**: centred vertically. The toast is the exception: fixed at the bottom of the
  screen, its width by the same rule.
- **An input whose submit can fail reserves an error row**: it opens with one error row in
  its height, blank while there is no error; a failed submit writes its error there (K3),
  and the box keeps its height. An input whose submit cannot fail (e.g. a multi-line editor)
  need not reserve one.
- **The terminal class is the exception**: it takes the whole available area (terminal
  width − 2 × height − 2), with no 120-column cap; the subprocess needs the room.

**Why**: when every popup sizes itself by its content, nobody can tell what it will look
like before it opens, and the box jumps whenever the content changes (L2). A common width
and a height fixed at opening make every box predictable; the 120-column cap keeps a menu's
names and descriptions from drifting apart on a wide screen. The error row lives inside the
box rather than in a popup of its own: the error stays in view while the user fixes it,
with no extra key to dismiss it first.

### F8 With popups stacked, everything below the top one is dimmed `fixed`

While a popup is open, **everything but the topmost popup** — the popups beneath it and
the whole base screen — is drawn in the dim colour. The same holds when popups open in a
row or one opens inside another: only the topmost is ever bright.

- Streaming content underneath (logs, remote sessions) and warning colours (components/color) are dimmed
  too (the exception to T2).
- **How to dim: fade every colour — foreground and background alike — toward the base,
  leaving shapes and layout untouched.** Never strip the colours and redraw, never drop
  backgrounds, never turn every foreground into one dim colour: that breaks whatever is
  drawn with a background (the body of a powerline capsule, a cursor bar, a selection).
  Layer colours, warning colours and streaming content go through the same fade and so
  become dimmed versions of themselves. The calculation is in [components/color](../components/color.md).
- **A toast does not trigger dimming**: it takes no key but `Esc` (F1) and is not a layer.
- **Borders are dimmed too, but keep their layer colour**: the borders of the popups below
  are drawn in a dimmed version of their own layer colour (components/color), not one common dim colour —
  dark, yet still showing which layer each is.

**Why**: all popups share one width (F7), so an upper one hides the side borders of the one
below and the boxes no longer show the layers; brightness is the one cue left, and it is
exactly what "lightness is the z-axis" (components/color) means: only the layer being worked on is bright.

---

## X Mouse

### X1 The mouse is optional `fixed`

The app must be fully usable without a mouse.

**Why**: the mouse is not a first-class terminal input, and many environments (tmux,
SSH, screen readers) don't have one at all.

### X2 The mouse only maps to the keyboard `fixed`

If the mouse is supported, every mouse action maps to a keyboard action; **nothing can be
done by mouse alone**.

**Why**: the mouse should be another way to press the keyboard, not another thing to learn.

---

## T Time axis

The rules in this chapter can't be seen in a screenshot; they exist only in the flow of use — they surface once an app is complete enough, and more will be added as implementation continues.

### T1 After the target completes, does the source still mean anything? `concept`

The source stays by default (F4). The target clears the source before it enters only when
it is clearly judged, by function, that "once the user completes the target, the source
has lost its meaning":

| Target | Clear the source? | Reasoning |
|---|---|---|
| A short confirm / message | keep | the user may want to go back to the menu and continue or cancel |
| A long session (shell, editor) | clear | coming out of the session their attention has moved on; an old menu floating there is disorienting |
| A big context switch (drill-down, page change) | clear | the view underneath has changed; the old menu's target is gone |

**Why**: this can't be written as a general rule — in code both cases look the same, and
a screenshot can't show it either. Only reasoning about "once done with the target, does
the user still want to see the source?" answers it.

### T2 Unfocused panels are dimmed, streaming content excepted `fixed`

An unfocused panel **has its content dimmed the same way as F8** (its border being components/color's
unfocused border); **streaming content (logs, live output, remote sessions) is not dimmed
on blur**. The exception is a popup on top: attention is on the popup then, and everything
below is dimmed as F8 says.

**Why**: dimming says "focus is elsewhere, look later". Streaming content has no later —
information is passing by, and dimming it cuts off the glance from the corner of the eye.
This is also the textbook case of "rules serve the UX" (Principle P0): the origin UX of
"dim on blur" is "don't compete for focus", while streaming's UX is "catch updates from
the corner of the eye" — two goals that happen to land on the same panel, so the rule is
extended rather than streaming sacrificed.

Dimming on blur used to be up to the app (the family default was not to); on 2026-10-07 the
user made it required across the family: only where the keys go is lit, the same as F8
(only the top layer is lit) and F1 (only the side of a finder holding the keys is lit).

---

## S Splash

The splash is the terminu family's shared easter egg, and the **only thing in tdp that is
deliberately not disclosed**. The disclosure rules (M1, M3, M4) and the core-key rule (K1)
do not apply to it; it is not a popup either, so chapter F does not apply. The splash is
documented only in tdp — never in an app's README, menus or help.

### S1 Every app has a splash, opened with `V` `fixed`

Every terminu app has a splash, opened with **`V`** on a panel. `V` is reserved for it:

- When a panel operation of some panel genuinely needs `V`, **that panel** may give `V`
  to the app; the splash cannot be summoned on that panel.
- But **at least one panel** in the app keeps `V` for the splash.

**Why**: an easter egg belongs to the family only if every member has it; and some apps'
domains really do need `V` (e.g. a selection mode) — giving up one panel is better than
the whole app losing the egg.

### S2 Not disclosed `fixed`

The splash does not appear in the Space menu, the global operation popup, the key reference, the
footer or panel hints, and is not written in the README.

**Why**: a listed easter egg is no longer an easter egg. It is the one and only exception
to "disclosure is the only mechanism" (Principle P2) — which is why it is written here
and in no app.

### S3 Any key only closes the splash `fixed`

While the splash is showing, **any key only closes it** — `q`, `Ctrl-C`, `Esc`, `Space`
and `?` included; the key does nothing else. A first `Ctrl-C` only closes the splash; it
does not quit the app.

**Why**: faced with a screen they have never seen, users press any key to make it go
away. If that key also did something else (quit, open a menu), the egg would be a trap.

### S4 On a panel only, and only when asked for `fixed`

- It is not played at start-up.
- It can only be summoned with `V` on a panel; with a popup open, in input state or in a
  PTY, `V` does not summon it (in input state `V` is a character, K8; in a PTY it belongs
  to the subprocess, K10).

**Why**: a splash played at start-up is an intro everyone waits through every time, not
an easter egg; and one that pops up inside a popup, an input box or a PTY interrupts what
the user is doing.

### S5 The content is the family icon `fixed`

The splash draws the app's `docs/icon.svg` — the terminu family mark — cell for cell,
with a reveal animation. How the animation runs is up to the app.

**Why**: the splash is the family's signature. Each member draws its own version of the
family mark, so pressing `V` tells you at once that this comes from the same family.

---

## E App and environment

What an app does off screen: the command line, environment variables, requirements, icon width, releases, documents.
Moved from Family defaults D6 and D7 on 2026-10-07 (the defaults were dissolved; see the table in the
[README](README.md)).

### E1 Command line: `version` and `help` `fixed`

Every app has:

- **`<app> version`**: prints the version. `--version` and `-v` may be aliases.
- **`<app> help`**: prints the command-line usage (unrelated to the `?` key reference inside the app). `-h` and `--help`
  may be aliases.

Other commands (e.g. `filu iconwidth`, `locku lock`, `webu <url>`) are up to the app.

**Why**: `help` and `version` are the first things anyone tries on a command-line tool. kbu once had only `--version`, so
one family app could not be asked its version with `<app> version` (set by the user, 2026-10-07).

### E2 Environment variable names `fixed`

`<APP IN CAPITALS>__<NAME>` — two underscores after the app
name, the name in capitals with single underscores between words (e.g. `FILU__ICON_WIDTH`,
`KBU__ALTERM_LOGIN_SHELL`). Every variable the app itself reads (tests and its own child
processes included) is named this way. Shared names:

| Variable | Meaning |
|---|---|
| `<APP>__CONFIG` | the config **directory** (the config file lives in it) |
| `<APP>__STATE` | the state directory (when the app keeps state separately) |
| `<APP>__DATA` | the data directory |
| `<APP>__CACHE` | the cache directory |
| `<APP>__ICON_WIDTH` | manual override of an icon's cell width (see the icons' real width below) |
| `TERMINU__ICON_WIDTH` | shared by the family: an app with a PTY sets it for its child to say how wide an icon is (see below) |

The exception: variables meant for another program follow that program's needs (e.g. the
`LC_SSHU_COLORTERM` sshu carries over ssh to the remote end — OpenSSH forwards only `LANG`
and `LC_*` by default). Renamed variables do not keep their old names.

**Why**: a variable shows at a glance which app it belongs to, and `TERMINU__` at once means the whole family (a family
rule the user set in v0.1.21).

### E3 Where config and data live `fixed`

Config in `$XDG_CONFIG_HOME/<app>` (falling back to `~/.config/<app>`); data in
  `~/.<app>/`.

**Why**: with the five apps in the same places, users know where to look and what to back up.

### E4 Requirements: a Nerd Font and truecolor `fixed`

- Requires a Nerd Font; PUA glyphs are written as code points in the source.
- Requires a truecolor (24-bit) terminal: catppuccin's pale colours and components/color's layer gradient are indistinguishable in 256 colours, and dimming always outputs 24-bit (components/color). READMEs say so in their requirements, next to the Nerd Font.

**Why**: the family's icons, loading icon, and radio and checkbox glyphs are Nerd Font glyphs; the reason for truecolor is
given above.

### E5 The icons' real width `fixed`

with some fonts an icon takes two cells (the cursor moves two),
while lipgloss measures one, and the borders go crooked. What counts is **how far the
cursor actually moves**: a font whose icon looks wider than a cell but moves the cursor one
(the glyph spills into the next cell) counts as one. The app detects this at startup (CPR:
print an icon, ask for the cursor position), and every width measurement (padding,
clipping, centring, joining, borders, overlaying popups) goes through one display-width
function; the L4 screen tests also run once with two-cell icons, opening each kind of popup
and measuring the bare box and the whole screen with it overlaid.

- Reference implementation: filu `internal/ui/width.go` — `isWideIcon()`, `dispWidth()`,
  `dispClip()`, `padDisp()`, `dispCutLeft()`, `compositeDisp()` (replaces overlay's
  `Composite`, same interface), `centerDisp()` (replaces `lipgloss.Place`), `joinH()` /
  `joinV()` (replace `lipgloss.JoinHorizontal` / `JoinVertical`); detection is
  `DetectIconWidth()` in `iconwidth_unix.go`, called before `tea.NewProgram`; tests follow
  `d6_test.go`.
- Manual override: the environment variable `<APP>__ICON_WIDTH` (filu's is
  `FILU__ICON_WIDTH`). Detection runs on unix only; Windows defaults to one cell,
  overridden by the variable.
- **Inside another app's PTY**: the probe is answered by the outer app's terminal
  emulator, which counts an icon as one cell, so the real width can't be measured. An app
  with a PTY therefore sets `TERMINU__ICON_WIDTH=<the cells it uses>` in its child's
  environment, and every app takes the icon width from `<APP>__ICON_WIDTH`, then
  `TERMINU__ICON_WIDTH`, then the probe. Any family app running inside another's PTY then
  gets it right (filu in kbu's Alterm, kbu in filu's shell). Environment variables don't
  cross ssh; remote nesting relies on the app's own channel (sshu's nesting channel).
- An overlaid popup may be wider or taller than the screen (the frame drawn during a
  resize still has the old size): start at 0 and clip what falls off the screen, and
  **never panic**; when it is larger in both directions it is clipped too, never handed
  back whole. The edge-case tests cover all three (filu's `TestD6CompositeDispOversized`).
- Done means: apart from the width functions themselves, `internal/ui` has no calls to
  `lipgloss.Width`, `lipgloss.Size`, `lipgloss.Place`, `ansi.StringWidth` or
  `ansi.Truncate`.

**Why**: crooked borders make the whole screen unreadable, and the same font can move the cursor differently on different
terminals, so it can only be measured at run time.

### E6 Releases, tests and family assets `fixed`

- A single static binary built with goreleaser; `install.sh` / `uninstall.sh`
  (`curl | sh`, no sudo), also published to the Homebrew tap `vulcanshen/homebrew-tap`.
- Screen tests across sizes: at several terminal sizes, every line is exactly the terminal
  width (L4).
- `docs/icon.svg` is the family mark; the splash (chapter S) is drawn from it cell
  for cell, with a test keeping the two identical.
- `V` is reserved for the splash (S1).
- Demo gifs are recorded with VHS, scripts in `.local/demos/`; the README carries a single
  representative gif.

**Why**: the five apps install, uninstall and release the same way; having installed one, users can install the others.

### E7 Documents `fixed`

**README**: `README.md` (English) and `README-zh_TW.md` (Traditional Chinese) stay in
step, and cover only what users need to know:

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

No "status" section with a hard-coded version number — versions are left to the badge and
the CHANGELOG.

Where the README talks about the icon width (usually the Nerd Font part of the
prerequisites), it names both `<APP>__ICON_WIDTH` and `TERMINU__ICON_WIDTH`, and says the
latter is shared by the whole family: set it once and every family app reads it; inside a
family app's PTY the outer app sets it (E5). The form is free (a table or a sentence). It
names no font as "always two cells" — the same font may move the cursor differently on
different terminals.

**`docs/dev-remarks.md`** (Traditional Chinese): what developers need to remind themselves
of during development, and decisions recorded while working with AI.

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

The skeleton above is kept in Chinese because the file itself is written in Chinese. In
order: title (`<app>` developer notes), a preface (one sentence + follows the terminu
design principle), how it works, design decisions (decision + reason), rejected — do not
raise again, known walls and not done, the "偏離 tdp" section (departures from tdp:
which rule, where, why), a guide to the design documents, building and development,
releasing (including pitfalls hit).

**`docs/<app>-terminu-fix.md`**: where the app does not yet follow tdp, item by item, to
fix (which rule is violated, where, the current state, and how to fix it).

**Other design documents** (`ui.md`, `ux.md`, `function.md`…) are each app's own
business — whether to have them and how to split them is not tdp's concern; the design
documents guide in dev-remarks points to them. There is no separate clause-by-clause map
against tdp: what complies needs no record, departures go in dev-remarks, violations in
the fix file.

**Why**: a README introduces the tool, and developer notes go elsewhere (the user's README rule, set in webu on
2026-09-26).

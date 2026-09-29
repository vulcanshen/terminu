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
| an input popup with several fields | fields |

- `Tab` does not cross screens or leave the current popup.
- With focus in a PTY, `Tab` belongs to the subprocess (K10).
- **In a single input box** (no other field to move to) with a greyed-out suggestion, `Tab`
  **accepts the suggestion** (autocomplete), and does nothing else. In an input group
  (several fields) `Tab` only switches fields; a suggestion there is accepted with a key the
  app chooses (e.g. `→`).
- In the writing state of multi-line text, `Tab` is an indent character, not a field switch (K8).
- Cycling backwards (e.g. `Shift-Tab`) is a hotkey; whether to offer it is up to the app.

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

- **`Enter` always submits.** What it submits may be the whole input group (the whole
  input popup) or a single field, as the app decides; either way it is a submit.
- Submitting the whole input group checks **every** field, and submits only if all are
  valid.
- If any field is invalid, **nothing is submitted**: focus jumps to **the first invalid
  field**, and the error (which field, and why) is written in the input popup's reserved error row (F7). It
  looks like `Tab`, but the logic is entirely different — it points at the problem after a
  failed submit; it does not move to the next field.
- `Enter` does not stand in for `Tab` to move to the next field; moving field by field is
  `Tab` alone (K2).
- In **multi-line text input**, `Enter` is a newline; submitting is triggered instead by
  `Enter` after leaving the writing state.

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

While the user is typing (form field, input box, search line), **every key that produces
a character is a character** and triggers nothing:

| Key | In input state |
|---|---|
| letter hotkeys, `Space`, `?`, `q` | typed as characters |
| `Esc` | cancels the input (K4) |
| `Enter` | submits (K3) |
| `Tab` | switches fields (K2); in the writing state of multi-line text, a character (indent) |
| `Ctrl-C` | starts the quit flow (K9) |

Normal behaviour returns the moment focus leaves the input surface.

**In the writing state of multi-line text**, `Tab` is a character (an indent), just as
`Enter` is a newline (K3); to switch fields or submit, leave the writing state first.
Whether the indent inserts `\t` or spaces is up to the app.

**Why**: `Space`, `?` and `q` are all printable. Without this, users could never type a
file name with a space or a password with a question mark. `Esc` and `Enter` stay,
because they do not compete with characters, and without them the input box is a trap
with no exit.

### K9 `q` and `Ctrl-C` quit the app `fixed`

- `q` and `Ctrl-C` do **the same thing**: start the app's quit flow. `q` is a character
  in input state (K8); `Ctrl-C` still works there.
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
  combination the subprocess almost never uses; the family uses `Alt-Esc`, see D5) and
  discloses it permanently while focus is in the PTY.
- Whether the app keeps other chords of its own inside the PTY besides the exit key (e.g.
  sshu's zoom, move to another cell and history scroll inside a cell) is up to the app.
  Any it keeps are disclosed permanently, like the exit key (M3).
- Where focus lands after the exit key is up to the app.

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

**Why**: a mode is always a special case; its keys are movement and selection, pressed
directly and in runs, not actions on an item, and there is no item / panel / global to
split them by. Turning them into a list you pick and run from (even `h j k l` run from a
list) only adds a detour; all the user needs is "what can I press here", which is exactly
`?`'s job.

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
| Sentence (empty states, toasts, error messages) | every key in square brackets | `Press [A] or [Space]`, `see App Log [!]` |
| Hint, footer | `key:description`, no space around the colon, one space between items | `j/k:move Enter:run Esc:close` |
| Key reference | two columns, key and description; no brackets, no colon on the key | key column `Esc`, description column `close this popup` |

- In hints and the footer the key and its description are told apart by colour: the key in
  one colour, the colon and description in another (family default in D2). A description
  may run to several words; the key's colour still shows where each item starts.

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
that fires is bright, the other dim (D2).

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

**Why**: users need to know where their keys will go; and if the screen jumps every time
focus moves, the eye has to find its place again.

---

## F Popups

### F1 Popups come in six classes, one class at a time `fixed`

The family's popups come in these six classes only, each with fixed key meanings:

| Class | What the user can do | E.g. |
|---|---|---|
| **menu** | `j/k` moves the cursor, `Enter` or a hotkey runs the row | Space menu, global operation popup, option lists, a jobs list (`Enter` opens the row in full) |
| **confirm** | read a reminder or warning; `Enter` accepts, `Esc` cancels (F6) | confirm before delete, the quit confirm, "Connect to X?" under the host's details |
| **input** | type (input state, K8), `Enter` submits (K3), `Tab` switches field or accepts a suggestion (K2) | rename, address bar, host form |
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
  layer). A preview beside it takes no focus and is not another surface.
- **An input may carry a candidate list** (a list filtered as you type): printable keys are
  always characters (`j` and `k` too, K8), only the arrow keys move among candidates, and
  `Enter` submits the chosen one. It is still an input, not two classes at once.
- **Each step of a multi-step flow is its own popup**: e.g. sorting by picking a column,
  then a direction, is two stacked popups (F4 keeps the source), not one box changing its
  content — each step has its own UX, and its own height fixed at opening (F7).
- Not in these six: the splash (chapter S), and panel content an app draws as a box (e.g.
  webu's page dialogs, webu's departure).

**Why**: the class is the user's expectation of "what keys do inside this box". With six
classes, each of fixed meaning, nothing is relearned from one app to the next; a popup of
two classes at once gives the same keys two possible meanings inside one box.

### F2 Opening and closing are both animated `fixed`

Popups **must animate** both when opening and when closing. The form and length of the
animation are up to the app (for the family's way, see D3).

**Why**: without animation, a popup "suddenly appears, suddenly vanishes", and users don't
feel the change of layer as it stacks on and steps back. How long it can be without
breaking the rhythm depends on the popup's size and the app's pace, so it is not fixed.

### F3 `Esc` closes any popup at once `fixed`

Any visible popup — auto-dismissing toasts included — starts closing **immediately** on
`Esc`, without waiting for a toast's countdown. Closing is animated as usual (F2); a popup
already running its closing animation ignores `Esc` and takes no other keys either.

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
  **always** sits after its title (spec in D3), whether or not its height changes; the
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

- Streaming content underneath (logs, remote sessions) and warning colours (D2) are dimmed
  too (the exception to T2).
- **How to dim: fade every colour — foreground and background alike — toward the base,
  leaving shapes and layout untouched.** Never strip the colours and redraw, never drop
  backgrounds, never turn every foreground into one dim colour: that breaks whatever is
  drawn with a background (the body of a powerline capsule, a cursor bar, a selection).
  Layer colours, warning colours and streaming content go through the same fade and so
  become dimmed versions of themselves. The calculation is in D2.
- **A toast does not trigger dimming**: it takes no key but `Esc` (F1) and is not a layer.
- **Borders are dimmed too, but keep their layer colour**: the borders of the popups below
  are drawn in a dimmed version of their own layer colour (D2), not one common dim colour —
  dark, yet still showing which layer each is.

**Why**: all popups share one width (F7), so an upper one hides the side borders of the one
below and the boxes no longer show the layers; brightness is the one cue left, and it is
exactly what "lightness is the z-axis" (D2) means: only the layer being worked on is bright.

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

### T2 Streaming content is not dimmed on blur `fixed`

If an app dims unfocused panels, that may apply only to static content; **streaming
content (logs, live output, remote sessions) is not dimmed on blur**. If the app doesn't
dim on blur, this rule does not apply. The exception is a popup on top: attention is on
the popup then, and everything below is dimmed as F8 says.

**Why**: dimming says "focus is elsewhere, look later". Streaming content has no later —
information is passing by, and dimming it cuts off the glance from the corner of the eye.
This is also the textbook case of "rules serve the UX" (Principle P0): the origin UX of
"dim on blur" is "don't compete for focus", while streaming's UX is "catch updates from
the corner of the eye" — two goals that happen to land on the same panel, so the rule is
extended rather than streaming sacrificed.

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

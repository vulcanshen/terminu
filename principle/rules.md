# tdp Rules

**Language**: English · [繁體中文](rules-zh_TW.md)

Every rule here **must hold**. Each carries a "why", which is its origin UX
([Principle P0](README.md#p0-rules-serve-the-ux-not-the-other-way-round)).

**What is a requirement**: everything stated in the rules, in [components](../components/README.md) and in
[project](../project/README.md) is a requirement. Only three kinds of text are not: examples (however they are
introduced: "e.g.", "for example", "Example:", "such as", an "Examples" column), the "why", and passages marked
"Implementation reference (not a requirement)". Diagrams are requirements too: their structure (frames, where glyphs go,
spacing, alignment, the colours noted beside them) is as drawn, while the names, values and descriptions in them are
examples; where the text and a diagram disagree, the text wins
("[Diagrams and spacing](../components/README.md#components2-diagrams-and-spacing)" in the components).

**Leaving it to the app**: wherever nothing is explicitly left to the app, the requirement is followed. What is left to
the app always says "the app may decide for itself" and states the scope, with the requirements that still hold inside
that scope written beside it; where tdp says "the app may…", it offers an option, which the app may decide for itself
whether to use, and once used it is followed as written there. tdp's scope and its larger openings (the function logic,
the domain's hotkeys and symbols) are in [Principle P5](README.md#p5-leaving-it-to-the-app-explicitly). When a fixed
part does not fit, it is reported as a gap in tdp, and tdp adds a solution or leaves it to the app explicitly; doing it
any other way, outside what is left to the app, is a violation.

**Citing**: a tdp clause is always cited as `tdp` plus its ID, e.g. `tdp K4`, `tdp panel.1`; `Rules K4` and a bare `K4`
do not count. tdp's own documents write `Rules K4`, meaning this document in the same set.

- The rules use the rule ID (`tdp K4`); the principle uses the P ID (`tdp P5`), and its terms `terms.` plus a number
  (`tdp terms.3`).
- The components and the project use section IDs: the file name, a `.` and a number (`tdp panel.1`, `tdp form.6`); a
  `README` uses its folder's name (`tdp components.2`, `tdp input.2`, `tdp project.3`). The section ID is written before
  each section's heading.
- When a whole component is used, the whole file may be cited (`tdp confirm`), meaning every section of it.
- Once published, IDs are never renumbered: a new rule or section gets a new ID; a part split out of a section gets a new
  ID, the old one staying with what was there; a retired one keeps its ID and is marked retired. Section IDs need not
  follow the order in the file. Each tdp version's CHANGELOG names the IDs it changed.

| Chapter | Scope |
|---|---|
| [K](#k-core-keys) | Core keys |
| [M](#m-menus-and-disclosure) | Menus and disclosure |
| [L](#l-layout) | Layout |
| [F](#f-popups) | Popups |
| [X](#x-mouse) | Mouse |
| [T](#t-time-axis) | Time axis |
| [S](#s-splash) | Splash (the family easter egg) |
| [E](#e-app-and-environment) | App and environment: command line, environment variables, requirements, releases, documents, the shared lib |

---

## K Core keys

### K1 Core keys mean the same thing everywhere in the app

| Key | Meaning | Rule |
|---|---|---|
| `Tab` | Move focus to the next object on the same level | K2 |
| `Enter` | Do the most intuitive action to what has focus; with focus on a value, confirm that value | K3 |
| `Esc` | Cancel / close the top layer | K4 |
| `Space` | On a panel, open / close the Space menu (what can be done here) | K5, M2 |
| `?` | Open / close the key reference: what keys work on the frontmost surface (read-only) | K6, M4 |
| `!` | On a panel, open the App Log: what the app has done and what went wrong (read-only) | F5, M1 |
| `q` | Quit the app | K9 |
| `1`–`9` | On a panel, jump to the Nth panel of the current screen (the `[N]` on its frame) | this rule, K11 |

These keys carry this meaning on **every surface**; the only exceptions are input state (K8), PTY (K10), modes (K11),
`q` on a form and on an app's own popup that works like a form, and a form's typing note (K9). A screen that is not
part of the TUI is not a surface and does not follow this table; the app may decide for itself there (Principle P5; e.g.
locku's screensaver and PIN box while locked). Whether to use all of them (a single-panel app has no use for `Tab`) and
whether to designate core keys of its own, the app may decide for itself; once designated, those also keep their meaning
on every surface. **No letter hotkey may take over a key
in this table.**

**The digit keys `1`–`9`**: on a panel (with no popup open) they are kept for jumping between panels, and an app may not
register a digit as a hotkey on a panel. **They work within the current screen only**: each screen numbers its own
panels from `[1]`, so after switching screens `1`–`9` are that screen's panels; a digit with no such panel on the screen
does nothing. Inside a popup the digits are free (e.g. a menu's `[3] Favorites`, digit hotkeys on a select's options); a
global hotkey that is a digit can only be pressed inside the global operation popup (M4). Inside a mode, K11 applies; the
key reference lists them in the core keys section as `1–N` ([components/dialog/note](../components/dialog/note.md)).

**Why**: what users learn is a **role** ("cancel", "move focus", "what can I do now"), not a key. With the roles fixed,
one lesson holds on every surface of every app in the family. A single surface where `Space` does something else adds a
rule to learn: "except here". Every panel has `[N]` drawn on its frame, which promises "press this digit to get here";
an app that takes the digit for something else makes the frame lie. Jumping to a panel is basic movement, like `Tab`, and
must always be reliable; the app loses only the digits on a panel, keeping the letters and the digits inside popups.

### K2 `Tab` switches focus between objects on the same level

`Tab` moves focus to **the next object on the same level within the current surface**, wrapping from the last to the
first:

| Focus is on | `Tab` switches between |
|---|---|
| a screen | panels |
| a popup with an action area: a form ([components/dialog/form](../components/dialog/form.md)), an input popup with a button ([components/input/color-picker](../components/input/color-picker.md)) | the field area and the action area, coming back to the item it left (the items within each area move with hjkl, K12) |
| a popup with several areas (a finder, a datetime picker) | areas |

- `Tab` does not cross screens or leave the current popup.
- With focus in a PTY, `Tab` belongs to the subprocess (K10).
- **On a typing row** (the typing row of a finder or a select, a panel filter): `Tab` goes to its list
  ([components/input/finder](../components/input/finder.md)).
- **An input popup with a single area**: with a greyed-out suggestion (the old value), `Tab` accepts the suggestion; with
  no suggestion it does nothing.
- In the writing state of multi-line text, `Tab` inserts spaces (an indent), not a field switch (K8).
- Cycling backwards (e.g. `Shift-Tab`) is a hotkey, and the app may decide for itself whether to offer it; a popup with an
  action area always has `Shift-Tab`.

**Why**: users press `Tab` expecting "the next one" — the next panel on a screen, the other of the field area and the
action area in a form or any other popup with an action area (as with a finder's typing row and list). It is the
same role at different levels. Switching screens is a global operation (P3).

### K3 `Enter` does the most intuitive thing to what has focus

`Enter` does **the most intuitive action** to the focused item — enter a directory, connect, open, flip a setting.
What that action is, the app may decide for itself; inside that scope, the same kind of item always gets the same
action within an app. When the panel itself is a content area with no "item" to pick (e.g. a preview, a log), `Enter`
does the most intuitive action to the whole panel, which the app may decide for itself (e.g. open a scrollable view).

**The focus moves only when the user expects it to**: after `Enter`, the focus normally stays where it was —
once a field's input popup on a form is confirmed, the focus is back on the same field; choosing a radio option or
flipping a checkbox in place does not move it either. Position normally changes with `Tab`, the digit keys, the movement
keys and a component's own keys (e.g. a form's `e`; K1, K2, K12). An app's action (`Enter` included) may move the focus
or switch screens, as long as the user expects the move when pressing it; which actions meet that expectation is
decided by the app's own experience. Three are fixed by the components: `Enter` on a typing row going to the list, a
blocked submit on a form jumping to the first field with a problem, and **details** ("Details" in
[components/layout/panel](../components/layout/panel.md)) — on a panel listing items, `Enter` may move the focus to the
panel showing that item's details (whether to, and on which items, the app may decide for itself).
**Something happening in the background never moves the focus or switches screens** (e.g. a load finishing, a job
ending, a change arriving from a remote): the user pressed nothing and could not expect it.
**After adding an item, the cursor moves to the new item**, scrolled into view (e.g. once New, Copy or Import is
confirmed): right after adding it, the user usually wants to see it or act on it; in a sorted list the new item may land
far away, and leaving the cursor where it was means hunting for it.

**In an input popup**, `Enter` acts on the area that has focus:

- **Focus on the value**: confirm the value — it is written back and the popup closes. If the value is invalid, it is
  **not written back**: the error goes in the reserved error row (F7) and the popup stays open.
  If the value is the same as when the popup opened and was already valid then (e.g. an old value left unchanged),
  nothing is written back and the popup just closes. A field that opens empty and may not be empty, with `Enter`
  pressed before typing anything, counts as invalid: the error shows and the popup stays open; when the app gives a
  suggested value, `Enter` takes the suggestion ([components/input/README](../components/input/README.md)).
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
or failing to confirm without saying why, both leave the user stuck; an empty required field that silently closes on
`Enter` leaves the user thinking the thing was created. The focus normally stays: pressing `Enter` again and again only
opens and closes things in the same place, and the user need not guess where a press will leave them. When it does
move, the test is whether the user expected it, not a fixed list of actions: details already follow the cursor, so on
the list the natural thing for `Enter` is often to go in and change them; the only place it can land is the details, so
the user still need not guess. When something in the background takes the focus, the next key the user is pressing
lands somewhere else.

### K4 `Esc` closes one layer at a time and never leaves the app

`Esc` cancels the current operation or closes the top layer: a popup if there is one (toasts included, F3); while the
popup is in a mode, it leaves the mode first (K11), and the next press closes the popup; with no popup, it leaves the
current mode (selection, dragging) or goes up one level (e.g. clearing a panel filter) — what "up one level" means, the
app may decide for itself. **One layer per press**, and **`Esc` never leaves the app** — at the top it does nothing.

When a popup opens another (e.g. Space menu → global operation popup → confirm), `Esc` **closes only the topmost one**;
the popups underneath stay and are shown exactly as they were; the next press closes the next layer (F4).

**Why**: a lost user presses `Esc` repeatedly to get back somewhere safe. If the end of that sequence is the app closing,
`Esc` becomes a dangerous key, users stop pressing it, and the safe way out that "cancel" provides is gone. Quitting has
its own key (K9).

### K5 `Space` opens and closes the Space menu on a panel

- With focus on a panel, `Space` opens the Space menu (M2); while the Space menu is open, `Space` closes it again.
  `Esc` closes it too.
- **`Space` closes only the Space menu it opened itself.** On any other popup (a confirm, input,
  note… opened by `Enter` or a hotkey), `Space` **does nothing**; those are closed by `Esc` or by their own flow. The
  exceptions: inside a mode (K11, a mode in a popup included), `Space` opens that mode's Space menu; on checkbox options (a checkbox popup's list, the checkboxes drawn on a form), `Space` checks or unchecks
  ([components/input/checkbox](../components/input/checkbox.md), [components/dialog/form](../components/dialog/form.md));
  in an app's own popup, when the focused cell has several values to cycle through (e.g. a cell in kamonu's popup for
  drawing cells), `Space` moves it to the next value (F1).
- A popup's own operations run by hotkey, disclosed in that popup's `?` help (K6; which of them the bottom-border hint
  shows follows each component's hint); no Space menu is stacked on top of a popup (except for a mode inside it, K11).

**Why**: an entry key that opens but cannot close is a trap — users reach for the same key to get out and nothing
happens. But if `Space` could also close a confirm, it would double as `Esc`'s "cancel" (P4); and if it could stack a
menu on a popup, boxes on boxes would have no end. The family's flow is always: `Space` on a panel opens the menu,
`Enter` on a row, and only then does the next popup open. The checkbox popup is the exception: for checking items on a
list, `Space` is the key everyone knows, and `Enter` there is kept for confirming the whole set (P0). A cell in an app's own popup is the same
thing — switching one cell's value in place — only with more than two values.

### K6 `?` opens and closes the key reference from anywhere

`?` responds on any surface; `?` again closes it, and so does `Esc`. It opens **the key reference of the frontmost
surface**: read-only and scrollable, with no cursor and nothing to run (M4; how it looks:
[components/dialog/note](../components/dialog/note.md)).

| Focus is on | The key reference lists |
|---|---|
| a panel | the keys that work on this panel (movement keys included), plus the core keys and global hotkeys that work here |
| a popup (the Space menu and the global operation popup included) | **only this popup's** keys: its own hotkeys, `Enter`, `Esc`, the movement keys |

- **The movement keys list everything K12 makes reachable**: a one-dimensional list (a form, a one-value-per-row panel
  with no tabs, a menu) lists `h|k` to go back and `j|l` to go on. An empty list has nothing to move through and content that
  fits has nothing to scroll; both count as the target not existing, so the movement and scroll keys are not listed (M6).
- **A one-value-per-row panel may add a "rows" section**, first: each row's name and what it means (the names are not
  keys and use the plain text colour), with the keys after it. Whether to have it, the app may decide for itself (how it looks:
  [components/dialog/note](../components/dialog/note.md)).

Input state, PTY and modes follow K8, K10 and K11.

**Why**: whoever presses `?` wants to **read** "what can I press here". Putting reading and doing in one box leaves the
user standing on a list with a cursor where every row can be pressed — and afraid to move (F1: a popup belongs to
exactly one class). What can be done is under `Space`; what can be pressed is under `?`.

### K7 Aliases are complete

When a role is bound to several keys, every alias must work **on every surface**. If that is not possible, don't alias.

**Why**: a partial alias (a key that cancels on the main screen but not in popups) is worse than none — it looks like a
convenience, but adds a rule to learn: "where it works and where it doesn't".

### K8 Input state: hotkeys are all off

The **input state** is when the content is text being typed: focus is on a typing row — an input popup's value, a
textarea's writing state, the typing row of a finder or a select, a panel filter. The list of a select or a picker, a
textarea's moving state and a form itself are not the input state.

In the input state, **every key that produces a character is a character** and triggers nothing:

| Key | In input state |
|---|---|
| letter hotkeys, `Space`, `?`, `q` | typed as characters |
| `Esc` | cancels the input (K4) |
| `Enter` | see K3 |
| `Tab` | accepts a grey suggestion; on a typing row, goes to the list (K2); in the writing state of multi-line text, inserts spaces (an indent) |
| `Ctrl-C` | starts the quit flow (K9) |

Normal behaviour returns the moment focus leaves the input surface.

**The writing state of multi-line text**: `Tab` inserts spaces (an indent), just as `Enter` is a newline (K3); to
confirm, leave the writing state first (`Esc`), then press `Enter`. How many spaces is the setting `input_tab_width`
(4 by default, E3); no `\t` is inserted: a terminal cannot line things up with tabs, and pressing `Tab` means "some
spaces".

**Why**: `Space`, `?` and `q` are all printable. Without this, users could never type a file name with a space or a
password with a question mark. `Esc` and `Enter` stay, because they do not compete with characters, and without them the
input box is a trap with no exit.

### K9 `q` and `Ctrl-C` quit the app

- `q` and `Ctrl-C` do **the same thing**: start the app's quit flow. `q` is a character in the input state (K8) and does
  nothing on a form or on an app's own popup that works like a form ([components/dialog/form](../components/dialog/form.md),
  F1); nor on the typing note a form pops up: that
  note takes only `Enter` and `Esc`, and every other key that types something (`q` and `?` included) is caught and does
  nothing. `Ctrl-C` still works in the input state, on a form and on the typing note. With focus in a PTY both belong to
  the subprocess (K10).
- **The app may decide for itself on the quit flow**: quit at once, confirm first, or let the user choose how to quit;
  inside that scope the next two points hold (with a popup open it always asks first; `Ctrl-C` again quits at once).
  E.g. sshu asks whether to close open sessions first; filu lets the user choose whether to switch the shell to the last
  directory.
- **With a popup open, the quit flow asks first**: with any popup open (a menu, a viewer, a picker, the comparison…; a
  toast is not a popup), the first `q` or `Ctrl-C` never quits. A flow whose first step already asks stays as it is
  (filu's choice of where the shell goes, sshu's question about open sessions); a flow that would quit at once at that
  moment opens the quit confirm instead (`Quit <app>?`, `Enter:quit Esc:cancel`,
  [components/dialog/confirm](../components/dialog/confirm.md)). `Esc` on what opened goes back to the popup. On a
  panel (a mode on a panel included) the app's flow runs as it is. What asks, the app may decide for itself; whether
  something asks is outside that scope: no app can turn this off.
- **Pressing `Ctrl-C` again during the quit flow quits at once**, with no further questions.
- Quitting is listed in the global operation popup (M4).

**Why**: `Ctrl-C` is in every terminal user's muscle memory, and `q` is the TUI convention; if the two behaved
differently, users would have to remember which one asks and which one doesn't. Pressing `Ctrl-C` twice to force quit
means users can never be trapped by their own confirm box. `q` on a form is the exception: a form looks like a place to
type, and a user who thinks they are typing, hits `q` and leaves the app pays too high a price. The typing note is the
next step of the same case: it pops up while the user is still typing, and the next characters keep coming; a `q` there
would open the quit confirm, and a habitual `Enter` would quit. An open popup is the other place where a stray `q` costs
too much: the user is in the middle of something (reading a viewer, picking from a menu, looking at a comparison) and
pressing keys in runs, and quitting at once would throw away what is open and where they were (the user, 2026-10-22).

### K10 PTY: keys belong to the subprocess, with at least one exit key

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
  spelled by "`Esc` then that key"; whether they confirm, the app may decide for itself.
- An interactive terminal (a PTY where the user types their own commands) always has the history mode (`PgUp`) and the
  selection mode (`Alt-v`); see [components/dialog/terminal](../components/dialog/terminal.md).
- Beyond that, whether the app keeps other chords of its own inside the PTY besides the exit key (e.g. sshu's zoom and
  cell switching inside a cell), the app may decide for itself. Any it keeps are disclosed permanently, like the exit key (M1).
- Where focus lands after the exit key, the app may decide for itself.
- While the subprocess is not ready for keys yet (e.g. the remote end is still connecting), the app may hold ordinary
  keys back (so they don't land on the remote end minutes later); but **`Ctrl-C` is still forwarded to the
  subprocess**, and the exit key still works and is still disclosed. With focus in a PTY the user takes every key as
  pressed inside the PTY; the only exceptions are the explicitly disclosed exit key, an interactive terminal's `Alt-v` and `PgUp`, and the
  chords the app keeps.

> **Implementation reference (not a requirement)**: measured with bubbletea v1.3.10, with keys already queued, two `Esc`s
> 150 ms apart still merged.

**Why**: with focus in a PTY, nearly everything the user does is the PTY's business; the more keys the app intercepts,
the likelier it breaks the subprocess, and the more "who owns this key right now" becomes something to remember. But a
PTY with no way out is a trap, so there must be at least one exit key, and it must be visible; whether to intercept the
rest depends on how the app's PTY is used — a single shell and a whole grid of live remote sessions have different
answers.

### K11 Core keys inside a mode

With focus inside a mode (the term "mode"), the core keys act like this:

| Key | Inside a mode |
|---|---|
| `Space` | opens the mode's Space menu (below) |
| `!` | does nothing (the App Log opens outside a mode) |
| `?` | the mode's key reference (read-only, K6): which keys work in the mode and what they do |
| `Esc` | leaves the mode (K4), back to the state before it was entered; in a mode with layers, back one layer at a time (e.g. `Visual>select` back to `Visual`) |
| `q`, `Ctrl-C` | run the quit flow, as K9 |
| `Tab`, `1`–`9` | with the mode on a panel: a mode may suspend `Tab` and the digit keys, but pressing them must respond, saying to leave the mode with `Esc` first (e.g. a toast); while the toast is up, the first `Esc` closes it (K4). With the mode in a popup, see below |

- **Inside a mode only the mode's own keys and the core keys above work**: panel hotkeys and global hotkeys do nothing,
  silently.
- **The mode's Space menu** ("Inside a mode" in [components/dialog/menu](../components/dialog/menu.md)): it lists only
  what can be done in the mode, in two sections — **item operations**: what can be done now to the item under the
  cursor (or the selected range), picking one being the same as pressing its key (e.g. `[C]ompare` in the Compare mode,
  `[y] Copy` once a selection has started); **mode operations**: the mode's own keys — the movement keys are only shown,
  not run, while what really does something, such as leaving the mode, runs as usual. Panel, item and global actions are
  never listed. The mode's keys are also disclosed in the `?` key reference and in the footer / bottom-border hint (how
  the footer looks inside a mode: [components/layout/screen](../components/layout/screen.md)).
- **A mode shows itself**: the mode name appears at the right of the top border of the frame the mode lives in (panel or
  popup), and the frame turns the mode colour; leaving the mode restores both. The mode name opens and closes with a
  short animation that never holds the mode up: the mode and the frame colour change at once. The mode name is a word,
  not colour alone: a focused panel in a mode still shows that it has focus (L5). A mode with layers adds each layer to its
  name after a `>` (e.g. a viewer's selection mode, once selecting, is `Visual>select`), and `Esc` goes back one layer
  at a time. How it looks:
  [components/layout/panel](../components/layout/panel.md).
- **A mode inside a popup** (e.g. a viewer's selection mode, a reorder's Drag mode): the frame and mode name, `Space`,
  `?`, `Esc`, `q` and `Ctrl-C` work as above; `Tab` and the digit keys keep whatever they do in that popup (in a popup
  they never switch panels) and need no extra response; the footer stays as it is while a popup is open and does not
  change to the mode's words ([components/layout/screen](../components/layout/screen.md), the footer).
- **A mode on a PTY** (e.g. a terminal's history mode or selection mode): the focus is still in the PTY, so any key other
  than the mode's own keys, `Space`, `?` and `Esc` first leaves the mode, then goes to the child process by K10 — `q` and `Ctrl-C`
  too; they do not start the quit flow ([components/dialog/terminal](../components/dialog/terminal.md)).

**Why**: "when in doubt, hit `Space`" holds inside a mode too — the family's idea is zero learning cost, so when the
user in a mode does not know what to do, `Space` must answer (the user, 2026-10-22). A mode's keys are mostly movement
and selection, pressed directly and in runs, so the menu has two sections: what can be done to the thing at hand runs
from the menu as usual, while the movement keys only tell what can be pressed — "running one step down" from a list
makes no sense.
Hotkeys do nothing inside a mode: a drag or a selection is never switched away from halfway (pressing the hotkey that
switches screens in the middle of a drag would leave the drag in a state nobody can describe), and the mode's `?` only
needs to list the mode's keys; to do something else, `Esc` first — the same idea as a PTY. The digit keys switch panels,
like `Tab`, so users expect a response and a suspended one must respond; other letters stay silent, so random presses do
not pop up a string of toasts. In a popup, `Tab` and the digits never switch panels anyway, so users expect no response,
and one would only be noise.

### K12 Navigation letters are kept for movement; hjkl are the arrow keys

Where you are not typing (outside the input state, K8), `j k u d g G h l` are kept for movement, and no action takes them. `h|j|k|l` are
`←|↓|↑|→`, meaning what the layout makes them mean:

- **With a left-right structure** (tabs within one surface, two sides, a grid): up, down, left and right. `j|k` move up
  and down a list, `h|l` go left and right — switching tabs, crossing to the other side, the day before or after in a
  calendar.
- **In a plain one-dimensional list with no left-right structure** (a form, a one-value-per-row panel without tabs, a
  menu): `h|k` (`←|↑`) go back, `j|l` (`↓|→`) go on.
- A one-dimensional list in a panel with tabs: `h|l` switch tabs, `j|k` still move in the list.
- Two-dimensional content (several items to a row, e.g. the links on one line of a web page, the cells of a table) in a
  panel with tabs: `h|l` switch tabs, `j|k` step item by item in reading order (left to right along a row, then the next
  row), wrapping at the ends; `u|d` and `gg|G` as usual.
- **`u|d` move half a page, `gg|G` to the top and the bottom.** `g` is only the start of a two-key chord: `gg` goes to
  the top, and other chords starting with `g` may be hotkeys (e.g. filu's and webu's `[go]to`); a single `g` does
  nothing. When the key after `g` is not a chord, it is as if `g` had not been pressed and that key works as usual (`g`
  then `j`: down a row). `Ctrl-U|Ctrl-D` are not taken as aliases.
- **`Home` and `End` only on a typing row**: the cursor to the start and the end
  ([components/input/README](../components/input/README.md)). On lists, menus, viewers and a textarea's moving state they
  do nothing: those have `gg|G` and `0|$`.
- **Stepping wraps at the ends**: moving one step at a time along a run of items (`j|k`, `h|l`, the arrow keys, `Tab`)
  — a panel's list, a one-value-per-row panel, a menu, a form, the list of a finder, a select or a checkbox popup, a
  panel's tabs, the columns and items inside a picker — one step past the last item goes to the first, and one step back
  from the first goes to the last. So does the item held in a Drag mode (a panel's Drag,
  [components/input/reorder](../components/input/reorder.md)): one step past the last, it goes to the first and every
  other item moves down one. `u|d` stop at the first and the last item and do not wrap; `gg|G` go to the top
  and the bottom anyway. What moves through space rather than along a run of items does not wrap: the days of a
  calendar, the month and the year, the two sides, moving within a piece of text (an input's typing-row cursor included).
- **Moving within a piece of text** (a viewer's selection mode, a textarea's moving state): add `w|b|e` (next word start,
  previous word start, word end) and `0|$` (line start, line end), as in vim. A viewer has no cursor by default, and
  `h|l` switch tabs as above; in its selection mode `h|l` move the cursor and tabs do not switch (the selection mode
  in [components/dialog/note](../components/dialog/note.md)).

**Why**: in the family hjkl are the arrow keys — forms, panels and lists all move with them; an app binding one to an
action has users trigger an action while they think they are moving. With a left-right structure, left and right are
left and right (filu's, kbu's and webu's `h|l` switch tabs, sshu's `h|l` cross to the other side); without one, the
left and right keys are idle and get "back" and "on", so all four arrow keys work on a one-dimensional list.
`Ctrl-U|Ctrl-D` are not taken: one set of keys per action is one set fewer to remember; and in shells and many input
boxes `Ctrl-U` means "clear this line", so the same chord would turn pages in one place in the family and delete text in
another — too high a price for a slip. Wrapping at the ends: the same key reacts the same way at the ends everywhere in
the family, so nobody has to remember where it wraps and where it stops; a half page across the ends would land
somewhere nobody can guess, so `u|d` stop. `Home` and `End` only on a typing row: there `g` and `0` are characters, so
they are needed; elsewhere a key already does the job, and no second key is given. A stray `g` does not make the next
key fail.

---

## M Menus and disclosure

### M1 The entry points are visible

Every screen outside the input state must **permanently show** `?`, and `Space` and `!` (inside a mode `Space` and `!`
do nothing and need not be shown, K11), so a first-time user who has read no documentation can see them. How it looks: the footer in
[components/layout/screen](../components/layout/screen.md).

With focus in a PTY, these keys belong to the subprocess (K10) and are not shown; what is disclosed permanently is the
exit key, an interactive terminal's `Alt-v` and `PgUp`, and the keys the app keeps (K10; how it looks: the footer in
[components/layout/screen](../components/layout/screen.md) and
[components/dialog/terminal](../components/dialog/terminal.md)).

**Why**: users cannot press a key they do not know exists. An undisclosed entry point might as well not exist, however
complete the disclosure behind it (Principle P2). In a PTY, `?` and `Space` go to the subprocess, so showing them anyway
teaches users to press the wrong key; what must be visible there is the exit key.

### M2 Space menu: item → panel → global, three regions

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

### M3 Every action can be found in a menu

- Every item operation and panel operation of every panel is in that panel's Space menu.
- Every global operation is in the global operation popup (opened from the Space menu's global row).
- A popup's own operations are all in that popup's `?` key reference (K6); which of them its bottom-border hint shows
  follows the hint in [components/layout/popup](../components/layout/popup.md) and the hint each component specifies.
- **A popup with only a typing row** (text, password, number): `?` is a character there (K8), so its hint lists every
  operation, and fits in 80 columns (the hint in [components/layout/popup](../components/layout/popup.md)).
- **A letter hotkey is a shortcut to a row in some list, not an extra feature.** An action triggered only by hotkey and
  found nowhere else is a violation.

Which region an action belongs to depends only on **what it acts on**, never on how important it is (Principle P3).

**Why**: a new user who has never seen a hotkey must be able to do everything, anywhere, with `Space` and `?` alone.
Each action that has to be learned in advance is a hole in "usable without the docs".

### M4 The global operation popup and the key reference

**The global operation popup** (doing)

- Opened with `Enter` on the Space menu's global row (M2), over the Space menu; it is a menu (F1) listing **all** of the
  app's global actions — `j|k` to pick, `Enter` or the hotkey to run. Quitting the app must be here (K9).
- `Esc` goes back to the Space menu (F4); an action that closes the whole stack once run follows T1.
- The row that switches to the current screen is disabled as M6 says (e.g. `[M]anage` while on `[M]anage`).
- **Global hotkeys**: with no popup open, the hotkeys in the global operation popup can also be pressed directly on a
  panel. When one clashes with a panel's own hotkey, the panel's wins, and that panel's key reference does not list the
  global key it overrides. `q` follows K9. A global hotkey that is a digit can only be pressed inside the global operation
  popup (a digit on a panel jumps to a panel, K1); inside a mode, global hotkeys do nothing (K11).

**The key reference** (reading)

- Opened with `?` (K6). Read-only and scrollable, with no cursor and nothing to run — not a menu.
- What it lists: see K6; how it looks: [components/dialog/note](../components/dialog/note.md).

**Why**: a read-only help page cannot replace a list you can run (Principle P2) — what can be done is under `Space` and
in the global operation popup, one step from running; `?` is a permanent cheatsheet to glance at alongside. Reading and
doing live in two boxes, each of one class (F1). With the global actions gathered in one popup, no Space menu has to list
them again; users who know them press the global hotkeys directly on a panel, without opening two layers of menu every
time.

### M5 Each row = name + description, hotkeys marked with `[]`

Each menu row has the **action name** on the left and a **one-line description** on the right:

```
 󰋘 ITEM OPERATION
 [o]pen                          open it with the OS default app
 [r]ename                                    this item, in place
 ╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌
 󰋘 PANEL OPERATION
 [/] Search                                everything under here
 ╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌
 Global operation                      actions for the whole app
```

How keys are written is one rule for the whole app (menus, footer, panel hints, popup hints, the key reference, and the
README). Marking inside a label:

| Case | Form |
|---|---|
| A single letter that appears in the label (either case) | wrapped in place, at its first appearance: `[r]ename`, `[n]ew`, `[D]elete`, `D[e]lete`, `UR[L]`, `Ex[P]ort` |
| A single letter not in the label | in front: `[x] Reset`, `[x] Delete` |
| With a modifier | `[Alt-t]erm` |
| Several characters | `[go]to` |
| Digits | always in front: `[3] Favorites`, never inside the word |
| A core key | in front: `[Enter] Edit` — it marks that pressing this key on the panel is this action; in a menu `Enter` still runs the row under the cursor |
| No hotkey | no brackets |

- **The hotkey and the label are two things**: when they happen to meet (the letter appears in the label) they are
  written together, and when they don't they are listed apart; the label keeps its own case and is never re-cased for
  the hotkey (`Export`, not `ExPort`).
- **What is in the brackets is exactly the key to press, case included**: `[A]dd` is `Shift-A`; when the letter in the
  label and the key differ in case, the brackets follow the key (`Export` with the hotkey `Shift-P` is `Ex[P]ort`).
- A row whose label already spells out the key (`[/] Search`) is not bracketed again.
- Colour or a glyph alone must not be the hint that "this is a hotkey"; mark it explicitly.
- What the description says, the app may decide for itself, but it must fit on one line.

**Key names** (the same everywhere on screen and in the README):

- The name printed on the key cap, UpperCamelCase, no abbreviations of our own: `Esc`, `Tab`, `Enter`, `Space`,
  `Backspace`, `Delete`, `Home`, `End`, `PgUp`, `PgDn`; arrows `↑` `↓` `←` `→`.
- Letters in the case actually pressed: `q`, `A` (that is `Shift-A`), `Alt-z`. The letter after `Ctrl` is always upper
  case (`Ctrl-C`, `Ctrl-U`): terminals can't tell the case of a `Ctrl` chord.
- Modifiers are joined with `-`: `Alt-t`, `Ctrl-C`, `Shift-Tab`, `Alt-Esc`.
- `|` joins two kinds of keys: **several keys doing one thing** (`h|k`, both going back on a one-dimensional list;
  `Enter|Esc:close`; `Enter|Tab`), and **a pair of keys in opposite directions told with one verb** (`j|k:move`, `u|d`,
  `gg|G`, `Tab|Shift-Tab`). The `|` takes the description colour (dim text in [components/color](../components/color.md)),
  not the key colour. A range uses `–`: `1–9`. Not `/`: `/` is itself a key (back to the typing row from a finder's
  list, the panel filter), and `Tab//:filter` cannot be read.

**By place**:

| Place | Form | Example |
|---|---|---|
| Label (menu rows, statusbar chips, panel titles) | the bracket marking above | `[r]ename`, `[Alt-t]erm` |
| Sentence (empty states, toasts, error messages, and keys mentioned in the description column of a menu or the key reference) | every key in square brackets | `Press [A] or [Space]`, `see App Log [!]`, `next tab [h]\|[l]` |
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

### M6 Actions that can't run right now: disabled

- **No target**: the row (or region) is not shown (M2).
- **A target, but the action can't run right now**: the row is still shown, in the disabled colour
  ([components/color](../components/color.md)), keeping its usual description with no reason added; the cursor skips it,
  and its hotkey does nothing.
- **The `?` key reference follows the same rule**: a key whose target exists but can't be pressed now is still listed,
  in the disabled colour; with no target it is not listed — an empty list with nothing to move through and content that
  fits with nothing to scroll also count as no target, so the movement and scroll keys are not listed. The
  bottom-border hint and the footer, short on room and
  always on screen, may list only the keys that work now, which the app may decide for itself, except where a component requires the
  keys to go: while a form's button is running, while a finder has no results, while a panel's list has no items
  (components/dialog/form, input/finder, layout/panel).
- A section of the key reference with a title of its own describing **another surface** (e.g. `ssh grid` in the `?` of
  sshu's list, since a cell shows no key reference) is not this surface's keys and is shown as usual, last (after
  `app-wide`, [components/dialog/note](../components/dialog/note.md)).

**Why**: users take a hidden action to mean the app doesn't support it; disabling tells them "this exists, just not
now". No reason is added because the reasons vary endlessly, and squeezing them into a one-line description would let
every row's length run out of control (M5). The cursor skips the row because landing on it would only lead to a key that
does nothing.

### M7 Entry points on a panel always respond

With focus on a panel, `Space` and `?` must both respond when pressed: `Space` opens the Space menu (the global row is
always there, so the menu is never empty, M2), and `?` opens the key reference. On a popup, the key that always responds
is `?` (K6).

**Why**: when a key does nothing, users think the key is broken, not that there is nothing to do here.

### M8 Other grouped menus: cursor-related first

Whether a menu other than the Space menu (e.g. a sort picker, an open-with list) groups its rows, the app may decide for
itself. A grouped menu puts the actions related to the current cursor first, and gives every group, the first included, a
header naming its kind (M2). A menu with no grouping is listed directly.

**Why**: when users open a menu, what they look for most often is what they can do "to the thing I picked" — the same
reason the Space menu puts the item region first (M2). Every grouped menu follows this order, so users need not search
anew in each menu.

### M9 When one key has two indicators, mark which one fires

When a hotkey does different things on different panels and both indicators are **on screen at the same time**, the user
must be able to see at a glance **which one fires when pressed on the current focus**: the one that fires is bright, the
one that doesn't is dim ([components/color](../components/color.md)).

**Why**: with two identical keys on screen at once, the user has no way to tell which thing pressing it will do. What is
bright is what has focus (Principle P6).

---

## L Layout

### L1 Minimum supported size: 80 columns × 40 rows

At **80 columns × 40 rows**, the app must be able to complete all its core tasks. That is roughly a terminal window on
half of a 16:9 screen (8:9). How the panels split, the app may decide for itself; how to draw when not every panel fits: narrow widths
in [components/layout/screen](../components/layout/screen.md).

**The minimum size**: every app has a minimum size, 80×40 by default; whether to lower it, the app may decide for itself,
but it never goes above 80×40. Between the minimum size and 80×40, the app shrinks by the narrow-width rules of components/layout/screen.

**Smaller than the minimum size** (too narrow or too short), the app's screen is not drawn; only two rows, in the centre:

| Row | Content | Colour |
|---|---|---|
| 1 | the app's name (the same name as the splash, S5) | Blue bold |
| 2 | `needs a terminal of at least <W>×<H>`, giving the app's minimum size (e.g. `needs a terminal of at least 80×40`) | Overlay0 |

- When the two rows don't fit, the hint goes first; the name always stays. Shrinking all the way to 1×1 must never crash.
- **No key does anything**: nothing goes to the app or into a PTY. Only pressing `Ctrl-C` twice quits at once (K9's
  forced quit); `q` and a single `Ctrl-C` do nothing.
- The app keeps its state: once the window is made larger, the screen is back as it was, with nothing changed.

**Why**: a terminal often takes only half the screen — the other half is an editor, a browser or another terminal. A TUI
that only works full screen is unusable in the everyday split window. 80×40 is the standard: above it, everything works
in full. Forcing a draw below the minimum size scrambles the borders and the truncation, and the user sees a broken screen;
saying how much room is needed lets them simply make the window larger. The minimum size is the app's to set because an app
with a simple layout fits in a smaller window, and stays usable in an 80×24 terminal and inside another app's PTY. Keys
pressed while the screen can't be seen act blindfolded, so none of them does anything; the quit flow may need to open a
confirm, which can't be drawn then, so only the forced quit, which asks nothing, is left.

### L2 Width does not follow content

Dynamic text in titles, statusbars, chips and the like uses fixed-width slots or padding; its width never changes with
the length of the content. The **last** dynamic slot in a row may go unpadded: nothing after it can be pushed; the slots
before it keep their fixed width.

**Why**: once widths float, the main view shifts sideways with them, and the whole screen shakes as popups open and
close.

### L3 Chrome has a fixed number of rows

Permanent chrome has a **fixed number of rows**: the top row (in an app with several screens, the screen chip row plus
the divider below it; in a single-screen app with a statusbar, one statusbar row) and one footer row — see
[components/layout/screen](../components/layout/screen.md); a panel's tabs are drawn on the panel's top border and take
no row of their own ([components/layout/panel](../components/layout/panel.md)). It does not change with the amount of
content; what doesn't fit is truncated or dropped from the end, never wrapped.

**Why**: one more chrome row is one less main row, and the whole layout shifts in a chain. Stability always beats saving
space.

### L4 Every line is exactly the terminal width

Every line on screen is exactly as wide as the terminal, no more, no less.

**Why**: one cell too many and the terminal wraps, knocking the whole screen out of place; one too few and stale cells
linger on screen. Misjudged CJK and icon widths are the usual cause.

### L5 Focus is visible, and moving it moves nothing else

The focused surface must be recognisable at a glance, and moving focus **must not shift any content**.

- **Focus is not told by colour alone**: something besides colour must differ (e.g. the line style). A mode turns its
  frame the mode colour (K11); with colour alone, focus vanishes the moment a mode starts. How it looks:
  [components/layout/panel](../components/layout/panel.md).

**Why**: users need to know where their keys will go; and if the screen jumps every time focus moves, the eye has to find
its place again.

---

## F Popups

### F1 Popups come in eight classes, one class at a time

The family's popups come in these eight classes only, each with fixed key meanings:

| Class | What the user can do | E.g. |
|---|---|---|
| **menu** | a list with no search: `j\|k` moves the cursor, `Enter` or a hotkey runs the row | Space menu, global operation popup, a sort picker, a jobs list (`Enter` acts on the row: opens it in full, or opens a confirm carrying it in full) |
| **confirm** | read a reminder or warning; `Enter` accepts, `Esc` cancels (F6); what to read first sits above, the question last | confirm before delete, the quit confirm, "Connect to X?" carrying the details |
| **input** | enter or pick one value, written back once confirmed; one value per popup. On the typing row it is the input state (K8); other parts follow K1 | rename, address bar, select, datetime picker, reorder |
| **form** | one value per row; `Tab` switches between the field area and the action area, hjkl move item by item within that area (K12), `Enter` acts on the focused item (opening that field's input popup, choosing a radio option, flipping a checkbox, pressing a button), a button submits or does its action ([components/dialog/form](../components/dialog/form.md)) | sshu's Host form, webu's Sign in and Add bookmark |
| **note** | read-only, scrollable (K12); no list of options to run with `Enter` | key reference, YAML viewer, App Log, error popup |
| **toast** | a short message popping up from the bottom, gone on `Esc` or on its timer; every key but `Esc` passes through it | "Copied", an operation failed |
| **terminal** | a subprocess running in the box; every key is its, only the exit key and the chords the app keeps (in an interactive terminal also `Alt-v` and `PgUp`) are the app's (K10) | kbu's Alterm, filu's shell |
| **an app's own popup** | content the seven classes cannot hold: how the content is drawn and the keys on it, the app may decide for itself; the box and the layers work as a popup; with values to submit it works like a form (see below) | kamonu's popup for drawing cells |

- **A note may have hotkeys and modes of its own**: e.g. the YAML viewer's `/` search. **Every viewer has a selection
  mode** (`v` select, `y` copy; a mode, K11; [components/dialog/note](../components/dialog/note.md)): any viewer in the
  family can select text and copy it. Its hotkeys are disclosed in `?` (the bottom-border hint as dialog/note says); but
  once it has a list of options to run with `Enter`, it is a menu, not a note.
- **A menu's `Enter` may open the row in full**: in a list with a cursor and no other action of its own (e.g. a jobs
  list), `Enter` opens a note showing the row's whole content; it is still a menu; its hint reads `Enter:detail`
  ([components/dialog/menu](../components/dialog/menu.md)). A row of a jobs list that can be acted on (e.g. a transfer
  in progress can be cancelled) keeps `Enter` as "act on this row": it opens a confirm carrying the row in full, and the
  hint names the action (e.g. `Enter:cancel`).
- **A confirm may carry content to read before answering**: the question is why a confirm exists, and above it may sit
  the information to look at before answering (e.g. the details of X above "Connect to X?"), scrolled with `j|k` when
  long; it is still just a confirm, not a note plus a confirm, and need not be split into two popups.
- **A popup may change class by phase, but belongs to one class at a time.** E.g. a finder is an input while typing and a
  menu while its result list has focus; `Tab` switches focus between typing and the list, and `Esc` closes the whole
  finder (K4: a phase is not a layer). A preview beside it takes no focus and is not another surface.
  **Which side has focus must show**: only the side with focus is bright (Principle P6; how it looks:
  [components/input/finder](../components/input/finder.md)).
- **A list plus search is a finder**: the plain finder, select, the checkbox popup and file-picker are all kinds of
  finder — the typing row is the input state, the list is for picking; for the typing row's keys see
  [components/input/finder](../components/input/finder.md). They are still inputs, not two classes at once. A list with
  no search is a menu, except reorder: it has no search either, but it moves items and writes the whole order back
  once confirmed, so it is an input ([components/input/reorder](../components/input/reorder.md)).
- **A toast is not a layer**: it triggers no dimming (F8) and does not count toward the layer colours' levels; but `Esc`
  closes it first (K4).
- **Each step of a multi-step flow is its own popup**: e.g. sorting by picking a column, then a direction, is two stacked
  popups (F4 keeps the source), not one box changing its content — each step has its own UX, and its own size fixed at
  opening (F7).
- **An app's own popup is only for content the seven classes cannot hold** (e.g. kamonu's popup drawing 25×19 cells).
  What the seven can hold — a list, a confirmation, one value, a form of one value per row, read-only content, a short
  message, a subprocess — is done as that class.
  - The box, the title, the hint, the opening and closing animation, the size and position and the dimming work as a
    popup (F2, F7, F8, "An app's own popup" in [components/layout/popup](../components/layout/popup.md)).
  - With values to submit inside it, it works like a form: `Tab` switches between the content and the action area, a
    button submits, `q` does nothing, and `Esc` asks first once something changed (K9, F3,
    [components/dialog/form](../components/dialog/form.md)).
  - How the content is drawn and the keys on it, the app may decide for itself; inside that scope, the core keys keep
    their meaning (K1; `Space` see K5), movement follows K12, and hotkeys are disclosed in `?` (K6, M5).
- The splash is not a popup (chapter S): it is not in these eight.
- **A box drawn by a panel's own content is content, not a popup** (e.g. a dialog popped up by a web page webu shows).
  It is not a layer: how it is drawn (whether the content under it is dimmed included), the app may decide for itself;
  keys work as on the panel it is in — `Space` is that panel's Space menu, `?` that panel's key reference, and `Esc` does
  what K4 says it does on a panel.

**Why**: the class is the user's expectation of "what keys do inside this box". With only eight classes in the family,
each of fixed meaning, nothing is relearned from one app to the next; a popup mixing two classes at once gives the same
keys two possible meanings inside one box. Content the seven cannot hold, forced into one of them, makes that class's keys
lie; an app's own popup keeps fixed what can be fixed (the box, the layers, submitting) and opens up only the content.

### F2 Opening and closing are both animated

Popups **must animate** both when opening and when closing, in one form and one length across the family: a line is
drawn out from the middle first, then the popup opens up and down; closing plays it backwards. 32ms a frame, 9 frames
each way (about 288ms); a popup takes no keys until its opening animation ends. The frames and how they are drawn are in
[components/layout/popup](../components/layout/popup.md).

**Several layers closing together** (e.g. T1 clearing a two-layer source, one action closing the whole stack): every
layer closes at the same time, each at its own size and in its own layer colour, still about 288ms in all — no layer
waits for another.

**Why**: without animation, a popup "suddenly appears, suddenly vanishes", and users don't feel the change of layer as it
stacks on and steps back. One form and one length: the same action looks the same and takes as long in every app of the
family, so the rhythm stays the same from one app to the next. No keys while it plays: on a frame not yet drawn, users
cannot see what their key landed on. Layers closing together: if the lower ones just vanish, that is "suddenly gone"
again; closing them one by one makes two layers take twice as long, three layers three times.

### F3 `Esc` closes any popup at once

Any visible popup — auto-dismissing toasts included — starts closing **immediately** on `Esc`, without waiting for a
toast's countdown. Closing is animated as usual (F2); a popup already running its closing animation ignores `Esc` and
takes no other keys either.

**Exceptions**:

- With focus in a PTY, `Esc` belongs to the subprocess (K10); a terminal is left with the exit key. A toast can then only
  wait for its timer to go.
- In a textarea's writing state, `Esc` leaves the writing state for the moving state (K8).
- While a popup is in a mode (e.g. a viewer's selection mode, a reorder's Drag mode), `Esc` leaves the mode first (K11);
  the next press closes the popup.
- In a form, a textarea, a reorder or an app's own popup that works like a form (F1) whose content changed, `Esc` first opens a confirm asking whether to discard it
  ([components/dialog/form](../components/dialog/form.md)).

**Why**: users are not obliged to wait out a countdown. If a popup that is already closing takes another `Esc`, or still
eats other keys, the user's next key goes to the wrong place. In a PTY and a textarea, `Esc` is already needed by the
subprocess and for writing; in a mode, `Esc` leaves the mode, one layer at a time as K4 says; throwing changed content
away in one go costs a lot, so it asks once more.

### F4 The source stays by default

When popup A opens popup B, A stays underneath by default; cancelling B returns to A. The same holds at any depth: `Esc`
closes only the topmost, and the stack underneath is shown as it was (K4).

**Why**: the user did not dismiss A, they just did one interaction in B. If cancelling B also removes A, they have to
walk the whole way again. (Whether A stays after B completes is T1.)

### F5 Errors show at once, without blocking the app

Errors must appear immediately, close on `Esc`, and **must not block the app**. Whether a toast or an error popup
follows "Use" in [components/dialog/toast](../components/dialog/toast.md); where that says nothing, the app may decide
for itself. Errors also go into
the App Log (`!`, [components/dialog/note](../components/dialog/note.md)), so they can be looked up after the toast
has gone; every app has an App Log.

**Why**: an error you can't see never happened; an error that blocks the app keeps the user from dealing with the error
itself.

### F6 Confirm: `Enter` accepts, `Esc` cancels, and it says what will happen

- **Which actions need a confirm, the app may decide for itself**, regardless of whether they are reversible. Once an action is set to
  be confirmed, it is confirmed every time. The exception: a choice made explicitly in a picker may count as the
  confirmation (e.g. picking the default app from an "open with" list), which the app may decide for itself.
- `Enter` accepts, `Esc` cancels (K3, K4). These are the only two answers, with no other keys such as `y` and `n`:
  `y` would only be `Enter` and `n` only `Esc`, a second set for the same thing.
- The prompt says **what accepting will do** (verb and object), not an abstract OK.
- A confirm cannot be completed by accident (e.g. a mouse click must not accept it).
- How it looks: [components/dialog/confirm](../components/dialog/confirm.md).

**Why**: users must know the consequence before pressing `Enter`. Whether to stop and confirm depends on how much the
action weighs for the user — launching an external program, cutting a session, deleting a file: the app knows the weight
best, and no rule such as "reversible means no need to ask" can judge it.

### F7 Popup size and position

- **Width**, fixed when the popup opens and unchanged while it is open:
  - **The content's width is known at opening** (e.g. an input with a length limit, a confirm, a menu, the key reference,
    a toast, an error popup, a datetime picker, a color picker, a select, a checkbox popup): the widest row + 4 (one
    cell of border and one blank cell on each side), at least wide enough for the title and the hint, and at most
    `min(terminal width − 2, 120)`.
  - **The content's width is not known** (e.g. free-typed text, a URL, streamed content, search results, a form):
    `min(terminal width − 2, 120)`.
  - Centred horizontally.
- **Height**: follows the content, **fixed when the popup opens** and not resized with the content afterwards; at most
  the screen height − 2 (the screen chip row or the statusbar and the footer always stay in view; the divider
  under the chip row may be covered), scrolling inside the box beyond that. Popups
  whose height cannot be known when they open — a finder with a preview, a textarea — always take the maximum. Only
  two cases may change the height while the popup is open:
  - **Loading**: a popup whose content is not known when it opens (streaming, loading) may change height while loading.
    When loading ends, the height is fixed.
  - **A change the user made**: when the user's own action in this popup changes its row count (removing a row, a choice
    that adds a row, filtering candidates as they type), the height **may** follow — the user expects that change; the
    app may also keep the height. The principle is that what is disclosed is correct.
- **Loading is always disclosed**: while a popup is loading, a spinning loading icon **always** sits after its title
  (spec in [components/layout/popup](../components/layout/popup.md)), whether or not its height changes; the icon goes
  when loading ends. Loading here means the content of the **whole popup** has not arrived (e.g. the list's items are not
  all loaded); a form's button that is still running shows the same icon, see the loading of components/layout/popup. If just **one item** is itself a continuous stream of data (e.g. a connection that keeps sending), it is
  that item that is loading, not the popup — how to disclose it, the app may decide for itself.
- **Position**: centred vertically. The toast is the exception: centred at the bottom of the screen, its bottom border on
  the third row from the bottom, so the two bottom rows always stay visible
  ([components/dialog/toast](../components/dialog/toast.md)).
- **A popup whose value can be invalid reserves an error row** (an input popup, a form): it opens with one error row in
  its height, blank while there is no error; an invalid value has its error written in this row (K3), and the box keeps
  its height. One whose value cannot be invalid (e.g. a multi-line editor) need not reserve one. When the action itself
  fails (writing a file fails, the remote end refuses), nothing goes in the error row; an error popup opens
  ([components/layout/popup](../components/layout/popup.md)).
- **The terminal class is the exception**: its width is `terminal width − 2`, with no 120-column cap; above it the
  statusbar or the screen's chip row (with the divider under it) stays, and below it runs down to the last row of the
  screen, covering the footer; inside the frame there is no padding on any side — the subprocess needs the room, and
  inside a PTY the outside footer is not needed
  ([components/dialog/terminal](../components/dialog/terminal.md)).

**Why**: when every popup keeps sizing itself by its content, nobody can tell what it will look like before it opens,
and the box jumps whenever the content changes (L2). With only two ways to work out the width, both fixed at opening,
every box is predictable; a popup whose content is known need not stretch to full width, so it is neither empty on a
wide screen nor cramped on a narrow one; the 120-column cap keeps a menu's names and descriptions from drifting too far
apart on a wide screen. The error row is reserved inside the box rather than opening another popup: the error stays in
view while the user fixes it, with no extra key to dismiss it first.

### F8 With popups stacked, everything below the top one is dimmed

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

### X1 The mouse is optional

The app must be fully usable without a mouse.

**Why**: the mouse is not a first-class terminal input, and many environments (tmux, SSH, screen readers) don't have one
at all.

### X2 The mouse only maps to the keyboard

If the mouse is supported, every mouse action maps to a keyboard action; **nothing can be done by mouse alone**.

**Why**: the mouse should be another way to press the keyboard, not another thing to learn.

---

## T Time axis

The rules in this chapter can't be seen in a screenshot; they exist only in the flow of use — they surface once an app is
complete enough, and more will be added as implementation continues.

### T1 After the target completes, does the source still mean anything?

The source stays by default (F4). The target clears the source only when it is clearly judged, by function, that "once
the user completes the target, the source has lost its meaning" — the source closing while the target opens, both
animations at once, without waiting for the source ([components/layout/popup](../components/layout/popup.md), the
open and close animation); a source of several layers closes all of them together (F2).

**Judged by what is done once confirmed**: the same kind of action is the same across the family.

| What is done once confirmed | Clear the source? | Reasoning |
|---|---|---|
| Opening something to look at (a YAML viewer, details, the full text) | keep | after looking, the user carries on in the source |
| Picking a value written back (an input popup, a select written back to a form or a picker) | keep | once the value is written back, the user carries on in the source |
| Editing that item in an editor (e.g. `kubectl edit`, `$EDITOR`) | keep | after editing, the user is back on the same item |
| An action after which the item is gone (delete, move away) | clear | the source's target is gone |
| Opening a shell | clear | coming out of the session their attention has moved on; an old menu floating there is disorienting |
| Switching screens (to another screen on the chip row) | clear | the whole screen has changed |
| Drill-down (e.g. into a directory, Deployment → Pods) | clear | the view underneath has changed; the old menu's target is gone |

- **A confirm is only a gate, not a kind of target**: when a confirm comes before the action (e.g. asking once before a
  delete), judge by the action done once confirmed; cancelling the confirm always goes back to the source (F4).
- For an action not in the table, whether the source is cleared, the app may decide for itself, judging by "once done
  with the target, does the user still want to see the source?".

**Why**: keeping is the safe default, and clearing needs a reason — otherwise users who finish something can't find their
way back. "Whether to clear" can't be settled across the board: in code both cases look the same, and a screenshot can't
show it either; it depends on the action actually taken. But if the same kind of action kept the source in one app and
cleared it in another, users would have to remember which app does what, so the actions in the table follow the table
across the family. A confirm only makes the user think once more; whether the source stays depends on what is really done
after it.

### T2 Unfocused panels are dimmed, streaming content excepted

An unfocused panel **has its content dimmed with the same fade as F8** (its border being components/color's unfocused
border); **streaming content (logs, live output, remote sessions) is not dimmed on blur**; the hint on a streaming
panel's bottom border is still dimmed — the hint is not streaming content. The exception is a popup on top: attention is
on the popup then, and everything below is dimmed as F8 says.

**Why**: dimming says "focus is elsewhere, look later" — what is bright is what has focus (Principle P6). Streaming
content has no later — information is passing by, and dimming it cuts off the glance from the corner of the eye; the hint
says "what can be pressed with focus here", and dims like any other unfocused panel's. This is
also the textbook case of "rules serve the UX" (Principle P0): the origin UX of "dim on blur" is "don't compete for
focus", while streaming's UX is "catch updates from the corner of the eye" — two goals that happen to land on the same
panel, so the rule is extended rather than streaming sacrificed.

---

## S Splash

The splash is the terminu family's shared easter egg, and the **only thing in tdp that is deliberately not disclosed**.
The disclosure rules (M1, M3, M4) and the core-key rule (K1) do not apply to it; it is not a popup either, so chapter F
does not apply. The splash is documented only in tdp — never in an app's README, CHANGELOG, release notes, menus or
help.

The splash **takes the whole screen**: while it is open nothing of the screen beneath is drawn (the chip row, panels,
footer), and closing it brings the screen back — like switching to another screen, plainly not a popup.

### S1 Every app has a splash, opened with `V`

Every terminu app has a splash, opened with **`V`** on a panel. `V` is reserved for it:

- When a panel operation of some panel genuinely needs `V`, **that panel** may give `V` to the app; the splash cannot be
  summoned on that panel.
- But **at least one panel** in the app keeps `V` for the splash.

**Why**: an easter egg belongs to the family only if every member has it; and some apps' domains really do need `V`
(e.g. a selection mode) — giving up one panel is better than the whole app losing the egg.

### S2 Not disclosed

The splash does not appear in the Space menu, the global operation popup, the key reference, the footer or panel hints,
and is not written in the README, the CHANGELOG or the release notes — entries already released and the release notes
already on GitHub are cleaned too (their version headings stay).

**Why**: a listed easter egg is no longer an easter egg. The release notes, published on GitHub from the CHANGELOG, are
read by users just the same. It is the one and only exception to "disclosure is the only
mechanism" (Principle P2) — which is why it is written here and in no app.

### S3 Any key only closes the splash

While the splash is showing, **any key only closes it** — `q`, `Ctrl-C`, `Esc`, `Space` and `?` included; the key does
nothing else. A first `Ctrl-C` only closes the splash; it does not quit the app.

**Why**: faced with a screen they have never seen, users press any key to make it go away. If that key also did
something else (quit, open a menu), the egg would be a trap.

### S4 On a panel only, and only when asked for

- It is not played at start-up.
- It can only be summoned with `V` on a panel; with a popup open, in input state or in a PTY, `V` does not summon it
  (in input state `V` is a character, K8; in a PTY it belongs to the subprocess, K10).

**Why**: a splash played at start-up is an intro everyone waits through every time, not an easter egg; and one that pops
up inside a popup, an input box or a PTY interrupts what the user is doing.

### S5 The content is the family icon

The splash draws the app's `docs/icon.svg` — the terminu family mark — cell for cell, with a reveal animation; under
the mark it writes the app's name and its author.

**The mark**: the svg's viewBox is 250 × 250, the background is one 250 × 250 `#000000` rect, and a cell is one 10 × 10 rect. The mark takes
25 × 19 cells (x 0–240, y 30–210).

- **The U frame**: `#205090`, the same in every family app, never changed.
- **The letters in the frame**: `#f2b753`, designed by each app, spelling its own name (e.g. kbu's K and B; locku's L, O,
  C and K, each wrapping the next). tdp's own mark is [`icon.svg`](icon.svg): a T in the frame.
- **Letters**: marked with XML comments. A comment starts a letter and names it (e.g. `<!-- L -->`); the rects after it
  belong to it until the next comment. The first comment is the U frame (`<!-- U -->`). The order of the comments is the
  order of the reveal.
- **Drawing**: each cell is one `nf-fa-square` (U+F0C8), two columns wide (with a space after it where icons take one
  cell, E5); the background cells are squares in Surface0 `#313244`.
  The mark's 25 columns already have a background cell at either side; one more background row is drawn above it and one
  below, 21 rows in all, so the margin is the same on all four sides.

**The text under it**: a blank row under the mark, then six rows, each centred within the mark's width. The name, version
and tagline come from the app; the two author rows are the same in every family member. **No row is wider than the mark
(50 columns)**: the text is designed beforehand, like the mark, not filled in freely by the app; the lib returns an
error when it builds a splash with a wider row (E8).

| Row | Content | Colour |
|---|---|---|
| 1 | the name: the app's command name (`locku`) | Blue, bold |
| 2 | the version, as `<app> version` prints it (`v0.2.0`) | Blue |
| 3 | a one-line tagline (`A screensaver with a PIN, for the terminal`) | Text |
| | a blank row | |
| 4 | `developed by` | Overlay0 |
| 5 | the author's e-mail address: `vulcan.shen.2304@gmail.com` in a family member; its own in an app made with tdp (start of chapter E) | the mark's gold `#f2b753` |
| | a blank row | |
| 6 | `Press any key to close` | Overlay0 |

**Position**: the whole block (the mark, a blank row and the text, 30 rows × 50 columns) is centred on the screen, both
ways.

**When it does not fit**: when the terminal cannot hold the whole block (under 50 columns or 30 rows), the mark is not
drawn, only the text under it, still centred both ways and still appearing in two batches (the name, version and
tagline 400ms after opening, the author and the hint 500ms later).

- **Too narrow**: the text wraps as in the components' "Wrapping", each wrapped row centred. A word wider than the terminal on
  its own (e.g. the 26-column e-mail) is cut by cells into pieces, each centred — nothing is lost.
- **Still too short**: rows are cut from the bottom up — the hint goes first, then the two author rows, then the
  tagline; **the name and the version always show**, and with a single row only the name is drawn. When a group goes,
  the blank row above it goes with it, so no blank row is left at the bottom.

**The reveal animation**: a tick is 10ms; it is drawn in stages. Stages 1–3 (the background, each gold letter, the U
frame) have a 250ms hold between one stage and the next; stage 4 (the text) keeps its own timing, 400ms counted from the
last cell of the U frame appearing, with no 250ms added.

1. **The background**: a whole row a tick, top to bottom.
2. **The gold letters**: in the order of the comments in the svg (the letters of the app's name), one letter a stage; 2 cells a tick, the cells of
   a letter appearing scattered.
3. **The U frame**: rising from the bottom row by row, one pair a tick (two mirrored cells; the 13th cell, on the centre
   line, takes a tick of its own); within a row from the middle outwards, the cells nearest the centre line first — the base spreads out from the
   middle and both sides rise at once.
4. **The text**: 400ms after the mark is complete, the name, version and tagline appear together; 500ms later,
   `developed by`, the e-mail address and the hint appear together.

**Why**: the splash is the family's signature. Each member draws its own version of the family mark, and the animation,
text and colours are the same in every app, so pressing `V` tells you at once that this comes from the same family. The
name is the command name, the one users type in the terminal; the hint says `any key`, since by S3 any key closes it.
The author's e-mail address is in the mark's gold, tying the signature to the mark. When the block does not fit, the
text stays and the mark goes: text can wrap, the mark cannot.

---

## E App and environment

What an app does off screen: the command line, environment variables, requirements, icon width, releases, documents,
and how the shared lib and an app split the work.
This chapter is not on-screen UX; its reason is family consistency — the five apps do things the same way, so users who
have installed one can install the others, and know where to find config and data.

**Family members and apps made with tdp**: the family members are vulcanshen's apps. An app someone else makes with tdp
replaces the few places tied to vulcanshen with its own: the repo path ([project](../project/README.md)), the Homebrew
tap (E6), the author's e-mail address on the splash (S5); the README's terminu family section says instead that the app
is "built with terminu design", with a link, and does not list the family members (E7). Every other rule is the same for
both.

**Why**: an app made with tdp is not under vulcanshen's account and does not go into the same tap; copied word for word,
it would carry the wrong path and someone else's e-mail address.

### E1 Command line: `version` and `help`

Every app has:

- **`<app> version`**: prints the version. `--version` and `-v` may be aliases.
- **`<app> help`**: prints the command-line usage (unrelated to the `?` key reference inside the app). `-h` and `--help`
  may be aliases.

Other commands (e.g. `filu iconwidth`, `locku lock`, `webu <url>`), the app may decide for itself.

**Why**: `help` and `version` are the first things anyone tries on a command-line tool. With the five apps using the
same pair, what can be asked of one app can be asked of every one.

### E2 Environment variable names

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
| `<APP>__POWERLINE_WIDTH` | manual override of how many cells a powerline symbol takes (E5) |
| `TERMINU__ICON_WIDTH` | shared by the family: an app with a PTY sets it for its subprocess, telling it how many cells an icon takes (E5) |
| `TERMINU__POWERLINE_WIDTH` | shared by the family: an app with a PTY sets it for its subprocess, telling it how many cells a powerline symbol takes (E5) |
| `LC_TERMINU_ICON_WIDTH` | shared by the family: an app with ssh carries it to the remote end when connecting, telling the family apps there how many cells an icon takes (E5) |
| `LC_TERMINU_POWERLINE_WIDTH` | shared by the family: an app with ssh carries it to the remote end when connecting, telling the family apps there how many cells a powerline symbol takes (E5) |

The exception: a variable carried over ssh to the remote end starts with `LC_` (OpenSSH forwards only `LANG` and `LC_*`
by default; e.g. the `LC_TERMINU_*` above, sshu's `LC_SSHU_COLORTERM`); other variables meant for another program follow
that program's needs. Renamed variables do not keep their old names.

**Why**: a variable shows at a glance which app it belongs to, and `TERMINU__` at once means the whole family. Two
underscores separate the app name from the variable name because the variable name itself has single underscores
(`ICON_WIDTH`); two underscores can't be mixed up with them.

### E3 Where config and data live

| What | Default location | Override (E2) |
|---|---|---|
| Config | `$XDG_CONFIG_HOME/<app>` (falling back to `~/.config/<app>`) | `<APP>__CONFIG` |
| State (when the app keeps it separately) | in the config directory | `<APP>__STATE` |
| Data | under `~/.<app>/` | `<APP>__DATA` |
| Cache | the system's cache directory (macOS `~/Library/Caches/<app>`; Linux `$XDG_CACHE_HOME/<app>`, falling back to `~/.cache/<app>`; Windows `%LOCALAPPDATA%\<app>\cache`, apart from `%LOCALAPPDATA%\<app>` where install.ps1 puts the executable, so deleting the cache never deletes the program) | `<APP>__CACHE` |

**Windows**: `~` is `%USERPROFILE%` — config in `%USERPROFILE%\.config\<app>`, data under `%USERPROFILE%\.<app>\`, worked
out as on macOS and Linux, not in `%APPDATA%`.

**The config file**: `config.yaml` in the config directory.

**Which kind a thing is: ask what deleting it would do**:

- **Config**: the app's own settings — the options the app starts and runs with (the config file `config.yaml`).
- **State**: deleting it only goes back to defaults (e.g. the tabs open last time, where the cursor was).
- **Data**: deleting it loses it for good, and the user would want a backup (e.g. bookmarks, records, logs). Lists the
  user writes for the app to use are data too, even when what they hold is how the app works (e.g. sshu's hosts and
  credentials, hostu's and locku's profiles, filu's Open with list, kbu's pins); so are original values the app keeps
  for the user (e.g. what ccdrawu notes before replacing Claude Code's theme). Config is left with the app's own
  single options.
- **Cache**: deleting it makes the app rebuild or fetch it again (e.g. a downloaded browser, an index).

**When a location changes**: when a new version of the app moves something to a new location, the first start moves it
item by item and shows a toast saying from where to where:

- An item missing at the new location is moved over.
- An item already at the new location (e.g. a cache the app itself has already started there): for a cache, the old one is
  deleted — it comes back when rebuilt; settings, state and data are not deleted but left at the old location, and an
  error popup gives both paths for the user to merge them.
- Once moved, the emptied old directory is removed.
- If it can't be moved, the app keeps using the old location and opens an error popup giving both paths, for the user to
  move it themselves.

Item by item, because the new location is often created by the app before the move (e.g. ccdrawu's mod writes to the new
cache directory as soon as a session starts); moving the whole directory would then never move the old one.

**Files no longer used**: a settings, state or data file that a new version of the app no longer uses is not deleted,
and no toast is shown: what to do with it is the user's call. While the file is there, every start writes an INFO entry
to the App Log giving its path and saying the app no longer uses it (e.g. `No longer used: ~/.sshu/errors.yaml; delete
it if you don't need it`); the CHANGELOG says so too.

The App Log is kept in memory only and starts empty every time, so the entry is written at every start, for whoever
opens it.

**When it cannot be read**: when the app's own settings, state or data cannot be read (bad format, a damaged file, no
permission… whatever the cause), the app does not go on working in that state: at start it opens a confirm
([components/dialog/confirm](../components/dialog/confirm.md)) giving the path and the reason:

```
┏━󰻌 MOVE ASIDE━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                               ┃
┃ ~/.hostu/profiles.yaml can't be read:         ┃
┃ line 3: mapping values are not allowed here   ┃
┃                                               ┃
┃ Move it to profiles.yaml.bak and start fresh? ┃
┃                                               ┃
┗━ Enter:move Esc:quit ━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **`Enter`** (`move`): renames that file to `<name>.bak` and starts as on the first start: settings take their
  defaults, state and data start empty, and a file the first start makes is made again, while one it does not make
  appears at the first save. If a `.bak` is already there, `.bak.1`, `.bak.2`… are used — nothing is ever overwritten;
  the question names the file that will really be used. When the data is one record per file (e.g. kamonu's one file
  per mark), the record that cannot be read is just renamed to `.bak`, nothing new is made, and the rest is read as
  usual; the question reads `Move it to <name>.bak and go on without it?`.
- **`Esc`** (`quit`): quits the app, rather than going back to it; the path and the reason are written to stderr, so the
  shell still shows what to fix.
- **A cache** that cannot be read: no question; it is thrown away and rebuilt.
- **Something outside the app** that cannot be read (a cluster, the network, a remote host): the app itself is fine and
  stays open; the panel shows it as "Loading and errors" in [components/layout/panel](../components/layout/panel.md)
  says, and the details go into the App Log (F5).

Working on as usual while a file cannot be read could overwrite the user's things at the next save; renaming it to
`.bak` starts again with one key and loses nothing. Whoever does not want the app to touch it presses `Esc`, quits and
deals with it themselves.

**Config keys shared by the family**: the same setting has the same name in every app's config file, in the apps that use
it.

| Key | Meaning | Default |
|---|---|---|
| `hide_secrets_in_preview` | hide private keys and owner-only files in the previews of popups ([components/input/file-picker](../components/input/file-picker.md)) | `false` |
| `input_tab_width` | how many spaces one `Tab` inserts in the writing state of multi-line text ([components/input/textarea](../components/input/textarea.md)); a Tab in content for reading (viewers, file previews, a log on a panel) is drawn as that many spaces too (the App Log every app has does not count as using it: an app with only that keeps the default and needs no such key); in names and short text (values on forms and panels, list cells, menu text…) and an input's typing row, a Tab is drawn as a red `\t` ("Control characters" in [components](../components/README.md)) | `4` |

**Why**: with the five apps in the same places, users know where to look and what to back up. macOS does not use the
system's usual `~/Library/Application Support`, nor Windows `%APPDATA%`: one way of working it out on every platform, the
same place on whatever machine. The cache goes in the
system's cache directory so that cache-cleaning tools can find it, and so it is not taken for data to back up. Sorting
by what deleting would do: from the location alone the user knows what to back up and what can go without harm; config
holds only the options the app itself runs with; lists the user writes for the app (connections, profiles,
bookmarks) took the user's effort, and original values the app keeps are the user's too; neither can be got back once
deleted, so like bookmarks they are data. One name and format
for the config file: whichever app's config directory the user opens, they know which file to edit. Moving things over
when a location changes: users never upgrade once and find their bookmarks and records gone; when the move fails, the
app names both paths instead of quietly starting a new copy. Shared config keys have one name: set once in one app, the
user knows how to set it in another.

### E4 Requirements: a Nerd Font and truecolor

- Requires a Nerd Font; PUA glyphs are written as code points in the source.
- Requires a truecolor (24-bit) terminal: catppuccin's pale colours and components/color's layer gradient are indistinguishable in 256 colours, and dimming always outputs 24-bit (components/color). READMEs say so in their requirements, next to the Nerd Font.

**Why**: the family's icons, loading icon, and radio and checkbox glyphs are Nerd Font glyphs; the reason for truecolor is
given above.

### E5 The icons' real width

With some fonts an icon takes two cells (the cursor moves two), while the width-measuring function measures one, and the
borders go crooked. What is measured is **how far the cursor actually moves**: a font whose icon looks wider than a cell
but moves the cursor one (the glyph spills into the next cell) counts as one.

- **Two kinds of glyph, each measured on its own**:
  - **Icons**: Nerd Font icons, the Private Use Area (U+E000–U+F8FF, U+F0000–U+FFFFD), except the powerline symbols below
    (e.g. the hexagon U+F02D8 before a menu section title is an icon).
  - **Powerline symbols**: U+E0A0–U+E0D7 — the ends and seams of capsules, the round ends of a popup title, the arrow at
    the end of the cursor.
- **Measured at run time**: the app probes at startup (CPR: print an icon, ask for the cursor position; print a powerline
  symbol, ask again). Every width measurement (padding, clipping, centring, joining side by side, borders, overlaying
  popups) goes through one display-width function.
- **Overrides and order**: each is taken in this order — icons from `<APP>__ICON_WIDTH`, then `TERMINU__ICON_WIDTH`, then
  `LC_TERMINU_ICON_WIDTH`, then the probe; powerline symbols from `<APP>__POWERLINE_WIDTH`, then `TERMINU__POWERLINE_WIDTH`,
  then `LC_TERMINU_POWERLINE_WIDTH`, then the probe. What the user set, and what an outer app set inside its PTY, is
  closest to the moment, so it comes first; what came over ssh (below) beats the remote side's own probe, so it comes
  before the probe. The probe
  runs on unix only; Windows defaults to one cell, overridden by the environment variables.
- **Inside another app's PTY**: the probe is answered by the outer app's terminal emulator, which counts both as one
  cell, so the real width can't be measured. An app with a PTY therefore sets `TERMINU__ICON_WIDTH` and
  `TERMINU__POWERLINE_WIDTH` (the cells it uses) in its subprocess's environment when it starts one. Any family app
  running inside another's PTY then gets it right (filu in kbu's Alterm, kbu in filu's shell).
- **Across ssh**: ordinary environment variables don't cross ssh (OpenSSH forwards only `LANG` and `LC_*` by default). An
  app with ssh puts the cells it uses into `LC_TERMINU_ICON_WIDTH` and `LC_TERMINU_POWERLINE_WIDTH` and carries them
  over when it connects (sending is that app's own business, e.g. sshu); a family app on the remote end reads the two
  variables at startup (receiving is done by the lib, E8), so whichever family app runs there gets them.
- **Overlaying a popup must not crash**: a popup may be wider or taller than the screen (the frame drawn during a resize
  still has the old size): start at 0 and clip what falls off the screen, and **never panic**; when it is larger in both
  directions it is clipped too, never handed back whole.
- **Tests**: the L4 screen tests run twice more — "icons take two cells, powerline symbols one" and "both take two
  cells" — opening each kind of popup once and measuring both the bare box and the whole screen with it overlaid (with
  the lib, who tests which part: E8); the edge cases include the popup wider than the screen, taller than it, and larger
  both ways, and sizes below L1's minimum size all the way down to 1×1 (e.g. 80×5, 1×1): no crash, and the name and the hint
  drawn.

> **Implementation reference (not a requirement)**: filu `internal/ui/width.go` — `isWideIcon()`, `dispWidth()`,
> `dispClip()`, `padDisp()`, `dispCutLeft()`, `compositeDisp()` (replaces overlay's `Composite`, same interface),
> `centerDisp()` (replaces `lipgloss.Place`), `joinH()` / `joinV()` (replace `lipgloss.JoinHorizontal` /
> `JoinVertical`); detection is `DetectIconWidth()` in `iconwidth_unix.go`, called before `tea.NewProgram`; tests follow
> `d6_test.go` and `TestD6CompositeDispOversized`. Once done, it can be checked like this: apart from the width functions
> themselves, `internal/ui` has no calls to `lipgloss.Width`, `lipgloss.Size`, `lipgloss.Place`, `ansi.StringWidth` or
> `ansi.Truncate`. filu measures icons only and counts powerline symbols as one cell; the powerline width is added the
> same way.
>
> bubbletea v1's renderer appends "erase to end of line" (`ESC [ K`) to a line it measures as narrower than the
> terminal, and it counts an icon as one cell. Where icons take two cells, that line is in fact already full and the
> cursor sits in the last column; a terminal following the xterm rules then erases the last cell (the right border) as
> well. L4 keeps every line full width, so this erase is always redundant: remove it in the output layer.

**Why**: crooked borders make the whole screen unreadable, and the same font can move the cursor differently on different
terminals, so it can only be measured at run time. Icons and powerline symbols are measured separately because the two
can differ on the same terminal: Nerd Fonts make the powerline symbols one cell so they join the borders, so where icons
take two cells they often still take one; and some setups make both take two. With a single width, one of the two
cases goes crooked. One set of `LC_TERMINU_` variables across ssh: only the apps with ssh send, but every family app
receives, so receiving is done once in the lib and is right whichever app runs on the remote end. The tiny sizes are
tested because a crash that only happens on a very small screen (e.g. opening a menu with only a few rows left) is never
caught when the edge cases don't ask for it.

### E6 Releases, tests and family assets

- A single static binary built with goreleaser; `install.sh` / `uninstall.sh` (`curl | sh`, no sudo),
  also published to the Homebrew tap `vulcanshen/homebrew-tap` (an app made with tdp publishes to its own tap; start of
  chapter E).
- The repo's directories, Makefile, version, CHANGELOG and release follow [project](../project/README.md); its
  template files are copied as they are.
- Screen tests across sizes: at several terminal sizes, every line is exactly the terminal width (L4).
- `docs/icon.svg` is the app's version of the family mark (what it looks like: S5; tdp's own is `principle/icon.svg`),
  and it is the original; the splash (chapter S) is drawn from it cell for cell. The program keeps a second copy for the
  splash (a copy of the file under `internal/`, or the cells written into the code; Go's `go:embed` cannot reach
  `docs/`), with a test keeping the two identical.
- Demo gifs are recorded with VHS, scripts in `.local/demos/` (how many go in the README: see E7).

**Why**: the five apps install, uninstall and release the same way; having installed one, users can install the others.
The screen tests guard L4; with the icon and splash test, the splash is not forgotten when the icon changes.

### E7 Documents

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
10. Related links: CHANGELOG; other links, the app may decide for itself
11. terminu family: follows terminu design, lists the other family members (an app made with tdp: says it is "built with
    terminu design", with a link, and lists no family members; start of chapter E)
12. License

- **All 12 sections are required, in this order.** Content that belongs to one of them goes into it as a subsection
  (e.g. updating goes under "Installation", next to removal).
- **Whether content that belongs to none of them gets a section of the app's own, the app may decide for itself**; the
  section goes right after the section it relates to most, but only between section 4 (Features) and section 9 (Limitations): the start (1–3) and the end (10–12) are fixed.
  Common sections get their place here: **Troubleshooting** goes after "Usage and keys".
- **Section 3 holds just one** representative gif. Whether other sections carry a gif or a screenshot explaining that
  section, the app may decide for itself — the fewer the better.

No "status" section with a hard-coded version number — versions are left to the badge and the CHANGELOG.

The README's settings section names the shared config keys of E3 the app uses (e.g. `hide_secrets_in_preview`,
`input_tab_width`) and their defaults.

Where the README talks about the icon width (usually the Nerd Font part of the prerequisites), it names the icon's
`<APP>__ICON_WIDTH` and `TERMINU__ICON_WIDTH` and the powerline symbols' `<APP>__POWERLINE_WIDTH` and
`TERMINU__POWERLINE_WIDTH`, and says the `TERMINU__` ones are shared by the whole family: set once and every family app
reads them; inside a family app's PTY the outer app sets them (E5). The form is free (a table or a sentence).
It names no font as "always two cells" — the same font may move the cursor differently on different terminals.

Developer documents (design records, notes on developing and releasing) are outside tdp's scope (Principle P5).

**Why**: a README introduces the tool, and what users want from it is "what is this, how do I install it, how do I use
it"; what is for developers stays out of it. With the 12 sections fixed, users know where to find the
installation, the keys and the configuration in any family app's README; with the start and the end fixed, the middle
can grow sections of the app's own. Too many gifs scatter the reader's attention: one representative gif at the start,
and others only where a section truly needs one.

### E8 The shared lib and its example app

The family's shared lib (terminu-go) turns the on-screen rules into code that apps call; its example app (the showcase)
shows every component and every combination, and is not released. A lib is not an app, and some rules do not fit it;
when an app uses the lib, which rules the lib covers and which stay with the app is set by this table:

| Rule | The lib | The example app | An app using the lib |
|---|---|---|---|
| The on-screen rules (K, M, L, F, X, T, S1–S4, components) | covers them | shows all of them | from the lib, not done again |
| E1 `version`, `help` | — | yes | its own |
| E2 naming environment variables | the variables the lib reads hang under the app's name (e.g. `<APP>__ICON_WIDTH`) | as E2 (e.g. `SHOWCASE__…`) | its own variables follow E2 |
| E3 where config and data live | — | stores nothing, not applicable | its own |
| E4 requirements | stated in the README | — | stated in the README |
| E5 the actual icon width | covers it: the probe (icons and powerline symbols), the display-width functions, setting `TERMINU__ICON_WIDTH` and `TERMINU__POWERLINE_WIDTH` for subprocesses, reading `LC_TERMINU_ICON_WIDTH` and `LC_TERMINU_POWERLINE_WIDTH` at startup; in E5's tests, measuring the bare box of each kind of popup (the lib draws the popups) | — | from the lib; an app with ssh sends `LC_TERMINU_*` itself when connecting. E5's tests cover its own whole screen only: its own layout plus the popups it opens, at E5's widths and sizes, every line full width |
| E6 releases | a git tag (a Go module), no binary; the L4 screen tests are required | not released; the L4 screen tests are required | as E6 (the screen tests split as in the row above) |
| S5 the icon the splash draws | the splash mechanism; building a splash, it returns an error for a row of text wider than 50 columns | tdp's `principle/icon.svg` (terminu's mark) | its own `docs/icon.svg` |
| E7 README | a structure of its own: installation is `go get`, the quick start is code, and it says how to run the example app | none of its own | as E7 |
| A requirement that cannot be met, or works badly ("Leaving it to the app" at the start of the Rules) | **the lib does not do its own thing**: it reports a gap in tdp, and the lib changes once the spec does | — | reports a gap in tdp |

- This only sets the split when an app uses the lib. Whether to use the lib, the app may decide for itself.

**Why**: an app moving to the lib needs to know what it can delete — the on-screen code and E5 go, while E1, E3, E6, E7
and its own icon stay — without every app working that out again. The lib holds the screen the family shares, so if the
lib does its own thing, every app using it stops following tdp with it; when the lib meets something it cannot do, it always reports a gap in tdp
and the spec changes first. The screen tests split by who draws what: the popup boxes are the lib's, tested once there;
the app's layout and the popups it opens over it exist only in the app, which tests them itself.

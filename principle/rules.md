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

---

## K Core keys

### K1 Core keys mean the same thing everywhere in the app `fixed`

| Key | Meaning | Rule |
|---|---|---|
| `Tab` | Move focus to the next object on the same level | K2 |
| `Enter` | Do the most obvious action to the focused item; in an input popup, submit | K3 |
| `Esc` | Cancel / close the top layer | K4 |
| `Space` | On a panel, open / close the Space menu (what can be done here) | K5, M2 |
| `?` | Open / close help: on a panel, the `?` menu (what the whole app can do); on a popup, that popup's help | K6, M4 |
| `q` | Quit the app | K9 |

These keys carry this meaning on **every surface**; the only exceptions are input state
(K8) and PTY (K10). An app need not use all of them (a single-panel app has no use for
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
| a panel made of several cells (e.g. sshu's SSH grid) | cells |

- `Tab` does not cross screens or leave the current popup.
- **When there is no other object on the same level** (e.g. an input with a single field),
  the app may use `Tab` to accept a greyed-out suggestion (autocomplete), and for nothing
  else.
- Cycling backwards (e.g. `Shift-Tab`) is a hotkey; whether to offer it is up to the app.

**Why**: users press `Tab` expecting "the next one" — the next panel on a screen, the
next field in a form. It is the same role at different levels. Switching screens is a
global operation (P3).

### K3 `Enter` does the most obvious action; in an input popup it submits `concept`

`Enter` does **the most obvious action** to the focused item — enter a directory,
connect, open, flip a setting. What exactly is up to the app, but the same kind of item
always gets the same action within an app.

**In an input popup, `Enter` submits** (fixed):

- Before submitting, check **every** field. Submit only if all of them are valid.
- If any field is invalid, **don't submit, and disclose the error**: which field, and
  why. How to disclose it is up to the app (a mark beside the field, a suffix on the box
  title, focus jumping to the first invalid field…).
- `Enter` does not stand in for `Tab` to move to the next field (K2).
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

### K6 `?` opens and closes help from anywhere `fixed`

`?` responds on any surface; `?` again closes it, and so does `Esc`. What it shows
depends on focus:

| Focus is on | `?` opens |
|---|---|
| a panel | the `?` menu: runnable global operations + key reference (M4) |
| a popup (the Space menu included) | **only this popup's help**: which keys work in this box and what they do; no item / panel / global |

Input state and PTY follow K8 and K10.

**Why**: `?` is the last way out for a lost user, so it must work everywhere. But a user
lost in a popup wants "how does this box work", not the whole app's global actions —
those can wait until they are back on a panel.

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
| `Tab` | switches fields (K2) |
| `Ctrl-C` | starts the quit flow (K9) |

Normal behaviour returns the moment focus leaves the input surface.

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
- Quitting is listed among the global operations of the `?` menu (M4).

**Why**: `Ctrl-C` is in every terminal user's muscle memory, and `q` is the TUI
convention; if the two behaved differently, users would have to remember which one asks
and which one doesn't. Pressing `Ctrl-C` twice to force quit means users can never be
trapped by their own confirm box.

### K10 PTY: keys belong to the subprocess, the app keeps one way out `concept`

With focus in a PTY (a shell, editor or remote session running inside the app), **every
key goes to the subprocess**, core keys included — vim needs `Esc`, the shell needs `Tab`
and `Ctrl-C`.

The app must provide **one** key that moves focus out of the PTY, choosing a combination
the subprocess almost never uses (e.g. kbu's `Alt-t`, sshu's `Alt+Esc`), and disclose it
permanently while focus is in the PTY.

**Why**: the program in the PTY has its own key language, and any key the app intercepts
breaks it. But a PTY with no way out is a trap, so the exit key must exist, and it must
be visible.

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
| 3 | `global operation` | **all** of the app's global actions — the same list, in the same order, as the global operations of the `?` menu |

- **The header strings are fixed**, word for word as in the table above, across the app
  and the family.
- **No target, no region**: an empty list has no item, so item operation disappears,
  header and all.
- **When only one region is left, it has no header** and is listed directly.
- Regions are separated by a divider line.

**Why**: users read top down, so they see "what can I do to the thing I picked" first,
then "to this whole panel", and global last. Fixed header strings let users recognise
"this is the same kind of menu" at a glance — a menu worded differently reads as a
different **kind** of menu. Putting global last means remembering the one key `Space` is
enough to find everything, without pushing the current panel's actions down.

### M3 Every action can be found in a menu `fixed`

- Every item operation and panel operation of every panel is in that panel's Space menu.
- Every global operation is in the `?` menu and in the global region of the Space menu.
- A popup's own operations are all in that popup's `?` help and bottom-border hint (K5,
  K6).
- **A letter hotkey is a shortcut to a row in some list, not an extra feature.** An
  action triggered only by hotkey and found nowhere else is a violation.

Which region an action belongs to depends only on **what it acts on**, never on how
important it is (Principle P3).

**Why**: a new user who has never seen a hotkey must be able to do everything, anywhere,
with `Space` and `?` alone. Each action that has to be learned in advance is a hole in
"usable without the docs".

### M4 `?` menu: runnable global operations + key reference `fixed`

With focus on a panel, the `?` menu has two parts:

1. **A `global operation` region**: every global action of the app, **runnable in
   place** (`j/k` to pick, `Enter` to run, or the row's hotkey where it has one).
   Quitting the app must be here (K9).
2. **A `key reference` region**: a read-only key table listing at least the core keys
   the app uses; whether to list anything else (navigation keys, hotkeys) is up to the
   app.

With focus on a popup, `?` shows only that popup's help (K6).

**Why**: a help page you can only read is documentation, not disclosure (Principle P2).
Global actions belong to no panel, so they need a place that can be summoned from any
panel and run from directly.

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

Hotkey marking is one rule for the whole app (menus, footer, panel hints and popup hints
alike):

| Case | Form |
|---|---|
| Single letter | `[r]ename`, `[D]elete` |
| With a modifier | `[Alt-t]erm` |
| Several characters | `[go]to` |
| Digits | always in front: `[3] Favorites`, never inside the word |
| No hotkey | no brackets |

- **What is in the brackets is exactly the key to press, case included**: `[A]dd` is
  `Shift+A`.
- Colour or a glyph alone must not be the hint that "this is a hotkey"; mark it
  explicitly.
- What the description says is up to the app, but it must fit on one line.

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

### F1 A popup belongs to exactly one class `fixed`

The app defines its own popup classes (e.g. menu, confirm, input, viewport, toast, PTY),
each with a fixed layout; **a popup belongs to exactly one class** — no hybrids (such as
something that is both a menu and a scrolling viewport).

**Why**: the class is the user's expectation of "what keys do inside this box". A hybrid
popup gives the same keys two possible meanings inside one box.

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
  reversible. Once an action is set to be confirmed, it is confirmed every time.
- `Enter` accepts, `Esc` cancels (K3, K4). A confirm may have hotkeys of its own (e.g.
  `y` / `n`), listed in the confirm's `?` help (K6).
- The prompt says **what accepting will do** (verb and object), not an abstract OK.
- A confirm cannot be completed by accident (e.g. a mouse click must not accept it).

**Why**: users must know the consequence before pressing `Enter`. Whether to stop and
confirm depends on how much the action weighs for the user — launching an external
program, cutting a session, deleting a file: the app knows the weight best, and no rule
such as "reversible means no need to ask" can judge it.

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
dim on blur, this rule does not apply.

**Why**: dimming says "focus is elsewhere, look later". Streaming content has no later —
information is passing by, and dimming it cuts off the glance from the corner of the eye.
This is also the textbook case of "rules serve the UX" (Principle P0): the origin UX of
"dim on blur" is "don't compete for focus", while streaming's UX is "catch updates from
the corner of the eye" — two goals that happen to land on the same panel, so the rule is
extended rather than streaming sacrificed.

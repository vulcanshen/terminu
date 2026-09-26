# tdp Rules

**Language**: English · [繁體中文](rules-zh_TW.md)

Every rule here **must hold**. Each carries a "why", which is its origin UX
([Principle P0](README.md#p0-rules-serve-the-ux-not-the-other-way-round)).

**Departure**: when an app's nature makes a rule inapplicable, the app may leave it, but
must write down **which rule, where, and why** in the "Departures from tdp" section of its
`docs/dev-remarks.md`. A departure with a written reason is a legitimate design decision;
not following a rule without one is a **violation**, listed in `docs/<app>-terminu-fix.md`.

**Citing**: `tdp` plus the ID, e.g. `tdp K4`, `tdp M2`. Once published, IDs are never
renumbered; a retired rule keeps its ID and is marked retired.

| Chapter | Scope |
|---|---|
| [K](#k-core-keys) | Core keys |
| [M](#m-menus-and-disclosure) | Menus and disclosure |
| [L](#l-layout) | Layout |
| [C](#c-colour) | Colour |
| [F](#f-popups) | Popups |
| [X](#x-mouse) | Mouse |
| [T](#t-time-axis) | Time axis |

---

## K Core keys

### K1 Core keys mean the same thing everywhere in the app

| Key | Meaning | Rule |
|---|---|---|
| `Tab` | Move focus to the next surface | K2 |
| `Enter` | Do the most obvious action to the focused item | K3 |
| `Esc` | Cancel / close the top layer | K4 |
| `Space` | Open / close the Space menu (what the current focus can do) | K5, M2 |
| `?` | Open / close the `?` menu (what the whole app can do) | K6, M4 |

These keys carry this meaning on **every surface**; the only exception is input state
(K8). An app need not use all of them (a single-panel app has no use for `Tab`), and may
designate core keys of its own; once designated, those also keep their meaning on every
surface. No letter hotkey may take over a key in this table.

**Why**: what users learn is a **role** ("cancel", "move focus", "what can I do now"),
not a key. With the roles fixed, one lesson holds on every surface of every app in the
family. A single surface where `Space` does something else adds a rule to learn: "except
here".

### K2 `Tab` cycles through the surfaces of the current screen

`Tab` moves focus to the next panel of the current screen, wrapping from the last to the
first. It does not cross screens or tab pages. Cycling backwards (e.g. `Shift-Tab`) is a
hotkey; whether to offer it is up to the app.

**Why**: users press `Tab` expecting "the next pane", not "another screen". Switching
screens is a global operation (M4).

### K3 `Enter` does the most obvious action, defined by the app

`Enter` does **the most obvious action** to the focused item — enter a directory,
connect, open, submit a form. What exactly is up to the app's context, but the same kind
of item always gets the same action within an app. In a popup, `Enter` accepts or submits.

**Why**: a literal definition such as "confirm / enter" does not survive real apps:
opening a file, connecting to a host and submitting a form are all `Enter`, and none of
them is literally "confirm". What users expect from `Enter` is "do the natural thing to
this".

### K4 `Esc` closes one layer at a time and never leaves the app

`Esc` cancels the current operation or closes the top layer: a popup if there is one
(toasts included); otherwise it leaves the current mode (search, selection, dragging) or
goes up one level. **One layer per press**, and **`Esc` never leaves the app** — at the
top it does nothing.

**Why**: a lost user presses `Esc` repeatedly to get back somewhere safe. If the end of
that sequence is the app closing, `Esc` becomes a dangerous key, users stop pressing it,
and the safe way out is gone. Quitting is a global operation with its own entry (K9, M4).

### K5 `Space` opens and closes the Space menu

`Space` opens the Space menu (M2); while it is open, `Space` closes it again. `Esc`
closes it too.

**Why**: an entry key that opens but cannot close is a trap — users reach for the same
key to get out and nothing happens.

### K6 `?` opens and closes the `?` menu from anywhere

`?` opens the `?` menu (M4) **on any surface, including on top of other popups**; `?`
again closes it, and so does `Esc`.

**Why**: `?` is the last way out for a lost user. If some popup swallows it, it is
missing exactly when it is needed most.

### K7 Aliases are complete or absent

When a role is bound to several keys (e.g. both `Esc` and `q` cancel), every alias must
work **on every surface**. If that is not possible, don't alias.

**Why**: a partial alias (`q` cancels on the main screen but not in popups) is worse than
none — it looks like a convenience, but adds a rule to learn: "where it works and where
it doesn't".

### K8 Input state: hotkeys are off

While the user is typing (form field, input box, search line), **every key that produces
a character is a character** and triggers nothing:

| Key | In input state |
|---|---|
| letter hotkeys, `Space`, `?` | typed as characters |
| `Esc` | cancels the input (K4) |
| `Enter` | submits (K3) |
| `Tab`, arrows | move within the input surface's own fields |

This is the only exception to K1; it holds only inside input state and ends the moment
focus leaves the input surface.

**Why**: `Space` and `?` are printable. Without this, users could never type a file name
with a space or a password with a question mark. `Esc` and `Enter` stay, because they do
not compete with characters, and without them the input box is a trap with no exit.

### K9 There is always a way out

The app must offer a way to quit, listed among the global operations of the `?` menu.
`Ctrl-C` ends the app from **any state**, including with a popup open, while searching,
while typing. The only exception is when focus is inside a PTY or subprocess; there
`Ctrl-C` belongs to that process.

**Why**: `Ctrl-C` is in every terminal user's muscle memory. If some state swallows it,
users assume the app has hung.

---

## M Menus and disclosure

### M1 The entry points are visible

Every screen outside input state must **permanently show** the two entry points, `Space`
and `?`, so a first-time user who has read nothing can see them. The form is up to the
app (footer, sidebar, empty-state hint).

**Why**: users cannot press a key they do not know exists. An undisclosed entry point
might as well not exist, however complete the disclosure behind it (Principle P2).

### M2 Space menu: item → panel → global

The Space menu lists **everything the current focus can do**, split by what it acts on
(Principle P3), in a fixed order:

| Order | Region header | Contents |
|---|---|---|
| 1 | `item operation` | what can be done to the one item under the cursor |
| 2 | `panel operation` | what can be done to the current panel (or its tab) as a whole |
| 3 | `global operation` | the app's global actions — the same list, in the same order, as the global operations of the `?` menu |

- **The header strings are fixed**, word for word as above, across the app and the family.
- **No target, no region**: an empty list has no item, so item operation disappears,
  header and all.
- **When only one region is left, it has no header** and is listed flat.
- Regions are separated by a rule line.

**Why**: users read top down, so they see "what can I do to the thing I picked" first,
then "to this panel", and global last. Fixed header strings let users recognise the same
kind of menu at a glance — a menu worded differently reads as a different **kind** of
menu. Putting global last means remembering `Space` alone is enough to find everything,
without pushing the current focus's actions down.

### M3 Every action can be found in a menu

- Every item operation and panel operation of the current focus is in the Space menu.
- Every global operation is in the `?` menu and in the global region of the Space menu.
- **A letter hotkey is a shortcut to a row in a menu, not an extra feature.** An action
  reachable only by hotkey, missing from the menus, is a violation.

Which region an action belongs to depends only on **what it acts on**, never on how
important it is (Principle P3).

**Why**: a new user who has never seen a hotkey must be able to do everything on every
focus with `Space` and `?` alone. Each action that has to be learned in advance is a hole
in "usable without the docs".

### M4 `?` menu: runnable global operations + key reference

The `?` menu has two parts:

1. **A `global operation` region**: every global action of the app, **runnable in
   place** (`j/k` to pick, `Enter` to run, or the row's hotkey). Quitting the app must be
   here (K9).
2. **A `key reference` region**: a read-only key table listing at least the core keys
   the app uses; anything else (navigation keys, hotkeys) is up to the app.

**Why**: a help page you can only read is documentation, not disclosure (Principle P2).
Global actions belong to no focus, so they need a place that can be summoned from any
surface and run from directly.

### M5 Each row = name + description, hotkeys marked with `[]`

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

Hotkey marking is one rule for the whole app (menus, footer, panel hints alike):

| Case | Form |
|---|---|
| Single letter | `[r]ename`, `[D]elete` |
| With a modifier | `[Alt-t]erm` |
| Several characters | `[go]to` |
| Digits | always in front: `[3] Favorites`, never inside the word |
| No hotkey | no brackets |

- **What is in the brackets is exactly the key to press, case included**: `[A]dd` is
  `Shift+A`.
- Colour or a glyph alone must not be the hint that "this is a hotkey"; mark it explicitly.

**Why**: the name answers "what action is this", the description answers "what does it
do to what" — the same verb can mean different things on different focuses (delete the
file, or remove the bookmark?). A description that won't fit on one line usually means
the action is badly named. Digits stay out of words because `432hz` would render as
`4[3]2hz`.

### M6 Actions that can't run right now: dimmed, with the reason

- **No target**: the row (or region) is not shown (M2).
- **A target, but the action can't run right now**: the row is still shown, **dimmed**,
  with the reason; the cursor can land on it, and its hotkey does nothing.

**Why**: users take a hidden action to mean the app can't do it; a dimmed row with a
reason tells them "this exists, just not now, because…".

### M7 Entry points always respond

`Space` and `?` open their menu on every surface, never nothing. With no runnable action,
the menu still opens and says there is nothing to do, and how to close it.

**Why**: when a key does nothing, users think the key is broken, not that there is
nothing to do here.

### M8 Other grouped menus: cursor-related first

Any menu other than the Space menu that groups its rows puts the actions related to the
current cursor first, then groups each under a header naming its kind. A menu that needs
no grouping is listed flat.

**Why**: as in M2 — users look first for "what I can do to the thing I picked".

---

## L Layout

### L1 Usable at narrow widths

At a reasonable minimum size (80×24, common for SSH sessions) the app must still get its
core tasks done. How the panels split, and what folds away when narrow, is up to the app.

**Why**: TUIs are often used on someone else's machine, in a split window, over SSH from
a phone. A TUI that needs a wide screen fails where it is needed most.

### L2 Width does not follow content

Dynamic text in titles, statusbars and chips uses fixed-width slots or padding; its width
never tracks the length of the content.

**Why**: once widths float, the main view shifts sideways and the whole screen shakes as
popups open and close.

### L3 Chrome has a fixed number of rows

The number of rows for footer, statusbar, tab row and other permanent chrome is **the
app's choice, and once chosen it is locked**; it does not change with the amount of
content. What doesn't fit is truncated or dropped from the end, never wrapped.

**Why**: one more chrome row is one less main row, and the whole layout shifts. Stability
always beats saving space.

### L4 Every line is exactly the terminal width

Every line on screen is exactly as wide as the terminal, no more, no less, guarded by
tests across several sizes.

**Why**: one cell too many and the terminal wraps, knocking the whole screen out of
place; one too few and stale cells linger. Misjudged CJK and icon widths are the usual
cause, and only tests catch them.

### L5 Focus is visible, and moving it moves nothing else

The focused surface must be recognisable at a glance, and moving focus **must not shift
any content**.

**Why**: users need to know where their keys will go; and if the screen jumps every time
focus moves, the eye has to find its place again.

---

## C Colour

### C1 Few anchors, everything else derived

Pick a few anchor colours first (e.g. background, user footprint, top popup layer) and
derive every other level from them, instead of picking a colour for each element.

**Why**: hue and lightness are all a TUI has to encode levels. With few anchors, meanings
stay clear; pick a colour per element and in the end no colour means anything.

### C2 Lightness is the z-axis, never reversed

From the background up to the topmost popup, lightness moves in one direction: **the
higher the layer, the lighter**. It never reverses.

**Why**: a TUI has no shadows or elevation; lightness is the only way to say "which one
is on top". Reverse it once and users can no longer tell the stacking order.

### C3 Lightness bands are dedicated

Each meaning owns one lightness band, and no other meaning may use it (Principle P4).

**Why**: if the "user footprint" band also colours popup borders, users seeing that
colour will wonder "is this something I set?"

### C4 Warning colours stay out of the z-axis

Strong signals such as error and warning colours are independent of the lightness system
and keep the same colour on every layer.

**Why**: a warning colour that brightens and dims with its layer reads as an ordinary
element of that layer.

### C5 When one key has two visible indicators, show which one fires

When a hotkey does different things on different focuses and both indicators are **on
screen at the same time**, use lightness to show **which one fires on the current
focus**: the one that fires is bright, the other dim.

**Why**: the brightness hand-off itself says "pressing this key here does this", with no
text or popup needed to explain it.

### C6 Dimming on blur is for static content only

If an unfocused panel is dimmed, that applies only to static content; **streaming content
(logs, live output) is never dimmed on blur**.

**Why**: dimming says "focus is elsewhere, look later". Streaming content has no later —
information is passing by, and dimming it cuts off the glance from the corner of the eye.

---

## F Popups

### F1 A popup belongs to exactly one class

The app defines its popup classes (e.g. menu, confirm, input, viewport, toast, PTY), each
with a fixed layout; **a popup belongs to exactly one class** — no hybrids (such as a
menu that is also a scrolling viewport).

**Why**: the class is the user's expectation of "what keys do inside this box". A hybrid
gives the same keys two possible meanings inside one box.

### F2 Opening and closing are animated, 100–200 ms

Popups animate both when opening and when closing, for 100–200 ms.

**Why**: without animation users don't feel the z-axis change; too long and it breaks
their rhythm.

### F3 Border colour follows the layer

A popup's border colour is derived from its stacking layer via the anchors (C1, C2) —
not hard-coded, never reversed.

**Why**: the border colour is the user's only cue that "this box is on top".

### F4 `Esc` closes any popup at once

Any visible popup — auto-dismissing toasts included — closes **immediately** on `Esc`,
without waiting for an animation. A popup that is closing no longer takes keys.

**Why**: users are not obliged to wait out a countdown. If a closing popup still eats
keys, the user's next key goes to the wrong place.

### F5 The source stays by default

When popup A opens popup B, A stays underneath by default; cancelling B returns to A.

**Why**: the user did not dismiss A, they just did one thing in B. If cancelling B also
removes A, they have to walk the whole way again. (Whether A stays after B *completes* is
T1.)

### F6 Errors show at once, without blocking the app

Errors must appear immediately (toast or popup), close on `Esc`, and **must not block the
app**. Whether there is an error history to look back at is up to the app.

**Why**: an error you can't see never happened; an error that blocks the app keeps the
user from dealing with the error itself.

### F7 Confirm: `Enter` accepts, `Esc` cancels, and it says what will happen

- `Enter` accepts, `Esc` cancels (K3, K4).
- The prompt says **what accepting will do** (verb and object), not an abstract OK.
- Irreversible or destructive actions are always confirmed; reversible toggles never are.
- A confirm cannot be completed by accident (e.g. a mouse click must not accept it).

**Why**: users must know the consequence before pressing `Enter`; and confirming every
step trains them to press without reading, so the one dangerous time goes unread.

---

## X Mouse

### X1 The mouse is optional

The app must be fully usable without a mouse.

**Why**: the mouse is not a first-class terminal input, and many environments (tmux,
SSH, screen readers) don't have one at all.

### X2 The mouse only maps to the keyboard

If the mouse is supported, every mouse action maps to a keyboard action; **nothing can be
done by mouse alone**.

**Why**: the mouse should be another way to press the keyboard, not another thing to learn.

---

## T Time axis

The rules in this chapter can't be seen in a screenshot; they exist only in the flow of
use (Principle P6).

### T1 After the target completes, does the source still mean anything?

The source stays by default (F5). The target clears the source before it enters only when
it is clear, by design, that "once the user completes the target, the source has lost its
meaning":

| Target | Clear the source? | Reasoning |
|---|---|---|
| A short confirm / message | keep | the user may want to go back to the menu and continue or cancel |
| A long session (shell, editor) | clear | coming out of the session their attention has moved on; an old menu floating there is disorienting |
| A big context switch (drill-down, page change) | clear | the view underneath has changed; the old menu's target is gone |

**Why**: this can't be written as a general rule — in code both cases look the same, and
a screenshot can't show it either. Only reasoning about "once done with the target, does
the user still want to see the source?" answers it.

### T2 Streaming content keeps its level on blur

See C6. This is the textbook case of "rules serve the UX" (Principle P0): the origin UX of
"dim on blur" is "don't compete for focus", while streaming's UX is "catch updates from
the corner of the eye" — two goals that happen to land on the same panel, so the rule is
extended rather than streaming sacrificed.

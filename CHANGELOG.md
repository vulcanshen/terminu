# Changelog

## v0.1.5 — 2026-09-27

- K8, K2: in the writing state of multi-line text `Tab` is a character (an indent), like `Enter`
  is a newline there (K3); leave the writing state to switch fields. `\t` or spaces is the app's call
  (webu's editor popup)

## v0.1.4 — 2026-09-27

- K10: a PTY needs **at least** one exit key; whether the app keeps other chords of its own in
  the PTY is up to the app, disclosed like the exit key (sshu's grid)

## v0.1.3 — 2026-09-27

- K3: `Enter` always submits — the whole input group or a single field, as the app decides.
  A failed group submit moves focus to the first invalid field and discloses the error; that is
  not `Tab`, which alone moves field by field
- K10: where focus lands after the PTY exit key is up to the app

## v0.1.2 — 2026-09-27

What sshu taught while being brought to tdp.

- **`?` only reads** (K6, M4): it opens the key reference of the frontmost surface — read-only,
  scrollable, nothing to run. The runnable global actions move to a **global operation popup**,
  opened from the Space menu's global region, which is now **always a single row** (M2), even with
  one global action; quitting lives there (K9)
- **PTY** (K10): in a PTY every key, core keys and all app hotkeys, belongs to the subprocess;
  only the exit key is the app's; app actions on a PTY are done after leaving it
- K2: the SSH-grid example is gone; `Tab` in a PTY belongs to the subprocess
- K4, F4: with popups stacked, `Esc` closes only the topmost and the stack below stays as it was
- K11: a mode whose keys overlap navigation moves its key list with the arrow keys only
- D3: the quit confirm is its own popup; "on top" is routing, `closeTop` and drawing alike.
  D4: key reference width follows its longest description

## v0.1.1 — 2026-09-27

What locku and webu taught while being brought to v0.1.0.

- **Modes** (new term, Rules K11): inside a mode `Space` lists the mode's keys, `?` is the mode's help,
  `Esc` leaves, `q` / `Ctrl-C` quit as K9, `Tab` may be suspended but must answer
- M2: a panel's Space menu always carries region headers (the global region is always there)
- D3: the `?` help is on top in routing and drawing; judge a layer by `owns()`, not `isActive()`
- D4: `key reference` rows are not selectable; a label that shows its key is not bracketed again

## v0.1.0 — 2026-09-26

First release of terminu design and the terminu design principle, grown out of VTP
(see [vtp/](vtp/), which also maps every VTP clause to its tdp ID).

- Principle P0–P5; Rules K1–K10, M1–M9, L1–L5, F1–F6, X1–X2, T1–T2, each marked
  `fixed` or `concept`; Family defaults D1–D7
- Three scopes of operation, with `global operation` in both the Space menu and the `?` menu
- `q` joins the core keys; `Ctrl-C` runs the same quit flow
- Minimum supported size 80×40
- The splash is the family easter egg and the one undisclosed thing (Rules S1–S5)
- Colour moves out of the rules into a colour system in the defaults (D2)
- Letter hotkeys and symbol vocabulary are left to each app (P5); D5 records the family's habits

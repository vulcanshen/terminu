# Changelog

## v0.1.11 — 2026-09-28

What filu, locku, webu and sshu taught while aligning to v0.1.8–v0.1.10.

- K3: when the panel is a content area with no item, `Enter` does the most obvious action to the
  whole panel, as the app decides
- F6: a choice made explicitly in a picker may count as the confirmation, as the app decides
- F7: the height fixed at opening may change in two cases only — while **loading** (disclosed by a
  spinning icon after the popup title) and when **the user's own action** changes the row count
- F8: dimming fades every colour, foreground and background, toward the base; never strip colours,
  drop backgrounds or collapse foregrounds to one dim colour (that broke powerline capsules)
- D2: the dim calculation, `c × 0.45 + base × 0.55`, with filu's `dim.go` as the reference

## v0.1.10 — 2026-09-28

- K11: inside a mode `Space` opens nothing — the mode's key list (runnable rows) is gone. `?` is
  the mode's key reference; the mode's keys are pressed directly and disclosed in `?` and the
  footer / hint. Also removes the v0.1.2 note about moving that list with the arrow keys

## v0.1.9 — 2026-09-28

- F1: a finder's `Tab` moves focus between typing and its list, `Esc` closes the whole finder; an
  input may carry a candidate list (arrows move, `j`/`k` stay characters, `Enter` submits the
  chosen one) and is still an input; each step of a multi-step flow is its own popup
- F7: only an input whose submit can fail reserves the error row; the terminal class takes the
  whole available area, no 120 cap
- F8: borders below the top are dimmed too, each in a dimmed version of its own layer colour

## v0.1.8 — 2026-09-28

- F1: popups come in **six classes** — menu, confirm, input, note, toast, terminal — each with fixed
  key meanings; a note may have its own hotkeys and modes; a popup may change class by phase (a
  finder: input, then menu) but is one class at a time
- F7 (new): every popup is `min(terminal width − 2, 120)` wide, centred; its height follows the
  content but is fixed when it opens, scrolling beyond the screen; the toast sits at the bottom;
  an input reserves one error row, where K3's failed submit writes its error
- F8 (new): with a popup open, everything below the topmost — popups and base screen, streaming
  content and warning colours included — is dimmed; a toast does not dim; border layer colours stay
- T2: a popup on top is the exception (F8). D4: the old "key reference as wide as its longest
  description" gives way to F7

## v0.1.7 — 2026-09-28

- M2: the Space menu's global row carries **no region header** — `global operation` over a single
  `Global operation` row only repeated itself; a divider still separates it. The item and panel
  regions keep their headers on a panel's Space menu

## v0.1.6 — 2026-09-27

- K2: in a single input box with a greyed-out suggestion, `Tab` **accepts** it (was: the app *may*);
  in an input group `Tab` only switches fields and the app picks another key for suggestions (e.g. `→`)

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

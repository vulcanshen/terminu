# Changelog

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

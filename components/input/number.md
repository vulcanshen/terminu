# number (a number)

**Language**: English · [繁體中文](number-zh_TW.md)

## Purpose

Entering a number: a port, seconds, a count, a number of columns. For a value with a small range, quicker to pick than
to type, use [`slider`](slider.md).

## Look

- The skeleton follows the one-line input popup in [`input/README`](README.md).
- **The explanation row gives the range** (`Port, 1-65535`), rather than waiting for a mistake to tell.
- **Unit** (only when the app gives one, e.g. seconds): a unit row below the typing row, the unit written as a whole
  word (`seconds`, not `s`), in grey (Overlay0), lined up with the value's first cell, not moving as characters are
  typed. On a form and a panel it shows as `10 seconds`, as in [`input/README`](README.md). A number with no unit has no
  such row.

```
┏━REFRESH━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                  ┃
┃ Seconds between runs while nothing happens, 1-60 ┃
┃                                                  ┃
┃  10█                                            ┃
┃   seconds                                        ┃   ← unit row: Overlay0, lined up with the value's first cell
┃                                                  ┃
┃                                                  ┃   ← error row
┃                                                  ┃
┗━ Enter:save Esc:cancel ━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **Width**: with a known range, the largest number of digits is known, so it follows "content width known when it
  opens" in [`layout/popup`](../layout/popup.md); with a unit row, that row counts towards the widest row too.

**Why**: with the unit in sight while typing, the user knows what is being entered — whether `10` is ten seconds or ten
minutes; written as a whole word, there is no abbreviation to guess.

## Keys

- Editing keys, the grey suggestion and pasting follow [`input/README`](README.md).
- **Only characters the field can use are taken as typed**: digits; `-` only if the field allows negatives, `.` only if
  it allows decimals. Other keys do nothing. Pasting keeps only the characters that are taken.
- No `↑|↓` stepping: a value to be picked uses a slider.

**Why**: a character that can never be right need not get in only to be refused.

## Value

- **The range is checked on `Enter`**, a mistake written in the error row naming the value (as in "What an input is" in [`README`](README.md):
  `Port must be 1-65535`).
- **A field that may be empty**: an empty value is not range-checked and is saved empty; what empty means is written in
  grey by the app on a form and a panel (as in "How a value shows in a form and a panel" in [`README`](README.md), e.g.
  `30 (default)`, `ssh decides`). Where the field cannot be empty, an empty value is handled as an error.

**Why**: the range can only be judged once the whole number is typed, never halfway — typing `22`, the first `2` is
still below the minimum.

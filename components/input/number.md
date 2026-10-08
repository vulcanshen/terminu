# number (a number)

**Language**: English · [繁體中文](number-zh_TW.md)

## Purpose

Entering a number: a port, seconds, a count, a number of columns. For a value with a small range, quicker to pick than
to type, use [`slider`](slider.md).

## Look

- The skeleton follows the one-line input popup in [`input/README`](README.md).
- **The explanation row gives the range** (`Port, 1-65535`), rather than waiting for a mistake to tell.
- **Width**: with a known range, the largest number of digits is known, so it follows "content width known when it
  opens" in [`layout/popup`](../layout/popup.md).

## Keys

- Editing keys, the grey suggestion and pasting follow [`input/README`](README.md).
- **Only characters the field can use are taken as typed**: digits; `-` only if the field allows negatives, `.` only if
  it allows decimals. Other keys do nothing. Pasting keeps only the characters that are taken.
- No `↑`/`↓` stepping: a value to be picked uses a slider.

**Why**: a character that can never be right need not get in only to be refused.

## Value

- **The range is checked on `Enter`**, a mistake written in the error row (`Port must be 1-65535`).

**Why**: the range can only be judged once the whole number is typed, never halfway — typing `22`, the first `2` is
still below the minimum.

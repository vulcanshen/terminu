# number (number)

**Language**: English · [繁體中文](number-zh_TW.md)

## Purpose

Entering a number: a port, seconds, a count, a number of columns.

## Look

- The skeleton follows "Look" in [`text`](text.md) (a one-line input popup).

## Keys

- Editing keys and pasting follow "Keys" and "Pasted line breaks and tabs" in [`text`](text.md).

## Value

Settled by the user, 2026-10-07.

- **Only characters the field can use are taken as typed**: digits; `-` only if negatives are allowed, `.` only if
  decimals are. Other keys do nothing (as sshu's Port does) — a character that can never be right need not get in to be
  refused later. Pasting follows text's rule: only what is taken stays.
- **The range is checked on `Enter`**, the error in the error row (`Port must be 1-65535`): a range can only be judged
  once the number is complete, not halfway (typing `22`, the first `2` is below the minimum).
- **The explanation row gives the range** (`Port, 1-65535`), rather than waiting for a mistake.
- Today: locku's number settings take any character and check on `Enter`; they change to filtering as typed.
- No `↑`/`↓` stepping: no family app has it, and small ranges to pick from use a slider or a list.

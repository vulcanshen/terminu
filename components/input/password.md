# password (masked input)

**Language**: English · [繁體中文](password-zh_TW.md)

## Purpose

Entering a value that is not shown: a password, a PIN, a passphrase.

## Look

- The skeleton follows the one-line input popup in [`input/README`](README.md).
- **Two options for the mask; the app picks by use**:

  | Option | Look | Suits |
  |---|---|---|
  | **Plain** | one `•` per character, left-aligned (sshu, webu) | passwords in forms, ordinary password boxes |
  | **Unlock** | one `●` per character with a space between, centred and growing both ways (locku) | unlocking a screen, PINs, verification codes — the whole box exists to enter this one value (like macOS verification codes) |

  The mask takes the value's colour (Lavender). The 8 grey dots of "a password is already set" use the same option's
  glyph. When it does not fit, "When the value is longer than the box" in the README applies (the cursor's end in
  sight).
- **The unlock style's cursor**: where the next `●` will appear (a space after the last dot); once the last digit is
  typed it rests on the last dot, with no extra cell. Centring counts the cursor: n digits typed (not full) take
  2n + 1 cells, all N digits 2N − 1 cells.

```
┃                 ● ● ● █                 ┃   ← 3 digits typed: the cursor where the next dot will appear
┃         ● ● ● ● ● ● ● ● ● ● ● █         ┃   ← all 12 typed: the cursor on the last dot (Lavender background, a Base `●`), no extra cell
```

- **The unlock style has no `nf-fa-angle_right`**: the whole box exists to enter this one value, and the centred dots
  say at once where to type; the angle marks the typing row in a box with an explanation.
- **Width**: with a length limit (e.g. a PIN), the width is set by the content (width in
  [`layout/popup`](../layout/popup.md)).

## States

**When a password is already set**:

```
┃  █•••••••                           ┃   ← an old password (plain): always 8 grey dots (Overlay0), the cursor on the first, not its real length
```

```
┃             █ ● ● ● ● ● ● ●             ┃   ← an old password (unlock): 8 grey dots a space apart, centred, the cursor on the first
```

- The box opens empty; with an old password, 8 grey dots are always drawn, saying "there is a password now". They start
  at the cursor's cell: the cursor sits on the first (Lavender background, a Base dot), the other 7 in Overlay0 — as the
  grey suggestion in [`input/README`](README.md). In the unlock look the 8 are a space apart and centred (15 cells).
  They do not follow the real length, so as not to give the length away.
- With nothing typed, `Enter` and `Esc` both keep the old password.
- Typing straight away: it is replaced with a new password, and the dots hide.
- No `Tab`: an old password that cannot be seen cannot be edited.
- Whether a new password is typed twice to confirm (e.g. locku's PIN setting, `new PIN` → `confirm PIN`) is the app's
  flow.

The grey dots are not a grey suggestion: there is no text behind them to take in, and the hint has no `Tab`; all they
share with a suggestion is "`Enter` with nothing typed keeps the old one".

## Keys

- Pasting follows "Pasted control characters" in [`input/README`](README.md) (masked values stay masked).
- **`Backspace` clears everything at once, not one character at a time**: with something typed it clears all of it,
  back to the dots (the old password kept); on an empty box it clears the old password, the dots go, and `Enter` then
  saves no password. The hint adds `Backspace:clear`.
- **Characters always go at the end**; `←|→`, `Home|End` and `Delete` do nothing.

**Why**: with the characters unseen, moving the cursor means nothing; a mistake cannot be located either, so clearing
it all with `Backspace` and typing again is fastest.

## Value

Leading and trailing whitespace is not trimmed (whitespace may be part of a password). In a form or a panel: a set password is
always 8 `•` in Text (the colour of values in a form or a panel), never giving away the length; not set follows the rule for empty values (e.g.
`not set`).

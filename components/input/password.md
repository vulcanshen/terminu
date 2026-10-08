# password (masked input)

**Language**: English · [繁體中文](password-zh_TW.md)

## Purpose

Entering a value that is not shown: a password, a PIN, a passphrase.

## Look

- The skeleton follows "Look" in [`text`](text.md) (a one-line input popup).
- **Two options for the mask; the app picks by use** (settled by the user, 2026-10-07):

  | Option | Look | Suits |
  |---|---|---|
  | **Plain** | one `•` per character, left-aligned (sshu, webu) | passwords in forms, ordinary password boxes |
  | **Unlock** | one `●` per character with a space between, centred and growing both ways (locku) | unlocking a screen, PINs, verification codes — a box that exists for this one value (the user: like macOS verification codes) |

  The mask takes the value's colour (Lavender). The 8 grey dots of "a password is set" use the same option's glyph. When it
  does not fit, text's rule for long values applies (the cursor's end in sight).

## States

**When a password is already set** (settled by the user, 2026-10-07):

```
│ ••••••••                             │   ← a password is set: always 8 grey dots (Overlay0), not its length
```

- The box opens empty; with a password set, 8 grey dots follow the cursor, saying "there is a password". They never follow
  the real length, which would give it away.
- With nothing typed, `Enter` and `Esc` both keep the old password.
- Typing replaces it with a new one and hides the dots.
- No `Tab`: an old password nobody can see cannot be edited.
- Whether a new password is typed twice (locku's PIN, `new PIN` → `confirm PIN`) is the app's flow, not set here.

## Keys

- Pasting follows "Pasted line breaks and tabs" in [`text`](text.md) (masked values stay masked).
- **`Backspace` clears everything at once, not one character at a time** (the user, 2026-10-07): with something typed it
  clears all of it, back to the dots (the old password kept); on an empty box it clears the old password, the dots go,
  and `Enter` then saves no password. The hint adds `Backspace:clear`.
- **Characters always go at the end**; `←`/`→`, `Home`/`End` and `Delete` do nothing: with nothing to see and `Backspace`
  clearing all, moving the cursor means nothing (inferred from the user's `Backspace`).

## Shown in a form or a panel

- Set: always 8 `•` in the value's colour, never the length (webu's page draws the real length today, up to 12, and
  changes). Not set: text's rule for empty values, grey text saying what empty means (`not set`).

# text (single-line text)

**Language**: English · [繁體中文](text-zh_TW.md)

## Purpose

Entering one line of text: a name, a URL, a command, a path. The skeleton of a one-line input popup (explanation row, value, error row) is set here and shared by password and number.

## Look

The skeleton of a one-line input popup, shared by text, password and number (settled by the user, 2026-10-07).

```
╭─ Rename ─────────────────────────────────╮
│                                          │
│ New name for assets                      │   ← explanation: one sentence, Overlay0
│                                          │
│ assets█                                  │   ← value: Lavender; cursor Lavender background, Base text
│                                          │
│                                          │   ← error row (layout/popup)
│                                          │
╰─ Enter:rename Esc:cancel ────────────────╯
```

- **The explanation row**: one sentence saying what to enter (`New name for assets`), in Overlay0, with a blank row
  between it and the value. What is being changed goes into that sentence.
- **The value**: Lavender — in [`color`](../color.md) Lavender is "what is being edited", and in an input popup that is the
  value. The cursor is one cell, Lavender background with Base text.
- **The hint**: `Enter:<verb> Esc:cancel`, the verb saying what pressing it does (rename, create, save).
- Today: locku, sshu and webu look like this; filu changes (no Peach `❯` and no underline below the input row, the value
  Lavender instead of the default foreground, and the explanation a sentence instead of the renamed item's icon and name).
- The three points left over from forms for the input files: "stacked also suits a single field whose label is a
  sentence" is exactly this (the explanation above, the value below); "a single field's label is always Lavender bold"
  and "a focused value's text is not Lavender" no longer apply — they were set when values were typed into the form;
  now Lavender is only the value's, and the explanation is Overlay0.

**When the value is longer than the box** (settled by the user, 2026-10-07): the box shows the stretch around the
cursor, with `…` on the side that is cut.

```
│ …/sideproj/terminu/components/layout█ │   ← typing: the cursor at the end, the start cut
│ █/Users/vulcan/Documents/sideproj/te… │   ← after Home: the cursor at the start, the end cut
```

- The cursor is always in sight; moving scrolls by just enough, never pinning the cursor to the middle (the same scrolling
  as a popup whose content does not fit).
- Width is display width (a CJK character is 2 cells; sshu counts characters today and changes). A character is never
  split, a red `\n` neither.
- Today: webu keeps the end; sshu keeps the start, so the end being typed is out of sight (a bug the survey found).

## States

**Changing an existing value: the old value is a suggestion, not prefilled** (settled by the user, 2026-10-07).

```
│ report-2025.pdf                      │   ← the box is empty; the old value after the cursor is grey (Overlay0)
```

- The box opens empty, the old value shown in grey (Overlay0) after the cursor.
- `Tab` takes the old value into the box, the cursor at its end, to be changed with `←`/`→` (K2: a single input with a
  grey suggestion accepts it on `Tab`).
- Typing starts a new value and hides the grey text; deleting all that was typed brings it back.
- `Backspace` on an empty value means "not this value": the grey text goes, and `Enter` then saves the value empty (where
  the field cannot be empty, as an error).
- `Enter` with nothing touched changes nothing and closes.
- With grey text the hint adds `Tab:edit Backspace:clear` (e.g. `Enter:rename Tab:edit Backspace:clear Esc:cancel`).
- Why: without `Ctrl-U`, replacing a long prefilled value means holding `Backspace` to the start; a suggestion makes
  "type anew" need no deleting, "small change" one `Tab` more, and "no change" a plain `Enter`.
- Today: locku's config file path and webu's Location work this way; filu's, sshu's and webu's Rename and locku's profile
  name are prefilled and change.

**No placeholder in an input popup** (settled by the user, 2026-10-07): what to enter is said by the explanation row, and
grey text is kept for suggestions. Two kinds of grey text that look alike, one taken in by `Tab` and one not, could not
be told apart.

## Keys

Settled by the user, 2026-10-07. The input state (K8): letters, `Space`, `?` and `q` are characters.

| Key | Does |
|---|---|
| Letters, `Space` | insert at the cursor |
| `←` / `→` | move the cursor one character left / right |
| `Home` / `End` | move the cursor to the start / the end |
| `Backspace` / `Delete` | delete the character before / under the cursor |

- **A character is what looks like one**: a CJK character, an emoji, a base letter with its combining marks; a pasted
  line break or tab is one each (see "Pasted line breaks and tabs").
- **No shell deletion shortcuts** (the user: no `Ctrl-U`, no `Ctrl-W`). locku's and webu's `Ctrl-U` clearing the value
  goes. Other `Ctrl-` and `Alt-` combinations do nothing in an input and type nothing (kbu and webu type `b` on `Alt-b`
  today).
- Today only sshu moves the cursor; filu, kbu, locku and webu only type and delete at the end, and change.

## Pasted line breaks and tabs

Settled before the 2026-10-06 releases and already done in all five apps (the user rejected "turn them into spaces": they
must show); the apps added a few points while fixing.

- **Scope**: one-line values (not the textarea). Digits-only fields keep their own filter.
- **Only pasted text counts**: pressed `Tab`, `Enter` and `Ctrl-J` keep their roles.
- **Line breaks and tabs stay in the value**, drawn as a red `\n` / `\t` (Red `#f38ba8`, 2 cells, never cut); in a row
  drawn grey as a whole (a filter row not being typed in, a suggestion) they are grey too. `\r\n` is one line break,
  stored as is or as `\n`. Other control characters (C0, DEL, C1) are dropped.
- **`Backspace` removes a whole `\n` or `\t`.**
- **Masked values stay masked** (password).
- **Prefilled values go through the same filter**: prefilled means every place text enters that the user did not type
  (the old name, a value from a file or another program, a value filled back from a menu, a default from the start
  directory, a suggestion…), not a list (sshu's feedback).
- **A value that is used (submitted, saved, run, handed to another program)** refuses it on `Enter`, the error row naming
  the field (e.g. `Name can't have line breaks or tabs`); an input that could not fail before gets an error row (F7).
  **Check before any trim** (filu: `Icon\r` + `Enter` was once renamed to `Icon`).
- **Search and filter rows only draw it.**

## Value

- **Leading and trailing spaces are trimmed on submit**, except in a password; the line break and tab check comes before
  the trim (see the paste rule above). sshu, locku and webu do this today (written down as it is, 2026-10-07).

## Shown in a form or a panel

- **An empty value** (settled by the user, 2026-10-07, the same for every kind of input): grey text (Overlay0) saying what
  empty means, written by the app (`not set`, `ssh decides`, `none`). A blank does not tell unset from an empty string from
  not loaded yet. locku's `not set` is Yellow today and turns grey (Yellow means selection and modes, [`color`](../color.md)).
  No text teaching keys (sshu's `enter to browse ~/.ssh`): the hint says `Enter:browse`.

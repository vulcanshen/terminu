# input (shared rules)

**Language**: English · [繁體中文](README-zh_TW.md)

Rules shared by every input popup; each input file writes only what differs from here.

## What an input is

A kind of popup: a value is entered or chosen, and written back once confirmed; one popup, one value (Rules F1).

- **The typing row is in the input state** (Rules K8): letters, `Space`, `?` and `q` are all characters. The parts
  where nothing is typed (a select's list, a picker) are not in the input state, and core keys follow Rules K1: `?`
  opens the key reference, `q` / `Ctrl-C` start the quit flow, `Space` does nothing (K5), `hjkl` move (K12).
- **`Enter`** (Rules K3): with the focus on the value, it confirms the value — written back, the popup closed. An invalid
  value is not written back: the error goes in the error row and the popup stays open. A value the same as when it
  opened is not written back; the popup just closes.
- **`Esc`**: closes, the value unchanged.
- **Opened from a form**: after confirming, the focus stays on the same field of the form (Rules K3).

## The skeleton of a one-line input popup

Shared by text, password and number.

```
╭─ Rename ─────────────────────────────────╮
│                                          │
│ New name for assets                      │   ← explanation row: one sentence, Overlay0
│                                          │
│ assets█                                  │   ← value: Lavender; cursor Lavender background, Base text
│                                          │
│                                          │   ← error row (layout/popup)
│                                          │
╰─ Enter:rename Esc:cancel ────────────────╯
```

- **The explanation row**: one sentence saying what to enter (`New name for assets`), in Overlay0, with a blank row
  between it and the value. What is being changed goes into that sentence.
- **The value**: Lavender — in [`color`](../color.md) Lavender is "what is being edited", and in an input popup what is
  being edited is this value. The cursor is one cell, Lavender background with Base text.
- **The error row**: as in [`layout/popup`](../layout/popup.md).
- **The hint**: `Enter:<verb> Esc:cancel`, the verb saying what pressing it does (rename, create, save). This kind of
  popup has only a typing row, where `?` is a character, so the hint must list every action (Rules M3).
- **Width**: a freely typed value has no known width and takes the maximum of Rules F7; a value with a length limit
  (e.g. a PIN, a number with a known range) has a known width and follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).

## When the value is longer than the box

The box shows the stretch around the cursor, with `…` on the side that is cut.

```
│ …/sideproj/terminu/components/layout█ │   ← typing: the cursor at the end, the start cut
│ █/Users/vulcan/Documents/sideproj/te… │   ← after Home: the cursor at the start, the end cut
```

- The cursor is always in sight; moving scrolls by just enough, never pinning the cursor to the middle (the same
  scrolling as a popup whose content does not fit).
- Width is display width (a CJK character is 2 cells). A character is never split in two, nor is a red `\n`.

## Editing keys

On the typing row:

| Key | Does |
|---|---|
| Characters, `Space` | insert at the cursor |
| `←` / `→` | move the cursor one character left / right |
| `Home` / `End` | move the cursor to the start / the end |
| `Backspace` / `Delete` | delete the character before / under the cursor |

- **A character is what looks like one**: a CJK character, an emoji, a combining mark together with the character
  before it each count as one; a pasted line break or tab is one each.
- **No shell deletion shortcuts**: `Ctrl-U` and `Ctrl-W` are not taken. Other `Ctrl-` and `Alt-` combinations do
  nothing on the typing row and type nothing.

**Why**: the editing keys are only those printed on the keycaps — seen, they are known. `Ctrl-U` and `Ctrl-W` behave
differently in different shells, so taking them would mean remembering "which kind is this one"; replacing a long value
is done with the grey suggestion below (typing a new value needs no deleting first).

## Changing an existing value: the old value is a grey suggestion

```
│ report-2025.pdf                      │   ← the box is empty; the old value after the cursor is grey (Overlay0)
```

- The box opens empty, the old value shown in grey (Overlay0) after the cursor.
- `Tab`: takes the old value into the box, the cursor at its end, to be changed with `←`/`→` (Rules K2).
- Typing straight away: a new value is typed and the grey text hides; deleting all that was typed brings it back.
- `Backspace` on an empty value: not this value; the grey text goes, and `Enter` then saves the value empty (where the
  field cannot be empty, it is handled as an error).
- `Enter` with nothing touched: no change; it closes.
- With grey text the hint adds `Tab:edit Backspace:clear` (e.g. `Enter:rename Tab:edit Backspace:clear Esc:cancel`).
- A grey suggestion has only this one source: the old value. With no suggestion, `Tab` does nothing.

**Why**: replacing a long prefilled value whole means holding `Backspace` down to the start; a suggestion makes "type
anew" need no deleting, "small change" one `Tab` more, and "no change" a plain `Enter`.

## No placeholder

An input popup has no placeholder: what to enter is said by the explanation row; grey text is kept for suggestions only.

**Why**: two kinds of grey text that look alike, one taken in by `Tab` and one not, could not be told apart.

## Pasted line breaks and tabs

- **Scope**: one-line values (not the textarea). Digits-only fields keep their own filter.
- **Only pasted text counts**: pressed `Tab`, `Enter` and `Ctrl-J` keep their own roles.
- **Line breaks and tabs stay in the value**, drawn as a red `\n` / `\t` (Red, 2 cells, never split); in a row drawn
  grey as a whole (a typing row without the focus, a suggestion) they are grey too. `\r\n` counts as one line break,
  stored as is or as `\n`, either way. Other control characters (C0, DEL, C1) are dropped.
- **`Backspace` deletes a whole `\n` or `\t` at once.**
- **Masked values stay masked** (password).
- **Values the user did not type go through the same filter**: the original name, a value from a file or another
  program, a value filled back from a list, a default from the start directory, a suggestion… not listed one by one.
- **A value that is used (submitted, saved, run, handed to another program)**: refused on `Enter`, the error row giving
  the reason and naming the field (e.g. `Name can't have line breaks or tabs`). **Check before trimming leading and
  trailing spaces**: trimmed, `Icon\r` becomes `Icon`, so trimming first leaves nothing to catch.
- **Search and filter typing rows only draw them, never refuse.**

**Why**: turning them into spaces would quietly change what the user pasted; drawn plainly, they are seen, and the user
decides whether to delete them.

## Value

- **A one-line value has leading and trailing spaces trimmed when confirmed**, except a password; the line break and tab
  check comes before the trim (see above).

## How a value shows in a form and a panel

- **Colour**: Text.
- **An empty value**: grey text (Overlay0) saying what empty means, written by the app (`not set`, `ssh decides`,
  `none`). A blank does not tell unset from an empty string from not loaded yet. No text teaching keys (e.g. `enter to
  browse ~/.ssh`): the hint says `Enter:edit`.
- **Too long**: cut from the end, with `…`; a path is cut from the start (`…/.ssh/id_ed25519`).
- **Each kind of input**:

  | Input | Shown as |
  |---|---|
  | text, number | the value itself |
  | password | set: always 8 `•`; not set: as an empty value |
  | textarea | the first line, with `…` when more follows |
  | select | the chosen option's text |
  | checkbox popup (several) | the chosen items joined with `, `, with `…` when too long |
  | radio, checkbox (drawn in the form) | the options themselves ([`radio`](radio.md), [`checkbox`](checkbox.md)) |
  | slider | a track and the number ([`slider`](slider.md)) |
  | datetime picker | the formatted date (and time), in the app's format (`2026-10-15`, `2026-10-15 10:05`) |
  | color picker | a small swatch and the hex (`███ #2A2A3C`) |
  | file-picker | the path, the home directory written as `~` |

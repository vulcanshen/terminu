# input (shared rules)

**Language**: English · [繁體中文](README-zh_TW.md)

Rules shared by every input popup; each input file writes only what differs from here.

## What an input is

A kind of popup: a value is entered or chosen, and written back once confirmed; one popup, one value (Rules F1).

- **The typing row is in the input state** (Rules K8): letters, `Space`, `?` and `q` are all characters. The parts
  where nothing is typed (a select's list, a picker) are not in the input state, and core keys follow Rules K1: `?`
  opens the key reference, `q|Ctrl-C` start the quit flow, `Space` does nothing (K5), `hjkl` move (K12).
- **`Enter`** (Rules K3): with the focus on the value, it confirms the value — written back, the popup closed. An invalid
  value is not written back: the error goes in the error row and the popup stays open. A value the same as when it
  opened is not written back; the popup just closes — but only a value that was valid when it opened: a field that
  opened empty and cannot be empty is still refused when `Enter` is pressed with nothing typed, the error going in the
  error row (with a suggested value, `Enter` takes it; see "A new value: the suggested value" below).
- **An error names the value by its name**: opened from a form's field, that field's name; an input opened on its own
  has a title saying what the popup does (`RENAME`, `SAVE AS` in [`layout/popup`](../layout/popup.md)), so the app gives
  the value's name besides (`Name`). E.g. on `SAVE AS`, `Name can't have control characters`, not `Save as can't have
  control characters` — the title says what is being done, not what the value is called.
- **`Esc`**: closes, the value unchanged.
- **Opened from a form**: after confirming, the focus stays on the same field of the form (Rules K3).
- **An input popup with a button** (e.g. the colour picker's `Choose`): the action area works as in
  [`dialog/form`](../dialog/form.md) — `Tab|Shift-Tab` go back and forth between the field area and the action area,
  coming back to the item they left; the hint says `Tab:actions` on a field and `Tab:fields` on a button (Rules K2).

## The skeleton of a one-line input popup

Shared by text, password and number.

```
┏━RENAME━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                          ┃
┃ New name for assets                      ┃   ← explanation row: one sentence, Overlay0
┃                                          ┃
┃  assets█                                ┃   ← typing row: `nf-fa-angle_right` in the layer colour, a space, then the value: Lavender; cursor Lavender background, Base text
┃                                          ┃
┃                                          ┃   ← error row (layout/popup)
┃                                          ┃
┗━ Enter:rename Esc:cancel ━━━━━━━━━━━━━━━━┛
```

- **The explanation row**: one sentence saying what to enter (`New name for assets`), in Overlay0, with a blank row
  between it and the value. What is being changed goes into that sentence.
- **The typing row**: it starts with `nf-fa-angle_right` (U+F105), one cell from the border, then a space before the
  value, as on a [`finder`](finder.md)'s typing row. Its colour follows the finder: the layer colour while typing — and a
  one-line input popup is always typing, so it is always the layer colour. The row the cursor waits on reads at once as
  the place to type.
- **The value**: Lavender — in [`color`](../color.md) Lavender is "what is being edited", and in an input popup what is
  being edited is this value. The cursor is one cell, Lavender background with Base text; resting on a control
  character, the whole control character is drawn with a Red background and Base text (see "Pasted control characters"
  below).
- **The error row**: as in [`layout/popup`](../layout/popup.md).
- **The hint**: `Enter:<verb> Esc:cancel`, the verb saying what pressing it does (rename, create, save). This kind of
  popup has only a typing row, where `?` is a character, so the hint must list every action (Rules M3).
- **Width**: a freely typed value has no known width and takes the maximum of Rules F7; a value with a length limit
  (e.g. a PIN, a number with a known range) has a known width and follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).
- **Two places that differ from the skeleton**: a password's unlock style has no explanation row, its title saying what
  to enter ([`password`](password.md)); a number with a unit has a unit row below the typing row
  ([`number`](number.md)).

## When the value is longer than the box

The box shows the stretch around the cursor, with `…` on the side that is cut.

```
┃  …ideproj/terminu/components/layout█ ┃   ← typing: the cursor at the end, the start cut
┃  █/Users/vulcan/Documents/sideproj/… ┃   ← after Home: the cursor at the start, the end cut
```

- The cursor is always in sight; moving scrolls by just enough, never pinning the cursor to the middle (the same
  scrolling as a popup whose content does not fit).
- Width is display width (a CJK character is 2 cells). A character is never split in two, nor is a red `\n` or `\x1b`.

## Editing keys

On the typing row:

| Key | Does |
|---|---|
| Characters, `Space` | insert at the cursor |
| `←\|→` | move the cursor one character left, right |
| `Home\|End` | move the cursor to the start, the end |
| `Backspace\|Delete` | delete the character before, under the cursor |

- **A character is what looks like one**: a CJK character, an emoji, a combining mark together with the character
  before it each count as one; a pasted control character is one each (`\n`, `\x1b`).
- **No shell deletion shortcuts**: `Ctrl-U` and `Ctrl-W` are not taken. Other `Ctrl-` and `Alt-` combinations do
  nothing on the typing row and type nothing.

**Why**: the editing keys are only those printed on the keycaps — seen, they are known. `Ctrl-U` and `Ctrl-W` behave
differently in different shells, so taking them would mean remembering "which kind is this one"; replacing a long value
is done with the grey suggestion below (typing a new value needs no deleting first).

## Changing an existing value: the old value is a grey suggestion

```
┃  █eport-2025.pdf                    ┃   ← the box is empty; the old value is grey (Overlay0), the cursor on its first character (`r`)
```

- **Single-line inputs only** (text, number; a password shows grey dots for its old value, see
  [`password`](password.md)); a textarea opens with the old value already in ([`textarea`](textarea.md)).
- The box opens empty, the old value shown in grey (Overlay0) starting at the cursor's cell: the cursor sits on its first
  character (as any cursor, Lavender background and a Base character; a Red background when that first character is a
  control character, as in "Pasted control characters"), the grey text after it — like a shell's autosuggestion.
- `Tab`: takes the old value into the box, the cursor at its end, to be changed with `←|→` (Rules K2).
- Typing straight away: a new value is typed and the grey text hides; deleting all that was typed brings it back.
- `Backspace` on an empty value: not this value; the grey text goes, and `Enter` then saves the value empty (where the
  field cannot be empty, it is handled as an error).
- `Enter` with nothing touched: no change; it closes.
- With grey text the hint adds `Tab:edit Backspace:clear` (e.g. `Enter:rename Tab:edit Backspace:clear Esc:cancel`).
- A grey suggestion has two sources: the old value, and, with no old value, the app's suggested value (next section);
  the two never show together. With no suggestion, `Tab` does nothing.

**Why**: replacing a long prefilled value whole means holding `Backspace` down to the start; a suggestion makes "type
anew" need no deleting, "small change" one `Tab` more, and "no change" a plain `Enter`. That is the case of single-line
values (file names, host names); a change to several lines of text is mostly a sentence added or a few words changed,
and in a textarea `Tab` indents, so it could not take a suggestion anyway.

## A new value: the suggested value

```
┃  █ssets.zip                         ┃   ← no old value; the value the app suggests is grey (Overlay0), the cursor on its first character (`a`)
```

- **With no old value and a sensible default from the app** (e.g. the file name `assets.zip` to pack into, the name of
  something new), it is shown as a grey suggestion, called the suggested value. Single-line inputs only (text, number),
  as with the old value.
- Its look, `Tab`, typing straight away, `Backspace` and the hint are all as for the old value's suggestion.
- **The only difference is `Enter` with nothing touched**: for the old value it means "no change" and closes; for the
  suggested value it means "use this value", handled as confirming a value — written back and checked as usual.
- A field that cannot be empty but has a suggested value takes the suggestion on `Enter` with nothing typed, so no
  "can't be empty" error shows; only after `Backspace` clears the grey text does `Enter` go to the error.

**Why**: creating something new, there is mostly a sensible name to use as it is; the suggested value makes "as
suggested" a plain `Enter`, "small change" one `Tab` more, and "my own" just typing. `Enter` with the old value untouched
does nothing; `Enter` with the suggested value untouched is the user accepting that value — not writing it back would
leave `Enter` doing nothing at all.

## No placeholder

An input popup has no placeholder: what to enter is said by the explanation row; grey text is kept for suggestions only.
The `nf-fa-angle_right` before a typing row (a one-line input, a finder, a panel filter; [`finder`](finder.md)) is a
glyph, not a placeholder: it is not text, `Tab` never takes it in, and it stays while typing.

**Why**: two kinds of grey text that look alike, one taken in by `Tab` and one not, could not be told apart.

## Pasted control characters

- **Scope**: one-line values. For the multi-line textarea see [`textarea`](textarea.md): a line break (a lone `\r`
  too) is a real line break, and other control characters are handled as here. Digits-only fields keep their own filter.
- **Only pasted text counts**: pressed `Tab`, `Enter` and `Ctrl-J` keep their own roles.
- **No control character is dropped; each is drawn as it is, in red** (Red, never split): `\r`, `\n` and `\t` by name
  (2 cells), every other C0, DEL and C1 as `\xNN` (4 cells, e.g. `\x1b`, `\x7f`, `\x85`). `\r\n` is drawn as it is
  too, as the two `\r\n`. In a row drawn grey as a whole (a typing row without the focus, a suggestion) they are grey too.
- **The cursor resting on a control character**: the whole control character (the four cells of `\x1b`, the two of
  `\r`) is drawn with a Red background and Base text; other characters keep the Lavender background. It shows both that
  the cursor is here and that it rests on a control character. The same when the first character of a grey suggestion
  is a control character.
- **`Backspace` deletes a whole one at once** (`\n`, `\x1b`…).
- **Masked values stay masked** (password).
- **Values the user did not type go through the same filter**: the original name, a value from a file or another
  program, a value filled back from a list, a default from the start directory, a suggestion… not listed one by one.
- **A value that is used (submitted, saved, run, handed to another program)**: refused on `Enter`, the error row giving
  the reason and naming the value (as in "What an input is"; e.g. `Name can't have control characters`). **Check before trimming leading and
  trailing whitespace**: trimmed, `Icon\r` becomes `Icon`, so trimming first leaves nothing to catch.
- **Search and filter typing rows only draw them, never refuse.**

**Why**: turning them into spaces or dropping them would quietly change what the user pasted; drawn as they are, what
the user sees is what was really pasted, and the user decides whether to delete them. Dropping control characters does
not even clean up: text copied in colour from a terminal, with `\x1b` dropped, leaves `[31m` behind. Under the cursor
they turn to a red background: red text on Lavender is too faint, and a plain cursor would hide that it is a control
character.

## Value

- **A one-line value has leading and trailing whitespace trimmed when confirmed**: every Unicode whitespace character
  (the ordinary space, the ideographic space U+3000, NBSP…), not just one kind of space; not for a password. The control
  character check comes before the trim (see above). Invisible whitespace is the hardest to track down: a host name
  copied from a web page with an NBSP at its end, or an ideographic space typed after a value, looks exactly the same on
  screen but does not work.

## How a value shows in a form and a panel

- **Colour**: Text.
- **An empty value**: grey text (Overlay0) saying what empty means, written by the app (`not set`, `ssh decides`,
  `none`). A blank does not tell unset from an empty string from not loaded yet. No text teaching keys (e.g. `enter to
  browse ~/.ssh`): the hint says `Enter:edit`.
- **Too long**: cut from the end, with `…`; a path is cut from the start (`…/.ssh/id_ed25519`).
- **Control characters**: as on the typing row, drawn as they are as red escapes (`\n`, `\x1b`; see "Pasted control
  characters" above), never dropped or turned into spaces.
- **Each kind of input**:

  | Input | Shown as |
  |---|---|
  | text | the value itself |
  | number | the value itself; with a unit, a space and the unit as a whole word (`10 seconds`, [`number`](number.md)) |
  | password | set: always 8 `•`; not set: as an empty value |
  | textarea | the first line, with `…` when more follows |
  | select | the chosen option's text |
  | checkbox popup (several) | the chosen items joined with `, `, with `…` when too long |
  | reorder | the items in their current order joined with `, `, with `…` when too long |
  | radio, checkbox (drawn in the form) | the options themselves ([`radio`](radio.md), [`checkbox`](checkbox.md)) |
  | slider | a track and the number ([`slider`](slider.md)) |
  | datetime picker | the formatted date (and time), in the app's format (`2026-10-15`, `2026-10-15 10:05`) |
  | color picker | a swatch 3 cells wide (`███`), a space, and the hex (`███ #2A2A3C`, always upper case, [`color-picker`](color-picker.md)) |
  | file-picker | the path, the home directory written as `~` |

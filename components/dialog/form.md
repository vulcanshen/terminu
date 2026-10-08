# form: Forms

**Language**: English · [繁體中文](form-zh_TW.md)

A form is a dialog: several values filled in and submitted together (sshu's Host form, webu's Sign in and Add bookmark).
The frame itself follows [`layout/popup`](../layout/popup.md).

Nothing is typed into a form itself. A field that takes typing (text, password…) or has more options than fit (select,
date, colour, file), opens its input popup on `Enter` ([`input/`](../README.md#input)); the value is entered there and,
once confirmed, written back to the form. A field with few options (radio, checkbox) has its options drawn in the form and
is chosen in place.

**Why** (the user, 2026-10-07): some inputs do not fit in a row of a form and must open a popup of their own — a colour
picker, a date picker, choosing from a list (sshu's Auth set to credential opens a menu on `Enter`). If the other fields
were typed into in place, one form would be operated in two ways. With every value entered in an input popup, every field
works the same: `Tab` to move, `Enter` to edit, `Enter` to confirm. The cost is one more `Enter` per field (the one that
opens it).

Later the same day, with hjkl added, radio and checkbox fields came to be chosen in the form itself. The line is "a popup
only for typing or for options that do not fit"; `Enter` always does the most direct thing to the focused item (K3) —
on Name it opens the popup to type in, on an option it chooses it, on a switch it flips it.

## Title

Says what this form does (`New host`, `Add bookmark`). Not the type (`number`, `path`, `email`): the type belongs to a
field, and with more than one field it would not fit in one title anyway; when the user needs to know it, the field marks
it, as each input file describes.

## How a field is arranged

Each field takes one of two arrangements.

| Arrangement | Look | Suits |
|---|---|---|
| **Stacked** | the label on one row, the value on the next, the value using the full inner width | long values (URLs, paths, commands) |
| **Side by side** | one row: the label in a left column, the value to its right | short values; forms with many fields |

- A form may mix the two, one field after another. All stacked or all side by side is fine as well.
- No blank row between fields, and none between a stacked label and its value. They are told apart by colour (a label
  and its value never share a colour, see "Focus and moving between fields") and by the input marker icon in front of
  the value (see each input file).
- Labels, values and errors share the same left edge.
- The label column of side-by-side fields is as wide as the longest label **among the side-by-side fields** (stacked
  labels do not count), with space between the label column and the values.

```
╭─ New profile ──────────────────────────────────╮
│                                                │
│ Name        clock3                             │   ← side by side
│ Timeout     30                                 │   ← side by side
│ Command                                        │   ← stacked
│ tmux new-session -A -s main                    │
│ Layout      row                                │   ← side by side
│                                                │
╰─ Enter:edit Ctrl-S:save Esc:cancel ────────────╯
```

(The drawings in this section and the next show the fields only; for the action row see "Submit".)

## Focus and moving between fields

In a form the focus moves by **item**: a field that takes typing or opens a popup is one item, each option of a radio or
checkbox field is an item of its own, and a button is one item; the error row, while it holds an error, is an item too
(just before the button; see the error row in [`layout/popup`](../layout/popup.md)).

- **`j`/`l`/`↓`/`→` to the next item, `h`/`k`/`↑`/`←` to the previous one** (the user, 2026-10-07). Whether options run
  across or down does not matter: on is on and back is back, hjkl being the arrow keys (a form is a one-dimensional list, see rules K12). Going on from the last option of a
  field enters the next field; going back from the first option returns to the previous one. A form is not in the input
  state (K8), so the letters are free; a user who thinks they can type straight in only moves around, and submits nothing.
- **`Tab`/`Shift-Tab` jump one field at a time** (K2); the error row while it holds an error, and the action row, are
  one stop each.
- **Where `Tab`/`Shift-Tab` land in a radio or checkbox field** (the user, 2026-10-07): a radio field on its chosen option,
  or the first one if none is chosen; a checkbox field on its first option. `Shift-Tab` coming from below lands the same
  way: `Tab` means "jump to that field", and where it lands does not depend on the direction. On a radio field the focus
  lands on the current value: `j`/`k` to a neighbour to change it, or `Tab` straight on to leave it, with nothing chosen
  by mistake; a checkbox field has no "current one", each option being ticked on its own, so starting from the top is the
  easiest to predict. (`j`/`k`, moving one item at a time, enter a field at the nearest option.)
- **Wrapping at both ends** (the user, 2026-10-07): the same for `Tab` and `j`/`k`. The button is the last item: going on
  from it returns to the first field, and going back from the first field reaches the button in one step — making up for
  the action row sitting at the bottom. This matches K2 (`Tab` returns to the first after the last) and [`menu`](menu.md) (`j/k`
  wrap at both ends).
- **Disabled fields and options are skipped** (the user, 2026-10-07): neither `Tab` nor `j`/`k` stops on them; they are
  still drawn in place (see the colour of the label below). Disabled means "cannot be changed now", and `Enter` on one
  would have nothing to do.
- **On opening** (the user, 2026-10-07): the focus is on the first item it can stop on (disabled ones skipped), for a new
  entry and an edit alike; when the app opens the form from one field (e.g. editing the Port row in a panel), it is on
  that field. A new entry does not open the first field's input popup by itself either: that would save one `Enter`, but
  a new entry would open differently from an edit, and giving up would take two `Esc`s (the first closing only the input
  popup). What opens is always the form itself, left with one `Esc`.

```
╭─ New host ─────────────────────────────────────╮
│                                                │
│ Name        web-01                             │   ← 1 item
│ Auth        (•) password                       │   ← 3 items
│             ( ) privatekey                     │
│             ( ) credential                     │
│ Agent       [x] forward                        │   ← 1 item
│                                                │
╰─ Enter:edit Ctrl-S:save Esc:cancel ────────────╯
```

`j` all the way: Name → password → privatekey → credential → forward. `Tab` all the way: Name → Auth → Agent.
(How options look is in `input/radio` and `input/checkbox`; the `(•)` and `[x]` here only illustrate.)

**How the focus looks** (the user, 2026-10-07): the focused item is drawn like a menu's cursor row — the layer colour as
background, dark bold text (see [`dialog/menu`](menu.md)). It runs from the start of the item to the inner right edge: from the value for a
field, from the option for an option, the button itself for a button; an empty value is still a full block of background.
A solid block differs in shape as well as colour, so the focus is not told by colour alone (in the spirit of L5). It is the
menu's way of drawing: in a family popup, the block on the layer colour is where `Enter` acts.

**The colour of the label** does not change with the focus.

| Label state | Colour |
|---|---|
| Normal | the layer colour (same as the title and the border) |
| Disabled | Surface2 |
| Its value has an error | Red, over any other colour |

- Before (popup question 4), a label turned Lavender bold when its value had the focus, back when values were typed into
  the form with a cursor. With values entered in an input popup, nothing in the form is "being edited": Lavender ([`color`](../color.md)) is
  left to the value actually being edited in the input popup, and "a glance tells which field" is the block's job — the
  block also tells which option of a radio field has the focus.
- A disabled field stays in place, neither removed nor changing the height (F7).
- What the input files must keep: a value never shares its label's colour in any state.

```
╭─ New host ─────────────────────────────────────╮
│                                                │
│ Name          web-01                           │   label in the layer colour
│ Host          10.0.0.5                         │   ← focus: from the value to the right edge, layer-colour background, dark bold text
│ Port          22                               │
│ Credential    —                                │   ← disabled: label Surface2
│                                                │
╰─ Enter:edit Ctrl-S:save Esc:cancel ────────────╯
```

## Editing a field

- `Enter` on a field that takes typing or opens a popup opens that field's input popup, stacked on the form (F8).
- `Enter` in the input popup confirms: the value is written back to the field, the input popup closes, and the focus
  **moves on to the next field** by itself (as `Tab` would). Filling the form from top to bottom, the focus lands on the submit button once
  the last field is confirmed, and one more `Enter` submits:
  `Enter` type `Enter` → `Enter` type `Enter` → … → `Enter` (the button).
- `Esc` in the input popup closes it (K4: the topmost layer) and leaves the field's value unchanged.
- `Enter` on a radio option chooses it; `Enter` on a checkbox option flips it in place. Neither opens a popup, and the focus
  stays where it is: the change is immediate, a wrong choice is undone by pressing again right there, and a focus that moved
  on would only have to come back.

## Submit

- The bottom of a form has an **action row** of real buttons, each saying what the form does (`Save`, `Connect`,
  `Sign in`). `Tab` to the button and `Enter` submits: only an explicit press of the button makes sure the user means to
  submit.
- No cancel button: cancelling is `Esc` (F3), shown in the hint.
- **`Ctrl-S`** anywhere in the form (wherever the focus is) presses the submit button. It is for changing one field and
  saving: to change the Port, `Enter` `22` `Enter` `Ctrl-S`, with no row of `Tab`s down to the button.
- No letter hotkey (such as `s`): a form looks like a row of fields, so users easily start typing straight away, and the
  first letter of `server` would submit the form. `Ctrl-S` types nothing, so it cannot collide.
- `Esc` does not move the focus to the action row (the user raised it and dropped it as counter-intuitive): F3 has `Esc`
  close any popup at once, and an exception for forms alone would leave users unable to close one.


**The button and where things sit** (the user, 2026-10-07):

```
╭─ New host ─────────────────────────────────────╮
│                                                │
│ Name        web-01                             │   ← field area: the only part that scrolls
│ Host                                           │
│ Port        22                                 │
│                                                │
│ Host is required                               │   ← error row (reserved, F7; blank when no error)
├────────────────────────────────────────────────┤   ← separator
│                                          Save  │   ← action row: the button on the right
│                                                │
╰─ Enter:edit Ctrl-S:save Esc:cancel ────────────╯
```

- **The button**: its text with one blank cell on each side, on a block of background. It has a background even without
  the focus (Surface1 background, Text), so it reads at once as an item that can take the focus and be pressed, not as a
  line of explanation; with the focus it is drawn like any other item, the layer colour as background with dark bold
  text (see "Focus and moving between fields").
- No `[ Save ]`: in the family square brackets mean a key (M5's `[A]`, a menu's `[r]ename`), and it would read as "press
  `S` to save". No powerline rounded capsule: those are Nerd Font glyphs, whose width differs between terminals (rules E5).
- **Where**: the field area → a blank row → the error row → a separator → the action row. The fields and the error row
  share the left edge; **the button sits on the right**, one cell from the border (the user). The error row sits just
  above the button: when a submit is refused, the eyes are already there.
- **The separator** (the user, 2026-10-07): above the action row, joined to the left and right borders (`├─┤`), in the
  border's colour (the layer colour), setting the action row apart from the content above.
- **The error row, the separator and the action row never scroll**: when the fields do not fit only the field area
  scrolls, and the button is always in sight.
- **The action row has one button for now (submit)**: every form so far needs one action. A form needing a second button
  is a gap in tdp, to be reported and added, and how to move between buttons is settled then.

## Hint

Settled by the user, 2026-10-07.

```
Enter:edit Ctrl-S:save Esc:cancel
```

- **The word after `Enter` follows the focused item**, saying what pressing it does: `Enter:edit` on a field that opens an
  input popup, `Enter:choose` on a radio option, `Enter:toggle` on a checkbox option, and the button's word on the button
  (in lower case: `Save` → `Enter:save`, `Connect` → `Enter:connect`). `Ctrl-S` is followed by the button's word too.
  On a field with a problem `e:error` is added (`Enter:edit e:error Ctrl-S:save Esc:cancel`); on the error row it reads
  `Enter:show e:edit Ctrl-S:save Esc:cancel`.
- **No movement keys** (`j/k`, `Tab`): users find them out by using the form (the user).
- `Esc:cancel` rather than `close`: `Esc` on a form throws its content away, the same meaning as a confirm's `Esc:cancel`.
- When it does not fit, items are dropped whole from the end as usual: `Esc:cancel` first (F3, the same across the family),
  then `Ctrl-S` (the button is on screen); `Enter` stays to the last.

## Cancel

- **A form with no changes**: `Esc` closes it at once (F3).
- **A form with changes**: `Esc` opens a confirm first (the user, 2026-10-07). The form keeps a single "changed" flag: it is
  set when a value is written back to the form (an input popup confirmed, a radio option chosen, a checkbox flipped) and
  never cleared; what changed is not compared, and changing a value back still counts. With the flag set, `Esc` first
  opens a confirm asking whether to discard (e.g. `Discard changes to New host?`): `Enter` discards and closes the form;
  `Esc` closes the confirm and returns to the form with every value still there (F6, K4).
- **Why** (the user): forms with no changes are not affected, and changed ones get a layer of protection; the program keeps
  no draft, only whether anything changed.
- I first suggested not asking, partly because pressing `Esc` repeatedly would go back and forth between the form and the
  confirm. On a second look that is no trap: the confirm says `Enter` discards, and someone pressing `Esc` repeatedly ends
  up on the form with its content intact — the "safe place" K4 is about.
- **Scope** (the user, 2026-10-07): ask only where a lot can be lost at once — forms and the textarea (see
  `input/textarea`). Other input popups (text, password, number, search, and those choosing a value) do not ask: they
  hold one value at most, easily typed again; giving up what was just typed with `Esc` is the most common thing done in
  them, and a confirm each time would wear; and inside a form, `Esc` in an input popup means "leave this field as it
  was", so asking there would take two keys to give up one field. The other dialogs (menu, confirm, note, toast) have
  nothing to change; leaving a terminal already asks (`Alt-Esc`, K10).
- This is an exception to F3 (`Esc` closes any popup at once), to be written into F3 with v0.2.0.

## Errors

Settled by the user, 2026-10-07.

- **A field's own rules** (format and range: Port within 1–65535, a keyword made of letters, digits and hyphens): refused
  in the input popup on `Enter`, the error written in the input popup's error row; the value is not written back and the
  popup stays open (see each input file). A value that fails never reaches the form.
- **Rules involving the whole form** are checked on submit (the button or `Ctrl-S`): a required field left empty, a field
  required because of another (Auth set to credential needs a Credential), a duplicate name.
- **A failed check**: nothing is saved; the form stays open with every value. The label of every field with a problem
  turns Red (all that needs fixing, at a glance); the error row gives the first problem in field order, and the focus
  moves to that field.
- **`e`** (the user, 2026-10-07): `e` (error) on a field with a problem (a Red label) moves the focus to the error row,
  which switches to **that field's** message (the whole form is checked at once, so every field's message is at hand);
  `Enter` on the error row opens a note with the whole message; `e` (edit) on the error row returns the focus to the
  field the message belongs to, where `Enter` opens its input popup. The error row can still be reached with `j`/`k` and
  `Tab`; `e` is the direct jump. A stray `e` only moves the focus and changes nothing (unlike the rejected "`s` submits").
- **The submit itself fails** (a submit error: the file changed underneath, a write failing, the remote refusing): it is
  not written in the error row; an error popup opens over the form (see the error row in
  [`layout/popup`](../layout/popup.md)); `Esc` closes it and returns to the form, every value still there, the focus
  where it was.
- **Errors follow the check** (changed by the user, 2026-10-07): the form as a whole is checked only on submit, so the Red
  labels and the error row stay, even when values change, until the next submit: then they turn into whatever is wrong
  then, or the form is saved. (What was settled first — "after a failed submit, check again on every write-back" — the
  user changed to follow the check alone.)
- **Before the first submit** the form as a whole is not checked: a new form does not open full of red "required".

(Where the error row sits and how it lines up with the action row are settled together with the look of a button.)

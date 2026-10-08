# form (forms)

**Language**: English · [繁體中文](form-zh_TW.md)

## Purpose

Several values filled in and submitted together (sshu's Host form, webu's Sign in and Add bookmark). For a single value,
use an input popup ([`input/`](../README.md#input)); for values that take effect when changed, with nothing to submit, use
a panel with one value per row ([`layout/panel`](../layout/panel.md)). The frame follows
[`layout/popup`](../layout/popup.md).

Nothing is typed into a form itself. A field that takes typing (text, password…) or has more options than fit (select,
date, colour, file) opens that field's input popup on `Enter`; the value is entered there and, once confirmed, written
back to the form. A field with few options (radio, checkbox) has its options drawn right in the form and is chosen in
place.

**Why**: some inputs do not fit in a row of a form and must open a popup of their own — a colour picker, a date picker,
choosing from a list. If the other fields were typed into right in the form, one form would be operated in two ways. With
every value entered in an input popup, every field works the same: `Enter` to go in and edit, `Enter` to confirm. The cost
is one more `Enter` per field (the one that goes in).

## Look

### Title

Says what this form does (`New host`, `Add bookmark`). Not the type (`number`, `path`, `email`): the type belongs to a
field, and with more than one field it would not fit in one title anyway.

### How a field is arranged

Each field takes one of two arrangements.

| Arrangement | Look | Suits |
|---|---|---|
| **Stacked** | the label on one row, the value on the next, the value using the full inner width | long values (URLs, paths, commands) |
| **Side by side** | one row: the label in a left column, the value to its right | short values; forms with many fields |

- A form may mix the two, one field after another. All stacked or all side by side is fine as well.
- No blank row between fields, and none between a stacked label and its value. They are told apart by colour: a label
  and its value never share a colour (see the label below).
- Labels, values and errors share the same left edge.
- The label column of side-by-side fields is as wide as the longest label **among the side-by-side fields** (stacked
  labels do not count), with space between the label column and the values.
- How a value is shown: see "How a value shows in a form and a panel" in [`input/README`](../input/README.md).

```
╭─ New profile ──────────────────────────────────╮
│                                                │
│ Name        clock3                             │   ← side by side
│ Timeout     30                                 │   ← side by side
│ Command                                        │   ← stacked
│ tmux new-session -A -s main                    │
│ Layout      row                                │   ← side by side
│                                                │
╰─ Enter:edit Esc:cancel ────────────────────────╯
```

(The drawings in this section and the next show the fields only; for the action row see "Action row".)

### Options drawn in the form

- Radio and checkbox fields with **five options or fewer** have them drawn in the form; with more than five, use a select
  or a checkbox popup instead (opened with `Enter`).
- Options run down by default; when they are all short and fit on one row, they may run across (e.g. `󰐾 asc  󰐽 desc`).
- The glyphs are in [`input/radio`](../input/radio.md) and [`input/checkbox`](../input/checkbox.md).

**Why**: beyond five, the form starts scrolling and the other fields drop out of sight.

### Focus and label

The focused item is drawn like a menu's cursor row — the layer colour as background, bold Base text
([`dialog/menu`](menu.md)). It runs from the start of the item to the inner right edge: from the value for a field, from
the option for an option, the button itself for a button; an empty value is still a full block of background.

**The colour of the label** does not change with the focus.

| Label state | Colour |
|---|---|
| Normal | the layer colour (same as the title and the border) |
| Disabled | Surface2 |
| Its value has an error | Red, over any other colour |

- A disabled field stays in place, neither removed nor changing the height (Rules F7).
- A value never shares its label's colour, in any state.

```
╭─ New host ─────────────────────────────────────╮
│                                                │
│ Name          web-01                           │   label in the layer colour
│ Host          10.0.0.5                         │   ← focus: from the value to the right edge, layer-colour background, bold Base text
│ Port          22                               │
│ Credential    —                                │   ← disabled: label Surface2
│                                                │
╰─ Enter:edit Esc:cancel ────────────────────────╯
```

**Why**: a solid block differs in shape as well as colour, so the focus is not told by colour alone (Rules L5); it is the
same way of drawing as a menu: in a family popup, the block on the layer colour is where `Enter` acts. Lavender is left
to the value actually being edited in an input popup; "a glance tells which field" is the block's job, and the block also
shows which option of a radio field the focus is on.

### Action row

```
╭─ New host ─────────────────────────────────────╮
│                                                │
│ Name        web-01                             │   ← field area: the only part that scrolls when it does not fit
│ Host                                           │
│ Port        22                                 │
│                                                │
│ Host is required                               │   ← error row (blank when there is no error)
│ ────────────────────────────────────────────── │   ← separator
│                                          Save  │   ← action row: the button on the right
│                                                │
╰─ Enter:edit Esc:cancel ────────────────────────╯
```

- **The button**: its text with one blank cell on each side, on a block of background. It has a background even without
  the focus (Surface1 background, Text), so it reads at once as an item that can take the focus and be pressed, not as a
  line of explanation; with the focus it is drawn like any other item, the layer colour as background with bold Base
  text. The button says what the form does (`Save`, `Connect`, `Sign in`).
- No `[ Save ]`: in the family square brackets mean a key (Rules M5's `[A]`, a menu's `[r]ename`), and it would read as
  "press `S` to save". No capsule: in the family a capsule is a name (a panel title, a tab, a screen), and a button drawn
  as a capsule would read as a title (Principle P4).
- **Where**: the field area → a blank row → the error row → a separator → the action row. The fields and the error row
  share the left edge; the button sits on the right, one cell from the border. The error row sits just above the
  button: when a submit is refused, the eyes are already nearby.
- **The separator**: above the action row, drawn like the separator in [`layout/popup`](../layout/popup.md) (not joined
  to the border, Overlay0), setting the action row apart from the content above.
- **The error row, the separator and the action row never scroll**: when the fields do not fit, only the field area
  scrolls, and the button is always in sight.
- **The action row has one button (submit)**: a form needing a second button is a gap in tdp, to be reported and added,
  and how to move between buttons is settled then.
- No cancel button: cancelling is `Esc` (Rules F3), shown in the hint.

## Keys

### Moving

In a form the focus moves by **item**: a field that takes typing or opens a popup is one item, each option of a radio or
checkbox field is an item of its own, and the button is one item; the error row, while it holds an error, is an item too
(just before the button).

- **`j`/`l`/`↓`/`→` to the next item, `h`/`k`/`↑`/`←` to the previous one** (a form is a one-dimensional list, Rules
  K12). Whether options run across or down does not matter; going on from the last option of a field enters the next
  field, and going back from the first option returns to the previous one. `gg` goes to the first item, `G` to the last
  (the button).
- **`Tab`/`Shift-Tab` jump one field at a time** (Rules K2); the error row while it holds an error, and the action row,
  are one stop each.
- **Jumping into a radio or checkbox field**: a radio field lands on its chosen option, or the first one if none is
  chosen; a checkbox group lands on its first option. `Shift-Tab` coming from below lands the same way: `Tab` means "jump
  to that field", and where it lands does not depend on the direction. On a radio field the focus lands on the current
  value: `j`/`k` to a neighbour to change it, or `Tab` straight on to leave it, with nothing chosen by mistake; in a
  checkbox group each option is ticked or not on its own, with no "current one", so starting from the top is the easiest
  to predict.
- **Wrapping at both ends**: the same for `Tab` and `j`/`k`. The button is the last item: going on from it returns to the
  first field, and going back one step from the first field reaches the button — making up for the action row sitting
  at the bottom.
- **Disabled fields and options are skipped**: neither `Tab` nor `j`/`k` stops on them; they are still drawn in place.
  Disabled means "cannot be changed now", and `Enter` on one would have nothing to do.
- **On opening**: the focus is on the first item it can stop on (disabled ones skipped), for a new entry and an edit
  alike; when the app opens the form from one field (e.g. editing the Port row in a panel), it is on that field. A new
  entry does not open the first field's input popup by itself either: that would save only one `Enter`, but a new entry
  would open differently from an edit, and giving up would take two `Esc`s (the first closing only the input popup).
  What opens is always the form itself, left with one `Esc`.

```
╭─ New host ─────────────────────────────────────╮
│                                                │
│ Name        web-01                             │   ← 1 item
│ Auth        󰐾 password                         │   ← 3 items
│             󰐽 privatekey                       │
│             󰐽 credential                       │
│ Agent       󰄲 forward                          │   ← 1 item
│                                                │
╰─ Enter:edit Esc:cancel ────────────────────────╯
```

`j` all the way: Name → password → privatekey → credential → forward. `Tab` all the way: Name → Auth → Agent.

### `Enter`

- **On a field that takes typing or opens a popup**: opens that field's input popup, stacked on the form (Rules F8).
  - `Enter` in the input popup confirms: the value is written back to that field of the form, the input popup closes,
    and **the focus stays on the same field** (Rules K3).
  - `Esc` in the input popup closes it, and the field's value is unchanged.
  - A checkbox popup opened from a form: `Space` ticks, `Enter` writes the whole group back, `Esc` cancels
    ([`input/checkbox`](../input/checkbox.md)).
- **On a radio option**: chooses it; **on a checkbox option**: flips it in place. Neither opens a popup; the focus stays
  where it is and the change is immediate; a wrong choice is undone by pressing again right there.
- **On the button**: submits.

### Submit

There is one way only: move the focus to the button and press `Enter`. Only an explicit press of the button makes sure
the user means to submit.

- The quick way there: `G` goes straight to the button; or `Shift-Tab` on the first field (wrapping at both ends). E.g.
  changing just the Port and saving — `Enter` on Port, type `2222`, `Enter`, `G`, `Enter`.
- No letter hotkey (such as `s`) submits: a form looks like a row of fields, so users easily start typing straight away,
  and the first letter of `server` would submit the form.
- `Esc` does not move the focus to the action row: Rules F3 has `Esc` close a popup at once, and if forms were an
  exception, users could not close one.

### Typing on a field

A form is not in the input state (Rules K8), yet users often think they can type straight in. When the focus is on a
field whose `Enter` opens an input popup for typing (text, password, number, textarea) and a printable character that is
not one of the form's keys is pressed (`q` included), a note pops up to explain:

```
╭─ Name ─────────────────────────╮
│                                │
│ Press [Enter] to edit Name.    │
│                                │
╰─ Enter/Esc:close ──────────────╯
```

- The title is the field's name; both `Enter` and `Esc` close it, back to the form with the focus unmoved
  ([`dialog/note`](note.md)).
- `Space` does nothing, as Rules K5 says, and brings up no note.
- The other items of a form (options, the button, the error row) bring up no note: a key with no use there simply does
  nothing.
- Letters on a form do nothing except movement and `e`; `q` does nothing either, and does not start quitting (Rules K9).

**Why**: a note rather than a toast: a note catches every character typed after it and does nothing with them, so the
form is not disturbed; a toast lets keys pass through, and an `e`, `h` or `l` typed after it would jump around between
fields. Users press `Enter` out of habit after typing, which just closes the note.

### Hint

```
Enter:edit Esc:cancel
```

- **The word after `Enter` follows the focused item**, saying what pressing it does: `Enter:edit` on a field that opens
  an input popup, `Enter:choose` on a radio option, `Enter:toggle` on a checkbox option, and the button's word on the
  button (in lower case: `Save` → `Enter:save`, `Connect` → `Enter:connect`).
- With the focus on a field with a problem, `e:error` is added (`Enter:edit e:error Esc:cancel`); on the error row it
  reads `Enter:show e:edit Esc:cancel`.
- No movement keys (`j/k`, `Tab`): users find them out by using the form.
- `Esc:cancel`, not `close`: `Esc` on a form throws its content away, the same meaning as a confirm's `Esc:cancel`.

## States

### Cancel

- **A form with no changes**: `Esc` closes it at once (Rules F3).
- **A form with changes**: `Esc` first opens a confirm asking whether to discard them (e.g. `Discard changes to New
  host?`): `Enter` discards and closes the form; `Esc` closes the confirm and returns to the form with every value still
  there (Rules F6, K4).
- **The "changed" flag**: set when a value is written back to the form (an input popup confirming a value different from
  the one it opened with, a radio option chosen, a checkbox flipped), and never cleared after that. Only the values when
  that one popup opened and when it was confirmed are compared, not the form's original values: changing a value and
  then changing it back still counts as a change.
- **Scope**: ask only where a lot can be lost at once — forms and the textarea ([`input/textarea`](../input/textarea.md)).
  Other input popups do not ask: they hold one value at most, easily typed again; giving up what was just typed with
  `Esc` is the most common thing done in them, and a confirm each time would wear. The other dialogs have nothing to
  change; leaving a terminal already asks first (`Alt-Esc`, Rules K10).

**Why**: forms with no changes are not affected, and changed ones get a layer of protection; the program keeps no draft,
only whether anything changed. Pressing `Esc` repeatedly goes back and forth between the form and the confirm, but that
is no trap: the confirm says `Enter` discards, and someone pressing `Esc` repeatedly ends up on the form with its content
intact — the "safe place" Rules K4 asks for.

### Errors

- **A field's own rules** (format and range: Port within 1–65535, a keyword made only of letters, digits and hyphens):
  refused in the input popup on `Enter`, the error written in the input popup's error row; the value is not written back
  and the popup stays open (see each input file). A value that fails never reaches the form.
- **Rules involving the whole form**: checked only when the button is pressed to submit — a required field left empty, a
  field required because of another (Auth set to credential needs a Credential chosen), a duplicate name.
- **A failed check**: nothing is saved; the form stays open with every value. The label of every field with a problem
  turns Red (all that needs fixing, at a glance); the error row gives the first problem in field order, and the focus
  jumps to that field.
- **`e`**: `e` (error) on a field with a problem (a Red label) moves the focus to the error row, which switches to **that
  field's** message (the whole form is checked at once, so every field's message is already at hand); `Enter` on the
  error row opens a note with the whole message (looking the same as an error popup, its title the field's name); `e`
  (edit) on the error row returns the focus to the field the message belongs to, where `Enter` opens its input popup to
  change it. The error row can still be reached with `j`/`k` and `Tab`; `e` is the shortcut that jumps straight there. A
  stray `e` only moves the focus and changes nothing.
- **The submit itself fails** (the file changed underneath, a write failing, the remote refusing): nothing is written in
  the error row; an error popup opens straight over the form (see the error row in [`layout/popup`](../layout/popup.md));
  once it is closed, the form is back with every value and the focus still on the button — one more `Enter` retries.
- **Errors follow the check**: the form as a whole is checked only on submit, so the Red labels and the error row stay,
  even when values change, until the next submit: then they turn into whatever is wrong then, or, with nothing wrong, the
  form is saved.
- **Before the first submit** the form as a whole is not checked: a new form does not open full of red "required".

# terminu components

**Language**: English · [繁體中文](README-zh_TW.md)

terminu components are the component specs under [tdp](../principle/README.md): the colour scheme, the screen, panels,
the frame floating over the screen, and each kind of content in that frame — what each looks like and how it is operated.
The principle gives the principles and rules; the components give the concrete parts. Versions and the CHANGELOG are
shared with tdp.

## What is a requirement

Everything written here is a requirement. Only four things are not: the parts stated as "up to the app", examples marked
"e.g.", the "Why", and paragraphs marked "Implementation reference (not a requirement)".

All of the components are in the fixed zone (["Departure" at the start of the Rules](../principle/rules.md)): what an app
cannot follow goes into the "偏離 tdp" (departures from tdp) section of its dev-remarks with the reason, and is reported
as a gap in tdp at the same time.

## Choosing among the options

Fields differ in nature — long or short values, few or many options — and so does the look that suits them. So the
components do not fix everything to one form; they list **a few options**, and the app picks by the nature of the field.
The choice is limited to the listed options: when none of them fits, that is a gap in tdp — report it and an option is
added, rather than inventing one inside the app.

## How to read

Read in order: **color → layout (screen, panel, popup) → dialog → input**. color and layout are the common base: every
component uses the colour scheme, and is drawn on the screen, in a panel or in a frame; dialog and input are what goes in
the frame.

## Three nouns

| Noun | What | File |
|---|---|---|
| **popup** | a frame floating over the screen: where the title, hint, padding, content area, scrolling and error row go. It sets only the look of the frame, not what goes in it | `layout/popup` |
| **input** | a kind of popup: enters or chooses one value and, once confirmed, writes it back. One file per kind of value | `input/` |
| **dialog** | a kind of popup that is not entering one value but the app talking to the user — a form, a list, a confirmation, read-only content, a message, a subprocess | `dialog/` |

- The seven classes of rules F1: the input class maps to `input/`, the other six to `dialog/`, one file each.
- Nothing is typed into a form (`dialog/form`): a field that takes typing or has more options than fit opens its value's
  input popup on `Enter`; a radio or checkbox with few options has them drawn in the form and is chosen in place.
- A list with search is a finder: a plain finder, a select, a checkbox popup and a file-picker are all kinds of finder
  (`input/finder`). A list without search is a menu (`dialog/menu`).
- Dialog rather than modal: modal names a behaviour — blocking what is underneath while open — and every popup but the
  toast does that, so it would not tell inputs from dialogs; dialog names the content — the app talking to you.

## color

| File | What |
|---|---|
| [`color`](color.md) | The colour scheme: presentation rules, calculation, colour codes |

## layout

| File | What |
|---|---|
| [`screen`](layout/screen.md) | The whole screen: footer, screen chip row, statusbar, narrow widths, empty states |
| [`panel`](layout/panel.md) | Panels: frame, lists, one value per row, panel filter |
| [`popup`](layout/popup.md) | The frame floating over the screen |

## dialog

| File | What |
|---|---|
| [`form`](dialog/form.md) | a form: several values filled in and submitted together |
| [`menu`](dialog/menu.md) | choose a row from a list and run it |
| [`confirm`](dialog/confirm.md) | one question, `Enter` accepts, `Esc` cancels |
| [`note`](dialog/note.md) | read-only content: the key reference, viewers, the error popup |
| [`toast`](dialog/toast.md) | a short message popping up from the bottom |
| [`terminal`](dialog/terminal.md) | a subprocess running in a frame |

## input

Each is a popup that enters or chooses that kind of value.

| File | What |
|---|---|
| [`README`](input/README.md) | rules shared by every input |
| [`text`](input/text.md) | single-line text |
| [`password`](input/password.md) | masked input |
| [`number`](input/number.md) | number |
| [`textarea`](input/textarea.md) | multi-line text |
| [`finder`](input/finder.md) | a list with search; select, the checkbox popup and file-picker are kinds of it |
| [`select`](input/select.md) | choose one value from a list |
| [`radio`](input/radio.md) | one of a few, drawn in a form |
| [`checkbox`](input/checkbox.md) | a switch, or ticking several |
| [`slider`](input/slider.md) | a value in a range |
| [`datetime-picker`](input/datetime-picker.md) | date and time |
| [`color-picker`](input/color-picker.md) | colour |
| [`file-picker`](input/file-picker.md) | choosing a file |

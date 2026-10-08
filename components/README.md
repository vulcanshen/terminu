# terminu components

**Language**: English · [繁體中文](README-zh_TW.md)

terminu components are the component specs under [tdp](../principle/README.md): the frame floating over the screen, each
kind of content in it, and values in a panel — what they look like and how they are operated. The principle gives the principles and rules; the components give
the concrete parts. Apps of the terminu family follow them, and write what they cannot follow under "departures from tdp"
in their dev-remarks. Versions and the CHANGELOG are shared with tdp.

## Three nouns

| Noun | What | Where |
|---|---|---|
| **popup** | a frame floating over the screen: title, hint, padding, content area, scrolling, where the error row sits. Only the look of the frame, not what goes in it | `layout/popup` |
| **input** | a kind of popup: shows a value being entered (the input state, K8). One file per kind of value | `input/` |
| **dialog** | a kind of popup that is not entering one value but the app talking to the user — a form, a list, a confirmation, read-only content, a message, a subprocess | `dialog/` |

- Nothing is typed into a form (`dialog/form`): a field that takes typing or has more options than fit opens its value's
  input popup on `Enter`; a radio or checkbox field with few options has them drawn in the form and is chosen in place.
  Values in a panel and search rows inside a panel are settled with the panel.
- The seven classes of rules F1: the input class maps to `input/`, the other six to `dialog/`, one file each (form being
  the seventh, added 2026-10-07).
- Dialog rather than modal: modal names a behaviour — blocking what is underneath while open — and every popup but the
  toast does that, so it would not tell inputs from dialogs; dialog names the content — the app talking to you.

## Choosing among the options

Fields differ — long or short values, few or many fields — and so does the look that suits them. So the components do not
fix everything to one form: they list **a few options**, and the app picks by the nature of each field. The choice is only
among the listed options: when none of them fits, that is a gap in tdp — report it and an option is added, rather than
inventing one inside the app.

## color

| File | What |
|---|---|
| [`color`](color.md) | Colour: presentation rules, calculation, colour codes (moved from defaults D2 on 2026-10-07) |

## layout

| File | What |
|---|---|
| [`screen`](layout/screen.md) | The whole screen: footer, screen chips, narrow widths, empty states |
| [`panel`](layout/panel.md) | Values and input in a panel |
| [`popup`](layout/popup.md) | The frame floating over the screen |

## dialog

| File | What |
|---|---|
| [`form`](dialog/form.md) | a form: several values filled in and submitted together |
| [`menu`](dialog/menu.md) | choose a row from a list and run it |
| [`confirm`](dialog/confirm.md) | one question, `Enter` accepts, `Esc` cancels |
| [`note`](dialog/note.md) | read-only content |
| [`toast`](dialog/toast.md) | a one-line message popping up from the bottom |
| [`terminal`](dialog/terminal.md) | a subprocess running in a frame |

## input

Each is a popup showing that kind of value being entered.

| File | What |
|---|---|
| [`text`](input/text.md) | single-line text |
| [`password`](input/password.md) | masked input |
| [`number`](input/number.md) | number |
| [`textarea`](input/textarea.md) | multi-line text |
| [`search`](input/search.md) | search and filter |
| [`select`](input/select.md) | choose from a list |
| [`radio`](input/radio.md) | one of a few |
| [`checkbox`](input/checkbox.md) | on / off |
| [`slider`](input/slider.md) | a value in a range |
| [`datetime-picker`](input/datetime-picker.md) | date and time |
| [`color-picker`](input/color-picker.md) | colour |
| [`file-picker`](input/file-picker.md) | choosing a file (a kind of finder) |

# toast (a short message)

**Language**: English · [繁體中文](toast-zh_TW.md)

## toast.1 Purpose

A short message popping up from the bottom, gone on `Esc` or when its time is up; every key but `Esc` passes through it
(Rules F1, F3): "Copied", a failed operation. A failure tied to a popup's action that the user needs to read before
deciding what to do uses an error popup ([`dialog/note`](note.md)), not a toast. What the item under the cursor is goes
in its note ([`layout/panel`](../layout/panel.md), panel.18), not in a toast.

## toast.2 Look

```
┏━󰗠 SUCCESS━━━━┓
┃                ┃
┃ Copied 3 paths ┃
┃                ┃
┗━ Esc:close ━━━━┛
```

- **Frame**: a popup's frame, always in the layer colour of layer 1. A toast is not a layer (Rules F1): it does not
  trigger dimming and is not dimmed.
- **Position**: at the bottom of the screen, centred horizontally; its bottom border is always on the third row from the
  bottom, whatever is underneath, so the two bottom rows always stay in sight: normally the panel's bottom border (hint,
  scroll position) and the footer; with a terminal popup open, the PTY's last row (the shell prompt) and the terminal's
  bottom border (the exit key); on a screen without panels, the same position. The toast saying a panel cannot be
  resized is the one exception: it sits on that panel (screen.9 in [`layout/screen`](../layout/screen.md)).
- **Width**: the message is known when it opens, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).
- **Text**: centred. It may have several rows, given by the app a row at a time ("Control characters" in
  [components](../README.md)), each starting a row of its own. When too long it wraps (as in [the components' "Wrapping"](../README.md)), every row centred. How
  many rows at most, the app may decide for itself; the spec sets no limit. When the app sets one and a message goes past it, the last
  row ends with `…`, and the full message goes to an error popup or the app's log. A success report the user needs to
  read whole (e.g. which files were written where) that does not fit opens instead a read-only viewer
  ([`dialog/note`](note.md)) holding the whole report, titled with what was done, in the layer colour; it pops up by
  itself, so `Enter` closes it as well as `Esc`; the report goes to the App Log too, as a Success. A toast goes before
  a long report is read, and the App Log has to be looked for (the user, 2026-11-18, from locku).
- **Capitalised**: each row starts with a capital letter, the rest as it is (`Copied`, `Can't save filu: permission
  denied`). A row starting with a name or a path keeps the name's case (`kbu.yaml saved`; "Uppercase" in the
  [components](../README.md): a name is content). Each App Log entry follows this too (the App Log in
  [`dialog/note`](note.md)).
- **Four kinds**: the title names the kind.

  | Kind | Title | Text |
  |---|---|---|
  | Success | `nf-md-check_circle` (U+F05E0) `SUCCESS` | Green |
  | Info | `nf-fa-flag` (U+F024) `INFO` | Text |
  | Warning | `nf-md-alarm_light` (U+F078F) `WARNING` | Peach |
  | Error | `nf-md-fire` (U+F0238) `ERROR` | Red |

- **Which kind follows what the colours mean** ([`color`](../color.md)):

  | Kind | When | E.g. |
  |---|---|---|
  | Success | an action finished successfully (Green: completed successfully) | `Copied 3 paths`, `Connected to web-01` |
  | Info | a neutral notice, neither good nor bad | `Switched to context prod`, `Nothing to paste` |
  | Warning | done, or still usable, but with something worth noticing (Peach: worth noticing, not broken) | `3 files skipped` |
  | Error | an action failed (Red: an error) | `Can't connect to cluster` |

  Whether something finished is told with Success or Info, the app may decide for itself: a Success is itself a kind of notice, and
  whether to mark it as a success is the app's call. A failure is always an Error, never a Warning; a failure tied to a popup's action, which the user must read before
  deciding, uses an error popup as "Purpose" says.
- **Time**: Success and Info 2200 ms; Warning and Error 4400 ms.
- **More than one**: toasts stack. A new one comes at the bottom, in the position above, and pushes the ones showing up;
  each keeps its own time and leaves when it is up, the others closing the gap. At most three show: a fourth pushes the
  oldest out (its words are in the App Log). The same words as a toast already showing make no new one: that toast's
  time starts over, and its title counts how many times they came (`INFO ×3`). One way for every toast, whatever sends
  it (the user, 2026-11-20, from kbu: a toast replacing the one before took away what the user had not read yet).

**Why**: a toast is a word in passing and should block nothing — hence at the bottom, taking no keys, and leaving on its
own when its time is up; nor should it cover the panel's bottom border and the footer, where the user looks for what to
press next. With a terminal popup open, `Esc` in the PTY cannot close a toast (Rules K10, F3); covering the prompt would
hide what the user is typing for a few seconds, and the terminal's bottom border carries the exit key, which like the
footer is "what can be pressed next". One position covers every case, so the toast does not jump around between
screens. Warning and Error get double the time because what they say matters more; Success, like Info, is just a word
that something is done. Success is a tick in a circle, not a ticked box: a ticked box is a checkbox, and one look
cannot have two meanings (Principle P4).

## toast.3 Keys

- `Esc` dismisses one toast at once, the oldest first, one a press (Rules F3), before any other popup is closed (Rules
  K4); every other key passes through it to what is underneath. With the focus in a PTY, `Esc` belongs to the
  subprocess, and the toast can only wait for its time to run out.
- **Hint**: `Esc:close`, on the oldest toast only, the one `Esc` closes next.

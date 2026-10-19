# toast (a short message)

**Language**: English · [繁體中文](toast-zh_TW.md)

## Purpose

A short message popping up from the bottom, gone on `Esc` or when its time is up; every key but `Esc` passes through it
(Rules F1, F3): "Copied", a failed operation. A failure tied to a popup's action that the user needs to read before
deciding what to do uses an error popup ([`dialog/note`](note.md)), not a toast.

## Look

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
  bottom border (the exit key); on a screen without panels, the same position.
- **Width**: the message is known when it opens, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).
- **Text**: centred. When too long it wraps (as in [the components' "Wrapping"](../README.md)), every row centred. How
  many rows at most is up to the app; the spec sets no limit. When the app sets one and a message goes past it, the last
  row ends with `…`, and the full message goes to an error popup or the app's log.
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
  | Warning | done, or still usable, but with something worth noticing (Peach: worth noticing, not broken) | `3 files skipped`, `Unknown key in config.yaml` |
  | Error | an action failed (Red: an error) | `Can't connect to cluster` |

  A failure is always an Error, never a Warning; a failure tied to a popup's action, which the user must read before
  deciding, uses an error popup as "Purpose" says.
- **Time**: Success and Info 2200 ms; Warning and Error 4400 ms.
- **When a second toast comes**: it replaces the first at once, and the timer starts over.

**Why**: a toast is a word in passing and should block nothing — hence at the bottom, taking no keys, and leaving on its
own when its time is up; nor should it cover the panel's bottom border and the footer, where the user looks for what to
press next. With a terminal popup open, `Esc` in the PTY cannot close a toast (Rules K10, F3); covering the prompt would
hide what the user is typing for a few seconds, and the terminal's bottom border carries the exit key, which like the
footer is "what can be pressed next". One position covers every case, so the toast does not jump around between
screens. Warning and Error get double the time because what they say matters more; Success, like Info, is just a word
that something is done. Success is a tick in a circle, not a ticked box: a ticked box is a checkbox, and one look
cannot have two meanings (Principle P4).

## Keys

- `Esc` dismisses it at once (Rules F3), before any other popup is closed (Rules K4); every other key passes through it
  to what is underneath. With the focus in a PTY, `Esc` belongs to the subprocess, and the toast can only wait for its
  time to run out.
- **Hint**: `Esc:close`.

# toast (a short message)

**Language**: English · [繁體中文](toast-zh_TW.md)

## Purpose

A short message popping up from the bottom, gone on `Esc` or when its time is up; every key but `Esc` passes through it
(Rules F1, F3): "Copied", a failed operation. A failure tied to a popup's action that the user needs to read before
deciding what to do uses an error popup ([`dialog/note`](note.md)), not a toast.

## Look

```
┏━INFO━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                   ┃
┃          Copied 3 paths           ┃
┃                                   ┃
┗━ Esc:close ━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **Frame**: a popup's frame, always in the layer colour of layer 1. A toast is not a layer (Rules F1): it does not
  trigger dimming and is not dimmed.
- **Position**: at the bottom of the screen, centred horizontally; its bottom border is always on the third row from the
  bottom, whatever is underneath, so the two bottom rows always stay in sight: normally the panel's bottom border (hint,
  scroll position) and the footer; with a terminal popup open, the PTY's last row (the shell prompt) and the terminal's
  bottom border (the exit key); on a screen without panels, the same position.
- **Width**: the message is known when it opens, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).
- **Text**: centred. When too long it wraps, every row centred; three rows at most, and beyond that the third row ends
  with `…`. A full message belongs in an error popup or the app's log.
- **Three kinds**: the title names the kind.

  | Kind | Title | Text |
  |---|---|---|
  | Info | `nf-fa-flag` (U+F024) `INFO` | Text |
  | Warning | `nf-md-alarm_light` (U+F078F) `WARNING` | Peach |
  | Error | `nf-md-fire` (U+F0238) `ERROR` | Red |

- **Time**: Info 2200 ms; Warning and Error 4400 ms.
- **When a second toast comes**: it replaces the first at once, and the timer starts over.

**Why**: a toast is a word in passing and should block nothing — hence at the bottom, taking no keys, and leaving on its
own when its time is up; nor should it cover the panel's bottom border and the footer, where the user looks for what to
press next. With a terminal popup open, `Esc` in the PTY cannot close a toast (Rules K10, F3); covering the prompt would
hide what the user is typing for a few seconds, and the terminal's bottom border carries the exit key, which like the
footer is "what can be pressed next". One position covers every case, so the toast does not jump around between
screens. Warning and Error get double the time because what they say matters more.

## Keys

- `Esc` dismisses it at once (Rules F3), before any other popup is closed (Rules K4); every other key passes through it
  to what is underneath. With the focus in a PTY, `Esc` belongs to the subprocess, and the toast can only wait for its
  time to run out.
- **Hint**: `Esc:close`.

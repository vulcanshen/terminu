# toast (a short message)

**Language**: English · [繁體中文](toast-zh_TW.md)

## toast.1 Purpose

A short message popping up from the bottom, gone on `Esc` or when its time is up; every key but `Esc` passes through it
(Rules F1, F3): "Copied", a failed operation. A failure tied to a popup's action that the user needs to read before
deciding what to do uses an error popup ([`dialog/note`](note.md)), not a toast. The inspect toast (toast.4) is the
exception: it says what the item under the cursor is, and is there only while the cursor is on it.

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
  bottom border (the exit key); on a screen without panels, the same position.
- **Width**: the message is known when it opens, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).
- **Text**: centred. It may have several rows, given by the app a row at a time ("Control characters" in
  [components](../README.md)), each starting a row of its own. When too long it wraps (as in [the components' "Wrapping"](../README.md)), every row centred. How
  many rows at most, the app may decide for itself; the spec sets no limit. When the app sets one and a message goes past it, the last
  row ends with `…`, and the full message goes to an error popup or the app's log.
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
  | Warning | done, or still usable, but with something worth noticing (Peach: worth noticing, not broken) | `3 files skipped`, `Unknown key in config.yaml` |
  | Error | an action failed (Red: an error) | `Can't connect to cluster` |

  Whether something finished is told with Success or Info, the app may decide for itself: a Success is itself a kind of notice, and
  whether to mark it as a success is the app's call. A failure is always an Error, never a Warning; a failure tied to a popup's action, which the user must read before
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

## toast.3 Keys

- `Esc` dismisses it at once (Rules F3), before any other popup is closed (Rules K4); every other key passes through it
  to what is underneath. With the focus in a PTY, `Esc` belongs to the subprocess, and the toast can only wait for its
  time to run out.
- **Hint**: `Esc:close`.

## toast.4 The inspect toast

A toast saying what the item under the cursor is, there for as long as the cursor is on it (the user, 2026-10-29,
from webu): e.g. in webu's Focus mode, the address a link goes to. Which items have one and what it says, the app may
decide for itself; an item with nothing to show has none.

```
┏━󰈈 INSPECT━━━━━━━━━━━━┓
┃                         ┃
┃ go.dev/doc/effective_go ┃
┃                         ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **Look**: as any toast (toast.2: the position, the frame, the width, the text), titled `nf-md-eye` (U+F0208)
  `INSPECT`, its text in Text. **No hint**: no key closes it.
- **When it is there**: from when the cursor lands on an item that has one until the cursor leaves that item; moving
  to another item that has one shows that item's at once. **No timer.**
- **A popup opened over it** (the Space menu, `?`…): the focus is then on the popup, so the inspect toast is not
  shown; when the popup closes and the cursor is still on the item, it comes back.
- **Not in the App Log** ([`dialog/note`](note.md), note.7): it comes and goes with the cursor, and moving the cursor
  is not recorded.
- **Keys**: every key passes through it, `Esc` included (the exception to toast.3, Rules K4 and F3): `Esc` does what it
  does underneath (e.g. leaves webu's Focus mode), and the toast goes with the cursor.
- **Another toast**: an ordinary toast replaces it, as toast.2 says; once that one is gone, if the cursor is still on
  the item, the inspect toast comes back.
- **The item under it**: when the inspect toast would cover the item the cursor is on, the view scrolls so that the
  item shows above it.

**Why** (the user, 2026-10-29): where a link goes is wanted only while on the link, so it takes no row or slot of its
own — the right of a panel's bottom border stays the scroll position ([`layout/panel`](../layout/panel.md)). A note
popup would take the keys, and `j|k` could no longer move the cursor; a toast already lets every key but `Esc` through.
`Esc` goes through too: the toast leaves by itself when the cursor does, so stopping `Esc` on it would only make
leaving take two presses on every link, and the next link would bring it back anyway. An eye, not a magnifier: in the
family a magnifier means searching (webu's and filu's search boxes), and one look cannot have two meanings (Principle
P4). A title of its own, not Info's: an Info leaves by itself after a while, and the inspect toast does not. Gone
under a popup: it is there while the focus is on the item, and a toast is drawn above every popup, undimmed, so it
would sit on a tall popup's last rows and its hint. Not recorded: walking along the links of a page would otherwise
write an entry for each one, burying what the user actually did.

# terminal (a subprocess in a frame)

**Language**: English · [繁體中文](terminal-zh_TW.md)

## Purpose

A subprocess running in a frame (a shell, an editor, a remote session): every key goes to it; only the exit key and the
key combinations the app keeps belong to the app (Rules F1, K10). A PTY placed in a panel (e.g. sshu's grid cells) is
not a popup: its frame follows [`layout/panel`](../layout/panel.md), and the PTY's keys are written in the footer
([`layout/screen`](../layout/screen.md)).

## Look

```
[M]ANAGE[F]ILE TRANSFER[S]SH        2 live sessions    ← statusbar / screen chip row: kept
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   ← the divider under the chip row: kept (a progress bar during a transfer)
┏━󰆍 ALTERM: myhost━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃$ kubectl get pods                                      ┃   ← the PTY touches the frame, no padding on any side
┃NAME          READY   STATUS    RESTARTS   AGE          ┃
┃nginx-7d4f    1/1     Running   0          3d           ┃
┃$ █                                                     ┃
┗━ Alt-Esc:exit Alt-t:hide PgUp:history ━━━━━━━━━━━━━━━━━┛   ← down to the screen's last row; the footer is not drawn
```

- **Size** (the terminal exception of Rules F7): width `terminal width − 2`, with no 120-column cap. Above, the
  statusbar or the screen chip row stays (with the divider under the chip row); below, it runs down to the screen's last row. In an app
  without a statusbar it starts from the first row.
- **No footer**: while a terminal popup is open the footer is not drawn at all. One column is left free on each side of
  the frame, so the two ends of the last row are blank, with none of the footer's text showing.
- **No padding**: the subprocess needs every row and every column, so the content is drawn from the first row inside
  the frame to the last and from the first column to the last, touching the frame on every side. This is the special
  case of the terminal kind of popup (the padding in [`layout/popup`](../layout/popup.md)). A PTY placed in a panel has
  no padding either: the panel's frame is drawn as usual and the PTY touches it (the padding of
  [`layout/panel`](../layout/panel.md) does not apply).
- **Title**: `nf-md-console` (U+F018D) plus what is running (`SHELL`, `ALTERM: myhost`, `EDIT: pod/x`; names and paths keep their case).
- **The subprocess's cursor**: the real cursor is hidden; one cell with a Text background and Base text, a reversed
  block, is drawn where the subprocess's cursor is; the shape it asks for with DECSCUSR (underline, bar) is ignored.
  The same for a PTY in a panel. This is a terminal's default cursor; the family's cursor colours each mean something
  (Lavender a value being edited, the layer colour a cursor moving through text), and a PTY shows the subprocess's own
  screen, so neither fits; a bar cannot be drawn on a screen drawn cell by cell without covering the character.

**Why**: the statusbar holds what is going on (kbu's context, sshu's transfer progress), worth a glance even while
working in the shell. The footer is not needed: with the focus in a PTY, the footer's `Space`, `?` and `q` all go to the
subprocess, so showing it as usual would mislead; the PTY's keys appear in one place only, this frame's bottom border,
with no two rows of hints.

## Keys

- Every key goes to the subprocess (Rules K10).
- **Hint**: the exit key always comes first, and is the last to be dropped when the hint does not fit. The verb says
  what pressing it really does:
  - `Alt-Esc:exit`: ends the subprocess.
  - `Alt-Esc:leave`: leaves, with the subprocess still running.
  - Never `close`.
- After the exit key come the key combinations the app keeps (e.g. `Alt-t:hide`, `PgUp:history`).
- `Alt-Esc` always asks for confirmation first (Rules K10).
- `Home` and `End` belong to the subprocess (Rules K10); to reach the top or the bottom of the history, use `gg|G` in
  history mode (below).

## History mode

On a PTY's live screen every letter belongs to the subprocess (a shell needs `j`, `k`, `g`), so scrolling up into the
history is a mode (Rules K11), and only there do the family's movement keys work.

- **Entering**: scrolling up with `PgUp` enters it. The frame and the mode name take the mode colour, as in K11; the mode
  name is `History` (`┫History┣`).
- **In the mode**: `j|k`, `u|d`, `gg|G` and `PgUp|PgDn` all scroll the history and are not sent to the subprocess.
- **`Esc`**: leaves the mode, back to the live screen.
- **Any other key**: leaves the mode first, back to the live screen, then goes to the subprocess as usual — typing
  right after reading the history puts the characters in the shell.
- **Disclosure**: as in K11, the keys of the mode are written in the bottom border's hint and in the `?` key reference.

**Why**: going to the top and the bottom is `gg|G` throughout the family, a PTY's history included; but on the live
screen every letter must reach the subprocess, so the family's movement keys can only work inside a mode. `PgUp` is the
old habit for scrolling back in a terminal, so pressing it gets you in; someone who starts typing does not have to press
`Esc` first, since the first character takes them back to the live screen.

## Selection mode

A PTY's selection mode follows the selection mode of [`dialog/note`](note.md): the same keys, colours, scroll
position, and toast after copying.

- **Entering**: every letter in a PTY belongs to the subprocess, so it is entered with a key combination the app keeps
  (e.g. sshu's `Alt-v`), disclosed all the time like the other kept keys (Rules K10, M1).
- **The screen freezes**: on entering, later output from the subprocess is not drawn yet, so new output does not push
  the selection away; the cursor can move up into the history. Leaving returns to the live screen.
- **After leaving**: keys go to the subprocess as usual.

**Why**: in a shell, what you most often want to copy is a piece of output; with the same keys as the viewer, learning
it once lets you select anywhere in the family.

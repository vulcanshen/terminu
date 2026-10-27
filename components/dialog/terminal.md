# terminal (a subprocess in a frame)

**Language**: English · [繁體中文](terminal-zh_TW.md)

## terminal.1 Purpose

A subprocess running in a frame (a shell, an editor, a remote session): every key goes to it; only the exit key, the
key combinations the app keeps, and an interactive terminal's `Alt-v` and `PgUp` ("Which PTYs have these
modes" below) belong to the app (Rules F1, K10). A PTY placed in a panel (e.g. sshu's grid cells) is
not a popup: its frame follows [`layout/panel`](../layout/panel.md), and the PTY's keys are written in the footer
([`layout/screen`](../layout/screen.md)).

## terminal.2 Look

```
[M]ANAGE[F]ILE TRANSFER[S]SH        2 live sessions    ← statusbar / screen chip row: kept
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   ← the divider under the chip row: kept (a progress bar during a transfer)
┏━󰆍 ALTERM: myhost━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃$ kubectl get pods                                      ┃   ← the PTY touches the frame, no padding on any side
┃NAME          READY   STATUS    RESTARTS   AGE          ┃
┃nginx-7d4f    1/1     Running   0          3d           ┃
┃$ █                                                     ┃
┗━ Alt-Esc:exit Alt-t:hide Alt-v:select PgUp:history ━━━━┛   ← down to the screen's last row; the footer is not drawn
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

## terminal.3 Keys

- Every key goes to the subprocess (Rules K10).
- **Hint**: the exit key always comes first, and is the last to be dropped when the hint does not fit. The verb says
  what pressing it really does:
  - `Alt-Esc:exit`: ends the subprocess.
  - `Alt-Esc:leave`: leaves, with the subprocess still running.
  - Never `close`.
- After the exit key come the key combinations the app keeps (e.g. `Alt-t:hide`), then, in an interactive terminal,
  `Alt-v:select` and `PgUp:history` (below).
- `Alt-Esc` always asks for confirmation first (Rules K10).
- `Home` and `End` belong to the subprocess (Rules K10); to reach the top or the bottom of the history, use `gg|G` in
  history mode (below).

## terminal.4 Which PTYs have these modes

The history and selection modes below go by what a PTY is for, not by its being a PTY:

- **An interactive terminal**: a PTY where the user types their own commands (a shell, an ssh session, `kubectl exec`)
  always has both modes.
- **A PTY the app opens to run a program for one job** (editing a file in `$EDITOR`, doas asking for a password): it has
  neither mode, and every key goes to that program, `PgUp` included. Scrolling, moving and selecting are that program's
  own business.
- **While the subprocess takes the whole screen** (vim, less or htop started in an interactive terminal, switching to the
  terminal's other screen): `PgUp` goes to it and the bottom border has no `PgUp:history`; once it is back on the normal
  screen, `PgUp` enters the history mode again. The selection mode works as usual, on the frozen screen.
- **While the user gives every key to the subprocess** (e.g. a locked cell in sshu, for a sshu started inside it): the
  selection mode steps aside; `PgUp|PgDn` go straight in, and the innermost PTY scrolls its own history, as if used
  directly. The key that unlocks is always shown, as in Rules K10, and both modes come back after unlocking.

**Why**: what the family looks after is the user's own commands: the output of what they typed in a shell has to scroll
back and be selectable. Editors and full-screen programs handle their own scrolling and selection; we have not rewritten
them, so we do not take their keys. Their screens never reach the history either: catching `PgUp` would only stop vim
from paging and give an empty history instead.

## terminal.5 History mode

On an interactive terminal's live screen every letter belongs to the subprocess (a shell needs `j`, `k`, `g`), so scrolling up into the
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

## terminal.6 Selection mode

An interactive terminal's selection mode follows the selection mode of [`dialog/note`](note.md): the same keys, colours, scroll
position, and toast after copying.

- **Entering**: the family enters the selection mode with `v`; every letter in a PTY belongs to the subprocess, so `v`
  would be typed into the shell, and `Alt` gets out of it: `Alt-v`. It is not a key the app picks; it is disclosed all
  the time like the kept keys (Rules K10, M1).
- **The screen freezes**: on entering, later output from the subprocess is not drawn yet, so new output does not push
  the selection away; the cursor can move up into the history. Leaving returns to the live screen.
- **After leaving**: keys go to the subprocess as usual.

**Why**: in a shell, what you most often want to copy is a piece of output; with the same keys as the viewer, learning
it once lets you select anywhere in the family.

## terminal.7 Raising privileges

When an app writes a system file (e.g. hostu writing `/etc/hosts`), the system's tool for raising privileges does it:

- First try without a password (e.g. `sudo -n`); if that works, write at once, opening nothing.
- When a password is needed, ask in a password popup ([`input/password`](../input/password.md), the unlock style, titled
  `PASSWORD`) and hand it to the tool on its standard input (e.g. `sudo -S`). A wrong password keeps the popup open, the
  dots cleared and `Wrong password` on the error row; `Esc` cancels, and nothing is written.
- **The password goes to the tool and nowhere else**: apart from the tool's standard input it is written to no file, not
  recorded in the App Log, not shown on screen (a toast, an error message) and not sent over the network; once handed
  over it is dropped. An app on the lib only gives the command to run: the lib asks for the password and hands it to the
  tool, and the app never gets hold of it (Rules E8).
- When the tool cannot read a password on its standard input (e.g. `doas`), open a terminal popup running it and let it
  ask; the popup closes itself when it is done. This PTY runs a program for one job, so it has no history or selection
  mode ("Which PTYs have these modes" above).
- Which tool, the app may decide for itself by the platform (e.g. sudo, doas when there is none; on Windows gsudo or the built-in
  sudo, with the system's UAC prompt).

**Why**: one line asking for a password needs no terminal filling the screen, and the password is asked for the way
every other password popup in the family asks. The password then passes through the app, but the family is open
source: what is done with it can be read in the code; the lib keeps it between asking and handing over, out of the
app's reach, so it cannot be stored, end up in the App Log or be sent anywhere (the user, 2026-10-27, hostu). How long
sudo remembers still works (`sudo -n` first); settings where the tool asks by itself, like fingerprint unlock, go unused.

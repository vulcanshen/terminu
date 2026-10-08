# terminal (a subprocess in a frame)

**Language**: English · [繁體中文](terminal-zh_TW.md)

## Purpose

A subprocess running in a frame (a shell, an editor, a remote session): every key goes to it; only the exit key and the
key combinations the app keeps belong to the app (Rules F1, K10). A PTY placed in a panel (e.g. sshu's grid cells) is
not a popup: its frame follows [`layout/panel`](../layout/panel.md), and the PTY's keys are written in the footer
([`layout/screen`](../layout/screen.md)).

## Look

```
 [M]anage  [F]ile transfer  [S]SH       2 live sessions    ← statusbar / screen chip row: kept
╭─ Alterm: myhost ───────────────────────────────────────╮
│ $ kubectl get pods                                     │
│ NAME          READY   STATUS    RESTARTS   AGE         │
│ nginx-7d4f    1/1     Running   0          3d          │
│ $ █                                                    │
╰─ Alt-Esc:exit Alt-t:hide PgUp:history ─────────────────╯   ← down to the screen's last row, covering the footer
```

- **Size** (the terminal exception of Rules F7): width `terminal width − 2`, with no 120-column cap. Above, the
  statusbar or the screen chip row stays; below, it runs down to the screen's last row, covering the footer. In an app
  without a statusbar it starts from the first row.
- **No padding**: the subprocess needs every row, so the content is drawn from the first row inside the frame to the
  last.
- **Title**: `nf-md-console` (U+F018D) plus what is running (`Shell`, `Alterm: myhost`, `Edit: pod/x`).

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

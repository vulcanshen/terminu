# file-picker (choosing a file)

**Language**: English · [繁體中文](file-picker-zh_TW.md)

## Purpose

Choosing one **file**, handed back as a value: sshu's Identity file, webu's Upload and Import. The file-picker is a
kind of finder ([`input/finder`](finder.md)): the skeleton, the two areas, `Tab`, `Enter` on the typing row entering the
list, which side is lit, and the preview all follow the finder; only what differs is written here.

## Look

```
╭─ Identity file · ~/.ssh ─────────────╮ ╭─ id_ed25519 ────────────────────╮
│                                      │ │                                 │
│                                  5/5 │ │ -----BEGIN OPENSSH PRIVATE KEY  │   ← typing row: empty when it opens
│ ──────────────────────────────────── │ │ (key, 411 B)                    │
│ 󰉋 ..                                 │ │                                 │
│ 󰉋 work                               │ │                                 │
│ 󰈔 config                             │ │                                 │
│ 󰈔 id_ed25519                         │ │                                 │   ← cursor: the original value, its text Green
│ 󰈔 id_ed25519.pub                     │ │                                 │
│                                      │ │                                 │
╰─ Enter:choose Tab:filter Esc:cancel ─╯ ╰─────────────────────────────────╯
```

- **The root directory**: given by the app, it is the directory the list shows when it opens (e.g. sshu `~/.ssh`, webu
  `~/Downloads`). It is only a start, not a fence: the top row of the list is `..`, to go up.
- **The current directory is written in the title**, after the field's name (`Identity file · ~/.ssh`); a path too long
  is cut from the start (`…/sideproj/terminu`).
- **The typing row is empty when it opens** (the placeholder rule in [`input/README`](README.md)).
- **An icon before every row**: one for directories, one for files, coloured by file type (content colours, the app's
  choice; e.g. filu uses eza's colours). When the field already has a value, the cursor opens on that file, its text in
  Green (the current value).
- **What the preview shows**: a directory lists what is inside, a text file shows its content (line numbers in
  Overlay0), anything else its type and size.

## Keys

- **`Enter` in the list**: on a directory it **goes in** — the typed filter is cleared, the focus stays on the list, and
  the cursor rests on the first item below `..`; only on a file does it **choose**, write back and close. **A directory
  is never chosen.**
- **What is typed in the typing row**:
  - Plain text (`ed25`): a fuzzy filter on the current level, matched as filu does (bonus at word starts, after
    separators, camelCase, runs, in the file name itself).
  - A path (starting with `/` or `~/`): the list jumps to that directory.
  - With `*` or `?`: a wildcard. `*` matches within one level, `**` goes down every subdirectory (the usual shell glob
    rules): `~/Downloads/*.png` lists every png in Downloads, `~/.ssh/**/*.pem` finds every pem under `.ssh`.
- **Hint**: on the list, `Enter:into Tab:filter Esc:cancel` on a directory and `Enter:choose Tab:filter Esc:cancel` on a
  file; on the typing row `Enter/Tab:list Esc:cancel`.

**Why**: what this field wants is a file; `Enter` on a directory most obviously means going in to look inside. With the
directory written in the title, the typing row is left for filtering.

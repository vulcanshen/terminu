# file-picker (choosing a file)

**Language**: English · [繁體中文](file-picker-zh_TW.md)

## Purpose

Choosing one **file**, handed back as a value: sshu's Identity file, webu's Upload and Import. The file-picker is a
kind of finder ([`input/finder`](finder.md)): the skeleton, the two areas, `Tab`, `Enter` on the typing row entering the
list, which side is lit, and the preview all follow the finder; only what differs is written here.

## Look

```
┏━IDENTITY FILE · ~/.ssh━━━━━━━━━━━━━┓ ┏━id_ed25519━━━━━━━━━━━━━━━━━━━━┓
┃                                      ┃ ┃                                 ┃
┃                                  5/5 ┃ ┃ -----BEGIN OPENSSH PRIVATE KEY  ┃   ← typing row: empty when it opens
┃ ──────────────────────────────────── ┃ ┃ (key, 411 B)                    ┃
┃ 󰉋 ..                                 ┃ ┃                                 ┃
┃ 󰉋 work                               ┃ ┃                                 ┃
┃ 󰈔 config                             ┃ ┃                                 ┃
┃ 󰈔 id_ed25519                         ┃ ┃                                 ┃   ← cursor: the original value, its text Green
┃ 󰈔 id_ed25519.pub                     ┃ ┃                                 ┃
┃                                      ┃ ┃                                 ┃
┗━ Enter:choose Tab:filter Esc:cancel ━┛ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **The root directory**: given by the app, it is the directory the list shows when it opens (e.g. sshu `~/.ssh`, webu
  `~/Downloads`). It is only a start, not a fence: the top row of the list is `..`, to go up. The root
  directory `/` has no `..`.
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
  - Plain text (`ed25`): filters the current level, as "Matching" in [`finder`](finder.md) says (contains,
    case-insensitive).
  - A path (starting with `/` or `~/`): **the path stays on the typing row, split at its last `/`** — before it the
    directory (the list shows it, the title names it), after it the filter text (as "Matching" says). A half-typed path
    already works, and typing and pasting give the same result:

    | Typed | The list |
    |---|---|
    | `~/.ss` | shows `~`, filtered by `.ss`: `.ssh` is left, `Enter` goes in |
    | `~/.ssh/` | all of `~/.ssh` |
    | `~/.ssh/id_` | `id_ed25519` and `id_ed25519.pub` in `~/.ssh` |
    | `~/.ssh/id_ed25519` | that file on the first row, `Enter` chooses it |
    | `~/nope/x` | the directory does not exist: the list is empty, as with no results |

    **`..` is not supported in a path**: a `..` segment is not resolved upwards; it counts as a directory that does not
    exist, and the list is empty. To go up, use the list's `..` row, or `Backspace` away the last segment of the path.
  - With `*` or `?`: a wildcard. `*` matches within one level, `**` goes down every subdirectory (the usual shell glob
    rules): `~/Downloads/*.png` lists every png in Downloads, `~/.ssh/**/*.pem` finds every pem under `.ssh`. Each row
    shows the path relative to the starting point (the directory before the first `*` or `?`; e.g. `keys/a.pem`,
    `old/b.pem`), and the title names the starting point; the results are found by a search, not one directory level,
    so there is no `..`.
- **Hint**: on the list, `Enter:into Tab:filter Esc:cancel` on a directory and `Enter:choose Tab:filter Esc:cancel` on a
  file; on the typing row `Enter/Tab:list Esc:cancel`.

**Why**: what this field wants is a file; `Enter` on a directory most obviously means going in to look inside. With the
directory written in the title, the typing row is left for filtering. With the path kept on the typing row and split at
its last `/`, the list always shows the directory on the typing row, and there is no "when does it jump" to define:
typing `~/Documents/sideproj` one character at a time never jumps away and clears at `~/Documents`, only to take the
`/sideproj` typed next as a path under the root; `Backspace` on the last segment goes back up a level.

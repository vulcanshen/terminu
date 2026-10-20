# file-picker (choosing a file)

**Language**: English · [繁體中文](file-picker-zh_TW.md)

## Purpose

Choosing one **file**, handed back as a value: sshu's Identity file, webu's Upload and Import. When the value is a
directory, "Choosing a directory" below applies. The file-picker is a kind of finder ([`input/finder`](finder.md)): the
skeleton, the two areas, `Tab`, `Enter` on the typing row entering the list, which side is lit, and the preview all
follow the finder; only what differs is written here.

## Look

```
┏━IDENTITY FILE · ~/.ssh━━━━━━━━━━━━━━━━━━━┓ ┏━id_ed25519━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                            ┃ ┃                                             ┃
┃                                       6/6 ┃ ┃ -----BEGIN OPENSSH PRIVATE KEY-----         ┃
┃ ────────────────────────────────────────── ┃ ┃ (sensitive content not shown)               ┃
┃ 󰉋 ..                                       ┃ ┃                                             ┃
┃ 󰉋 work                                     ┃ ┃                                             ┃
┃ 󰈔 config                                   ┃ ┃                                             ┃
┃▓󰈔▓id_ed25519▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃ ┃                                             ┃
┃ 󰈔 id_ed25519.pub                           ┃ ┃                                             ┃
┃ 󰈔 known_hosts                              ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃ ─────────────────────────────────────────── ┃
┃                                            ┃ ┃ TYPE      private key                       ┃
┃                                            ┃ ┃ SIZE      411 B                             ┃
┃                                            ┃ ┃ MODIFIED  2026-09-30 14:02                  ┃
┃                                            ┃ ┃ MODE      -rw-------                        ┃
┃                                            ┃ ┃                                             ┃
┗━ Enter:choose Tab|/:filter Esc:cancel ━━━━━┛ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

The diagram shows `hide_secrets_in_preview` turned on; it is off by default, and then a private key shows in full like
any text file (see "Hiding secrets" below).

- **Four parts**: the typing row, the list, the preview and the metadata. The left box is "typing row / separator /
  list", the right box "preview / separator / metadata"; with a terminal under 96 wide, the metadata moves next to the
  list in a box of its own and the preview takes the full width below ("Layout" in [`finder`](finder.md)).
- **The root directory**: given by the app, it is the directory the list shows when it opens (e.g. sshu `~/.ssh`, webu
  `~/Downloads`). It is only a start, not a fence: the top row of the list is `..`, to go up. The root
  directory `/` has no `..`.
- **The current directory is written in the title**: the field's name (uppercase), then ` · `, then the directory (e.g.
  `IDENTITY FILE · ~/.ssh`); a path too long is cut from the start (`…/sideproj/terminu`).
- **It opens with the focus on the list**, like a select and a checkbox popup.
- **The typing row is empty when it opens** (the placeholder rule in [`input/README`](README.md)), with
  `nf-fa-angle_right` before it as in the finder.
- **The list's order**: `..` → directories → files, each sorted by name, case-insensitive.
- **Hidden files** (starting with `.`) are not listed by default; they are listed when the filter on the typing row (the
  last segment of a path) starts with `.` (`.ss` and `~/.ss` bring up `.ssh`). The same as shell globs: `*` does not
  match hidden files and `**` does not go into hidden directories, unless the pattern starts with `.`.
- **An icon before every row**: `nf-md-folder` (U+F024B) for directories, `nf-md-file` (U+F0214) for files, coloured by
  file type (content colours, the app's choice; e.g. filu uses eza's colours). When the field already has a value, the
  cursor opens on that file, its text in Green (the current value).

**Why**: a home directory holds dozens of hidden files, and listing them all would fill the top of the list; someone
looking for a hidden file types `.` anyway — the shell's own rule, with no toggle key to learn.

### The preview

The entry under the cursor, drawn by kind. At most 64 KB is read.

**Read in the background**: the preview and the metadata are not read while the screen is drawn, so typing and moving
the cursor never wait for them (on a remote or slow file system too). While it is being read, the preview frame has the
loading icon after its title (as when a finder lists while searching), the frame reads `(loading…)` in grey, and the
metadata values stay empty (not `—`, which means it could not be got); it is drawn once read. What has been read is kept
by path, so while the popup is open the cursor coming back to an entry does not read it again.

| Kind | Preview |
|---|---|
| directory | a tree (below) |
| archive (zip, tar, tar.gz, tar.bz2) | its contents as a directory tree |
| text file | the content, with syntax colours (chroma's catppuccin-mocha, foreground only) and line numbers (Overlay0, right-aligned, one space after); Tabs and control characters as in a [`dialog/note`](../dialog/note.md) viewer (a Tab as `input_tab_width` spaces, no `\r` of a CRLF, colour codes coloured, only the last state of a `\r` within a line, any other control character by name in Red) |
| PDF | a grey first row with the page count (`12 pages`), a blank row, then the text of the first 20 pages (at most 128 KB); `(no extractable text)` when there is none |
| image (png, jpg, gif, bmp, webp, tiff, ico, avif, heic) | a grey first row `data:image/png · 12.4 KB`, a blank row, then the base64 data URI wrapped at the preview's width; over 1 MB only `(1.4 MB — too large to inline as a data URI)` |
| anything else | hexadecimal, always 8 bytes a row, followed by ASCII (`89 50 4e 47 0d 0a 1a 0a  .PNG....`, 33 cells); a side-by-side preview is at most 56 cells wide, too narrow for 16 bytes |
| unreadable | `(unreadable)` |

**A directory's tree**: at most three levels. The first level has no branches; from the second on, `├─`, `└─` and `│`
join them, the branches in Overlay0; each entry's icon, colour and order are the same as in the list, and hidden files
are not listed. The preview takes no focus and cannot scroll: it is drawn until the preview area is full, with `…` on the
last row. An empty directory reads `(empty)`, an unreadable one `(permission denied)`, both in grey.

```
󰉋 keys
  ├─ 󰈔 a.pem
  └─ 󰉋 old
     └─ 󰈔 b.pem
󰈔 config
󰈔 id_ed25519.pub
…
```

A subdirectory is expanded to the bottom before the next one: a large subdirectory can fill the preview area and hide
the rest of the first level.

### Metadata

Always four rows, for files and directories alike, so the preview area keeps its height from entry to entry. Labels
in uppercase and the layer colour, values in Text; the label column as wide as the longest label, two cells before the
value (as in the one-value panel of [`layout/panel`](../layout/panel.md)).

| Label | File | Directory |
|---|---|---|
| `TYPE` | the preview's kind: `text`, `private key`, `image`, `PDF`, `archive`, `binary`; a symlink is `link → <target>` | `directory` |
| `SIZE` | `411 B`, `4.2 KB`, `3.4 MB` (powers of 1024, one decimal) | `12 items`, `1 item` for one (as in the list, hidden files not counted) |
| `MODIFIED` | `2026-09-30 14:02` (local time, to the minute) | the same |
| `MODE` | written as `ls -l` does: `-rw-------` | `drwx------` |

- `private key`: the first line is a private key's header (below). It does not depend on `hide_secrets_in_preview`;
  the kind is not a secret.
- **A symlink**: `SIZE`, `MODIFIED` and `MODE` are the **target's**, matching the preview — what is chosen is that file,
  and its `MODE` is the permission that actually applies. E.g. `/etc/localtime` reads `761 B` and `-rw-r--r--`, not the
  link's own `37 B` and `lrwxr-xr-x` (as `ls -l` writes them). That it is a link, and to where, `TYPE` already says.
- **A value that cannot be read is `—`**: the `SIZE` of an unreadable directory (its items cannot be counted; the time
  and permissions are written as usual); the `SIZE`, `MODIFIED` and `MODE` of a broken link; every row that cannot be
  read of a file gone since it was listed (deleted, moved). The four rows stay — no
  row is left out, and no `0 items`, which would read as empty.
- No path (the title and the list already have it), owner, or access and creation times: choosing a file does not need
  them.

**Why**: choosing a file means checking "is it this one" — kind, size, time modified; the permissions matter for a
private key (ssh wants `600`). `TYPE` uses the preview's kinds, so it tells what the preview will draw; the values are
written for people, not as MIME types or octal.

### Hiding secrets

The user's setting **`hide_secrets_in_preview`**, in each app's config file (Rules E3), defaults to `false`: everything
shows as usual. When it is on (`true`):

| File | Preview |
|---|---|
| the first line is a private key's header: it starts with `-----BEGIN` and contains `PRIVATE KEY` (OpenSSH, RSA, EC, PKCS#8, PGP), or starts with `PuTTY-User-Key-File-` | the first line, then the grey line `(sensitive content not shown)` |
| a file readable by its owner only (no read permission for group or other, e.g. `600`, `400`), of any kind; not a directory (`~/.ssh` itself is `700`) | not a single line, only that grey line |
| anything else | as usual |

The metadata shows as usual either way. The setting covers the previews in popups: the file-picker, and finders that
preview files or directories.

**Why**: in a local TUI, whether to hide is the user's call (turned on to share a screen or record a demo), and by
default it stays out of the way. It does not go by a list of file names (everything off the list slips through) or by
keywords in the content (`password_min_length` gets blocked, `pw:` slips through): a private key is told by its first
line, whatever it is named; other secret files by their permissions — readable by the owner only is the owner's or the
tool's own mark for "not for others" (ssh private keys, `~/.aws/credentials`, `~/.kube/config`, `.netrc` and `.pgpass`
are all `600`). A wrong guess errs on the safe side: an ordinary file that is held back just has no preview. A private
key's header is not itself a secret, and it shows which kind of key it is.

## Keys

- **`Enter` in the list**: on a directory it **goes in** — the typed filter is cleared, the focus stays on the list, and
  the cursor rests on the first item below `..`; only on a file does it **choose**, write back and close. **When choosing a
  file, a directory is never chosen** (choosing a directory: below).
- **What is typed in the typing row**:
  - Plain text (`ed25`): filters the current level, as "Matching" in [`finder`](finder.md) says (contains,
    case-insensitive).
  - A path (starting with `/` or `~/`): **the path stays on the typing row, split at its last `/`** — before it the
    directory (the list shows it, the title names it), after it the filter text (as "Matching" says). A half-typed path
    already works, and typing and pasting give the same result:

    | Typed | The list |
    |---|---|
    | `~/.ss` | shows `~`, filtered by `.ss`: `.ssh` is left (`Enter` to the list, `Enter` again to go in) |
    | `~/.ssh/` | all of `~/.ssh` |
    | `~/.ssh/id_` | `id_ed25519` and `id_ed25519.pub` in `~/.ssh` |
    | `~/.ssh/id_ed25519` | that file on the first row (`Enter` to the list, `Enter` again to choose it) |
    | `~/nope/x` | the directory does not exist: the list is empty, as with no results |

    **`..` is not supported in a path**: a `..` segment is not resolved upwards; it counts as a directory that does not
    exist, and the list is empty. To go up, use the list's `..` row, or `Backspace` away the last segment of the path.
  - With `*` or `?`: a wildcard. `*` matches within one level, `**` goes down every subdirectory (the usual shell glob
    rules): `~/Downloads/*.png` lists every png in Downloads, `~/.ssh/**/*.pem` finds every pem under `.ssh`. Each row
    shows the path relative to the starting point (the directory before the first `*` or `?`; e.g. `keys/a.pem`,
    `old/b.pem`), and the title names the starting point; the results are found by a search, not one directory level,
    so there is no `..`.
- **Hint**: on the list, `Enter:into Tab|/:filter Esc:cancel` on a directory and `Enter:choose Tab|/:filter Esc:cancel` on
  a file; on the typing row `Enter|Tab:list Esc:cancel`.

**Why**: what this field wants is a file; `Enter` on a directory most obviously means going in to look inside. With the
directory written in the title, the typing row is left for filtering. With the path kept on the typing row and split at
its last `/`, the list always shows the directory on the typing row, and there is no "when does it jump" to define:
typing `~/Documents/sideproj` one character at a time never jumps away and clears at `~/Documents`, only to take the
`/sideproj` typed next as a path under the root; `Backspace` on the last segment goes back up a level.

## Choosing a directory

A field whose value is a directory (e.g. where to download, a project's path) uses the file-picker's "choosing a
directory". Everything else is as above: the current directory in the title, paths typed on the typing row, the rule for
hidden directories, the preview drawing the tree of the directory under the cursor, the four rows of metadata.

```
┏━DOWNLOAD TO · ~/Downloads━━━━━━━━━━━━━━━━┓ ┏━Downloads━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                            ┃ ┃                                             ┃
┃                                       4/4 ┃ ┃ 󰉋 music                                     ┃
┃ ────────────────────────────────────────── ┃ ┃   ├─ 󰈔 a.flac                               ┃
┃▓󰉒▓. (this directory)▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃ ┃   └─ 󰈔 b.flac                               ┃
┃ 󰉋 ..                                       ┃ ┃ 󰉋 papers                                    ┃
┃ 󰉋 music                                    ┃ ┃   └─ 󰈔 tdp.pdf                              ┃
┃ 󰉋 papers                                   ┃ ┃ 󰈔 invoice.pdf                               ┃
┃                                            ┃ ┃ 󰈔 photo.jpg                                 ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃ ─────────────────────────────────────────── ┃
┃                                            ┃ ┃ TYPE      directory                         ┃
┃                                            ┃ ┃ SIZE      4 items                           ┃
┃                                            ┃ ┃ MODIFIED  2026-10-12 21:40                  ┃
┃                                            ┃ ┃ MODE      drwxr-xr-x                        ┃
┃                                            ┃ ┃                                             ┃
┗━ Enter:choose Tab|/:filter Esc:cancel ━━━━━┛ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **The list shows directories only**, no files: what a directory holds is in the preview's tree. The order is `.` →
  `..` → directories.
- **The first row is `.`** (`. (this directory)`), its icon `nf-md-folder_move` (U+F0252); the other directories keep
  their icon. `Enter` on `.` chooses the current directory — writes it back and closes; `Enter` on another directory goes
  in, as when choosing a file.
- **While the typing row holds a filter or a wildcard, there is no `.` row**: wildcard results list directories only,
  with no `.` (as they have no `..`). `Enter` on a directory in the results goes into it, and that level's `.` is back;
  to choose the current directory, clear the filter (or type the path up to a trailing `/`).
- **Hint**: `Enter:choose Tab|/:filter Esc:cancel` on `.`, `Enter:into Tab|/:filter Esc:cancel` on a directory.

**Why**: `Enter` goes into a directory whether choosing a file or a directory, so there is no "choose this directory"
key to learn; with `..` (the level above) already at the top of the list, one more row `.` (this level) reads at once.
No files: the list is kept for what can be chosen, and the preview is where to check the choice.

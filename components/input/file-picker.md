# file-picker (choosing a file)

**Language**: English · [繁體中文](file-picker-zh_TW.md)

## Purpose

Choosing one **file**, handed back as a value (sshu's Identity file, webu's Upload and Import). **It is a kind of finder**
(the user, 2026-10-07): the skeleton, the two areas, `Tab`, `Enter` while typing entering the list, which side is lit
and the preview follow the finder in [`search`](search.md); only what differs is written here. Made after filu's Search
(the user: filu put a lot of work into it).

## Look

```
╭─ Identity file ──────────────────────────────╮ ╭─ id_ed25519 ─────────────────────╮
│  ~/.ssh/█                                    │ │ -----BEGIN OPENSSH PRIVATE KEY-- │
│──────────────────────────────────────────────│ │ (key, 411 B)                     │
│ 󰉋 ..                                         │ │                                  │
│ 󰉋 work                                       │ │                                  │
│ 󰈔 config                                     │ │                                  │
│ 󰈔 id_ed25519                                 │ │                                  │
│ 󰈔 id_ed25519.pub                             │ │                                  │
╰─ Enter:list Tab:list Esc:cancel ─────────────╯ ╰──────────────────────────────────╯
```

- **The root directory**: given by the app, it is the directory the list shows when it opens (sshu `~/.ssh`, webu
  `~/Downloads`). It is a start, not a fence: the top row of the list is `..`, to go up.
- **An icon before every row**: one for directories, one for files, coloured by file type (filu uses eza's colours). When
  the field already has a value, the cursor opens on that file, its text in Green ("the chosen value" in
  [`color`](../color.md)).
- **What the preview shows**: a directory lists what is inside, a text file shows its content (line numbers in Overlay0),
  anything else its type and size.

## Keys

- **`Enter` in the list**: on a directory it **goes in**; only on a file does it **choose**, write back and close. **A
  directory is never chosen** (the user). This is where it differs from a plain finder, whose `Enter` means "go there",
  directories included.
- **What is typed in the input area** (wildcards are the user's, never done in the family yet; the other details are mine,
  unopposed):
  - Plain text (`ed25`): fuzzy filter on the current level, matched as filu does (bonus at word starts, after separators,
    camelCase, runs, in the file name itself).
  - A path (starting with `/` or `~/`): the list jumps to that directory.
  - `*` or `?`: a wildcard. `*` matches within one level, `**` goes down every subdirectory (the usual shell glob):
    `~/Downloads/*.png` lists every png in Downloads, `~/.ssh/**/*.pem` finds every pem under `.ssh`.

# tdp Family defaults

**Language**: English · [繁體中文](defaults-zh_TW.md)

The concrete values and habits the terminu family's apps have actually converged on.
**Using them is the easy path**: a new app that adopts them looks and behaves like its
siblings. **Departing from them is not a violation** and needs no written reason — as
long as the app still follows the [Rules](rules.md).

Cite as `tdp D3` and so on.

---

## D1 Layout and chrome

- **A one-row footer**, always reading:

  ```
  Space:menu ?:help Tab/1–N:panels q:quit
  ```

  Written like a hint (Rules M5); when too narrow, whole pairs are dropped from the end; keys
  Blue, colon and description Overlay0 (D2).
- **Panel capsules**: each panel's top border carries an `[N] label` capsule (powerline,
  rounded); `N` is also the digit key that jumps straight to that panel.
- **Apps with several screens**: a row of screen chips on top (`[W]eb ╱ [B]ookmarks …`),
  then a full-width divider that doubles as a progress bar during long work.
- **Narrow threshold**: below 72 columns (60 for apps with a narrower sidebar) only the
  focused side is drawn.
- **Empty states**: one centred fact, plus a hint naming the key (e.g. "No hosts — press
  `[A]` or `[Space]`").

## D2 Colour system

A complete colour scheme: **presentation rules + calculation + colour codes**. An app that
doesn't want to deal with colour adopts the whole set; an app that customises decides for
itself which parts to use and which not. Whether meaning is also expressed by means other
than colour (borders, symbols) is up to the app as well.

**Presentation rules**

1. **Few anchors, everything else derived**: pick three anchors first — background, user
   footprint, top popup layer — and derive every other level from them, instead of
   picking a colour for each element.
2. **Lightness is the z-axis, never reversed**: from the background up to the topmost
   popup, lightness moves in one direction, the higher the layer the lighter. A TUI has
   no shadows or elevation; lightness is the only tool that can say "which one is on top".
3. **Lightness bands are dedicated**: each meaning owns one lightness band, and no other
   meaning uses the same one (Principle P4). E.g. if "user footprint" uses lavender,
   popup borders don't use lavender.
4. **Warning colours stay out of the z-axis**: error and warning colours are the same
   colour on every layer, never brightening or dimming with the level.
5. **One key, two indicators** (Rules M9): the one that fires is bright, the other dim.
6. **Blur changes only the border**: an unfocused panel changes only its border colour
   and line style; its content is not dimmed.

**Calculation: dim (Rules F8)**

Rewrite every colour code (SGR) in the already-drawn screen, leaving text and layout alone:

```
dim(c) = c × 0.45 + base × 0.55        base = #1e1e2e
```

- Both foreground and background go through it; 16- and 256-colour codes are turned into
  RGB first.
- **Dimming never lightens a colour**: each channel takes the smaller of its original and
  dimmed value — a colour darker than base (e.g. `#000000`) would get lighter, so it keeps
  its original.
- Output is always 24-bit (`38;2;…` / `48;2;…`): the family requires a truecolor terminal
  (D6), so dimming need not step down to the terminal's colour depth.
- Text with no foreground of its own gets the dimmed default text colour (`dim(Text #cdd6f4)`).
- Bold, reverse, cursor movement and the text itself are untouched.
- filu's `internal/ui/dim.go` is the reference implementation.

**Calculation: popup borders interpolated by layer**

```
border colour of layer K = lerp(user footprint, top popup layer, K / N)    N = 4
for K ≥ N it stays at the top popup layer
```

With catppuccin-mocha plugged in (Lavender → Sapphire):

| layer | 1 | 2 | 3 | 4+ |
|---|---|---|---|---|
| Border colour | `#A4C0FA` | `#94C3F5` | `#84C5F0` | `#74c7ec` |

**Colour codes (catppuccin-mocha)**

| Use | Colour |
|---|---|
| Background | Base `#1e1e2e` |
| Focused border | Blue `#89b4fa`, double line `╔═╗` |
| Unfocused border | Surface2 `#585b70`, rounded `╭─╮` (same width as double, so switching shifts nothing) |
| Popup border | see the table above |
| What is being edited, user footprint | Lavender `#b4befe` |
| Error | Red `#f38ba8` |
| Worth noticing, not broken | Peach `#fab387` |
| Selection; a mode (its frame and the mode name at top right, Rules K11) | Yellow `#f9e2af` |
| Dim text; the colon and description in hints and the footer | Overlay0 `#6c7086` |
| Keys in hints, the footer and the key reference | Blue `#89b4fa` |
| Descriptions in the key reference | Text `#cdd6f4` |
| Hints on an unfocused panel's border: key / colon and description | Overlay0 `#6c7086` / Surface2 `#585b70` (Blue is the focus colour, kept for where the keys are) |

## D3 Popups

- One popup, one file, one animator.
- Title on the top border: glyph + text; hint set into the bottom border; one blank row
  above and below the content.
- Animation (Rules F2): 8 frames × 16 ms ≈ 128 ms, symmetric for opening and closing.
- **Loading icon** (Rules F7; taken from the icon webu shows while loading a URL):
  - Glyphs: Nerd Font `nf-md-circle_slice_1` to `_8` (U+F0A9E–U+F0AA5), eight frames, a
    circle filling slice by slice, then starting over.
  - Speed: 90 ms a frame, 720 ms a turn.
  - The frame comes from the clock, `frames[(now / 90ms) % 8]`, not a counter; the tick is
    only rescheduled while something is loading.
  - Width: one cell, the same as the static glyph it replaces, so nothing shifts (braille
    dots were tried; their shape and width don't fit).
  - Colour: the same as the text beside it; after a popup title, that layer's colour (bold).
- Toast: shown for 2200 ms, fixed at the bottom of the screen.
- `Esc` is handled in one place only (`closeTop`).
- The quit confirm is a popup of its own, on top of the whole stack: `Ctrl-C` may come while another confirm is open, and borrowing that one would overwrite the question the user is answering.
- "On top" means three places at once: key routing, `closeTop`, and drawing order.
- When the `?` key reference sits on another popup, it is on top in key routing and in drawing alike; boxes such as confirm and options take keys before the menu under them.
- Whether a layer is "still there" is judged by opening-or-open (`owns()`), never by an `isActive()` that includes closing (Rules F3).
- Confirm hint on the bottom border: `Enter:<verb> Esc:cancel` (e.g. `Enter:delete Esc:cancel`).
- When a bottom-border hint doesn't fit, whole items are dropped from the end (like the
  footer in D1), never cut mid-item.
- **Finder focus** (Rules F1): while typing, the filter row is lit and the list's cursor row
  is a faint highlight; after `Tab` to the list, the filter row is drawn all in grey
  (Overlay0, D2's dim text) rather than F8's fade, with no highlight or cursor, and the
  list's cursor row turns to the popup's layer colour behind dark bold text (like a menu's
  cursor row). Only the side holding the keys is lit, the same language as F8's "only the
  top is lit" (kbu `40a0573`).
- **The mode name label** (Rules K11): the junctions take the frame's colour and follow its
  line style — `╡` `╞` on a double frame, `┤` `├` on a single one; the name is bold in the
  mode colour; one word if possible (`Drag`, `Visual`, `Select`: a narrow panel has no room
  for two, and the whole top-right text would be dropped); when space runs out the title is
  clipped first and the mode name stays. A panel's `[N] label` capsule turns the mode colour
  with its frame (kbu `248f883`).
- Cancelling returns to the source; completing an action clears the whole stack (the
  usual answer to T1).

## D4 Menus

- Menu rows: ` [k]label` left-aligned, description right-aligned and dim.
- If the hotkey is the label's first letter, bracket it in place (`[r]ename`); if it is
  inside the word, bracket it there (`UR[L]`); otherwise put it in front (`[n] New`).
  Core keys are written into the label: `[Enter] Edit`.
- Inside a menu: `j/k` move (wrapping), `Enter` runs, hotkeys run directly; bottom hint
  `j/k:move Enter:run Esc:close`.
- The menu title is the focused panel's `[N] label`.
- Popup width follows Rules F7 throughout; a description too long for it wraps or is cut inside the box, never widening the box.
- A label that already shows its key (`[/] Search`) is not bracketed again.

## D5 Hotkey reference

**tdp does not define hotkeys** ([Principle P5](README.md#p5-fixed-zone-and-concept-zone)); this only
records what the family does today, for a new app that wants the easy path:

| Key | Habit |
|---|---|
| `j` `k` / `↑` `↓` | Move up and down; lists with a cursor wrap |
| `u` `d` / `Ctrl-U` `Ctrl-D` | Half a page |
| `gg` `G` | Top, bottom |
| `h` `l` | Switch tabs within a panel |
| `/` | Search |
| `1`–`9` | Jump to panel `[N]` |
| `z` / `Z` | Zoom |
| `Alt-Esc` | The PTY exit key (Rules K10); what it does is up to the app |
| In a text-selection mode: `h/j/k/l`, `w/b/e`, `0/$`, `gg/G`, `u/d` | Move as vim does: a cell, a word (`w` next word start, `b` previous word start, `e` word end), line start and end, top and bottom, half a page |

- **Quit flow** (tdp K9): confirm first when something would be lost (a transfer in
  progress, an unsaved draft).
- **Navigation letters are never bound to actions**: `j k u d g G h l` are reserved for
  movement, and no action takes them.
- **Case carries scope**: lower case acts on the item, upper case on the panel or the app.
- **Delete is `x`** (`d` is half a page).
- **`Alt-Esc` always confirms first**: whenever it would move focus out of the PTY or end the
  subprocess, whether or not the subprocess stays alive, a confirm comes first (`Enter`
  leaves, `Esc` returns to the PTY); what it does inside the PTY (e.g. stepping zoom down
  one level) needs no confirm. Why: terminals send an Alt chord as "`Esc` plus the key", so
  `Alt-Esc` is byte for byte two `Esc`s. When the app is busy the reading end stalls, and two
  `Esc` presses pile up and are read as `Alt-Esc` (measured 2026-09-29 with bubbletea
  v1.3.10: with keys already queued, two `Esc`s 150 ms apart still merged). Pressing `Esc`
  twice is common in vim; the confirm lets whoever misfired press `Esc` to go back.
- **Other Alt-chord exit keys** (e.g. kbu's `Alt-t` hiding Alterm, sshu's `Alt-Enter` on a
  locked cell) can be spelled the same way by "`Esc` then that key"; whether they confirm is
  up to the app.

## D6 Distribution and environment

- A single static binary built with goreleaser; `install.sh` / `uninstall.sh`
  (`curl | sh`, no sudo), also published to the Homebrew tap `vulcanshen/homebrew-tap`.
- Config in `$XDG_CONFIG_HOME/<app>` (falling back to `~/.config/<app>`); data in
  `~/.<app>/`.
- **Environment variable names**: `<APP IN CAPITALS>__<NAME>` — two underscores after the app
  name, the name in capitals with single underscores between words (e.g. `FILU__ICON_WIDTH`,
  `KBU__ALTERM_LOGIN_SHELL`). Every variable the app itself reads (tests and its own child
  processes included) is named this way. Shared names:

  | Variable | Meaning |
  |---|---|
  | `<APP>__CONFIG` | the config **directory** (the config file lives in it) |
  | `<APP>__STATE` | the state directory (when the app keeps state separately) |
  | `<APP>__DATA` | the data directory |
  | `<APP>__CACHE` | the cache directory |
  | `<APP>__ICON_WIDTH` | manual override of an icon's cell width (see the icons' real width below) |
  | `TERMINU__ICON_WIDTH` | shared by the family: an app with a PTY sets it for its child to say how wide an icon is (see below) |

  The exception: variables meant for another program follow that program's needs (e.g. the
  `LC_SSHU_COLORTERM` sshu carries over ssh to the remote end — OpenSSH forwards only `LANG`
  and `LC_*` by default). Renamed variables do not keep their old names.
- Requires a Nerd Font; PUA glyphs are written as code points in the source.
- Requires a truecolor (24-bit) terminal: catppuccin's pale colours and D2's layer gradient are indistinguishable in 256 colours, and dimming always outputs 24-bit (D2). READMEs say so in their requirements, next to the Nerd Font.
- Screen tests across sizes: at several terminal sizes, every line is exactly the terminal
  width (Rules L4).
- **The icons' real width**: with some fonts an icon takes two cells (the cursor moves two),
  while lipgloss measures one, and the borders go crooked. What counts is **how far the
  cursor actually moves**: a font whose icon looks wider than a cell but moves the cursor one
  (the glyph spills into the next cell) counts as one. The app detects this at startup (CPR:
  print an icon, ask for the cursor position), and every width measurement (padding,
  clipping, centring, joining, borders, overlaying popups) goes through one display-width
  function; the L4 screen tests also run once with two-cell icons, opening each kind of popup
  and measuring the bare box and the whole screen with it overlaid.
  - Reference implementation: filu `internal/ui/width.go` — `isWideIcon()`, `dispWidth()`,
    `dispClip()`, `padDisp()`, `dispCutLeft()`, `compositeDisp()` (replaces overlay's
    `Composite`, same interface), `centerDisp()` (replaces `lipgloss.Place`), `joinH()` /
    `joinV()` (replace `lipgloss.JoinHorizontal` / `JoinVertical`); detection is
    `DetectIconWidth()` in `iconwidth_unix.go`, called before `tea.NewProgram`; tests follow
    `d6_test.go`.
  - Manual override: the environment variable `<APP>__ICON_WIDTH` (filu's is
    `FILU__ICON_WIDTH`). Detection runs on unix only; Windows defaults to one cell,
    overridden by the variable.
  - **Inside another app's PTY**: the probe is answered by the outer app's terminal
    emulator, which counts an icon as one cell, so the real width can't be measured. An app
    with a PTY therefore sets `TERMINU__ICON_WIDTH=<the cells it uses>` in its child's
    environment, and every app takes the icon width from `<APP>__ICON_WIDTH`, then
    `TERMINU__ICON_WIDTH`, then the probe. Any family app running inside another's PTY then
    gets it right (filu in kbu's Alterm, kbu in filu's shell). Environment variables don't
    cross ssh; remote nesting relies on the app's own channel (sshu's nesting channel).
  - An overlaid popup may be wider or taller than the screen (the frame drawn during a
    resize still has the old size): start at 0 and clip what falls off the screen, and
    **never panic**; when it is larger in both directions it is clipped too, never handed
    back whole. The edge-case tests cover all three (filu's `TestD6CompositeDispOversized`).
  - Done means: apart from the width functions themselves, `internal/ui` has no calls to
    `lipgloss.Width`, `lipgloss.Size`, `lipgloss.Place`, `ansi.StringWidth` or
    `ansi.Truncate`.
- `docs/icon.svg` is the family mark; the splash (Rules, chapter S) is drawn from it cell
  for cell, with a test keeping the two identical.
- `V` is reserved for the splash (Rules S1).
- Demo gifs are recorded with VHS, scripts in `.local/demos/`; the README carries a single
  representative gif.

## D7 Documentation

**README**: `README.md` (English) and `README-zh_TW.md` (Traditional Chinese) stay in
step, and cover only what users need to know:

1. Title, badges, language switch (`English · 繁體中文`)
2. A one-line positioning plus a paragraph on what it can do
3. **One** representative demo gif
4. Features: what users get, not how it is done
5. Installation: prerequisites, how to install, what happens on first launch, removal
6. Quick start
7. Usage and keys
8. Configuration and where data is stored
9. Limitations (written in the user's language)
10. Related links: CHANGELOG, `docs/dev-remarks.md`
11. terminu family: follows terminu design, lists the other family members
12. License

No "status" section with a hard-coded version number — versions are left to the badge and
the CHANGELOG.

Where the README talks about the icon width (usually the Nerd Font part of the
prerequisites), it names both `<APP>__ICON_WIDTH` and `TERMINU__ICON_WIDTH`, and says the
latter is shared by the whole family: set it once and every family app reads it; inside a
family app's PTY the outer app sets it (D6). The form is free (a table or a sentence). It
names no font as "always two cells" — the same font may move the cursor differently on
different terminals.

**`docs/dev-remarks.md`** (Traditional Chinese): what developers need to remind themselves
of during development, and decisions recorded while working with AI.

```
# <app> 開發者備忘
前言（一句話 + 遵循 terminu design principle）
## 運作方式
## 設計決定（決定 + 理由）
## 已否決，不要重提
## 已知的牆與未做
## 偏離 tdp（哪一條、在哪裡、為什麼）
## 設計文件導讀
## 建置與開發
## 發布（含踩過的坑）
```

The skeleton above is kept in Chinese because the file itself is written in Chinese. In
order: title (`<app>` developer notes), a preface (one sentence + follows the terminu
design principle), how it works, design decisions (decision + reason), rejected — do not
raise again, known walls and not done, the "偏離 tdp" section (departures from tdp:
which rule, where, why), a guide to the design documents, building and development,
releasing (including pitfalls hit).

**`docs/<app>-terminu-fix.md`**: where the app does not yet follow tdp, item by item, to
fix (which rule is violated, where, the current state, and how to fix it).

**Other design documents** (`ui.md`, `ux.md`, `function.md`…) are each app's own
business — whether to have them and how to split them is not tdp's concern; the design
documents guide in dev-remarks points to them. There is no separate clause-by-clause map
against tdp: what complies needs no record, departures go in dev-remarks, violations in
the fix file.

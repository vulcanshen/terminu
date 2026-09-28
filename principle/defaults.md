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
  space menu   ? help   tab/1-N panels   q quit
  ```

  When too narrow, whole pairs are dropped from the end; keys are bright, descriptions dim.
- **Panel capsules**: each panel's top border carries an `[N] label` capsule (powerline,
  rounded); `N` is also the digit key that jumps straight to that panel.
- **Apps with several screens**: a row of screen chips on top (`[W]eb ╱ [B]ookmarks …`),
  then a full-width divider that doubles as a progress bar during long work.
- **Narrow threshold**: below 72 columns (60 for apps with a narrower sidebar) only the
  focused side is drawn.
- **Empty states**: one centred fact, plus a hint naming the key (e.g. "No hosts — press
  `[A]` or `Space`").

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
| Selection | Yellow `#f9e2af` |
| Dim text, hints | Overlay0 `#6c7086` |

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
- Confirm hint on the bottom border: `Enter <verb> · Esc cancel`.
- Cancelling returns to the source; completing an action clears the whole stack (the
  usual answer to T1).

## D4 Menus

- Menu rows: ` [k]label` left-aligned, description right-aligned and dim.
- If the hotkey is the label's first letter, bracket it in place (`[r]ename`); if it is
  inside the word, bracket it there (`UR[L]`); otherwise put it in front (`[n] New`).
  Core keys are written into the label: `[Enter] Edit`.
- Inside a menu: `j/k` move (wrapping), `Enter` runs, hotkeys run directly; bottom hint
  `j/k move · Enter run · Esc close`.
- The menu title is the focused panel's `[N] label`.
- Popup width follows Rules F7 throughout; a description too long for it wraps or is cut inside the box, never widening the box.
- A label that already shows its key (`[/] Search`) is not bracketed again.

## D5 Hotkey reference

**tdp does not define hotkeys** ([Principle P5](README.md#p5-fixed-zone-and-concept-zone)); this only
records what the family does today, for a new app that wants the easy path:

| Key | Habit |
|---|---|
| `j` `k` / `↑` `↓` | Move up and down; lists with a cursor wrap |
| `u` `d` / `Ctrl-u` `Ctrl-d` | Half a page |
| `gg` `G` | Top, bottom |
| `h` `l` | Switch tabs within a panel |
| `/` | Search |
| `1`–`9` | Jump to panel `[N]` |
| `z` / `Z` | Zoom |

- **Quit flow** (tdp K9): confirm first when something would be lost (a transfer in
  progress, an unsaved draft).
- **Navigation letters are never bound to actions**: `j k u d g G h l` are reserved for
  movement, and no action takes them.
- **Case carries scope**: lower case acts on the item, upper case on the panel or the app.
- **Delete is `x`** (`d` is half a page).

## D6 Distribution and environment

- A single static binary built with goreleaser; `install.sh` / `uninstall.sh`
  (`curl | sh`, no sudo), also published to the Homebrew tap `vulcanshen/homebrew-tap`.
- Config in `$XDG_CONFIG_HOME/<app>` (falling back to `~/.config/<app>`), overridable
  with `<APP>_CONFIG`; data in `~/.<app>/`.
- Requires a Nerd Font; PUA glyphs are written as code points in the source.
- Requires a truecolor (24-bit) terminal: catppuccin's pale colours and D2's layer gradient are indistinguishable in 256 colours, and dimming always outputs 24-bit (D2). READMEs say so in their requirements, next to the Nerd Font.
- Screen tests across sizes: at several terminal sizes, every line is exactly the terminal
  width (Rules L4).
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

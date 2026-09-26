# tdp Family defaults

**Language**: English · [繁體中文](defaults-zh_TW.md)

The concrete values and habits the terminu family's apps have converged on. **Using them
is the easy path**: a new app that adopts them looks and behaves like its siblings.
**Departing from them is not a violation** and needs no written reason — as long as the
app still follows the [Rules](rules.md).

Cite as `tdp D3` and so on.

---

## D1 Layout and chrome

- **A one-row footer**, always:

  ```
  space menu   ? help   tab/1-N panels   q quit
  ```

  When too narrow, whole pairs are dropped from the end; keys are bright, descriptions dim.
- **Panel capsules**: each panel's top border carries an `[N] label` capsule (powerline,
  rounded); `N` is also the digit key that jumps straight to that panel.
- **Apps with several screens**: a row of screen chips on top (`[W]eb ╱ [B]ookmarks …`),
  then a full-width divider that doubles as a progress bar during long work.
- **Narrow threshold**: below 72 columns (60 for apps with a narrow sidebar) only the
  focused side is drawn.
- **Empty states**: one centred fact, plus a hint naming the key (e.g. "No hosts — press
  `[A]` or `Space`").

## D2 Colour (catppuccin-mocha)

| Use | Colour |
|---|---|
| Background | Base `#1e1e2e` |
| Focused border | Blue `#89b4fa`, double line `╔═╗` |
| Unfocused border | Surface2 `#585b70`, rounded `╭─╮` (same width as double, so switching shifts nothing) |
| Popup border, layer 1 → 4+ | `#A4C0FA` → `#94C3F5` → `#84C5F0` → Sapphire `#74c7ec` |
| What is being edited, user footprint | Lavender `#b4befe` (**never on popup borders**) |
| Error | Red `#f38ba8` |
| Worth noticing, not broken | Peach `#fab387` |
| Selection | Yellow `#f9e2af` |
| Dim text, hints | Overlay0 `#6c7086` |

- An unfocused panel **only changes its border**; its content is not dimmed.

## D3 Popups

- One popup, one file, one animator.
- Title on the top border: glyph + text; hint set into the bottom border; one blank row
  above and below the content.
- Animation: 8 frames × 16 ms ≈ 128 ms.
- Toast: shown for 2200 ms, fixed at the bottom of the screen.
- `Esc` is handled in one place only (`closeTop`).
- `Space` on any **non-input** popup closes it.
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
- If only one row is runnable, `Space` runs it directly instead of opening the menu.
- The menu title is the focused panel's `[N] label`.

## D5 Key habits

**These are hotkeys, which tdp does not define** ([Principle P5](README.md#p5-out-of-scope-letter-hotkeys));
they are listed because most of the family does it this way:

| Key | Habit |
|---|---|
| `j` `k` / `↑` `↓` | Move up and down; lists with a cursor wrap |
| `u` `d` / `Ctrl-u` `Ctrl-d` | Half a page |
| `gg` `G` | Top, bottom |
| `h` `l` | Switch tabs within a panel |
| `/` | Search |
| `1`–`9` | Jump to panel `[N]` |
| `q` | Quit; confirm first when something would be lost (a transfer in progress, an unsaved draft) |
| `V` | Splash easter egg; not shown at start-up, not listed in menus |
| `z` / `Z` | Zoom |

- **Navigation letters are never bound to actions**: `j k u d g G h l` are reserved for
  movement.
- **Case carries scope**: lower case acts on the item, upper case on the panel or the app.
- **Delete is `x`** (`d` is half a page).

## D6 Distribution and environment

- A single static binary built with goreleaser; `install.sh` / `uninstall.sh`
  (`curl | sh`, no sudo), also published to the Homebrew tap `vulcanshen/homebrew-tap`.
- Config in `$XDG_CONFIG_HOME/<app>` (falling back to `~/.config/<app>`), overridable
  with `<APP>_CONFIG`; data in `~/.<app>/`.
- Requires a Nerd Font; PUA glyphs are written as code points in the source.
- `docs/icon.svg` is the family mark; the splash is drawn from the icon cell for cell,
  with a test keeping the two identical.
- Demo gifs are recorded with VHS, scripts in `.local/demos/`; the README carries a single
  representative gif.

## D7 Documentation

- `README.md` (English) and `README-zh_TW.md` (Traditional Chinese) stay in step and cover
  only what users need to know.
- `docs/dev-remarks.md` (Traditional Chinese): decisions made during development, their
  reasons, rejected approaches, departures from tdp, building and releasing.
- `docs/<app>-terminu-fix.md`: where the app does not yet follow tdp, item by item, to fix.

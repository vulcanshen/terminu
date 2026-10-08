# color: Colour

**Language**: English · [繁體中文](color-zh_TW.md)

A complete colour scheme: **presentation rules + calculation + colour codes**, used across the family. Moved here from
defaults D2 on 2026-10-07, from a default to a requirement (the user; it used to read "an app that doesn't want to deal
with colour adopts the whole set; an app that customises decides which parts to use"). Whether meaning is also expressed by
means other than colour (borders, symbols) is up to the app — except where the rules say otherwise (e.g. focus is not told
by colour alone, L5).

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
6. **An unfocused panel** changes its border colour and line style, and its content is
   dimmed as in F8, streaming content excepted (Rules T2, since 2026-10-07; before, the
   content was not dimmed).

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
  (rules E4), so dimming need not step down to the terminal's colour depth.
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
| The chosen value (the chosen or ticked rows of a select or a checkbox group; added 2026-10-07) | Green `#a6e3a1` |
| Selection; a mode (its frame and the mode name at top right, Rules K11) | Yellow `#f9e2af` |
| Dim text; the colon and description in hints and the footer | Overlay0 `#6c7086` |
| Keys in hints, the footer and the key reference | Blue `#89b4fa` |
| Descriptions in the key reference | Text `#cdd6f4` |
| Hints on an unfocused panel's border: key / colon and description | Overlay0 `#6c7086` / Surface2 `#585b70` (Blue is the focus colour, kept for where the keys are) |

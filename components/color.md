# color (colour scheme)

**Language**: English · [繁體中文](color-zh_TW.md)

A complete colour scheme: **presentation rules + colour codes + calculation**, used across the family. Whether a meaning
is also expressed by means other than colour (borders, symbols) is up to the app — except where the rules say otherwise
(e.g. focus is not told by colour alone, L5). The colours of the content itself (file types, pod states, log levels,
syntax highlighting) are up to the app; this file governs the interface elements tdp defines (Principle P4).

## Presentation rules

1. **Few anchors, everything else derived**: pick three anchors first — the background, the user footprint, the popups'
   end colour — and derive every other level from them, instead of picking a colour for each element.
2. **The layer colour is the z-axis**: a popup's frame and title take the layer colour. It starts at the user footprint
   (Lavender) and ends at Sapphire, in N = 4 steps; layer K takes step K, and layer N and above stay at the end colour.
   The bottom popup is layer 1; a toast is not a layer and always takes the colour of layer 1 (Rules F1).
3. **Colours are dedicated**: each meaning owns one colour, and no other meaning uses the same one (Principle P4). E.g.
   "user footprint" uses Lavender, so popup frames don't use Lavender — the layer colour starts from it, but layer 1 has
   already moved one step towards the end.
4. **Warning colours do not change with the layer**: errors and warnings are the same Red and Peach on every layer; when
   covered, they are dimmed with the rest as F8 says.
5. **What is lit is what has the focus** (Principle P6): everything but the top layer is dimmed (F8), an unfocused panel
   is dimmed (T2, streaming content excepted), of one key's two indicators the one that fires is lit (M9), and the cursor
   on a part without the focus is dimmed.
6. **Bold is used only for**: text on the cursor, popup titles, text in capsules, mode names, and the loading icon after
   a title.

## Colour codes (catppuccin-mocha)

| Meaning | Used for | Colour |
|---|---|---|
| Background | the screen's background; what dimming fades towards | Base `#1e1e2e` |
| Focus | the focused frame (double line `╔═╗`); keys that can be pressed now in hints, the footer and the key reference; the labels and header row of the focused panel; the screen chip row | Blue `#89b4fa` |
| Unavailable | an unfocused frame (rounded `╭─╮`, the same width as the double line, so switching shifts nothing); disabled rows, labels and options; days out of range | Surface2 `#585b70` |
| Layer colour | a popup's frame and title; the cursor block in a popup | see "Popup layer colours" below |
| Being edited, user footprint | the value and the text cursor in an input popup; positions the user leaves behind (the "you are here" of breadcrumbs, the "where you are now" values on the statusbar) | Lavender `#b4befe` |
| In effect | the value now in effect (the one a select chose, the ticked ones, the ones switched on); live sessions; work in progress and progress bars; what completed successfully | Green `#a6e3a1` |
| Mode | a mode's frame and mode name, the range selected in a mode (Rules K11) | Yellow `#f9e2af` |
| Warning: worth noticing, not broken | the warning sentence in a confirm; the text of a Warning toast | Peach `#fab387` |
| Error | the error row, a label in error, the error popup, the text of an Error toast, pasted `\n` `\t` | Red `#f38ba8` |
| Dim text | descriptions and section titles in a menu; the colon and description in hints and the footer; description rows; grey suggestions; the description of an empty value; an unfocused typing row; empty states; separators (inside popups, below the screen chip row) | Overlay0 `#6c7086` |
| Normal text | values in forms and panels; menu labels; descriptions in the key reference | Text `#cdd6f4` |
| Panel cursor | the background of the cursor row in a panel, its text Base bold | Subtext1 `#bac2de` |
| Button | the background of an unfocused button, its text in Text | Surface1 `#45475a` |

- **The cursor block**: the layer colour as its background in a popup, Subtext1 in a panel, the text Base bold in both;
  a cursor on a part without the focus is the focused cursor dimmed once more (P6).
- Text placed on a cursor block always turns Base; its original colour is not kept.

## Popup layer colours

```
layer colour of layer K = lerp(user footprint, end colour, K / N)    N = 4
for K ≥ N it stays at the end colour
```

With catppuccin-mocha plugged in (Lavender → Sapphire):

| Layer | 1 | 2 | 3 | 4+ |
|---|---|---|---|---|
| Layer colour | `#A4C0FA` | `#94C3F5` | `#84C5F0` | `#74c7ec` |

## Dimming (Rules F8, T2)

Rewrite every colour code (SGR) in the already-drawn screen, leaving text and layout alone:

```
dim(c) = c × 0.45 + base × 0.55        base = #1e1e2e
```

- Both foreground and background go through it; 16- and 256-colour codes are turned into RGB first.
- **Dimming never lightens a colour**: each channel takes the smaller of its original and dimmed value — a colour darker
  than base (e.g. `#000000`) would get lighter, so it keeps its original.
- Output is always 24-bit (`38;2;…` / `48;2;…`): the family requires a truecolor terminal (Rules E4), so dimming need not
  step down to the colour depth.
- Text with no foreground of its own gets the dimmed default text colour (`dim(Text #cdd6f4)`).
- Bold, reverse, cursor movement and the text itself are untouched.
- **The drawn screen is dimmed once**: what is already dimmed (an unfocused panel) gets a little darker again under a
  popup, which shows where the focus was before the popup opened (F8).

> **Implementation reference (not a requirement)**: filu's `internal/ui/dim.go`.

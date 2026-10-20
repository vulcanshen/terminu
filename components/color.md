# color (colour scheme)

**Language**: English · [繁體中文](color-zh_TW.md)

A complete colour scheme: **presentation rules + colour codes + calculation**, used across the family. Whether a meaning
is also expressed by means other than colour (borders, symbols) is up to the app — except where the rules say otherwise
(e.g. focus is not told by colour alone, L5). The colours of the content itself (file types, pod states, log levels,
syntax highlighting) are up to the app; this file governs the interface elements tdp defines (Principle P4).

## Presentation rules

1. **Few anchors, everything else derived**: pick three anchors first — the background, the user footprint, the popups'
   end colour — and derive every other level from them, instead of picking a colour for each element.
2. **The layer colour is the z-axis**: a popup's frame and title take the layer colour (Red for the error popup, see
   [`dialog/note`](dialog/note.md)). It starts at the user footprint (Lavender) and ends at Sapphire, in N = 4 steps;
   layer K takes step K, and layer N and above stay at the end colour. The bottom popup is layer 1; a toast is not a
   layer and always takes the colour of layer 1 (Rules F1).
3. **Colours are dedicated**: each meaning owns one colour, and no other meaning uses the same one (Principle P4). E.g.
   "user footprint" uses Lavender, so popup frames don't use Lavender — the layer colour starts from it, but layer 1 has
   already moved one step towards the end.
4. **Warning colours do not change with the layer**: errors and warnings are the same Red and Peach on every layer; when
   covered, they are dimmed with the rest as F8 says.
5. **What is lit is what has the focus** (Principle P6): everything but the top layer is dimmed (F8), an unfocused panel
   is dimmed (T2, streaming content excepted), of one key's two indicators the one that fires is lit (M9), and the cursor
   on a part without the focus is dimmed.
6. **Bold is used only for**: text on the cursor, popup titles, text in selected capsules, mode names, the loading icon
   after a popup title, the splash's name (Rules S5), and the app's name in the middle of a screen smaller than the
   app's minimum size (Rules L1, [`layout/screen`](layout/screen.md)).

## Colour codes (catppuccin-mocha)

| Meaning | Used for | Colour |
|---|---|---|
| Background | not painted on the screen; used where a background colour has to be written out: text on a block (the cursor, capsules), the unfilled side of a capsule seam, what dimming fades towards | Base `#1e1e2e` |
| Focus | the focused frame (heavy line `┏━┓`); keys that can be pressed now in hints, the footer and the key reference; the labels and a list's header row in the focused panel; the screen chip row | Blue `#89b4fa` |
| Unavailable | an unfocused frame (light line `┌─┐`, the same width as the heavy line, so switching shifts nothing); disabled rows, labels and options; a checkbox option not available (a state only, still tickable); days out of range | Surface2 `#585b70` |
| Layer colour | a popup's frame (heavy line `┏━┓`) and the fill of its title capsule; the cursor block in a popup | see "Popup layer colours" below |
| Being edited, user footprint | the value and the text cursor in an input popup; positions the user leaves behind (a panel's location row — the breadcrumb, the current path or the level drilled down to, see [`layout/panel`](layout/panel.md); the "where you are now" values on the statusbar) | Lavender `#b4befe` |
| In effect | the value now in effect (the one a select chose, the ticked ones, the ones switched on; in a popup it follows the tick on screen, read as "the value `Enter` gives"); live sessions; work in progress and progress bars (a single-screen app writes it in the work's own row, see [`layout/screen`](layout/screen.md)); what completed successfully (the text of a Success toast) | Green `#a6e3a1` |
| Mode | a mode's frame and mode name, the range selected in a mode, the row held in a Drag (Rules K11) | Yellow `#f9e2af` |
| Warning: worth noticing, not broken | the warning sentence in a confirm; the text of a Warning toast | Peach `#fab387` |
| Error | the error row, a label in error, the error popup, the text of an Error toast, control characters drawn by name (`\n`, `\x1b`…, "Control characters" in [components](README.md); their background, with Base text, while the cursor rests on one) | Red `#f38ba8` |
| Dim text | descriptions and section titles in a menu; the header row of a one-value-per-row panel; the colon and description in hints and the footer, and the `\|` between keys (`j\|k`); description rows; grey suggestions; the description of an empty value; an unfocused typing row; empty states; the hint under the name on a screen smaller than the minimum size; separators (inside popups, below the screen chip row) | Overlay0 `#6c7086` |
| Normal text | values in forms and panels; menu labels; descriptions in the key reference | Text `#cdd6f4` |
| Panel cursor | the background of the cursor row in a panel, its text Base bold | Subtext1 `#bac2de` |
| Button | the background of an unfocused button, its text in Text | Surface1 `#45475a` |

- **The cursor block**: the layer colour as its background in a popup, Subtext1 in a panel, the text Base bold in both;
  a cursor on a part without the focus is the focused cursor dimmed once more (P6).
- **Searching in text** (e.g. a viewer's `/`) adds no colour: every match is underlined and keeps its own colour; the
  current match is drawn as the cursor block, meaning "you are here". The mode's Yellow is kept for a selected range;
  searching does not use it.
- Text placed on a cursor block always turns Base; its original colour is not kept. **Swatches are the exception**:
  cells whose content is a colour (the `███` of a colour value in a form or on a panel, the cells kamonu draws a mark
  in) keep their own colour, while the other text on the block still turns Base. The colour is that cell's value, and
  it matters most just when it is about to be changed.
- **The screen's background is not painted**: cells with no background of their own are left to the terminal's own
  background. When the terminal's background is not Base, a small patch of Base shows at a capsule seam and dimming leans
  towards Base; the family colours are designed for a dark background, so on a dark terminal the difference is small.

**Why**: the user's terminal theme, transparency and background image stay; none of the family apps paints the
background today, so moving to the shared lib does not change the screen.

## Popup layer colours

```
layer colour of layer K = lerp(user footprint, end colour, K / N)    N = 4
for K ≥ N it stays at the end colour
```

Each channel is rounded half up (.5 goes up), as in dimming.

With catppuccin-mocha plugged in (Lavender → Sapphire):

| Layer | 1 | 2 | 3 | 4+ |
|---|---|---|---|---|
| Layer colour | `#A4C0FA` | `#94C3F5` | `#84C5F1` | `#74c7ec` |

- **A closing popup does not count toward K**: once it starts closing it is no longer the top (the open and close
  animation in [`layout/popup`](layout/popup.md)). When a target opens while its source closes (Rules T1), the target
  takes the layer colour of the layer it ends up on from its first frame, and nothing changes colour when the source
  is gone.

## Dimming (Rules F8, T2)

Rewrite every colour code (SGR) in the already-drawn screen, leaving text and layout alone:

```
dim(c) = c × 0.45 + base × 0.55        base = #1e1e2e
```

- Both foreground and background go through it; 16- and 256-colour codes are turned into RGB first: colours 16–255 of the
  256 by their standard values; 0–15 (the 16 colours) by the terminal's palette — asked with OSC 4 at startup (at the
  same time as the icon-width probe of Rules E5), with the xterm defaults when there is no answer.
- **Each channel is rounded half up** (.5 goes up) before it is compared with the original.
- **Dimming never lightens a colour**: each channel takes the smaller of its original and dimmed value — a colour darker
  than base (e.g. `#000000`) would get lighter, so it keeps its original.
- Output is always 24-bit (`38;2;…` / `48;2;…`): the family requires a truecolor terminal (Rules E4), so dimming need not
  step down to the colour depth.
- Text with no foreground of its own gets the dimmed default text colour (`dim(Text #cdd6f4)`).
- Bold, reverse, cursor movement and the text itself are untouched.
- **The drawn screen is dimmed once**: what is already dimmed (an unfocused panel) gets a little darker again under a
  popup, which shows where the focus was before the popup opened (F8).

**Why**: what the 16 colours actually look like is set by the user's palette; dimmed by the xterm values, the hue jumps
when the palette is not xterm's — e.g. with the palette's blue set to `#89b4fa`, dimming the xterm `(0,0,238)` gives a
saturated dark blue `(0,0,132)`, while the actual colour dims to a greyish blue `(78,98,138)`, breaking "the same
colour, only fainter". With no answer, the xterm values are what the family apps use today.

> **Implementation reference (not a requirement)**: filu's `internal/ui/dim.go` (the xterm 16 colours are there). Asking
> for the palette: send the 16 queries `ESC ] 4 ; n ; ? ESC \` (n = 0–15) together, followed by a DA1 (`ESC [ c`); the
> terminal answers in order with `ESC ] 4 ; n ; rgb:RRRR/GGGG/BBBB` (take the high 8 bits of each channel), and a colour
> still unanswered when the DA1 reply arrives is not available — a terminal without OSC 4 still answers DA1, so there is
> no timeout to wait for. If DA1 is not answered either, after an overall timeout (e.g. 200ms) all of them take the xterm
> values.

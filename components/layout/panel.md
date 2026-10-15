# panel (frame, lists, values and filter)

**Language**: English · [繁體中文](panel-zh_TW.md)

A panel's frame, ordinary lists (groups included), panels with one value per row, details, and the panel filter. How the whole screen is laid out is
in [`screen`](screen.md).

## Frame

- **Line style and colour**: Blue heavy line `┏━┓` when focused, Surface2 light square line `┌─┐` when not; both are
  the same width, so switching shifts nothing (Rules L5, [`color`](../color.md)). Unfocused, the content is dimmed, streaming
  content excepted (Rules T2).
- **Left of the top border: the `[N] label` capsule**, right after the corner. `N` is also the digit key that jumps
  straight to that panel (within the current screen only, Rules K1). When the panel has tabs, `[N]` is a part of its
  own, the tabs follow it, and the first tab's name is the label (see the capsule chain below). While the panel is loading, the loading icon sits after the whole capsule chain (tabs
  included), with one space on each side (e.g. `┏[2] PODSEVENTSYAML 󰪞 ━━━┓`; the loading in [`popup`](popup.md)).
- **Right of the top border: the mode name** (Rules K11), set between two border junctions like a tag inlaid in the
  frame: `┏[1] KINDS━━━┫Drag┣━┓`, `┏━YAML━━━━┫Visual┣━┓`. The junctions take the frame's colour and follow its
  line style — `┫` `┣` on a heavy frame (a focused panel, a popup), `┤` `├` on a light one (an unfocused panel); the mode
  name is bold in the mode colour, its case as written. The mode name is
  one word if possible (`Drag`, `Visual`, `Select`: a narrow panel has no room for two, and the whole top-right text
  would be dropped); when space runs out, the title is clipped first and the mode name stays. The capsule turns the mode
  colour along with the frame.
- **Left of the bottom border: the hint**, which every panel must have — the exceptions are while the focus is on a
  panel filter's typing row and while it is in a PTY in the panel: no hint then, and it comes back on the list or on
  leaving the PTY. Right of the bottom border: the scroll position
  (see "Ordinary lists" below).
- **Text on the frame always keeps one line segment away from the corner**; only the `[N] label` capsule sits right after
  the top-left corner: the hint is `┗━ Enter:logs`, the scroll position `3 of 40 ━┛`, the mode name `┫Drag┣━┓`.

```
┏[2] PODS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ ...                                             ┃
┗━ .:helm Enter:logs ━━━━━━━━━━━━━━━━━━━ 3 of 40 ━┛
```

**Hint**: written like the hint in [`popup`](popup.md). It holds this panel's own keys — what `Enter` does here, the
common hotkeys; not the movement keys, nor the core keys the footer already has; all the keys are in the Space menu and
`?`. When focused, keys Blue and descriptions Overlay0; unfocused, it stays and is dimmed with the panel. When it does
not fit, whole pairs are dropped from the end, and the scroll position stays.

**Why**: the hint on a panel's bottom border tells the user "what pressing what does on this panel", while the footer
covers only the keys common to the whole screen; each covers one level, and with every panel having one, the user's eyes
know where to look when changing panels. No hint while typing in a panel filter: the hint lists the panel's own hotkeys,
which are all characters while typing (Rules K8), and listing them would teach the wrong keys; the footer already shows
the keys for typing. The same in a PTY: the panel's keys all go to the subprocess, and the exit keys that do not are
already in the footer ([`screen`](screen.md)). Text on the frame keeps away from the corners, the capsule alone excepted — the same rule for all
four corners, so there is no odd one to remember; the capsule is the panel's name, easiest to find against the corner.
The loading icon follows the whole capsule chain: the chain is one whole (where this is), loading is a state, and it
does not split a row of tabs.

## Capsule chain

The capsule of a panel title, a panel's tabs, the screen chips of [`screen`](screen.md), and the tabs after a popup title
are all drawn the same way:

- **Ends**: slanted, U+E0BA (`nf-ple-lower_right_triangle`) on the left and U+E0B0 (`nf-pl-left_hard_divider`) on the
  right. A popup's title is not part of the chain: it is a rounded capsule of its own (the title in [`popup`](popup.md));
  the tabs after a popup title follow the chain.
- **Selected**: filled with the chain's colour, text Base bold. On a panel the chain's colour is the border colour
  (changing with focus, unfocus and mode); in a popup it is the layer colour; for the screen chips it is Blue. The `[N]`
  capsule and the current tab both count as selected.
- **Unselected**: no fill, text in the chain's colour.
- **Joins**: U+E0B0 (`nf-pl-left_hard_divider`) where the colour changes, U+E0B1 (`nf-pl-left_soft_divider`) between
  parts of the same colour.
- **Colours of the ends and joins** (as in Powerline): the foreground is the fill of the part on the left, the
  background the fill of the part on the right; an unselected part's fill counts as Base, and outside the chain is the
  terminal's own background.
  - Selected → unselected: U+E0B0, foreground the chain's colour, background Base; unselected → selected: U+E0B0,
    foreground Base, background the chain's colour.
  - Both unselected: U+E0B1 in the chain's colour; both selected: U+E0B1, foreground Base, background the chain's colour.
  - Each end takes the fill of the part beside it: when the first or last part is unselected, that end is Base
    (invisible on a Base terminal background, leaving one empty cell).
  - Every end and join takes one cell (the powerline symbol width of Rules E5), so changing the selected part shifts no
    text.
- No space before or after the text inside a capsule: `[1] TABS`. The text is uppercase, the letters in a hotkey marker
  as written ("Uppercase" in the [components](../README.md)).
- **A panel's tabs**: `[N]` is a part of its own and always selected; each tab after it is a part, and only the current
  tab is selected. The panel has no other name: the first tab's name is the label. When `[N]` and the first tab are
  both selected (on the first tab), a space joins them instead of a seam, so it looks like a panel without tabs:

  ```
  ┏[2] PODSEVENTSYAML━━━━━━━━━┓   ← on PODS: "[2] PODS" filled
  ┏[2]PODSEVENTSYAML━━━━━━━━━┓   ← on EVENTS: "[2]" and "EVENTS" filled
  ```

- **Tabs after a popup title**: one line segment away from the rounded title (the title in [`popup`](popup.md)).
- **When it does not fit**: first shrink the unselected ones to their first character or glyph (`[M] [F] [S]`); if it
  still does not fit, fold away unselected ones from the end and draw a `…` instead. The selected one always stays, and
  the frame is never stretched wider (Rules L4).

**Why**: in the family a capsule means "a name" — what the panel is called, which page, which screen (Principle P4).
With all these uses sharing one look, the user who recognises one recognises them all. Unselected ones do not use
Surface2: Surface2 means disabled, and unselected pages would look as if they could not be switched to. The joins use the
two symbols of the original Powerline, the most widely supported by fonts; they are coloured as in Powerline too, so a
block of colour appears only on the selected part, which shows at a glance which one is selected, and no coloured point
sticks out beside an unselected one. `[N]` is a part of its own: apart from the number only the current tab is lit, so
there are never two blocks that both look current; on the first tab a space joins them, the same as a panel without tabs,
and no panel with tabs needs a name of its own. Slanted ends here and a rounded popup title: a panel fixed on the screen
and a popup floating above it can be told apart by the ends of their capsules.

## Ordinary lists

A panel with one entry per row, like kbu's resource list or filu's file list.

```
┏[2] PODS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃   NAME          READY  STATUS     RESTARTS  AGE ┃  ← header: Blue, fixed, never scrolls
┃   nginx-7d4f    1/1    Running           0   3d ┃
┃ 󰄲 web-a8k2      0/1    CrashLoo…        12   2h ┃  ← a marked row: a Green tick
┃▓▓▓coredns-7w9z▓▓1/1▓▓▓▓Running▓▓▓▓▓▓▓▓▓▓▓0▓▓▓9d┃  ← cursor: Subtext1 background, Base bold
┃   prome-er-0    0/2    Pending           0   5m ┃
┗━ Enter:logs ━━━━━━━━━━━━━━━━━━━━━━━━━━ 3 of 40 ━┛
```

- **Cursor**: Subtext1 background, Base bold, across the whole inner width; the whole cursor row is Base text, and the
  columns' own colours are not kept. Its right padding holds U+E0B0 (`nf-pl-left_hard_divider`) in Subtext1, an arrow
  pointing at the row. The padding is as wide as the arrow (the powerline symbol width of Rules E5: one cell as a rule;
  on a terminal where it takes two, every row keeps two on the right), so the arrow fits and the text does not move.
  When the panel is unfocused it is dimmed as a whole (Rules T2), the cursor with it,
  not given another colour.
- **Header**: Blue, not bold, uppercase, fixed at the top and never scrolled. Each column holds numbers or text: numbers align right
  and sort by value (`9` before `10`), text aligns left and sorts as text. Two cells between columns
  ("Diagrams and spacing" in the [components](../README.md)). A column being sorted on gets `nf-fa-sort_amount_asc` (U+F160, ascending) or `nf-fa-sort_amount_desc` (U+F161, descending) after its title;
  when several columns sort together, the rank goes before the arrow, e.g. `Name (2)` followed by the arrow.
- **Scroll position**: when the content does not fit, the right of the bottom border reads `N of M` (which entry the
  cursor is on, how many in all), in the border colour; nothing when everything fits. A panel without a cursor (a
  preview, a log) shows the visible lines, `N-M of T`.
- **Marked rows** (the "batch of marked items" of Principle P3): every row keeps a one-cell mark column at its very start.
  A marked row shows a Green `nf-md-checkbox_marked` (U+F0132); an unmarked one leaves it blank, the column width always
  kept, so rows never shift sideways when marked or unmarked (Rules L2). Domain flags such as favourites and pins belong
  to the content and are up to the app.
- **The row held in the Drag mode** (Rules K11; the key that enters the Drag is up to the app, e.g. `D` in the
  showcase and kbu): drawn as the cursor with Subtext1 swapped for the mode colour — a Yellow background, Base bold,
  the arrow on the right Yellow too; the mark column shows `nf-md-swap_vertical` (U+F04E2), and the row's own mark
  comes back once it is dropped. A panel with a Drag keeps the mark column on every row too. The keys are those of
  [`input/reorder`](../input/reorder.md) while holding an item: `j|k` move it (wrapping at the ends, Rules K12),
  `Enter` drops it, `Esc` puts it back.
- **Truncation**: cut at the end, with `…`. Where the end matters more, such as paths and file names, it may be cut at
  the front (`…/.ssh/id_ed25519`).
- **Empty**: as the empty states in [`screen`](screen.md).

**Loading and errors**:

- **Loading**: the loading icon sits after the whole capsule chain (tabs included), with one space on each side, in the border colour ([`popup`](popup.md)'s loading). While the panel has no content yet, one line is written in the
  middle in the empty-state look, e.g. `󰪞 loading pods…`. On reload, the old content stays and is not cleared.
- **Errors, lost connections, no permission**: two centred lines in the empty-state look: a fact in Red (e.g.
  `Forbidden: pods in kube-system`) and a hint in Overlay0 (e.g. `Press [R] to retry`). If the old content is still there
  it stays, and the error is reported in a toast as Rules F5 says.

**Why**: the cursor is "the row `Enter` acts on"; a solid background across the whole row, ending in an arrow, says so
in both shape and colour (L5). Marks use the checkbox tick: marked means "picked", the same thing as a ticked checkbox, in the same colour.
With the header fixed, what each column is stays visible however far you scroll.

### Groups

When a list's items fall into groups (kbu's resource kinds, locku's sidebar), each group starts with a group title row.

```
┏[1] KINDS━━━━━━━━━━━━━━━┓
┃ WORKLOADS              ┃  ← group title: Blue, uppercase, not bold; the cursor skips it
┃   pods                 ┃
┃▓▓▓deployments▓▓▓▓▓▓▓▓▓▓┃  ← cursor
┃   statefulsets         ┃
┃ NETWORK                ┃
┃   services             ┃
┃   ingresses            ┃
┗━ Enter:open ━━ 2 of 5 ━┛
```

- **Group title**: Blue, uppercase ("Uppercase" in the [components](../README.md)), not bold, no glyph; one cell from the
  frame. It is of a kind with the header: it says "what the rows below are", not a row of data.
- **Items**: two cells further in than the group title.
- **The cursor skips group titles** and stops only on items: `j|k` step over them; `gg|G` go to the first and last item;
  the `N of M` scroll position counts items only. When scrolling puts the cursor on a group's first item, that group's
  title stays on screen too.
- **Between groups**: no blank row, no separator.
- **A group with no items has no title**: when the panel filter leaves none of its items, or the app's group is empty.
- **Unfocused**: dims with the panel (Rules T2).

**Why**: a group title says "what the rows below are", as the header does, so it is drawn as the header is (Blue,
uppercase, not bold); with the items two cells further in, which group a row belongs to shows at a glance, with no
separator to draw. The cursor stops only on rows that do something, as with a menu's section titles. A group title left
over an empty group looks as if it were still loading.

## One value per row

A panel with one value per row, like a settings screen (locku's preference, webu's Settings, the fields on a webu page).

```
┏[2] PREFERENCE━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ PROPERTY            VALUE                     ┃
┃ PIN                 not set                   ┃
┃ PROFILE             clock                     ┃
┃ SHOW_STATUS         on                        ┃
┃ PIN_PROMPT_TIMEOUT  30                        ┃
┗━ Enter:edit ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **The rules of [`dialog/form`](../dialog/form.md) apply**: the focus moves one item at a time (`j|l|↓|→` on,
  `h|k|↑|←` back; in a panel with tabs, `h|l` switch tabs, Rules K12); `Enter` opens the value's input popup,
  and radio and checkbox options are chosen in place; once confirmed, the focus stays on the same row (Rules K3); values
  are shown as [`input/README`](../input/README.md) says.
- **What differs: there is no submit.** Each value takes effect and is saved the moment it is confirmed in the input
  popup, and a switch or radio option the moment it is chosen in place. So there is no action area, and no "ask first when
  changed".
- **The focus block**: a Subtext1 background with Base bold text, drawn the same way as the cursor of an ordinary list
  (its right padding is the arrow); it spans as in a form, from the start of the item to the panel's inner right edge (from the value for a field, from the
  option for an option).
- **Labels**: uppercase; Blue normally, Surface2 when disabled, Red when its value has an error (over any other colour). They are
  dimmed with the panel when it is unfocused (T2). The label column is as wide as the longest label, with two cells
  between it and the values.

**Why**: a settings screen and a form are the same thing — one value per row, changed one by one — except that a change
takes effect at once. With one set of rules, what the user learns in a form works on a settings screen too. Labels are
Blue, the colour of the focused frame: the same idea as a form's labels taking the layer colour, which is the colour of
the popup frame.

## Details

A panel that shows the item under another panel's cursor: locku's `[2]` property sheet, filu's preview, kbu's details.

- **It follows the cursor at once**: when that panel's cursor moves, the details switch to the new item straight away,
  with no `Enter`; when the label names the item (locku's `[2] clock`), the label switches too.
- **The focus stays**: as the cursor moves, the focus remains on the panel it was on; to work in the details, go there
  with `Tab` or a number key (Rules K2, K1). The app may also let `Enter` on the list send the focus to the details,
  whether and on which items being its call (the one place Rules K3 lets `Enter` change panels).
- The details themselves are drawn as what they are: an ordinary list, one value per row, a preview.

**Why**: the details answer "what does the item under the cursor look like". If they changed only on `Enter`, what you
saw while moving would always be the previous item; changing at once, you see wherever you are.

## Panel filter

`/` brings up a typing row at the top of the panel, and the list is filtered live as you type, with no popup (kbu's panel
search, sshu's Hosts, webu's list filters).

```
┏[2] HOSTS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  prod                                   2/5 ┃   ← typing row: `nf-fa-angle_right` before it, the filtered count on its right
┃ prod-web-01  deploy    10.0.3.14             ┃
┃ prod-db      postgres  10.0.3.20             ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

The typing row takes the same keys and the same matching as a finder's typing row ([`input/finder`](../input/finder.md)):
the filtered list keeps the panel's own order. The typing row starts with `nf-fa-angle_right` (U+F105), lined up with
the list's text (one cell from the frame), then one space before the typed text; its colour follows the row: the
panel's frame colour with the focus on the typing row, Overlay0 on the list. The count on its right reads
`matches/total` (`2/5`), in Overlay0. What differs all comes from the panel being on the screen level:

| | panel filter |
|---|---|
| `Tab` on the list | the next panel (Rules K2) |
| `Esc` on the list | clears the filter (Rules K4: one layer at a time) |
| After an item is chosen | the list keeps its filtered look and works as usual; the typing row is drawn in grey (Overlay0) |
| `/` on the list | back to the typing row, continuing the old text; to start over, `Esc` to clear it first, then `/` |

The focus leaving and returning:

- **The filter stays when the focus leaves the panel**, whichever way it leaves: the filter is how this panel looks now,
  and a glance at another panel should not make it disappear.
- **When the focus returns to a panel with a filter, it lands straight on the typing row**, without pressing `/` again;
  to work on the filtered list, `Enter` or `Tab` to the list. So `Tab` stops twice on a panel with a filter: once on the
  typing row, once on the list.

**Why**: a panel filter and a finder do different jobs — a finder is "go to one item", and closes once one is chosen; a
panel filter is "narrow the list and keep using it" (in kbu, keeping the pods whose names contain api to watch their
status; in sshu, typing `prod` to list a whole group of hosts and connect to them one by one). Their typing rows share
one set of keys; only `Tab` and `Esc`, which concern the level, differ.

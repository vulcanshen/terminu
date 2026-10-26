# panel (frame, lists, values and filter)

**Language**: English · [繁體中文](panel-zh_TW.md)

A panel's frame, ordinary lists (the location row and groups included), panels with one value per row, details, and the panel filter. How the whole screen is laid out is
in [`screen`](screen.md).

## panel.1 Frame

- **Line style and colour**: Blue heavy line `┏━┓` when focused, Surface2 light square line `┌─┐` when not; both are
  the same width, so switching shifts nothing (Rules L5, [`color`](../color.md)). Unfocused, the content is dimmed, streaming
  content excepted (Rules T2). A panel a list's cursor points at turns its frame colour, see "A pointed panel" below.
- **Left of the top border: the `[N] label` capsule**, right after the corner. `N` is also the digit key that jumps
  straight to that panel (within the current screen only, Rules K1). When the panel has tabs, `[N]` is a part of its
  own, the tabs follow it, and the first tab's name is the label (see the capsule chain below). A name in the label keeps
  its case, as in a popup title (`[2] PODS: nginx-7d4f`, `[1] prod-web-01`; "Uppercase" in the
  [components](../README.md)). While the panel is loading, the loading icon sits after the whole capsule chain (tabs
  included), with one space on each side (e.g. `┏[2] PODSEVENTSYAML 󰪞 ━━━┓`; the loading in [`popup`](popup.md)).
- **Right of the top border: the mode name** (Rules K11), see "The mode name" below.
- **Left of the bottom border: the hint**, which every panel must have — the exceptions are while the focus is on a
  panel filter's typing row and while it is in a PTY in the panel: no hint then, and it comes back on the list or on
  leaving the PTY; nor when no key on the panel does anything (see the hint below). Right of the bottom border: the
  scroll position
  (see "Ordinary lists" below).
- **Text on the frame always keeps one line segment away from the corner**; only the `[N] label` capsule sits right after
  the top-left corner: the hint is `┗━ Enter:logs`, the scroll position `3 of 40 ━┛`, the mode name `┫Drag┣━┓`.

```
┏[2] PODS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ ...                                             ┃
┗━ Enter:logs .:helm ━━━━━━━━━━━━━━━━━━━ 3 of 40 ━┛
```

**Hint**: written and ordered like the hint in [`popup`](popup.md) (`Enter` first). It holds this panel's own keys —
what `Enter` does here, the common hotkeys; not the movement keys, except the `h|l` that switches tabs: with two tabs or
more it is written `h|l:tab`, after `Enter` (as in the [`popup`](popup.md) hint); nor the core keys the footer already has; all the keys
are in the Space menu and `?`. When the list has no items (a panel filter matched nothing, or it was empty to begin
with), `Enter` and the hotkeys on an item are dropped, and only those on the whole panel stay — as with a finder and a
form's buttons, the hint shows only keys that do something ([`input/finder`](../input/finder.md),
[`dialog/form`](../dialog/form.md)). When no key is left after that (e.g. a read-only panel, or an empty list with no
key on the whole panel), the left of the bottom border has no hint, only the line. When focused, keys Blue and descriptions Overlay0; unfocused, it stays and is dimmed with
the panel. When it does not fit, whole pairs are dropped from the end, and the scroll position stays.

**Why**: the hint on a panel's bottom border tells the user "what pressing what does on this panel", while the footer
covers only the keys common to the whole screen; each covers one level, and with every panel having one, the user's eyes
know where to look when changing panels. No hint while typing in a panel filter: the hint lists the panel's own hotkeys,
which are all characters while typing (Rules K8), and listing them would teach the wrong keys; the footer already shows
the keys for typing. The same in a PTY: the panel's keys all go to the subprocess, and the exit keys that do not are
already in the footer ([`screen`](screen.md)). Text on the frame keeps away from the corners, the capsule alone excepted — the same rule for all
four corners, so there is no odd one to remember; the capsule is the panel's name, easiest to find against the corner.
The loading icon follows the whole capsule chain: the chain is one whole (where this is), loading is a state, and it
does not split a row of tabs. The `h|l` that switches tabs is in the hint as the datetime picker's `h|l:month` is: it changes
the whole page rather than moving between items, but it is a movement key, and left out, the other tabs are hard to
find (the user, 2026-10-24, filu's FL27).

### panel.2 A pointed panel

When the cursor's row in a focused list stands for another panel on screen
(e.g. sshu's session list and the PTY panels in its grid on the right), that panel is "pointed": it stays an
unfocused light square frame and never takes the focus; only the frame's colour turns from Surface2 to Lavender
("user footprint" in [`color`](../color.md)), the capsule chain turning with it. Which row stands for which panel,
and whether to use it at all, the app may decide for itself.

- The cursor moving to another row points at that row's panel instead; when that row's panel is not on screen, no
  panel is pointed.
- It points only while that list has the focus: with the focus on the pointed panel, it is drawn as focused; with
  the focus on another panel, no panel is pointed.
- The content is dimmed as unfocused (streaming content excepted); under a popup it is dimmed with everything else
  (Rules F8).

**Why**: a row in the list and a panel on screen are two sides of one thing (an sshu session and its cell), so
scanning the list tells which cell it is without reading titles, and a new cell is pointed at as soon as it
appears, showing it is done. The focus is still on the list, so it cannot become the focus and keeps the unfocused
line; Lavender is the colour of "where the user is now" (the location row, the statusbar), and here it says "the
cursor points here now" (the user, 2026-10-25, sshu's SS44).

### panel.3 The mode name

The right of the top border holds the mode name (Rules K11), set between two border junctions like a tag inlaid in the
frame: `┏[1] KINDS━━━┫Drag┣━┓`, `┏━YAML━━━━┫Visual┣━┓`. The junctions take the frame's colour and follow its
line style — `┫` `┣` on a heavy frame (a focused panel, a popup), `┤` `├` on a light one (an unfocused panel); the mode
name is bold in the mode colour, its case as written. The mode name is
one word if possible (`Drag`, `Visual`, `Select`: a narrow panel has no room for two, and the whole top-right text
would be dropped); when space runs out, the title is clipped first and the mode name stays. The capsule turns the mode
colour along with the frame.
A mode with layers (e.g. a viewer's selection mode, once selecting) adds each layer to its name after a `>`, with no
spaces: `┫Visual>select┣`; each part is one word if possible. The `>` reads as one layer in, and `Esc` goes back one
layer at a time (Rules K11).

- **It opens and closes**: entering the mode, the tag opens from its middle: the two junctions start side by side
  there and move apart, the name showing from its middle; leaving plays it backwards, down to the plain line. The
  junctions take the first frame and every frame after shows one more letter, 32ms a frame as in a popup (Rules F2):
  every frame changes something, so the length follows the name (`Drag` 5 frames, about 160ms; `Compare` 8, about
  256ms), the progress taken from the clock. An odd length leaves the middle half a cell off, either side will do. The title keeps room for the whole tag for as long
  as the tag is there, so it never shifts frame by frame.

  ```
  ━━━━━━━━━┓   before
  ━━━━┫┣━━━┓   the junctions appear side by side at the tag's middle
  ━━━┫ra┣━━┓   moving apart, the name showing from its middle
  ━━┫Drag┣━┓   open
  ```

- **Turning around**: switched again halfway (entering and leaving in quick runs), the tag turns around from where it
  is and does not start over: half open, it closes from half; closing, it opens again from where it got to.
- **A layer added or taken off**: the right end stays; the layer added grows from the tail a letter a frame, the left
  junction moving left with it, and going back a layer takes it off from the tail a letter at a time. 32ms a frame,
  turning around as above. The title keeps room for the longest name in the animation. Leaving the whole mode straight
  from a layer (e.g. `y` in the selection mode) closes the whole tag from its middle as above.

  ```
  ━━━━━━━━┫Visual┣━┓   before
  ━━━━━━━┫Visual>┣━┓   a letter a frame
  ━━━━━━┫Visual>s┣━┓
  ━┫Visual>select┣━┓   grown
  ```

- **Only the tag animates**: the mode takes effect at once and the frame turns its colour at once; keys are taken all
  along (unlike a popup opening, Rules F3). While closing, the name stays in the mode colour and the junctions take the
  frame's colour as usual.

**Why**: as with a popup, the animation lets the switch be felt; modes are entered and left in quick runs, so the
animation never holds a key and never starts over (the user, 2026-10-22). A tag has only as many steps as its name
has letters: spread over a fixed 288ms, each step held for about 72ms and the tag stuttered, so it goes a letter a
frame instead (the user, testing kbu). A layer added moves only what it adds: the mode has not changed, and `Visual`
stays in sight. The `>` reads as one layer in, where a colon is how hints are written and a slash looks like the
joins of a capsule chain, which part things side by side (the user, 2026-10-24).

## panel.4 Capsule chain

The capsule of a panel title, a panel's tabs, the screen chips of [`screen`](screen.md), and the tabs after a popup title
are all drawn the same way:

- **Ends**: slanted, U+E0BA (`nf-ple-lower_right_triangle`) on the left and U+E0B0 (`nf-pl-left_hard_divider`) on the
  right. A popup's title is not part of the chain: it is a rounded capsule of its own (the title in [`popup`](popup.md));
  the tabs after a popup title follow the chain.
- **Selected**: filled with the chain's colour, text Base bold. On a panel the chain's colour is the border colour
  (changing with focus, unfocus and mode); in a popup it is the layer colour; for the screen chips it is Blue. The `[N]`
  capsule and the current tab both count as selected.
- **Unselected**: filled with Mantle, text in the chain's colour, not bold.
- **Joins**: always a slant, leaning the same way as the left end. Where the colour changes, a solid slant: selected →
  unselected U+E0BC (`nf-ple-upper_left_triangle`), unselected → selected U+E0BA (`nf-ple-lower_right_triangle`);
  between two unselected parts a thin slant, U+E0BB (`nf-ple-forwardslash_separator`).
- **Colours of the ends and joins**:
  - A join in the middle: foreground the chain's colour, background Mantle. Only `[N]` and the first tab are ever both
    selected, and there it is as in "A panel's tabs" below: a blank one powerline symbol wide, no seam.
  - The ends: foreground the fill of the part beside them (the chain's colour for a selected part, Mantle for an
    unselected one); outside, no background is painted: it is the terminal's own.
  - Losing focus: the chain's colour turns to the unfocused border colour and Mantle stays (T2 dims a panel's content,
    and the chain is on the border). Covered: dimmed with the whole screen under F8, Mantle turns exactly into Crust
    (dimming in [`color`](../color.md)).
  - Every end and join takes the width of one powerline symbol (Rules E5: one cell as a rule; two on a terminal where it
    takes two), so changing the selected part shifts no text.
- No space before or after the text inside a capsule: `[1] TABS`. The text is uppercase, a name as it is
  (`[2] PODS: nginx-7d4f`), the letters in a hotkey marker as written ("Uppercase" in the [components](../README.md)).
- **A panel's tabs**: `[N]` is a part of its own and always selected; each tab after it is a part, and only the current
  tab is selected. The panel has no other name: the first tab's name is the label. When `[N]` and the first tab are
  both selected (on the first tab), a blank joins them instead of a seam, so it looks like a panel without tabs; the
  blank takes the width of one powerline symbol, as a seam does (two blank cells on a terminal where the symbol takes
  two), so changing tabs shifts no text:

  ```
  ┏[2] PODSEVENTSYAML━━━━━━━━━┓   ← on PODS: "[2] PODS" filled
  ┏[2]PODSEVENTSYAML━━━━━━━━━┓   ← on EVENTS: "[2]" and "EVENTS" filled
  ```

- **Tabs after a popup title**: one line segment away from the rounded title (the title in [`popup`](popup.md)).
- **When it does not fit**: first shrink the unselected ones to their first character or glyph (`[M] [F] [S]`); if it
  still does not fit, fold away unselected ones from the end and draw a `…` instead. The selected one always stays, and
  the frame is never stretched wider (Rules L4). When the selected part is too long on its own, its text is cut at the
  end with `…`; the slanted ends are still drawn, and a line segment still stays between it and the frame's corner
  (e.g. `┏[2] DEPLOYM…━┓`).

**Why**: in the family a capsule means "a name" — what the panel is called, which page, which screen (Principle P4).
With all these uses sharing one look, the user who recognises one recognises them all. Unselected ones do not use
Surface2: Surface2 means disabled, and unselected pages would look as if they could not be switched to.
Unselected parts are filled with Mantle and every join is a slant: every cell of the chain has its colour written out and
only the outside is left to the terminal, so it looks the same on any background, a transparent one or a background
image, without depending on the terminal's background being Base (kbu's KB26: with any other background, the old seams
showed patches of Base). Mantle is a step darker than Base, so the unselected parts stay in the back and the selected one shows
at a glance; the slants lean the same way as the left end, so the chain reads as one band. Between two unselected parts
both sides are Mantle and a solid slant would not show, hence the thin one. When covered, Mantle dims into Crust and the
whole chain falls back.
`[N]` is a part of its own: apart
from the number only the current tab is lit, so there are never two blocks that both look current; on the first tab a
blank joins them, the same as a panel without tabs, and no panel with tabs needs a name of its own; the blank is as wide
as a seam, so moving between the first tab and the others never jumps the text by a cell. A selected part that is too
long loses text, not its slants: the slants are the shape that says "a capsule", and without them it no longer reads as
a name. Slanted ends here and
a rounded popup title: a panel fixed on the screen and a popup floating above it can be told apart by the ends of their
capsules.

## panel.5 Ordinary lists

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
- **Header**: a list with several columns always has one; for a single-column list, the app may decide for itself. Blue, not bold,
  uppercase, fixed at the top and never scrolled. Each column holds numbers or text: numbers align right
  and sort by value (`9` before `10`), text aligns left and sorts as text. Two cells between columns
  ("Diagrams and spacing" in the [components](../README.md)). Sorting: see "Sorting" below.
- **The list's order is fixed**: every time it opens and every time it is fetched again, the same data comes out in the
  same order. When the data has no order of its own (e.g. kubeconfig's contexts, which may read back in a different
  order each time), the app sorts it before showing it, by name by default, numbers by value; data with an order of its
  own (a history by time, something the user ordered) keeps that order.
- **Column widths**: the app marks the **columns that may be cut short** (long values such as names, URLs, a line of
  text); they share the width that is left and are cut their own way when too long (at the end, or in the middle for
  values that matter at both ends). The other columns (short values such as states, numbers, dates) take their widest
  value and never shrink.
- **When the columns do not fit**: first the columns that may be cut short narrow down to their least width (the app's
  to set, e.g. 12 cells); only then do whole columns go. The app gives each column an order in which it goes, and the
  most important one (the name) never goes; the least important column is taken away whole (its header with it) until
  they fit. When the terminal grows, the columns come back in the same order and the columns cut short grow back.
- **Scroll position**: when the content does not fit, the right of the bottom border reads `N of M` (which entry the
  cursor is on, how many in all), in the border colour; nothing when everything fits. A panel without a cursor (a
  preview, a log) shows the visible lines, `N-M of T`.
- **Truncation**: cut at the end, with `…`. Where the end matters more, such as paths and file names, it may be cut at
  the front (`…/.ssh/id_ed25519`); where both ends matter (e.g. a pod's name: the deployment at the front, the random
  part that tells one from another at the end), it is cut in the middle, with the `…` there (`demo-app…66-gm72n`). Where
  each column is cut, the app may decide for itself.
- **Control characters**: a value in a cell (a file name or a name that came from a file or another program) holding
  control characters shows them as red escapes, as on the typing row and as a value on a form (`\n`, `\t`, `\x1b`;
  "Control characters" in [components](../README.md)): never dropped, never turned into spaces, never sent to
  the terminal as they are. Dropping them makes two different names look the same (`report.txt` and a `report⏎.txt`
  with a newline in the middle); sending them as they are scrambles the screen and recolours what follows.
- **Empty**: as the empty states in [`screen`](screen.md). The empty state takes the whole panel, the header included,
  its sentence centred in the panel; a location row, when there is one, stays (see "Location row").

While loading and when the content cannot be read: see "Loading and errors" below.

**Why**: the cursor is "the row `Enter` acts on"; a solid background across the whole row, ending in an arrow, says so
in both shape and colour (L5).
A list with several columns always has a header: what the columns mean and the sort arrows both rest on it. With the
header fixed, what each column is stays visible however far you scroll. A long value cut short is still recognisable
(cut in the middle, it keeps both ends), while a short value cut at all can no longer be read, so the long columns
give way and the short ones keep their width; one very long name no longer pushes every other column out. Only when
they still do not fit do whole columns go: with every column shrunk a little, none can be read in full; with the least
important one taken away, the rest still read in full, and the name is always there to tell which entry it is. An empty list loses its header too: with no data, the column names have nothing
to label, and one centred sentence says it best.

### panel.6 Sorting

- **A column being sorted on**: its title in the header gets `nf-fa-sort_amount_asc` (U+F160, ascending) or
  `nf-fa-sort_amount_desc` (U+F161, descending) after it; when several columns sort together, the rank goes before the
  arrow, e.g. `Name (2)` followed by the arrow. A number column sorts by value, a text column as text (see "Header"
  above).
- **Sort groups**: whether to give each row a group, and the groups' order, the app may decide for itself; sorting works
  only within a group, and no title is drawn between groups (e.g. filu's directories always come before its files, and
  sorting by name sorts each on its own).

**Why**: sort groups keep a fixed order such as "directories first" from being scattered by sorting.

### panel.7 Marked rows

A list whose rows can be marked and worked on as a batch (the "batch of marked items" of Principle P3): every row keeps a one-cell mark column at its very start.
A marked row shows a Green `nf-md-checkbox_marked` (U+F0132); an unmarked one leaves it blank, the column width always
kept, so rows never shift sideways when marked or unmarked (Rules L2). Domain flags such as favourites and pins belong
to the content, and the app may decide for itself.

**Why**: marks use the checkbox tick: marked means "picked", the same thing as a ticked checkbox, in the same colour.

### panel.8 Drag mode

A list with a Drag mode (Rules K11; the key that enters the Drag, the app may decide for itself, e.g. `D` in the
showcase and kbu): the row held is drawn as the cursor with Subtext1 swapped for the mode colour — a Yellow background, Base bold,
the arrow on the right Yellow too; the mark column shows `nf-md-swap_vertical` (U+F04E2), and the row's own mark
comes back once it is dropped. A panel with a Drag keeps the mark column on every row too. The keys are those of
[`input/reorder`](../input/reorder.md) while holding an item: `j|k` move it (wrapping at the ends, Rules K12),
`Enter` drops it, `Esc` puts it back.

### panel.9 Compare mode

A list with a compare mode (Rules K11; the compare key, the app may decide for itself, e.g. `C` in kbu): the compare key on a row enters
the mode and makes that row the anchor; then another row is picked and the two are compared ("Compare" in
[`dialog/note`](../dialog/note.md)).

- **Text only**: text, or content shown as text (e.g. a kbu resource's YAML, a text file in filu). A file goes by the
  kind of its preview in [`input/file-picker`](../input/file-picker.md); anything but `text` (image, PDF, archive,
  binary…) cannot be compared: the item has no compare action (Rules M2), and in the mode the compare key is
  disabled while the cursor rests on it (M6).
- **The anchor row**: the whole row in the mode colour — a Yellow background, Base text, not bold, no arrow on the
  right ("the range selected in a mode" in [`color`](../color.md)); the cursor is drawn as usual, and on the anchor
  the cursor is what is drawn.
- **The mode's keys**: `j|k`, `u|d`, `gg|G` move; the compare key or `Enter` opens the comparison with the anchor,
  and closing it goes back to the mode with the anchor kept, ready for the next row; both keys are disabled while
  the cursor rests on the anchor (M6). When the two are identical nothing opens: an Info toast says so (`No
  differences between <a> and <b>`) and the mode stays. `Esc` leaves the mode and drops the anchor; `Tab` and the
  number keys are paused (K11).
- **When the anchor is gone** (deleted, moved away): the mode is left, with a Warning toast saying why.

### panel.10 Location row

A row above the list giving where you are now (a path, the level drilled down to), e.g. filu's directory, sshu's remote
path, the level kbu reaches going from a Deployment into its Pods. **Whether there is one, the app may decide for itself**.

```
┏[2] FILES━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ …/sideproj/terminu/components/layout          ┃  ← location row: Lavender, cut at the front when too long
┃   NAME              SIZE  MODIFIED            ┃
┃   panel.md         12 KB  2026-10-19 14:02    ┃
┗━ Enter:open ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **Where**: the first row in the panel, one cell from the frame; above the header when there is one, and above a panel
  filter's typing row when that shows. Fixed at the top, never scrolled.
- **Colour**: Lavender (the user footprint and breadcrumb in [`color`](../color.md)); dimmed with the panel when it is
  unfocused (Rules T2).
- **Too long**: cut at the front with `…`, keeping the end (the level you are on is the last part).
- **Shown only**: it cannot be acted on; the cursor never stops on it, and the scroll position does not count it.
- **Stays when the list is empty**: the empty state replaces the header and the list, not the location row — it says
  where you are, not what the list holds, and an empty directory needs saying which one it is all the more.

**Why**: "where am I now" written in the label makes the label longer and longer, until the capsule's truncation eats
it; written in a row of its own inside the panel, the whole path fits, and the label stays the panel's name. Lavender:
it is the footprint the user left on the way here, the same meaning as the "where you are now" values on the statusbar.
Not every app has a "where" to show, so the row is optional.

### panel.11 Groups

When a list's items fall into groups (kbu's resource kinds, locku's sidebar), each group starts with a group title row.

```
┏[1] KINDS━━━━━━━━━━━━━┓
┃ WORKLOADS              ┃  ← group title: Blue, uppercase, not bold; the cursor skips it
┃   pods                 ┃
┃▓▓▓deployments▓▓▓▓▓▓▓▓▓┃  ← cursor
┃   statefulsets         ┃
┃ NETWORK                ┃
┃   services             ┃
┃   ingresses            ┃
┗━ Enter:open ━━ 2 of 5 ━┛
```

- **Group title**: Blue, uppercase ("Uppercase" in the [components](../README.md)), not bold, no glyph; one cell from the
  frame. It is of a kind with the header: it says "what the rows below are", not a row of data.
- **Items**: two cells further in than the group title. When the list has a mark column ("Marked rows" above), the mark
  goes in those two extra cells: the mark one cell from the frame, a space, the text three cells from the frame; a group
  title row keeps no mark column.
- **The cursor skips group titles** and stops only on items: `j|k` step over them; `gg|G` go to the first and last item;
  the `N of M` scroll position counts items only. When scrolling puts the cursor on a group's first item, that group's
  title stays on screen too.
- **Between groups**: no blank row, no separator.
- **A group with no items has no title**: when the panel filter leaves none of its items, or the app's group is empty.
- **Unfocused**: dims with the panel (Rules T2).

**Why**: a group title says "what the rows below are", as the header does, so it is drawn as the header is (Blue,
uppercase, not bold); with the items two cells further in, which group a row belongs to shows at a glance, with no
separator to draw. The mark goes in the two extra cells: the text stays three cells from the frame, as without marks and
as in an ordinary list with marks, and shifts nothing. The cursor stops only on rows that do something, as with a menu's
section titles. A group title left over an empty group looks as if it were still loading.

## panel.12 One value per row

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
  dimmed with the panel when it is unfocused (T2). The label column is as wide as the longest of the labels and the
  header's first column name (e.g. a 7-cell `SETTING` header over a longest label `DRAWER` of 6 cells gives 7), with two
  cells between it and the values; the header's second column name lines up with the values.
- **Header** (`PROPERTY  VALUE` in the example): whether there is one, the app may decide for itself. If there is, it takes Overlay0
  (dim text in [`color`](../color.md)); otherwise as an ordinary list's header (uppercase, not bold, fixed at the top
  and never scrolled).
- **Scroll position**: as in a form, counted in fields — in `N of M`, N is the field the focus is on and M the number of
  fields; a radio's options count as one field (["When the content does not fit"](popup.md) in popup).
- **The "each row" section of `?`** (whether there is one, the app may decide for itself): the key reference may open with a section
  saying what each row is — the setting's name on the left (in normal text), its description on the right; the key
  sections follow it (the key reference in [`dialog/note`](../dialog/note.md)).

**Why**: a settings screen and a form are the same thing — one value per row, changed one by one — except that a change
takes effect at once. With one set of rules, what the user learns in a form works on a settings screen too. Labels are
Blue, the colour of the focused frame: the same idea as a form's labels taking the layer colour, which is the colour of
the popup frame. The header is not Blue: the labels under it already are, and a Blue header would run into them
and not read as a header; an ordinary list's header has Text data under it, which is what sets it apart. A header says
what a column is and cannot be acted on, so it takes dim text, as a menu's section titles do. The header is optional:
each row's label already says what the row is. The label column is measured with the header: measured on the labels
alone, a wider header would push its second column out of line with the values. The scroll position counts fields, as in
a form: the user counts settings, not rows of text. When a label of a word or two cannot say what a row governs, the
"each row" section at the top of `?` fills it in; an app with few settings whose names say enough needs no such section.

## panel.13 Details

A panel that shows the item under another panel's cursor: locku's `[2]` property sheet, filu's preview, kbu's details.

- **It follows the cursor at once**: when that panel's cursor moves, the details switch to the new item straight away,
  with no `Enter`; when the label names the item (locku's `[2] clock`), the label switches too.
- **The focus stays**: as the cursor moves, the focus remains on the panel it was on; to work in the details, go there
  with `Tab` or a number key (Rules K2, K1). The app may also let `Enter` on the list send the focus to the details,
  whether and on which items, the app may decide for itself (the one place Rules K3 lets `Enter` change panels).
- The details themselves are drawn as what they are: an ordinary list, one value per row, a preview.

**Why**: the details answer "what does the item under the cursor look like". If they changed only on `Enter`, what you
saw while moving would always be the previous item; changing at once, you see wherever you are.

## panel.14 Panel filter

`/` brings up a typing row at the top of the panel (below the location row when there is one; above the header, when the
list has one), and the list is filtered
live as you type, with no popup (kbu's panel search, sshu's Hosts, webu's list filters).

```
┏[2] HOSTS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  prod                                   2/5 ┃   ← typing row: `nf-fa-angle_right` before it, the filtered count on its right
┃ NAME         USER      HOSTNAME              ┃   ← header: below the typing row
┃ prod-web-01  deploy    10.0.3.14             ┃
┃ prod-db      postgres  10.0.3.20             ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

The typing row takes the same keys and the same matching as a finder's typing row ([`input/finder`](../input/finder.md)):
the filtered list keeps the panel's own order. The typing row starts with `nf-fa-angle_right` (U+F105), one cell
from the frame (as in a finder's typing row), then one space before the typed text; its colour follows the row: the
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

## panel.15 Loading and errors

The same for every kind of panel: an ordinary list, one value per row, details, a preview, a log, a PTY cell
([`dialog/terminal`](../dialog/terminal.md): its frame is a panel's).

- **Loading**: the loading icon sits after the whole capsule chain (tabs included), with one space on each side, in the
  border colour ([`popup`](popup.md)'s loading). While the panel has no content yet, one line is written in the middle in
  the empty-state look, e.g. `󰪞 loading pods…`, `󰪞 connecting to prod-web-01…`. On reload, the old content stays and is
  not cleared.
- **Errors, lost connections, no permission**: two centred lines in the empty-state look: a fact in Red (e.g.
  `Forbidden: pods in kube-system`) and a hint in Overlay0 (e.g. `Press [R] to retry`). If the old content is still there
  it stays, and the error is reported in a toast as Rules F5 says.

**Why**: while a panel waits, or cannot read anything, users look at the same place — its middle — whether it usually
holds a list, values or a terminal; written the same way, "still coming" and "cannot come" read the same in every kind of
panel. These two points used to sit under the ordinary lists, but the empty state in screen and the loading icon on the
frame both speak of every panel, so they got a section of their own (reported by sshu, 2026-10-26).

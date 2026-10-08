# panel (frame, lists, values and filter)

**Language**: English · [繁體中文](panel-zh_TW.md)

A panel's frame, ordinary lists, panels with one value per row, and the panel filter. How the whole screen is laid out is
in [`screen`](screen.md).

## Frame

- **Line style and colour**: Blue double line `╔═╗` when focused, Surface2 rounded `╭─╮` when not; both are the same
  width, so switching shifts nothing (Rules L5, [`color`](../color.md)). Unfocused, the content is dimmed, streaming
  content excepted (Rules T2).
- **Left of the top border: the `[N] label` capsule**, right after the corner. `N` is also the digit key that jumps
  straight to that panel. When the panel has tabs, they follow the capsule (see the capsule chain below). While the panel
  is loading, the loading icon sits after the capsule (the loading in [`popup`](popup.md)).
- **Right of the top border: the mode name** (Rules K11), set between two border junctions like a tag inlaid in the
  frame: `╔═[1] Kinds════╡Drag╞═╗`, `╭─ YAML ────┤Visual├─╮`. The junctions take the frame's colour and follow its line
  style — `╡` `╞` on a double frame, `┤` `├` on a single one; the mode name is bold in the mode colour. The mode name is
  one word if possible (`Drag`, `Visual`, `Select`: a narrow panel has no room for two, and the whole top-right text
  would be dropped); when space runs out, the title is clipped first and the mode name stays. The capsule turns the mode
  colour along with the frame.
- **Left of the bottom border: the hint**, which every panel must have; right of the bottom border: the scroll position
  (see "Ordinary lists" below).

```
╔([2] Pods)═══════════════════════════════════════╗
║ ...                                              ║
╚═ .:helm Enter:logs ════════════════════ 3 of 40 ╝
```

**Hint**: written like the hint in [`popup`](popup.md). It holds this panel's own keys — what `Enter` does here, the
common hotkeys; not the movement keys, nor the core keys the footer already has; all the keys are in the Space menu and
`?`. When focused, keys Blue and descriptions Overlay0; unfocused, it stays and is dimmed with the panel. When it does
not fit, whole pairs are dropped from the end, and the scroll position stays.

**Why**: the hint on a panel's bottom border tells the user "what pressing what does on this panel", while the footer
covers only the keys common to the whole screen; each covers one level, and with every panel having one, the user's eyes
know where to look when changing panels.

## Capsule chain

The capsule of a panel title, a panel's tabs, the screen chips of [`screen`](screen.md), and the tabs after a popup title
are all drawn the same way:

- **Ends**: the rounded U+E0B6 (`nf-ple-left_half_circle_thick`) and U+E0B4 (`nf-ple-right_half_circle_thick`).
- **Selected**: filled with the chain's colour, text Base bold. On a panel the chain's colour is the border colour
  (changing with focus, unfocus and mode); in a popup it is the layer colour; for the screen chips it is Blue. The `[N]`
  capsule and the current tab both count as selected.
- **Unselected**: no fill, text in the chain's colour.
- **Joins**: U+E0B0 (`nf-pl-left_hard_divider`) where the colour changes, U+E0B1 (`nf-pl-left_soft_divider`) between
  parts of the same colour.
- No space before or after the text inside a capsule: `[1] Tabs`.
- **When it does not fit**: first shrink the unselected ones to their first character or glyph (`[M] [F] [S]`); if it
  still does not fit, fold away unselected ones from the end and draw a `…` instead. The selected one always stays, and
  the frame is never stretched wider (Rules L4).

**Why**: in the family a capsule means "a name" — what the panel is called, which page, which screen (Principle P4).
With all these uses sharing one look, the user who recognises one recognises them all. Unselected ones do not use
Surface2: Surface2 means disabled, and unselected pages would look as if they could not be switched to. The joins use the
two symbols of the original Powerline, the most widely supported by fonts.

## Ordinary lists

A panel with one entry per row, like kbu's resource list or filu's file list.

```
╔([2] Pods)═══════════════════════════════════════╗
║   Name          Ready  Status    Restarts  Age  ║  ← header: Blue, fixed, never scrolls
║   nginx-7d4f    1/1    Running          0   3d  ║
║ 󰄲 web-a8k2      0/1    CrashLoo…       12   2h  ║  ← a marked row: a Green tick
║▓▓▓coredns-7w9z▓▓1/1▓▓▓▓Running▓▓▓▓▓▓▓▓▓▓0▓▓▓9d▓▓║  ← cursor: Subtext1 background, Base bold
║   prome-er-0    0/2    Pending          0   5m  ║
╚═ Enter:logs ═════════════════════════════ 3 of 40 ╝
```

- **Cursor**: Subtext1 background, Base bold, across the whole inner width; the whole cursor row is Base text, and the
  columns' own colours are not kept. When the panel is unfocused it is dimmed as a whole (Rules T2), the cursor with it,
  not given another colour.
- **Header**: Blue, not bold, fixed at the top and never scrolled. Text aligned left, numbers right. A column being sorted
  on gets `nf-fa-sort_amount_asc` (U+F160, ascending) or `nf-fa-sort_amount_desc` (U+F161, descending) after its title;
  when several columns sort together, the rank goes before the arrow, e.g. `Name (2)` followed by the arrow.
- **Scroll position**: when the content does not fit, the right of the bottom border reads `N of M` (which entry the
  cursor is on, how many in all), in the border colour; nothing when everything fits. A panel without a cursor (a
  preview, a log) shows the visible lines, `N-M of T`.
- **Marked rows** (the "batch of marked items" of Principle P3): every row keeps a one-cell mark column at its very start.
  A marked row shows a Green `nf-md-checkbox_marked` (U+F0132); an unmarked one leaves it blank, the column width always
  kept, so rows never shift sideways when marked or unmarked (Rules L2). Domain flags such as favourites and pins belong
  to the content and are up to the app.
- **Truncation**: cut at the end, with `…`. Where the end matters more, such as paths and file names, it may be cut at
  the front (`…/.ssh/id_ed25519`).
- **Empty**: as the empty states in [`screen`](screen.md).

**Loading and errors**:

- **Loading**: the loading icon sits after the capsule. While the panel has no content yet, one line is written in the
  middle in the empty-state look, e.g. `󰪞 loading pods…`. On reload, the old content stays and is not cleared.
- **Errors, lost connections, no permission**: two centred lines in the empty-state look: a fact in Red (e.g.
  `Forbidden: pods in kube-system`) and a hint in Overlay0 (e.g. `Press [R] to retry`). If the old content is still there
  it stays, and the error is reported in a toast as Rules F5 says.

**Why**: the cursor is "the row `Enter` acts on"; a solid background across the whole row says so in both shape and
colour (L5). Marks use the checkbox tick: marked means "picked", the same thing as a ticked checkbox, in the same colour.
With the header fixed, what each column is stays visible however far you scroll.

## One value per row

A panel with one value per row, like a settings screen (locku's preference, webu's Settings, the fields on a webu page).

```
╔([2] preference)═══════════════════════════════╗
║ Property                   Value              ║
║ PIN                        not set            ║
║ profile                    clock              ║
║ show_status                on                 ║
║ pin_prompt_timeout         30                 ║
╚═ Enter:edit ══════════════════════════════════╝
```

- **The rules of [`dialog/form`](../dialog/form.md) apply**: the focus moves one item at a time (`j`/`l`/`↓`/`→` on,
  `h`/`k`/`↑`/`←` back; in a panel with tabs, `h`/`l` go to the tabs, Rules K12); `Enter` opens the value's input popup,
  and radio and checkbox options are chosen in place; once confirmed, the focus stays on the same row (Rules K3); values
  are shown as [`input/README`](../input/README.md) says.
- **What differs: there is no submit.** Each value takes effect and is saved the moment it is confirmed in the input
  popup, and a switch or radio option the moment it is chosen in place. So there is no action row, and no "ask first when
  changed".
- **The focus block**: a Subtext1 background with Base bold text, drawn the same way as the cursor of an ordinary list; it
  spans as in a form, from the start of the item to the panel's inner right edge (from the value for a field, from the
  option for an option).
- **Labels**: Blue normally, Surface2 when disabled, Red when its value has an error (over any other colour). They are
  dimmed with the panel when it is unfocused (T2).

**Why**: a settings screen and a form are the same thing — one value per row, changed one by one — except that a change
takes effect at once. With one set of rules, what the user learns in a form works on a settings screen too. Labels are
Blue, the colour of the focused frame: the same idea as a form's labels taking the layer colour, which is the colour of
the popup frame.

## Panel filter

`/` brings up a typing row at the top of the panel, and the list is filtered live as you type, with no popup (kbu's panel
search, sshu's Hosts, webu's list filters).

```
╔([2] Hosts)═══════════════════════════════════╗
║  prod                                    2/5 ║   ← typing row, the filtered count on its right
║ prod-web-01        deploy   10.0.3.14        ║
║ prod-db            postgres 10.0.3.20        ║
╚══════════════════════════════════════════════╝
```

The typing row takes the same keys as a finder's typing row ([`input/finder`](../input/finder.md)); the count on its
right reads `matches/total` (`2/5`). What differs all comes from the panel being on the screen level:

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

# panel: Inputs in a panel

**Language**: English · [繁體中文](panel-zh_TW.md)

## Frame

The panel's frame (moved here from defaults D1 and D3 on 2026-10-07, from a default to a requirement). Border colours and
line styles follow [`color`](../color.md) (double when focused, rounded when not, Rules L5); unfocused, the content is
dimmed, streaming content excepted (Rules T2).

- **The `[N] label` capsule**: each panel's top border carries an `[N] label` capsule (powerline rounded), where `N` is
  also the digit key that jumps straight to that panel.
- **The mode name label** (Rules K11): the junctions take the frame's colour and follow its line style — `╡` `╞` on a
  double frame, `┤` `├` on a single one; the name is bold in the mode colour; one word if possible (`Drag`, `Visual`,
  `Select`: a narrow panel has no room for two, and the whole top-right text would be dropped); when space runs out the
  title is clipped first and the mode name stays. A panel's `[N] label` capsule turns the mode colour with its frame (kbu
  `248f883`).

## One value per row

A panel with one value per row, like a settings screen (locku's preference, webu's Settings, the fields on a webu page).
Settled by the user, 2026-10-07.

```
╔[2] preference═════════════════════════════════╗
║ Property                   Value              ║
║ PIN                        not set            ║
║ profile                    clock              ║
║ show_status                on                 ║
║ pin_prompt_timeout         30                 ║
╚═══════════════════════════════════════════════╝
```

- **The rules of [`dialog/form`](../dialog/form.md) apply**: the focus moves one item at a time (`j`/`l`/`↓`/`→` on,
  `h`/`k`/`↑`/`←` back); `Enter` opens the value's input popup, and radio and checkbox options are chosen in place; the
  focus is a block; the label colours; a value's own errors are refused in the input popup.
- **What differs: there is no submit.** Each value takes effect and is saved the moment it is confirmed with `Enter` in
  the input popup, and a switch or radio option the moment it is chosen in place. So there is no action row, no `Ctrl-S`,
  and no "ask first when changed". locku and webu already work this way.
- **The focus block** (the user, 2026-10-07): a Subtext1 background with Base bold text, spanning as in a form from the
  start of the item to the panel's inner right edge (from the value for a field, from the option for an option). It is
  the cursor colour the family already uses in panels (locku's settings, webu's page fields and lists); a popup uses its
  layer colour and a panel Subtext1 — one way of drawing "the cursor is here", the background following where it is.
- **Label colours** (the user, 2026-10-07):

  | Label state | Colour |
  |---|---|
  | Normal | Blue (as the focused double frame) |
  | Disabled | Surface2 |
  | Its value has an error | Red, over any other colour |

  The same idea as a form, whose labels take the layer colour — the popup frame's colour. An unfocused panel has its
  whole content dimmed by Rules T2, Blue included, so Blue is bright only in the panel holding the keys ([`color`](../color.md)'s "Blue only
  for where the keys go"). How it came about: the user asked what was wrong with plain Blue; I first proposed Text (values
  are mostly Text too, breaking "a label and its value never share a colour"), then "Blue when focused, Overlay0 when
  not", which turned out to break defaults D2 rule 6 (now in `color`), "unfocused content is not dimmed"; the user pointed out that unfocused panels
  should be dimmed, logs and the like excepted — the rules said "up to the app, not dimmed by default", and the user made
  it required across the family (T2 and that rule changed), so labels are simply Blue.
- **`h`/`l`** move between items in a one-value-per-row panel, by the form's hjkl. As rules K12 says: back and on in a panel without tabs; in a panel with tabs, `h`/`l` switch tabs and `j`/`k` move
  between items.

## A search row typed into a panel

`/` brings up a row at the top of the panel, and the list is filtered live as you type, with no popup (kbu's panel search,
sshu's Hosts, webu's list filters). Settled by the user, 2026-10-07.

```
╔[2] Hosts═════════════════════════════════════╗
║  prod                                  2 of 5║   ← search row
║ prod-web-01        deploy   10.0.3.14        ║
║ prod-db            postgres 10.0.3.20        ║
╚══════════════════════════════════════════════╝
```

The search row has two states:

- **Typing**: the input state (K8); letters are characters, and the list is filtered live.
  - `↑`/`↓` move the cursor among the matches (arrow keys type nothing, so there is no clash).
  - `Enter` ends typing, keeps the filter, and **moves the focus to the cursor item without running it**; a second `Enter`
    runs it (changed by the user, 2026-10-07: first settled as "`Enter` also does the item's action", which made the only
    way from typing back to the list open something on the way). With no match, `Enter` is the same as `Esc`.
  - `Esc` clears the filter and ends typing.
  - `Tab` ends typing, keeps the filter, and moves the focus to the next panel as K2 says (`Tab` changes panels while typing
    too, so nobody is trapped in the search row).
- **Filter kept**: the panel works as usual on the filtered list; `j`/`k`, hotkeys and `Enter` do what they normally do.
  The search row stays on screen, drawn in grey (Overlay0, like the side of a finder that does not hold the keys). `Esc`
  clears the filter; `/` goes back to typing.

The focus leaving and returning (settled by the user, 2026-10-07):

- **The filter stays when the focus leaves the panel**, whichever way it leaves: the filter is how this panel looks now,
  and a glance at another panel should not wipe it.
- **When the focus returns to a panel with a search row, it is typing at once**, without `/` (the user; sshu's way). To
  work on the filtered list, `Enter` moves the focus to the item.
- **`/` with a kept filter** continues the old text, the cursor at its end; to start over, `Esc` to clear it, then `/`.

# checkbox (a switch, or ticking several)

**Language**: English · [繁體中文](checkbox-zh_TW.md)

## Purpose

A switch, or ticking several from a group. A switch and a group of five or fewer are drawn straight in the form or the
panel and flip in place; more than five open a checkbox popup (e.g. kbu's namespace picker). The checkbox popup is a
kind of finder ([`input/finder`](finder.md)): only what differs is written here.

## Look

- Glyphs: ticked `nf-md-checkbox_marked` (U+F0132, a solid tick), not ticked `nf-md-checkbox_blank_outline` (U+F0131).
  A ticked one's text is Green (in effect); in a popup it follows the tick on screen, Green as soon as `Space` ticks it
  ("Markers in the list" in [`finder`](finder.md)).
- **An option not available** (e.g. ccdrawu's item that needs an API it cannot get yet): drawn in its place, the whole
  row Surface2, the tick too — Unavailable in [`color`](../color.md) wins over In effect; a ticked one shows by the solid
  tick's shape. It only shows a state and blocks nothing (see Keys); under the cursor it is drawn as the cursor block,
  like any other row. The same in a form, on a panel and in a checkbox popup.
- **The checkbox popup**: the finder's skeleton without a preview; a checkbox glyph before every row ("Markers in the
  list" in the finder); the width set by the options.

**Why**: a tick in a square and a dot in a circle (radio) are the convention of GUI forms, understood by everyone
(Principle P1). The tick is the solid one: in a TUI an outline glyph's lines may be too thin to see clearly. An option not available is Surface2 all along the row, its tick
not Green: Green says in effect, and a ticked option not available gets no effect; the solid tick's shape already says
it is ticked.

## Keys

**In a form or a panel**: `Enter` flips it in place; the focus stays, and it takes effect at once. In a form `Space`
flips it too (the exception of Rules K5, as in a checkbox popup); on a panel `Space` still opens the Space menu.

**The checkbox popup**:

- It opens with the focus on the list and the cursor on the option the app names (where it starts is the app's choice;
  the first option when none is named).
- **`Space`**: ticks or unticks the cursor's row — only the tick on screen changes; nothing is written back and nothing
  takes effect (an exception to Rules K5).
- **`Enter`**: writes back the whole set currently ticked at once and closes the popup; only then does it take effect.
  Opened from a form, it is written back to that field, the form notes it as changed, and the focus stays on that
  field; opened on its own, it applies only then (e.g. kbu's panel 2 refetches only then). `Enter` with nothing
  changed: no change; it closes.
- **`Esc`**: cancels; none of the ticks count, and the value stays as it was when opened. No asking first: a popup has
  only one value.
- **An option not available works like any other**: the cursor stops on it, `Space` ticks or unticks it, and `Enter`
  writes back the ticks on screen. What not available means and what to do with a ticked one (e.g. the drawer shows
  `api unavailable`) is the app's choice; tdp only draws the state.
- The typing row follows the finder; with many options, typing filters, and options not available are listed too.
- **Hint**: on the list `Enter:apply Space:toggle Tab|/:filter Esc:cancel`; on the typing row
  `Enter|Tab:list Esc:cancel`. Filtered down to no results: on the list `Enter` still writes back the whole set ticked (the
  filter does not change what is ticked, and ticks filtered out count too), and `Space` has nothing to tick, so the hint
  drops `Space`: `Enter:apply Tab|/:filter Esc:cancel`; on the typing row `Enter` does nothing as in the finder:
  `Tab:list Esc:cancel`.

E.g. it opens with `default` ticked. Press `j` `Space` (ticking `kube-system`), then `j` `Space` (ticking
`monitoring`); panel 2 has not changed yet. On `Enter`, the three take effect together; on `Esc`, it is still only
`default`.

**Why**: ticking with `Space` is the familiar way (GUI check boxes, the multi-select lists of many TUIs); `Enter` is
kept for confirming the whole set, as in every other input popup; and `Esc` goes back to meaning "cancel". Options not available are still drawn, can be stopped on and
ticked: if a ticked one could not be reached, the user could not take it off (an Account left on by an old config could
only be removed by editing the config file); whether it works and what a tick on it does are the app's business, and tdp
only shows that it is not available now. Hidden, the user would think the option is not there (the same idea as Rules M6).

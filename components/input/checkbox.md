# checkbox (a switch, or ticking several)

**Language**: English · [繁體中文](checkbox-zh_TW.md)

## Purpose

A switch, or ticking several from a group. A switch and a group of five or fewer are drawn straight in the form or the
panel and flip in place; more than five open a checkbox popup (e.g. kbu's namespace picker). The checkbox popup is a
kind of finder ([`input/finder`](finder.md)): only what differs is written here.

A group of options always comes with a `Select all` row of its own, not an option (see "Select all" below); a switch
has none.

A switch may instead be drawn as a [`radio`](radio.md) with two options, `off` and `on`, the app's choice.

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

## Select all

- A group of options (a switch is not one) always comes with a `Select all` row, drawn first: in a form or on a panel on
  the label's row, the options below it; in a checkbox popup as the list's first row, scrolling with the list. Its
  glyph and colour are drawn as an option's, Green when ticked; the focus and the cursor stop on it.
- **It is not an option**: it is not part of the value and does not count towards the five; only the options' ticks are
  written back. The app adds no option of its own standing for all of them (e.g. kbu's old `All Namespaces`): that is a
  misuse. What every option ticked means is the app's reading (e.g. kbu reads it as the whole cluster, namespaces
  created later included).
- **Flipping it**: ticking it ticks every option, unticking it unticks them all, options not available included. The
  key and when it takes effect are an option's: at once in a form or on a panel; in a checkbox popup only the ticks on
  screen change, written back on `Enter`.
- **It shows the state as it is**: it is ticked only while every option is. Unticking any option unticks it; ticking
  them all one by one ticks it; opened with all of them ticked, it is ticked.
- **Hidden while filtering**: while the checkbox popup's typing row holds text, the row is not drawn; it comes back when
  the text is cleared.

E.g. `default`, `kube-system`, `kube-public` and `monitoring`, with `kube-system` and `kube-public` ticked: `Select all`
is not ticked. `Space` on `Select all` ticks all four, and it is ticked too; `Space` on `default` then unticks it, and
`Select all` goes off with it while the other three stay.

**Why**: ticking and unticking a whole group is something every group needs (the GUI convention); in the component it
is the same in every app, and no app builds its own. An app's own "all" option fights the other ticks: tick it, then
`default`, and what is written back is still all, `default` quietly lost (kbu's KB31). The row shows the group's true
state; while filtering, the options filtered out cannot be seen, and however it were drawn it would not be the true
state at that moment, so it is hidden (the user, 2026-10-24).

## Keys

**In a form or a panel**: `Enter` flips it in place; the focus stays, and it takes effect at once. In a form `Space`
flips it too (the exception of Rules K5, as in a checkbox popup); on a panel `Space` still opens the Space menu. The
hint: `Enter|Space:toggle` in a form ([`dialog/form`](../dialog/form.md)); on a panel only `Enter` flips it, so
`Enter:toggle`.

**The checkbox popup**:

- It opens with the focus on the list and the cursor on the option the app names (where it starts is the app's choice;
  the first option, not `Select all`, when none is named).
- **`Space`**: ticks or unticks the cursor's row (the whole group on `Select all`, see "Select all") — only the tick on screen changes; nothing is written back and nothing
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

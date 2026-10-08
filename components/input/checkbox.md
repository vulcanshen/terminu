# checkbox (a switch, or ticking several)

**Language**: English · [繁體中文](checkbox-zh_TW.md)

## Purpose

A switch, or ticking several from a group. A switch and a group of five or fewer are drawn straight in the form or the
panel and flip in place; more than five open a checkbox popup (e.g. kbu's namespace picker). The checkbox popup is a
kind of finder ([`input/finder`](finder.md)): only what differs is written here.

## Look

- Glyphs: ticked `nf-md-checkbox_marked` (U+F0132, a solid tick), not ticked `nf-md-checkbox_blank_outline` (U+F0131).
  A ticked one's text is Green (in effect).
- **The checkbox popup**: the finder's skeleton without a preview; a checkbox glyph before every row ("Markers in the
  list" in the finder); the width set by the options.

**Why**: a tick in a square and a dot in a circle (radio) are the convention of GUI forms, understood by everyone
(Principle P1). The tick is the solid one: in a TUI an outline glyph's lines may be too thin to see clearly.

## Keys

**In a form or a panel**: `Enter` flips it in place; the focus stays, and it takes effect at once.

**The checkbox popup**:

- It opens with the focus on the list.
- **`Space`**: ticks or unticks the cursor's row — only the tick on screen changes; nothing is written back and nothing
  takes effect (an exception to Rules K5).
- **`Enter`**: writes back the whole set currently ticked at once and closes the popup; only then does it take effect.
  Opened from a form, it is written back to that field, the form notes it as changed, and the focus stays on that
  field; opened on its own, it applies only then (e.g. kbu's panel 2 refetches only then). `Enter` with nothing
  changed: no change; it closes.
- **`Esc`**: cancels; none of the ticks count, and the value stays as it was when opened. No asking first: a popup has
  only one value.
- The typing row follows the finder; with many options, typing filters.
- **Hint**: on the list `Enter:apply Space:toggle Tab:filter Esc:cancel`; on the typing row
  `Enter/Tab:list Esc:cancel`.

E.g. it opens with `default` ticked. Press `j` `Space` (ticking `kube-system`), then `j` `Space` (ticking
`monitoring`); panel 2 has not changed yet. On `Enter`, the three take effect together; on `Esc`, it is still only
`default`.

**Why**: ticking with `Space` is the familiar way (GUI check boxes, the multi-select lists of many TUIs); `Enter` is
kept for confirming the whole set, as in every other input popup; and `Esc` goes back to meaning "cancel".

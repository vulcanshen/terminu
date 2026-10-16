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
- **A disabled option** (one that cannot be changed now): drawn in its place, the whole row Surface2, the tick too —
  Unavailable in [`color`](../color.md) wins over In effect; a ticked one shows by the solid tick's shape. The same in
  a form, on a panel and in a checkbox popup.
- **The checkbox popup**: the finder's skeleton without a preview; a checkbox glyph before every row ("Markers in the
  list" in the finder); the width set by the options.

**Why**: a tick in a square and a dot in a circle (radio) are the convention of GUI forms, understood by everyone
(Principle P1). The tick is the solid one: in a TUI an outline glyph's lines may be too thin to see clearly. A disabled option is Surface2 all along the row, its tick not
Green: a bright green tick would read as still usable, and the solid tick's shape already says it is ticked.

## Keys

**In a form or a panel**: `Enter` flips it in place; the focus stays, and it takes effect at once. In a form `Space`
flips it too (the exception of Rules K5, as in a checkbox popup); on a panel `Space` still opens the Space menu.

**The checkbox popup**:

- It opens with the focus on the list and the cursor on the option the app names (where it starts is the app's choice;
  the first option when none is named). When that option is disabled, the cursor goes on to the first one after it that
  can be chosen, or back to one before it when none after can (skipping disabled ones, as a
  [`dialog/form`](../dialog/form.md) opens).
- **`Space`**: ticks or unticks the cursor's row — only the tick on screen changes; nothing is written back and nothing
  takes effect (an exception to Rules K5).
- **`Enter`**: writes back the whole set currently ticked at once and closes the popup; only then does it take effect.
  Opened from a form, it is written back to that field, the form notes it as changed, and the focus stays on that
  field; opened on its own, it applies only then (e.g. kbu's panel 2 refetches only then). `Enter` with nothing
  changed: no change; it closes.
- **`Esc`**: cancels; none of the ticks count, and the value stays as it was when opened. No asking first: a popup has
  only one value.
- **A disabled option**: the cursor skips it (`j|k` do not stop on it, as with a disabled option in a
  [`dialog/form`](../dialog/form.md) and Rules M6), so `Space` never reaches it; a ticked one stays ticked and is still
  part of the set `Enter` writes back. No reason is written (M6).
- The typing row follows the finder; with many options, typing filters. **Disabled options still appear in the
  results**, Surface2 and skipped by the cursor; when only disabled options are left, it is as with no results — the
  cursor has nowhere to stop (e.g. `Enter` on the typing row does nothing, as in the [`finder`](finder.md)'s typing row).
- **Hint**: on the list `Enter:apply Space:toggle Tab|/:filter Esc:cancel`; on the typing row
  `Enter|Tab:list Esc:cancel`.

E.g. it opens with `default` ticked. Press `j` `Space` (ticking `kube-system`), then `j` `Space` (ticking
`monitoring`); panel 2 has not changed yet. On `Enter`, the three take effect together; on `Esc`, it is still only
`default`.

**Why**: ticking with `Space` is the familiar way (GUI check boxes, the multi-select lists of many TUIs); `Enter` is
kept for confirming the whole set, as in every other input popup; and `Esc` goes back to meaning "cancel". Disabled options are still drawn, and still listed when filtering: hidden,
the user would think the option is not there (Rules M6).

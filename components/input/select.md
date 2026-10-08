# select (choose one value from a list)

**Language**: English · [繁體中文](select-zh_TW.md)

## Purpose

Choosing **one** value from a list: a `<select>` on a webu page, kbu's context picker, a form field with more options
than fit; a slider's list of numbers and a color picker's 00–FF are selects too. For five options or fewer drawn in a
form, use [`radio`](radio.md); for several values, the popup of [`checkbox`](checkbox.md).

A select is a kind of finder ([`input/finder`](finder.md)): only what differs from the finder is written here.

## Look

- The finder's skeleton, **without a preview**; the typing row is always shown, even for a short list.
- A radio glyph before every row, the current value in Green ("Markers in the list" in the finder).
- Options may have hotkeys (e.g. webu's digit keys), written as in Rules M5; whether to have them is the app's choice.
- **Width**: the options are known when it opens, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).

## Keys

- **It opens with the focus on the list, the cursor on the current value.**
- `Enter` on the list: chooses — the value written back, the popup closed; opened from a form, the focus stays on that
  field.
- Other keys of the typing row and the list follow the finder.
- **Hint**: on the list `Enter:choose Tab:filter Esc:cancel`; on the typing row `Enter/Tab:list Esc:cancel`.

**Why**: choosing a value is mostly moving a step or two from the current one: opening on the list, `Enter` (to open)
`j` `Enter` is all it takes; opening on the typing row would need one more press. With the typing row always shown, the
box's height need not change to filter (Rules F7).

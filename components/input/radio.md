# radio (one of a few)

**Language**: English · [繁體中文](radio-zh_TW.md)

## Purpose

One of a few, five options or fewer: drawn straight in the form or the panel ("Options drawn in the form" in
[`dialog/form`](../dialog/form.md)). More than five use [`select`](select.md).

## Look

```
Auth        󰐾 password
            󰐽 privatekey
            󰐽 credential
```

- Glyphs: chosen `nf-md-radiobox_marked` (U+F043E), not chosen `nf-md-radiobox_blank` (U+F043D). A select uses the same
  pair.
- The chosen one's text is Green (in effect), the others Text.
- Always down, one option a row: the focus block runs from the option to the frame, and across it would cover the
  options after it and hide whether they are chosen; nor is "short enough to run across" left to the app.

## Keys

- Each option is an item; `j|k` (or `h|l`) move between the options (Rules K12).
- `Enter`: chooses it; the focus stays, and it takes effect at once.

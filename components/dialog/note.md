# note (read-only content)

**Language**: English · [繁體中文](note-zh_TW.md)

## Purpose

Read-only content that scrolls (`j`/`k`, `u`/`d`, `gg`/`G`, K12) and may have hotkeys and modes of its own (F1): the key reference, a YAML view, the app log, the error popup.

## Error popup

The note laid over a popup whose action failed (a submit error; see the error row in [`layout/popup`](../layout/popup.md)).
The whole message opened with `Enter` on a form's error row is one too. Settled by the user, 2026-10-07.

- **Look**: frame, title and text in Red. The message wraps inside the frame; when long it scrolls with `j`/`k`, like any
  other note.
- **Title**: what failed (`Rename failed`, `Save failed`), following "the title says what the popup is for". Opened from a
  form's error row, it is the field's name (`Port`).
- **Closing**: both `Enter` and `Esc` close it, hint `Enter/Esc:close`. There is nothing on it to run, and `Enter` once it
  is read is a reflex (K3); pressing `Enter` repeatedly does no harm — the first closes it, the next only submits again
  from the button.
- **After closing**: back to the popup underneath, the focus where it was, every value still there (F4).

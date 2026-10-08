# datetime-picker (date and time)

**Language**: English · [繁體中文](datetime-picker-zh_TW.md)

An input popup for choosing a date (date picker) or a date and time (datetime picker). The calendar takes after
[pickdate](https://github.com/maraloon/pickdate), made the family's own. Settled by the user, 2026-10-07.

## Purpose

Choosing a date, or a date and a time.

## Look

**The date**:

```
╭─ Due date ─────────────────────────────────╮
│                                            │
│         October    2026                    │   ← month, year: each an item that can take the focus, layer colour bold
│    Mo  Tu  We  Th  Fr  Sa  Su              │   ← weekdays: Overlay0
│                 1   2   3   4              │
│     5   6   7   8   9  10  11              │   ← the 7th is today: underlined
│    12  13  14  15  16  17  18              │   ← the 15th is the current value (Green), where the cursor opens
│    19  20  21  22  23  24  25              │
│    26  27  28  29  30  31                  │
│                                            │
╰─ Enter:choose t:today Tab:month Esc:cancel ╯
```

- The calendar day under the cursor is drawn like a menu's cursor (layer colour background, dark bold). The field's
  current value is in Green (as select's "chosen value"); the cursor opens on it, or on today when there is none.
- Today is underlined, with no colour of its own; weekends get no colour either (P4: no new colour meanings; pickdate
  colours both).
- The week starts on Monday or Sunday, as the app decides (calendars in Taiwan mostly start on Sunday, ISO on Monday).
- When the month or the year has the focus, that word is drawn as a cursor (layer colour background, dark bold).

**Date and time**: a vertical separator on the right sets off another area for the time (the user); a date picker has no
such area.

```
╭─ Meeting ──────────────────────────────────┬────────────╮
│                                            │            │
│         October    2026                    │ 󰐽 09:50    │
│    Mo  Tu  We  Th  Fr  Sa  Su              │ 󰐽 09:55    │
│                 1   2   3   4              │ 󰐽 10:00    │
│     5   6   7   8   9  10  11              │ 󰐾 10:05    │   ← 10:05 is the current value: Green
│    12  13  14  15  16  17  18              │ 󰐽 10:10    │
│    19  20  21  22  23  24  25              │ 󰐽 10:15    │
│    26  27  28  29  30  31                  │ 󰐽 10:20    │
│                                            │            │
╰─ Enter:time t:today Tab:time Esc:cancel ───┴────────────╯
```

- The separator takes the border's colour and joins the top and bottom borders (`┬`, `┴`), the same way as the separator
  above a form's action row.
- Times start at 00:00, **one every 5 minutes** (the user: 15 was too coarse). The list follows [`select`](select.md): a
  radio glyph before every row, the current value in Green; as tall as the calendar, scrolling beyond; `/` filters by
  typing (`10:3` leaves 10:30, 10:35). When the current value falls between steps (10:07), the cursor opens on the step
  before it (10:05).
- The cursor in the area holding the keys has the layer colour background, the cursors elsewhere a faint highlight
  (Subtext1 background), as in a finder.

## Keys

Four areas can take the focus: **month, year, calendar, time** (no time in a date picker). The whole picker uses `Tab`,
hjkl, `Enter` and `Esc`, plus `t` (settled by the user, 2026-10-07; pickdate's `p`/`n`/`P`/`N` for months and years are
dropped — they are movement, absent from the hint, and hard to discover).

- **`Tab`** moves the focus in screen order: month → year → calendar → time → back to month. It opens on the calendar.
- **On the month or the year**: `h`/`l` (`←`/`→`) go to the previous or next month or year; the calendar turns with it,
  the cursor on the same day (on the last day when the month has no such day).
- **On the calendar**: `h`/`l` a day back or on, `j`/`k` a week, crossing into the next month naturally — arrow keys in a
  grid mean up, down, left and right (back and on in a one-dimensional list; rules K12).
- **`Enter`**:
  - On the month or the year: moves the focus to the calendar, choosing nothing ("`Enter` first focuses the item").
  - On the calendar: a date picker **confirms** (writes back and closes); a datetime picker takes the date and moves the
    focus to the time.
  - On the time: confirms the date and time together and closes.
- **`t`**: jumps the date to today, from any area; on the time it also moves the time's cursor to now (the step before
  it — added by me).
- **`Esc`**: closes, changing nothing.
- **Hint** (the user: `t` goes on the hint):

| Focus on | Hint |
|---|---|
| Calendar (datetime) | `Enter:time t:today Tab:time Esc:cancel` |
| Calendar (date only) | `Enter:choose t:today Tab:month Esc:cancel` |
| Month | `h/l:month Enter:days t:today Tab:year Esc:cancel` |
| Year | `h/l:year Enter:days t:today Tab:days Esc:cancel` |
| Time | `Enter:choose t:today Tab:month Esc:cancel` |

  The order is changing the value (`h/l`) → `Enter` → `t` → `Tab` → `Esc`; `Tab` names the next area (a key that switches
  phase is written). The longest is 48 characters, which fits an 80-column terminal (popup width as F7); when it does not
  fit, items go whole from the end: `Esc:cancel` first, then `Tab:…`.

## Value

- **Range**: as with a slider, an earliest and a latest may be set; days outside are drawn in Surface2 and the cursor does
  not stop on them.
- **In a form or a panel**: the formatted date (and time), in the app's format (`2026-10-15`, `2026-10-15 10:05`); empty
  follows text's rule for empty values.
- Today: webu has users type a format string; it changes to this picker.

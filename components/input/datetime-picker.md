# datetime-picker (date and time)

**Language**: English · [繁體中文](datetime-picker-zh_TW.md)

## Purpose

Choosing a date (date picker), or a date and a time (datetime picker). The calendar takes after
[pickdate](https://github.com/maraloon/pickdate), made the family's own.

## Look

**The date**:

```
╭─ Due date ───────────────────────────────────╮
│                                              │
│     October   2026                           │   ← month, year: each an item that can take the focus
│     Mo  Tu  We  Th  Fr  Sa  Su               │   ← weekdays: Overlay0
│                  1   2   3   4               │
│      5   6   7   8   9  10  11               │   ← the 7th is today: underlined
│     12  13  14  15  16  17  18               │   ← the 15th is the current value: Green; the cursor opens here too
│     19  20  21  22  23  24  25               │
│     26  27  28  29  30  31                   │
│                                              │   ← the 6th row: unused this month, kept all the same
│                                              │
╰─ Enter:choose t:today Tab:month Esc:cancel ──╯
```

- The month and the year are each an item that can take the focus; with the focus, that word is drawn as a cursor
  (layer colour background, Base bold).
- The calendar **always draws 6 rows**: a month spans 4 to 6 weeks, and with 6 rows fixed the box's height does not
  change with the month (Rules F7).
- The calendar day under the cursor is drawn like a menu's cursor. **The day under the cursor is the day to be written
  back**; there is no separate "chosen but not yet confirmed" state.
- The field's original value is in Green (as a select's current value); the cursor opens on this day, or on today when
  there is no value.
- Today is underlined, with no colour of its own; weekends get no colour either (Principle P4: no extra colour
  meanings).
- The week starts on Monday or Sunday, as the app decides.
- Days outside the range are in Surface2 (disabled), and the cursor does not stop on them.

**Date and time**: a vertical separator on the right sets off another area for the time; a date-only picker has no such
area.

```
╭─ Meeting ───────────────────────────────────╮
│                                             │
│     October   2026              │  06   50  │
│     Mo  Tu  We  Th  Fr  Sa  Su  │  07   55  │
│                  1   2   3   4  │  08   00  │
│      5   6   7   8   9  10  11  │  09   05  │
│     12  13  14  15  16  17  18  │  10   10  │   ← hour 10 and minute 05 are the current value: Green
│     19  20  21  22  23  24  25  │  11   15  │
│     26  27  28  29  30  31      │  12   20  │
│                                 │  13   25  │
│                                             │
╰─ Enter:time t:today Tab:time Esc:cancel ────╯
```

- The separator follows [`layout/popup`](../layout/popup.md): it does not join the top and bottom borders and is drawn
  only on the content rows.
- **The time is split into two columns, hour and minute**: hours 00–23, minutes one step every 5 minutes (00–55). Both
  columns are short and need no search, so this area is not a finder. The current value is in Green; as tall as the
  calendar, scrolling beyond. When the current value falls between steps (10:07), the cursor opens on the nearest step
  before it (10:05).
- In the area holding the focus the cursor has the layer colour background; in the area without the focus, the cursor
  is the layer colour cursor, dimmed once more (Principle P6).
- **Width**: the layout is fixed, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md).

**Why**: choosing a date and time is "picking", and moving is enough for it; split into hour and minute columns, the
time is read at a glance.

## Keys

What can take the focus: **month, year, calendar, time** (no time in a date-only picker). The whole picker uses only
`Tab`, hjkl, `Enter` and `Esc`, plus `t`.

- **`Tab`** moves the focus in screen order: month → year → calendar → time → back to month. It opens with the focus on
  the calendar.
- **On the month or the year**: `h`/`l` (`←`/`→`) go to the previous or next month or year; the calendar turns with it,
  the cursor on the same day (on the last day when that month has no such day).
- **On the calendar**: `h`/`l` a day back or on, `j`/`k` a week back or on, crossing the month's end into the next
  month naturally (in a grid the arrow keys are up, down, left and right, Rules K12). Days outside the range are
  skipped, stopping on the next day within the range in that direction; when there is none left in that direction, it
  does not move.
- **On the time**: `j`/`k` move within a column, `h`/`l` switch between the hour and minute columns.
- **`Enter`**:
  - On the month or the year: moves the focus to the calendar, choosing nothing.
  - On the calendar: date only → **confirms** (writes back and closes); datetime → moves the focus to the time.
  - On the time: confirms, writing back "the day under the calendar's cursor" plus "the step under the time's cursor",
    and closes.
- **`t`**: jumps the date to today, from any area; pressed on the time, the time's cursor also jumps to now (the minute
  rounded down to the nearest 5).
- **`Esc`**: closes, changing nothing.
- **Hint** (order as in [`layout/popup`](../layout/popup.md): `Enter` first, `Esc` last; `Tab` names the next area):

| Focus on | Hint |
|---|---|
| Calendar (datetime) | `Enter:time t:today Tab:time Esc:cancel` |
| Calendar (date only) | `Enter:choose t:today Tab:month Esc:cancel` |
| Month | `Enter:days h/l:month t:today Tab:year Esc:cancel` |
| Year | `Enter:days h/l:year t:today Tab:days Esc:cancel` |
| Time | `Enter:choose t:today Tab:month Esc:cancel` |

**Why**: months and years are not changed with pickdate's `p`/`n`/`P`/`N`: those are movement, absent from the hint,
and hard for users to discover; `t` does get used, so it is written on the hint.

## Value

- **Range**: an earliest and a latest may be set.
- **In a form or a panel**: the formatted date (and time), in the app's format (`2026-10-15`, `2026-10-15 10:05`);
  empty follows the rule for empty values in [`input/README`](README.md).

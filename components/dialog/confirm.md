# confirm (confirmation)

**Language**: English · [繁體中文](confirm-zh_TW.md)

## Purpose

One question, `Enter` accepting and `Esc` cancelling, saying what follows (Rules F6): before deleting, before quitting,
"Connect to X?", before doing something to a row of a jobs list (its content is the row's full text; the jobs list in
[`dialog/menu`](menu.md)). Which actions ask is up to the app (F6).

## Look

```
┏━󰻌 QUIT━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                 ┃
┃ 2 live sessions will be closed. ┃  ← content to read first: Overlay0; the warning sentence in Peach
┃                                 ┃
┃ Quit sshu?                      ┃  ← the question: Text, last
┃                                 ┃
┗━ Enter:quit Esc:cancel ━━━━━━━━━┛
```

- **Title**: `nf-md-shield_alert` (U+F0ECC) plus the action's name (`DELETE`, `QUIT`, `CONNECT`).
- **The question comes last**, with the hint right below it. What to read before answering sits above the question, with
  a blank row between them (Rules F1); with nothing to read, there is only the question. The content may have several
  sentences, given by the app a row each ("Control characters" in [components](../README.md)), with no blank row
  between them.
- **Colours**: the question in Text, not bold; the content in Overlay0; the warning sentence in the content (e.g. "This
  cannot be undone", "2 sessions will be closed") in Peach, which sentence counts as a warning being up to the app.
- **Too long**: the question and the content both wrap (as in [the components' "Wrapping"](../README.md)), never cut. When the content is long, only the content scrolls
  with `j|k`; the question stays fixed at the end.
- **Width**: the content is known when it opens, so it follows "content width known when it opens" in
  [`layout/popup`](../layout/popup.md); anything longer wraps at the cap.

**Why**: the reading order is the content first, then the question, and the keys last; the question sits right against
the hint, so on reaching the question the answer is on the next row. A shield in the title: a confirm exists to stop
this one moment and make the user think again; a warning ⚠ hung on every confirm would use up what a warning means
(Principle P4). Peach rather than Red for a warning: Red is an error that has already happened, and at this point
nothing has gone wrong yet.

## Keys

- `Enter` accepts, `Esc` cancels (Rules F6); these are the only two answers (no `y` or `n`).
  `Space` does nothing (Rules K5).
- **Hint**: `Enter:<verb> Esc:cancel`, the verb saying what accepting does (e.g. `Enter:delete Esc:cancel`). The one exception is "When it cannot be
  read" in Rules E3: `Esc` quits the app, written `Esc:quit`.
- **Opened from a menu**: `Esc` cancels and always returns to the menu (Rules F4); after `Enter`, whether the menu
  stays follows the table in Rules T1, by what accepting does — a confirm is only a gate, not a kind of target.

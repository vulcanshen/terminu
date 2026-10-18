# terminu checklist

**Language**: English · [繁體中文](README-zh_TW.md)

terminu checklist is the item list of [tdp](../principle/README.md): the requirements of the principle, the components
and the project spec, broken into items that can each be checked, for judging how much of tdp a family app meets.
Versions and the CHANGELOG are shared with tdp; each tdp version has its own list. The items are in
[`items.md`](items.md).

## The spec is what counts

- The list is broken out of the spec; where the two disagree, the spec's text wins, and the disagreement is reported as
  a gap in tdp.
- **Judged on tdp alone, never on the implementation**: whether an app uses terminu-go, and whatever language it is
  written in, it is judged by the same list. An app on terminu-go does not meet everything by default either — what
  the app supplies itself (e.g. `docs/icon.svg`, the README, the dev-remarks) is beyond the library.
- The parts the spec leaves up to the app, examples, the "Why" and "Implementation reference (not a requirement)" are
  not broken into items.

## Each item

| Column | What it holds |
|---|---|
| ID | `<source>-<number>` (e.g. `K4-1`, `form-3`), see "IDs" below |
| Source | for the rules, the rule (`K4`); for the components and the project spec, `<file> §<section>` (e.g. `popup §Frame`); for the principle, `P3` or `Terms`. An item taken from a diagram is marked `(diagram)`. IDs are the same in both languages; sources name the sections in each language |
| What to check | one thing that can be answered yes or no |
| Applies to | which feature an app must have for the item to count, see "Applies to" below |
| How to check | which key to press, where on the screen to look; what the screen cannot show says "read the code" or "read the file" |

## IDs

- **Fixed**: when a requirement is removed its ID is retired and never reused; a new requirement goes at the end of the
  same source. Reports from different versions line up by ID.
- **Prefixes**: the rules use the rule (`K4-1`); the components and the project spec use the file name (`popup-3`,
  `checkbox-4`), with `components-` for `components/README`, `input-` for `input/README` and `project-` for
  `project/README`. Passages with no rule number: the rules' opening "Departure" and "Citing" use `departure-` and
  `references-`, the principle's terms use `terms-`, and the opening of chapter S (the splash fills the whole screen)
  uses `S0-`. IDs are plain ASCII, the same in both languages, so that tools can read them.

## Applies to

- **`everyone`**: every family app must meet it.
- **A feature's name**: the item counts only when the app has that feature. Names joined by "or" mean any one of them;
  names joined by "+" mean all of them.
- **A case within a feature**: when an item names a case (e.g. "when a confirm has a warning…"), an app that has the
  feature but never that case has the item ruled not applicable.

| Feature | An app has it when it has |
|---|---|
| several screens | two screens or more (the screen chip row) |
| several panels | a screen with two panels or more |
| panel tab | a panel with tabs |
| one value per row | a one-value-per-row panel |
| grouped list | a grouped list on a panel |
| detail panel | a detail that follows another panel's cursor |
| header | a list with a header (a multi-column ordinary list always has one) |
| sorting | a list that can be sorted |
| marks | a list that can be marked for batch operations |
| Drag | a Drag mode |
| panel filter | a panel filter |
| statusbar | a statusbar |
| streaming content | content that keeps coming in (e.g. a log) |
| loading | a panel or popup that waits for its content |
| mode | a mode (Rules K11) |
| disabled | actions that cannot run for now, or disabled items or fields |
| long task | a long task (the progress under the screen chip row) |
| PTY | a PTY (in a panel or a terminal popup) |
| terminal popup | a terminal popup |
| popup tab | a popup with tabs |
| form | a form |
| viewer | a viewer |
| toast | a toast |
| error popup | an error popup |
| confirm | a confirm |
| input | any kind of input (an input popup, or a field on a form or a panel) |
| text, password, number, select, radio, checkbox, slider, textarea, color picker, datetime picker, file-picker, reorder | that kind of input |
| finder | a finder, or any kind of finder (a select, a checkbox popup and a file-picker are each a kind of finder, input/finder) |
| stores settings or data | settings, data, state or a cache written to disk |
| Windows build | a Windows release |
| mouse | mouse support |

The two languages' lists line up by ID; the Traditional Chinese list names the same features in Chinese
([README-zh_TW.md](README-zh_TW.md)).

## Verdicts

Each item is ruled one of:

| Verdict | Meaning |
|---|---|
| Meets | the item is done |
| Departs | not done, but the "偏離 tdp" (departures from tdp) section of the dev-remarks names the item and the reason (the rules' opening "Departure") |
| Violates | not done, and not written as a departure |
| Not applicable | the app lacks the feature the item applies to, or never has the case the item names |

A judgement names the tdp version it was judged against.

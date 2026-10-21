# terminu checklist

**Language**: English · [繁體中文](README-zh_TW.md)

terminu checklist is the item list of [tdp](../principle/README.md): the requirements of the principle, the components
and the project spec, broken into items that can each be checked, saying what an app made by tdp must do, when, and
where it can be seen. Versions and the CHANGELOG are shared with tdp; each tdp version has its own list. The items are
in [`items.md`](items.md).

The list only says what to check. How to judge — which verdicts there are, how they are counted, what passes — is
decided by the terminu harness, not in tdp (see "How to judge" below).

## The spec is what counts

- The list is broken out of the spec; where the two disagree, the spec's text wins, and the disagreement is reported as
  a gap in tdp.
- **Checked on tdp alone, never on the implementation**: whether an app uses terminu-go, and whatever language it is
  written in, it is checked against the same list. An app on terminu-go does not meet everything by default either —
  what the app supplies itself (e.g. `docs/icon.svg`, the README, the dev-remarks) is beyond the library.
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
  same source. Results from different versions line up by ID.
- **Prefixes**: the rules use the rule (`K4-1`); the components and the project spec use the file name (`popup-3`,
  `checkbox-4`), with `components-` for `components/README`, `input-` for `input/README` and `project-` for
  `project/README`. Passages with no rule number: the rules' opening "Departure" and "Citing" use `departure-` and
  `references-`, the principle's terms use `terms-`, and the opening of chapter S (the splash fills the whole screen)
  uses `S0-`. IDs are plain ASCII, the same in both languages, so that tools can read them.

## Applies to

- **`everyone`**: every app must meet it.
- **A feature's name**: the item counts only when the app has that feature. Names joined by "or" mean any one of them;
  names joined by "+" mean all of them.
- **A case within a feature**: when an item names a case (e.g. "when a confirm has a warning…"), an app that has the
  feature but never that case has the item not applying.
- **A screen that is not part of the TUI** (e.g. locku's screensaver and PIN box while locked) is not a surface: the
  items about "every surface" do not cover it (Rules K1).

| Feature | An app has it when it has |
|---|---|
| several screens | two screens or more (the screen chip row) |
| several panels | a screen with two panels or more |
| panel tab | a panel with tabs |
| one value per row | a one-value-per-row panel |
| grouped list | a grouped list on a panel |
| detail panel | a detail that follows another panel's cursor |
| header | a list with a header (a multi-column ordinary list always has one) |
| location row | a panel's location row (layout/panel) |
| sorting | a list that can be sorted |
| marks | a list that can be marked for batch operations |
| Drag | a Drag mode |
| panel filter | a panel filter |
| statusbar | a statusbar |
| zoom | zooming a panel (layout/screen) |
| streaming content | content that keeps coming in (e.g. a log) |
| panel without a cursor | a panel without a cursor (a preview, a log) |
| loading | a panel or popup that waits for its content |
| mode | a mode (Rules K11) |
| mode (on a panel) | a mode opened on a panel (e.g. a panel's Drag) |
| mode (in a popup) | a mode opened in a popup (e.g. a viewer's selection mode, a reorder's Drag) |
| disabled | actions that cannot run for now, or disabled items or fields |
| long task | a long task (the progress under the screen chip row, or in the task's row in a single-screen app) |
| jobs list | a jobs list: a menu listing the work the app is running or has run (e.g. sshu's Jobs) |
| PTY | a PTY (in a panel or a terminal popup) |
| interactive terminal | a PTY where the user types their own commands (a shell, an ssh session, `kubectl exec`); one the app opens to run a program for one job (an editor, sudo asking for a password) does not count |
| terminal popup | a terminal popup |
| raising privileges | writing files outside the app with the system's tool for raising privileges (e.g. sudo) |
| popup tab | a popup with tabs |
| form | a form |
| viewer | a viewer |
| toast | a toast |
| error popup | an error popup |
| confirm | a confirm |
| input | any kind of input (an input popup, or a field on a form or a panel) |
| text, password, number, select, radio, checkbox, slider, textarea, color picker, datetime picker, file-picker, reorder | that kind of input |
| finder | a finder, or any kind of finder (a select, a checkbox popup and a file-picker are each a kind of finder, input/finder) |
| finder with a preview | a finder with a preview: an ordinary finder, a file-picker (a select and a checkbox popup have none) |
| file preview | a popup previewing files and directories: a file-picker, or a finder previewing files |
| stores settings or data | settings, data, state or a cache written to disk |
| a file no longer used | a new version stopped using a settings, state or data file (e.g. sshu's errors.yaml, kbu's theme.yaml) |
| Windows build | a Windows release |
| has released | a release made (a tag and a GitHub release); for an app not yet released, what only exists after a release (the release, the formula on the tap…) does not apply, and what can be seen is checked on the repo as it is now |
| mouse | mouse support |

A color picker counts as having a select (R, G and B open a 00–FF select on `Enter`), and so a finder.

The two languages' lists line up by ID; the Traditional Chinese list names the same features in Chinese
([README-zh_TW.md](README-zh_TW.md)).

### Family members and apps made by tdp

Where an item gives two ways (the repo's account, the Homebrew tap, the splash's e-mail address, the README's terminu
family section; the opening of chapter E in the rules), check the one for what the app is: a family member, or an app
made by tdp. Every other item is the same for both.

### Screens below the minimum size

Where "How to check" says to shrink the terminal (e.g. narrow widths, when things do not fit), shrink it only as far as
the app's minimum size (Rules L1). Below the minimum size only the name and the hint are drawn: there only L1-3 to L1-6
and the tiny sizes of E5-13 apply, and no other item about the screen does.

## How to judge

The list only says what to check, when an item counts, and where to look. Which verdicts there are, how they are
counted, what passes, how much error to allow when timing from the screen, and how to judge the details of something
an app has not done at all are all decided by the terminu harness.

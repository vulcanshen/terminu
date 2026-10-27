# Changelog

## v0.11.3 — 2026-10-27

What demou met following v0.11.2 (DM42), settled with the user.

- dialog/note: going into the detail with `Enter` on a list (or with its row in the menu) moves the focus (Rules K3)
  and is not recorded in the App Log — the detail already follows the cursor, and going in shows nothing more (note.7)
- changed in this version: note.7
- checklist: no item changed (1453 items); the header names v0.11.3

## v0.11.2 — 2026-10-27

What sshu and kbu met following v0.11.0 (SS46, KB34), settled with the user.

- dialog/note: an operation is done once it is accepted — cancelled with `Esc` at the confirm before it, or at the
  form or input popup that takes its values, it was not done and is not recorded (a confirm is only a door, Rules T1);
  a panel's compare mode (note.8) is not recorded either (note.7)
- changed in this version: note.7
- checklist: note-77 changed (1453 items)

## v0.11.1 — 2026-10-27

Settled with the user (from terminu-go, G103).

- dialog/note: the panel filter is not recorded in the App Log — filtering only changes what is in view, like moving the
  cursor (note.7)
- changed in this version: note.7
- checklist: note-77 changed (1453 items)

## v0.11.0 — 2026-10-27

What the harness trials of hostu and demou found (hostu, DM41), settled with the user. Every app follows this round.

- Rules L1: the standard size is 60×32, not 80×40 — at 60 columns × 32 rows every core task can be completed with
  every panel side by side (two panels split 1:2 still have 20 | 40); a terminal split in half is often under 80
  columns (the user's tmux pane is 77×32). The minimum size defaults to 60×32 and may not be above it; the narrow-width
  threshold may not be above 60 (screen.5); the hint of a popup with only a typing row fits in 60 columns (M3, popup.1)
- Rules L1, layout/screen: below the minimum size a third row says how to quit, `Press [Ctrl-C] twice to quit`
  (Overlay0, written as an empty state's hint); when the rows don't fit, the size hint goes first, then this row, the
  name always staying; a row wider than the screen doesn't fit either (screen.7)
- dialog/note: the App Log's "what the user did" is an operation of the three kinds of Rules P3 — item, panel, global —
  run from a menu, a letter hotkey or `Enter`, one that only looks included (opening a viewer, switching screens);
  moving the cursor or the focus, opening the Space menu, `?` or `!` are not recorded (note.7)
- changed in this version: L1, M3; screen.5, screen.7, popup.1, note.7
- checklist: L1-1 to L1-4, M3-5, screen-26 and note-77 changed (1453 items); the header names v0.11.0

## v0.10.3 — 2026-10-26

What terminu-go met checking an app's project files against the templates (G102), and what the hostu trial of the
harness found (an old `family.mk` without `make dev`), settled with the user.

- project: how far a mark reaches — a `# app:` comment in `goreleaser.yaml` stays as it is and covers the value of the
  key right below it, a list or a whole block included; when the key it names is not in the template yet
  (`dependencies`) the app adds it where the comment is; other keys stay as they are. Opening `Windows` takes the line
  marked `# Windows` with the commented lines of its block, removing only the leading `# `; the trailing `# Windows`
  stays. The `<APP>` in a comment of `uninstall.sh` is not `<app>` and stays as it is. The templates did not change:
  nothing to copy again
- changed in this version: project.2
- checklist: unchanged (1453 items)

## v0.10.2 — 2026-10-26

What the members found moving to v0.10.0 (sshu, kbu, filu: KB32, KB33, FL29), settled with the user.

- layout/panel: loading and errors get a section of their own, panel.15, holding for every kind of panel — an ordinary
  list, one value per row, details, a preview, a log, a PTY cell (e.g. `󰪞 connecting to prod-web-01…`); panel.5 and
  screen.8 point there
- Rules (opening), citing: a project template is cited by its path (`tdp project/install.sh`), meaning that template,
  as the comment at the top of each template says; a checklist item may be cited by its ID (`tdp K9-6`), pointing at
  that item's source, the spec's text still what counts
- dialog/toast: each row starts with a capital letter, the rest as it is; a row starting with a name or a path keeps
  the name's case; each App Log entry follows this too (note.7 points there)
- changed in this version: Rules (opening); panel.5, panel.15 (new), screen.8, toast.2, note.7
- checklist: panel-75 to panel-80 now give panel.15 as their source; toast-20 added (1453 items)

## v0.10.1 — 2026-10-26

Settled with the user (from terminu-go, G101).

- layout/popup: an app's own popup with values to submit leaves to the app how an invalid value is reported — where
  the error row goes and whether it takes the focus — the error still visible (Rules F5)
- changed in this version: popup.8

## v0.10.0 — 2026-10-25

tdp becomes the universe: every decision an app makes has its ground in tdp, either a requirement to follow or a place
tdp explicitly leaves to the app. Asked for by the terminu harness, settled with the user.

- principle: P5 is now "Leaving it to the app explicitly" in place of the fixed and concept zones. What is left to the
  app always says "the app may decide for itself", with its scope and the requirements still holding inside it; what a
  fixed part cannot do is reported as a gap in tdp, which adds a solution or leaves it to the app; the "departure" is
  gone. P5 also sets tdp's scope: the function logic is the app's; the screen requirements cover only the TUI screens
  the app draws itself; developer documents are outside tdp. The term "departure and violation" is retired
- rules: the `fixed` / `concept` tags are gone; the opening says what a requirement is, how things are left to the app
  and how to cite. K3, M8, F5 and T1 (the old concept rules) state what holds and leave the how to the app; every "up to
  the app" across the rules, the components and the project now reads "the app may decide for itself" (K1, K2, K4, K6,
  K9, K10, M5, M6, L1, F6, F7, E1, E7)
- Rules F1 and layout/popup: popups come in eight classes; the eighth, an app's own popup, holds only content the seven
  cannot (e.g. kamonu's popup for drawing cells): its frame and layers work as a popup, with values to submit it works
  like a form, and how its content is drawn and the keys on it are left to the app, the core keys, K12 and `?` still
  holding (K5: `Space` moves a cell with several values to the next one; K9, F3 follow). A box drawn by a panel's own
  content (e.g. a web page's dialog in webu) is content, not a popup
- Rules E7 and E8, project: the dev-remarks and `docs/<app>-terminu-fix.md` are no longer required, nor is "no
  clause-by-clause mapping"; README section 10 links the CHANGELOG; `docs/` holds `icon.svg` and the README's gif; the
  lib's "does not depart" becomes "reports a gap in tdp"
- IDs: every section of the components and the project spec gets an ID, written before its heading: the file name, a
  `.` and a number (`panel.1`), a `README` taking its folder's name (`components.1`, `input.1`, `project.1`); the
  principle's terms get `terms.1` to `terms.12`. A whole component may be cited as its file (`tdp confirm`). IDs are
  never renumbered, and each version's CHANGELOG names the IDs it changed
- layout/panel: features only some lists have get sections of their own: a pointed panel (panel.2), the mode name
  (panel.3), sorting (panel.6), marked rows (panel.7), Drag mode (panel.8), compare mode (panel.9)
- changed in this version: P4, P5, terms.5; K1–K6, K9, K10, M5, M6, M8, L1, F1, F3, F5–F7, T1, E1, E7, E8; components.1,
  components.2, components.6, components.8, color (opening), popup (opening), popup.1, popup.7, popup.8 (new), panel.1–panel.3,
  panel.5–panel.10, panel.12, panel.13, screen.1, screen.4–screen.6, confirm.1, confirm.2, form.1, form.5, form.7,
  note.2, note.5, terminal.7, toast.2, input.10, checkbox.1, checkbox.3, checkbox.4, datetime-picker.2–4, file-picker.2,
  finder.7, password.2, radio.1, select.2, slider.2, project.1, project.3
- checklist: the source column gives the section ID (`popup.1`) instead of the section's name; departure-1, E7-22 to
  E7-37 and project-17 retired; references-1, F1-1, F3-1, E7-13, screen-33, panel-74, toast-6 and toast-16 reworded;
  K5-6, K9-7, F1-18 to F1-20, F3-8, popup-71 to popup-73 added, with two new applicabilities, "an app's own popup" and
  "panel content box" (1452 items)

## v0.9.16 — 2026-10-25

What the user found testing sshu by hand, settled with the user (from sshu, SS44).

- layout/panel: a pointed panel, the app's choice: when the cursor's row in a focused list stands for another panel on
  screen, that panel's frame turns Lavender ("user footprint") and stays an unfocused light line; it points only while
  the list has the focus (color follows)
- checklist: panel-151 to panel-153 added, with a new applicability, "pointed panel" (1461 items)

## v0.9.15 — 2026-10-24

What the user found testing sshu by hand, settled with the user (from sshu, SS43).

- components: the app's own text carries no line breaks. Where there are several rows (an error popup's message, a
  toast, a confirm's content), the app gives them a row at a time, each starting a row of its own, with no blank row
  between them; so a `\n` on screen always comes from outside and is drawn by name. Several lines from outside go into
  short text as the line saying why, the whole into the App Log (dialog/note, dialog/toast and dialog/confirm follow)
- checklist: components-30 to components-32 added (1458 items)

## v0.9.14 — 2026-10-24

What the user asked for in filu, settled with the user (from filu, FL27).

- layout/panel and layout/popup: wherever `h|l` switches tabs, the hint writes `h|l:tab`, right after `Enter`: it
  changes the whole page rather than moving between items, as the datetime picker's `h|l:month` does, and left out the
  other tabs are hard to find. Not with only one tab, nor while `h|l` does something else (dialog/note follows)
- checklist: panel-17, panel-19, popup-10 and popup-11 reworded (1455 items)

## v0.9.13 — 2026-10-24

Settled with the user.

- Rules K11 and layout/panel: a mode with layers adds each layer to its name after a `>`, with no spaces: a viewer's
  selection mode, once selecting, is `Visual>select`. A layer added grows from the tail of the tag a letter a frame,
  the right end staying, and going back takes it off the same way; `Esc` goes back one layer at a time
- dialog/note: in the selection mode, `Esc` while selecting goes back to `Visual` (the selection gone, the cursor where
  it is) instead of leaving the whole mode; the hint while selecting is `y:copy Esc:unselect` (dialog/menu follows)
- checklist: K11-3, note-34 and note-37 reworded, panel-149 and panel-150 added (1455 items)

## v0.9.12 — 2026-10-24

Settled with the user after terminu-go drew v0.9.11's `Select all` (KB31).

- input/checkbox: the options sit two cells further in than `Select all`, as a panel group's items, so the row reads as
  over them; hidden by a filter, the options stay where they are. Disabled options are not flipped by it and not
  counted; with every option disabled it is disabled too. The focus and the cursor never start on it (dialog/form's
  opening follows)
- checklist: form-14 and form-59 reworded, checkbox-31 to checkbox-33 added (1453 items)

## v0.9.11 — 2026-10-24

What the user found testing kbu by hand, settled with the user (from kbu, KB31).

- input/checkbox: every group of options comes with a `Select all` row of its own, first in the group: in a form or on
  a panel on the label's row, in a checkbox popup the list's first row. It is not an option and never part of the
  value; ticking it ticks every option, unticking it unticks them all, and it is ticked only while every option is. In
  a checkbox popup it is hidden while the typing row holds text. An app's own "all" option is a misuse (dialog/form
  follows)
- checklist: checkbox-12, form-49 and form-62 reworded, checkbox-26 to checkbox-30 added (1450 items)

## v0.9.10 — 2026-10-22

What the user found testing kbu by hand, settled with the user (KB30).

- layout/panel: the mode name opens a letter a frame, 32ms a frame as in a popup, instead of over a fixed 288ms: a tag
  has only as many steps as letters, and spread over 288ms each step held for about 72ms and stuttered. The length now
  follows the name (`Drag` about 160ms, `Compare` about 256ms)
- checklist: panel-146 reworded (1445 items)

## v0.9.9 — 2026-10-22

What the user asked for while testing kbu by hand, settled with the user (KB30).

- layout/panel: the mode name opens and closes: entering a mode, the tag opens from its middle (the junctions side by
  side, moving apart, the name showing from its middle), and leaving plays it backwards, about 288ms whatever the
  name's length; switched again halfway, it turns around from where it is. Only the tag animates: the mode takes
  effect at once, the frame turns its colour at once and keys are taken all along (Rules K11 follows)
- checklist: panel-146 to panel-148 added (1445 items)

## v0.9.8 — 2026-10-22

What the user found testing kbu by hand, settled with the user (from kbu, KB29).

- Rules K9: with a popup open, the first `q` or `Ctrl-C` never quits. A quit flow whose first step already asks stays as
  it is; one that would quit at once at that moment opens the quit confirm `Quit <app>?` instead, and `Esc` goes back to
  the popup. On a panel the app's flow runs as it is. What asks is up to the app; that something asks is not
- dialog/menu: the row that leaves a mode is named with the verb `Esc` has in the mode's hint (`[Esc] Leave` in the
  Compare mode, `[Esc] Cancel` where the hint says `Esc:cancel`)
- checklist: K9-4 and menu-26 reworded, K9-6 added (1442 items)

## v0.9.7 — 2026-10-22

What the user found testing kbu by hand, settled with the user (from kbu, KB28).

- Rules K11: "when in doubt, hit `Space`" holds inside a mode too: `Space` opens the mode's Space menu, with the item
  operations (what can be done to the item under the cursor or the selected range, run like any row) and the mode
  operations (the movement keys only shown, leaving the mode runnable); panel, item and global actions are never listed.
  Modes in a popup and on a PTY have it too (Rules K5, dialog/menu, layout/screen's footer and input/reorder follow)
- checklist: K5-3, K5-5, K11-1, M1-1, screen-8 and reorder-19 reworded, menu-23 to menu-27 added (1441 items)

## v0.9.6 — 2026-10-22

What the user found testing kbu by hand, settled with the user (from kbu, KB27).

- layout/panel: a compare mode (Rules K11; the key is the app's): the compare key on a row makes it the anchor, drawn
  all in the mode colour; another row is then compared with it, and closing the comparison goes back to the mode with
  the anchor kept; identical ones only get an Info toast. Only text, or content shown as text, is compared
- dialog/note: the comparison is a viewer titled `DIFF — <anchor> ↔ <the other>` (`nf-md-compare`) with two tabs,
  `UNIFIED` and `SPLIT`, switched with `h|l` and remembered, always UNIFIED below 96 columns; only the parts that
  differ with 3 lines around; added lines Green, removed Red (layout/popup and color follow)
- checklist: panel-138 to panel-145 and note-80 to note-85 added, with a new applicability, "compare mode" (1436 items)

## v0.9.5 — 2026-10-21

Settled with the user before terminu-go drew v0.9.4's capsule chain.

- color: dimming leans towards `#0c0c13`, the step after Crust (catppuccin-mocha's Base, Mantle and Crust lose 3% of
  lightness at each step; this is the next one), instead of Base; the ratio stays 0.45 and dimming still never lightens
  a colour. Colours darker than Base now dim too
- layout/panel: the unselected parts of a capsule chain and its joins are Mantle instead of Crust; covered, they dim
  exactly into Crust; on an unfocused panel the chain is on the border and Mantle stays (layout/screen follows)
- checklist: color-19, panel-31 to panel-37, panel-137 and screen-14 reworded (1422 items)

## v0.9.4 — 2026-10-21

What the user found testing the apps by hand, settled with the user.

- layout/panel: the capsule chain no longer leans on the terminal's background being Base (from kbu, KB26). Unselected
  parts are filled with Crust; every join is a slant, U+E0BC from selected to unselected, U+E0BA from unselected to
  selected, U+E0BB between two unselected parts, all on Crust; the ends keep the terminal's own background outside.
  Crust is not dimmed. The panel title, a panel's tabs, the screen chips and the tabs after a popup title all change
  (color, layout/screen, layout/popup and dialog/terminal follow)
- project: family.mk gains `make dev`, which builds `./<app>` as `make build` does and runs it
- checklist: panel-31 to panel-37 and screen-14 reworded, panel-137 added (1422 items)

## v0.9.3 — 2026-10-21

What the members found while moving to tdp v0.9.2 and terminu-go v0.4.3, settled with the user.

- Rules E3: a settings, state or data file a new version of the app no longer uses is not deleted and gets no toast;
  while it is there, every start writes an INFO entry to the App Log with its path, and the CHANGELOG says so too
  (from sshu, SS42). The question on the confirm for an unreadable file now ends `and start fresh?`, as no new file
  may be made (from terminu-go)
- checklist: E3-23 added, with a new applicability, "a file no longer used" (1421 items)

## v0.9.2 — 2026-10-21

What hostu's review found after moving to tdp v0.9.1, settled from what tdp already says.

- Rules E3: `Enter` on the confirm for an unreadable file starts the app as on its first start — a file the first start
  makes is made again, one it does not make appears at the first save (from hostu, HU21)
- dialog/note: the App Log's examples start with a capital, as a toast does, since an entry holds the toast's own words
  (from hostu, HU23)
- checklist: E3-18 and note-78 reworded (1420 items)

## v0.9.1 — 2026-10-20

What the members found while moving to tdp v0.9.0 and terminu-go v0.4.0, settled with the user.

- Rules E3: lists the user writes for the app are data even when they hold how the app works (locku's and hostu's
  profiles, filu's Open with list, kbu's pins), and so are original values the app keeps for the user (ccdrawu's);
  config is left with the app's own single options. When the data is one record per file, an unreadable record is
  moved to `.bak` and the rest goes on, with nothing new made (kamonu's KM18). The App Log alone does not count as
  using `input_tab_width`.
- components: a list column the app marks as "a line of text" draws a Tab as spaces (webu's DevTools source, WB21).
- checklist: E3-11's applicability narrowed, E3-13 reworded, E3-22 and components-29 added (1420 items)

## v0.9.0 — 2026-10-20

What the rebuilt hostu (its judge, then its reviewer) and terminu-go's tdptest found, settled with the user.

- dialog/terminal: the history and selection modes go by what a PTY is for — an interactive terminal (a shell, an ssh
  session, `kubectl exec`) always has both; a PTY the app opens to run a program for one job (an editor, sudo asking for
  a password) has neither and gives that program every key, `PgUp` included. While the subprocess takes the whole
  screen (vim, less, htop), `PgUp` goes to it; while the user gives every key to the subprocess (sshu's locked cell),
  the selection mode steps aside and `PgUp|PgDn` go straight in. The selection mode is entered with `Alt-v`: the
  family's `v`, with `Alt` to get out of the subprocess, not a key the app picks (Rules K10, M1 and layout/screen follow)
- components: control characters are never sent to the terminal as they are, wherever the app's text shows (from
  terminu-go's tdptest, G100). Content for reading (a viewer, a log on a panel, a file preview) is drawn as a terminal
  would: `\n` breaks the line, even inside a line the app hands over; a Tab is spaces; colour codes colour the text; a
  `\r` within a line keeps only the last state; anything else is a red name. Names and short text (values, list cells,
  menus, titles, toasts, confirms, error popups, options, empty states, the statusbar…) interpret nothing: every
  control character, a Tab and a colour code's ESC included, is a red name, as on a form (dialog/note, input/file-picker,
  layout/panel and color follow)
- dialog/note: every app has an App Log, opened with `!` on a panel (a new core key, Rules K1, F5, M1): what the app
  has done and what went wrong — the user's actions, every toast, the app's background work — one entry per line with
  time and level, kept in memory only; layout/screen: the footer always shows `!:log`, which becomes `!:2 errors` or
  `!:1 warning` until the App Log is opened (from hostu, HU15)
- Rules E3: when the app's own settings, state or data cannot be read, a confirm at start offers to move it to `.bak`
  (never overwriting an older one) and start a new one, or to quit with the reason on stderr; a cache is just rebuilt;
  things outside the app stay a panel error with details in the App Log (dialog/confirm: the one `Esc:quit`). Config
  is only the options the app runs with: lists the user writes for the app are data, the exception for hand-written
  connection lists is gone (sshu's hosts and credentials move to the data directory) (from hostu, HU15, HU17)
- dialog/terminal: raising privileges — the app never asks for or handles a password; the system's tool asks in a
  terminal popup (from hostu, HU18)
- dialog/toast: Success or Info for something finished is the app's call (HU19); input/README: an error need not carry
  the field's name when it can point at what is wrong (HU16)
- checklist: terminal-15–20 apply to an interactive terminal, terminal-18 reworded, panel-31 and panel-64 name the
  features they need, the features "interactive terminal", "panel without a cursor" and "raising privileges" added;
  E3-13, E3-14, K1-1, M1-1, M1-2, screen-6, screen-7, toast-16 and input-1 reworded; terminal-21–24, panel-136,
  components-27–28, note-74–79, file-picker-93, E3-17–21, K1-9, K11-13, F5-3 and screen-35 added (1418 items)
- principle/README and README: the checklist is for checking whether an app does what tdp asks, no longer for counting
  genes (the harness dropped its judge and gene count)

## v0.8.3 — 2026-10-19

From webu, moving a web page's `prompt()` onto the library's input.

- input: a single-line input popup's explanation row wraps when it is too long (several sentences from a web page's
  `prompt()`), and the popup grows by F7's height; when it still does not fit at the tallest, the last row ends with `…`
  (webu's WB20)
- checklist: input-78 added (1395 items)

## v0.8.2 — 2026-10-19

What the apps found while moving to terminu-go v0.2.0, settled with the user.

- layout/panel: column widths reworked (S13 again, from kbu, webu and filu) — the app marks the columns that may be cut
  short (names, URLs, a line of text); they share the width left and are cut their own way, while short columns keep
  their widest value and never shrink. When they do not fit, the columns that may be cut short narrow to their least
  width first, and only then do whole columns go, by the app's order, never the name. One long name no longer pushes
  every other column out, and short columns are no longer squeezed to `…`
- input/file-picker: the preview and the metadata are read in the background; while reading, the preview frame has the
  loading icon after its title, reads `(loading…)` in grey, and the metadata values stay empty; what has been read is
  kept by path (sshu's SS40). input/finder: a preview starting at a line draws a file that fits whole from line 1
- dialog/note: in the key reference, a long explanation in the "Each row" section wraps in the right column instead of
  being cut; the sections of keys still cut (locku's LK18)
- checklist: panel-127 reworded; panel-135, file-picker-92, note-73 added (1394 items)

## v0.8.1 — 2026-10-19

What turned up while terminu-go and the apps followed v0.8.0, settled with the user.

- layout/panel: the location row stays when the list is empty; only the header and the list give way to the empty
  state (G98)
- dialog/note: in an unwrapped viewer the selection cursor can walk into the cut part — the view scrolls sideways just
  enough, with `…` where lines are cut on the left, and returns to the left edge on leaving the mode (G99)
- E3: on Windows the cache is `%LOCALAPPDATA%\<app>\cache`, apart from the executable's folder, so deleting the cache
  never deletes the program (CD52); a moved location is moved item by item — an item already at the new place keeps the
  new one when it is a cache, and leaves settings, state and data at the old place with an error popup giving both
  paths; the emptied old directory is removed (CD54)
- S2: entries already released and release notes already on GitHub do not mention the splash either; version headings
  stay
- checklist: E3-7, E3-14, S2-2 reworded; E3-16, panel-134, note-72 added (1391 items)

## v0.8.0 — 2026-10-19

From the whole-family refactor to tdp v0.7.4 and terminu-go v0.1.13: eight apps reported what tdp did not say, what it
said twice, and what they had lost; each was settled with the user one at a time. Behaviour changes, so a minor.

Screen and size
- L1: every app has a minimum size, 80×40 by default; it may be lowered, never raised. Smaller than that, only the app's
  name (Blue bold) and `needs a terminal of at least W×H` (Overlay0) are drawn in the centre; no key does anything and
  nothing goes into a PTY, except `Ctrl-C` twice, which quits; the state is kept. Narrow widths apply only above it.
  E5's tests go down to 1×1
- S5: with a single row the splash draws only the name; CHANGELOG and release notes do not mention the splash either
- A single-screen app shows long work's progress in the work's own row; zoom has a default (only the focused panel,
  filling the panel area, and the panel switched to stays zoomed) and the app decides how it zooms
- The empty state replaces the whole list, header included, and wraps when too long; a list's order is fixed (data
  with no order of its own is sorted first)
- K1: a screen that is not part of the TUI (locku's screensaver while locked) is not a surface

Keys and focus
- K3: the focus moves only when the user expects it (the details panel's `Enter` is one); nothing in the background
  takes it; after adding an item the cursor moves to the new item. K3-8 covers only a value that was valid when the popup opened: an empty required field blocks `Enter`
- K6, M6: a one-dimensional list lists `h|k`, `j|l`; no movement or scroll keys when the list is empty or the content
  fits. K12: two-dimensional content in a panel with tabs walks `j|k` in reading order, `h|l` switches tabs
- K11: a mode in a popup keeps the popup's `Tab` and digits and the footer; a mode on a PTY sends any other key, `q` and
  `Ctrl-C` too, to the child after leaving the mode
- M5: a hotkey letter found in the label is bracketed in place, case-insensitive, the first one (`[n]ew`, `Ex[P]ort`),
  otherwise apart (`[x] Reset`); `|` also joins a pair of opposite keys under one verb (`j|k:move`, `gg|G`)
- dialog/form: the typing note takes `Enter` and `Esc` only; every other printable key, `q` and `?` included, is eaten

Popups and components
- T1: the table goes by what happens after confirming (view, write back, editor: keep; item gone, shell, screen
  switch, drill-down: clear); a confirm is only a gate, and cancelling always returns to the menu. F2: several layers
  closing together all collapse at once, about 288ms
- dialog/toast: a fourth kind, Success (`nf-md-check_circle` `SUCCESS`, Green, 2200ms); the kind follows what the colours
  mean (Success done, Info neutral, Warning done but worth noticing, Error failed — a failure is never a Warning); a long
  message wraps, how many rows is the app's
- dialog/note: every viewer has a selection mode; it wraps by default and the app may keep aligned content unwrapped;
  line numbers are the app's choice; search hits are underlined, the current one is the cursor block; a key reference
  may start with "what each row is" on a one-value-per-row panel
- dialog/terminal: a selection mode like a viewer's; a history mode (`History`): `PgUp` enters, `j|k`, `u|d`, `gg|G`,
  `PgUp|PgDn` scroll, `Esc` returns to live; a PTY in a panel has no padding; the footer is not drawn under a terminal
  popup
- dialog/menu: a jobs list's rows follow the job; a row that can be acted on opens a confirm with the full text
- layout/panel: an optional location row; columns drop whole by the app's order before shrinking; sort groups; names in
  a panel title keep their case; middle truncation for values that matter at both ends; the label column fits the
  header too; the space after `[N]` takes a powerline width; no hint when no key works
- layout/popup: a hint that does not fit keeps the last `Esc`; the error row may count down a pause after too many wrong
  values; a form's focus block keeps the right padding
- input: a suggested value for a new item; number may be empty when optional and may carry a unit row (`10 seconds`
  on forms and panels); password's unlock style has no prompt row, the title says what to type; color picker hex is
  always uppercase and an empty old value reads `none`; a switch may be an off/on radio; finder's match subject is the
  app's (shown text by default), select and checkbox popup widths follow their options; reorder takes `h|l`
- Values on forms and panels draw control characters, Tab included, as red escapes; content draws a Tab as
  `input_tab_width` spaces. Wrapping: a word longer than a row starts a new row before it is cut; notes wrap

Environment and documents
- E3: settings, state, data and cache are told apart by what deleting them costs (a hand-written connection list is
  settings); the settings file is `config.yaml`; a moved location is migrated on first start
- E5: widths cross ssh as `LC_TERMINU_ICON_WIDTH` and `LC_TERMINU_POWERLINE_WIDTH`, sent by the app with ssh, read by
  the library; order `<APP>__` → `TERMINU__` → `LC_TERMINU_` → probe. E8: an app on the library tests its whole
  screen, the library tests each popup's own frame
- E7: the twelve README sections are required; other content goes in as a subsection or as an own section between
  sections 4 and 9; troubleshooting follows usage; other sections may carry a gif or screenshot, but few
- Family members and apps built with tdp: the latter use their own account, tap and e-mail, and their README says
  "built with terminu design"
- Citations: an app's files cite `tdp X`; tdp itself keeps `Rules X`
- project: goreleaser `app:` ignore, uninstall asks about `<APP>__STATE`, truecolor in caveats and NOTE, `tools/` for
  developer tools, `(terminu family)`

Checklist
- The verdicts, gene counting and the pass line move to the terminu harness; tdp keeps the items and the "applies to"
  table. New "applies to" entries: location row, zoom, mode (on a panel), mode (in a popup), jobs list, finder with a
  preview, file preview, has released
- Release items judge what the repo shows now, not the latest tag; what exists only after a release applies to an app
  that has released. The splash animation is checked by reading the code, not by recording
- Every rule above gets its items; the items the apps found wrong (scope, missing splits, how to check) are fixed.
  M5-2 (merged into M5-1) and note-5 (a viewer always has line numbers) are retired (1388 items)

## v0.7.4 — 2026-10-18

From the user, while working out how the harness's judge runs: a judge may not be able to check every item.

- checklist: a fifth verdict, "cannot tell", for an item that could not be checked (e.g. a file to read with no repo at
  hand, a screen that needs a special environment to open), written with its reason; like departures, violations and
  items not applicable, it counts for no gene

## v0.7.3 — 2026-10-18

From the user: the checklist counts genes instead of judging a share; and G94 narrowed back to where it was asked.

- checklist: each item is one terminu gene; an app has the genes of the items it meets — departures, violations and
  items not applicable count for none — written as a count tied to its tdp version (`tdp-0.7.2 860 gene`), not as a
  ratio. A version's total of genes is its number of items; counts from different versions are not compared directly.
  What an app does that tdp does not specify is no gene and costs nothing; it is reported as a gap
- components "Wrapping": the space at a break goes to the next row's first cell only in a textarea and a viewer, where
  every character is drawn; text that is only shown (a confirm, a toast, an error popup, the splash) does not draw it
  (G95). checklist: components-24 added (1302 items)

## v0.7.2 — 2026-10-18

Three gaps left over from v0.7.1: one from terminu-go, two found while building the checklist.

- components "Wrapping": when a word fills a row exactly and a space follows, the space starts the next row, so every
  character can be drawn and a textarea's text cursor on it has a cell (G94)
- A panel filter that matches nothing: while typing, the footer is `Tab:list Esc:clear`; when a panel's list has no
  items, filtered to nothing or empty to begin with, its hint drops `Enter` and the hotkeys on an item, as a finder and
  a form's buttons already do; M6 names these three places where the keys must go
- F7: a popup is at most the screen height − 2 — the screen chip row or the statusbar and the footer stay in view, and
  the divider under the chip row may be covered
- checklist: F7-6 reworded; components-23, screen-31 and panel-124 added (1301 items)

## v0.7.1 — 2026-10-18

From the user: the check layer of the terminu harness — tdp gets an item list for judging how much of tdp an app meets.
Breaking tdp into items turned up gaps, fixed here; most were places where a rule had not followed an earlier decision.

- checklist (new): the principle, the rules, the components and the project spec broken into 1298 items, each with an
  ID that never changes, its source, what to check, what it applies to and how to check, in Traditional Chinese and
  English, lined up by ID. Judged on tdp alone, not on the implementation; the verdicts are meets, departs, violates
  and not applicable. It is not a requirement itself: where it disagrees with the spec, the spec wins
- Rules: the Core key term lists `1`–`9` (G11); P5's `Shift-Tab` covers every popup with an action area (CD6); K4, F3:
  in a popup's mode `Esc` leaves the mode first; M1: in a PTY `?` and `Space` are not shown, the exit keys are; M3, K5,
  F1: a popup's operations are all in its `?`, the hint as each component says; K3: what moves the focus, and the three
  places `Enter` does; L3: the always-on rows are fixed; F1: a frame outside the seven kinds is a departure, the splash
  is not; S5: 250 ms between the first three stages, the text 400 ms after the mark (G66); E5: across ssh, the app's own
  channel carries both widths to the same app, other family apps take `TERMINU__` set by the user; E6: `docs/icon.svg`
  is the original, the copy in the code is held to it by the test (demou DM1); E7: a dev-remarks heading has no
  brackets, a fix file exists only while there is something to fix
- components: a "Wrapping" rule for all text that wraps — between words and between wide characters, a word longer than
  a row cut by cells, a wide character never cut in half (demou DM2); the error popup's frame and title are Red; bold
  only on the selected capsule and the popup title's loading icon; the thin line between two unselected parts paints no
  background; a multi-column ordinary list always has a header, with the panel filter's typing row above it; the footer
  is per screen; a grouped list's marks sit in the two indented cells; a panel's hint puts `Enter` first; diagrams
  fixed: capsule ends, cursor arrows, title glyphs, widths by the formula, the datetime picker's time columns
- dialog: a long submit shows the loading icon too; typing on a field that opens another input popup does nothing; the
  key reference also closes with `?`; a viewer's title is `KIND — name`, and its syntax colours, where the content has
  no fixed format, are up to the app
- input: a finder opens on its typing row, a file-picker on its list; with no results `Enter` does nothing and the hint
  drops it, while a checkbox popup's `Enter` still writes back the set (G93); the colour picker's `h|l` stays among R,
  G and B; the colour swatch is 3 cells; a file-picker's title is `FIELD · directory` and its icons' code points are
  written out; the datetime picker keeps `?` and `q`
- project: `go.mod` and `go.sum` are in the tree; top-level files not in the tree are the app's choice, like
  directories; the goreleaser template's scoop description is marked `app:` (G92)

## v0.7.0 — 2026-10-18

From the user: one shape for every family repo, so the apps are laid out, built and released the same way.

- project (new, a fourth layer beside the principle, the rules and the components): what a family app's repo looks
  like — Go code only in `cmd/<app>/` and `internal/`; the version in `internal/version` (`Version` without the v,
  `Display()` with it, `dev` for a local build); each CHANGELOG heading is the tag and the tdp version it follows
  (`## v0.1.2 — tdp v0.6.11`), with an `## Unreleased` section that a release renames, while releases made before
  v0.7.0 keep their headings; the release steps and the token
- Template files, copied as they are and changed only where project says: `family.mk` (the make targets every app
  shares; an app's Makefile sets `BINARY`, includes it, and puts its own targets in a last section), `release.yml`,
  `goreleaser.yaml`, `install.sh`, `uninstall.sh`, `version.go`, `gitignore`
- `check` runs `test-race`, as CI does, and `check-lib` when there is a `go.work`; `release-check` prints goreleaser's
  deprecation of `brews` but does not fail on it alone; `uninstall.sh` finds the settings, data and cache where Rules E3
  puts them
- Rules E6 points to project; the reference implementation is demou, the family's app for learning the operations

## v0.6.15 — 2026-10-16

From the user, on v0.6.13: a ticked option that cannot be reached cannot be taken off.

- input/checkbox: an option is now marked not available instead of disabled — drawn in its place, the whole row
  Surface2, the tick too, but it blocks nothing: the cursor stops on it, `Space` ticks or unticks it, and `Enter` writes
  back the ticks on screen. What not available means and what to do with a ticked one is the app's choice; tdp only
  draws the state
- The cursor skipping, "only disabled options left is as no results" and v0.6.14's "a disabled starting option moves
  the cursor on, then back" are gone; the popup opens on the option the app names, the first when none is named
- dialog/form: a checkbox option not available is not disabled, so the focus stops on it; color: Unavailable lists it

## v0.6.14 — 2026-10-16

A correction to v0.6.13, from terminu-go.

- input/checkbox: the popup opens with the cursor on the option the app names, the first when none is named — where it
  starts stays the app's choice; v0.6.13's "the first option that can be chosen" had taken that away. When the named
  option is disabled, the cursor goes on to the first one after it that can be chosen, or back when none after can

## v0.6.13 — 2026-10-16

From ccdrawu: a checkbox option that cannot be chosen.

- input/checkbox: a disabled option is drawn in its place, the whole row Surface2, its tick too (Unavailable wins over
  In effect); in a checkbox popup the cursor skips it, as in a form and Rules M6, so `Space` never reaches it; a ticked
  one stays ticked and is part of the set `Enter` writes back
- The popup opens with the cursor on the first option that can be chosen; filtering still lists disabled options, and
  when only they are left it is as with no results

## v0.6.12 — 2026-10-15

From ccdrawu: the header of a one-value-per-row panel.

- layout/panel: a one-value-per-row panel's header (`PROPERTY  VALUE`) is Overlay0, otherwise drawn as an ordinary
  list's header — the labels under it are Blue, and a Blue header ran into them
- color: Focus keeps a list's header row; Dim text adds the header row of a one-value-per-row panel

## v0.6.11 — 2026-10-15

From kamonu: what an input's error names when its title is an action.

- input: an error names the value by its name — opened from a form's field, that field's name; an input opened on its
  own has a title saying what the popup does (`RENAME`, `SAVE AS`), so the app gives the value's name besides
  (`Name can't have control characters`, not `Save as can't have control characters`)
- The pasted-control-character error, number's range error and textarea's error follow it

## v0.6.10 — 2026-10-15

From terminu-go and kamonu: a target opening while its source closes.

- T1: when the target clears the source, the source closes while the target opens — both animations at once, not
  waiting for the source
- color, layout/popup: a closing popup does not count as a layer, so the target has the layer colour it ends up with
  from its first frame and does not change colour when the source is gone; the half-closed source lies under it,
  dimmed as F8 says

## v0.6.9 — 2026-10-15

From kamonu, whose export form has a button `Overwrite KBU.svg`.

- dialog/form: a button's hint lowers only its verb, names and paths keep their case — `Overwrite KBU.svg` →
  `Enter:overwrite KBU.svg`
- components README, Uppercase: names and paths are content and keep their case in a hint as well as in a title

## v0.6.8 — 2026-10-15

From terminu-go, building the form's actions: what happens while one is still running.

- dialog/form: while a button's work runs (an action that keeps the form open, or a submit that takes a while),
  `Enter` on it does nothing and the hint drops its `Enter` until it is done
- An action still running when the form closes (`Esc`, or another submit) is cancelled — stopped if it can be — and
  its result is not shown

## v0.6.7 — 2026-10-15

From kamonu: a form with more than one button, and a cursor over a colour.

- dialog/form: the action row becomes the action area, and it may hold more than one button — the main submit always in
  the bottom-right corner, the others another way to submit (`Save As`) or an action that keeps the form open (`Test`),
  laid out in rows by the app. `Tab|Shift-Tab` switch between the field area (the fields and the error row) and the
  action area, landing on the main submit the first time; hjkl move only within the area, each wrapping at its own ends,
  the action area in reading order; `gg|G` go to the ends of the area
- An action that keeps the form open checks only the fields it needs, shown as a refused submit is; success is a
  toast, failure an error popup (`Enter` again retries), a result to read a note; errors stay until the next check
- The error row's hint is `Enter:show e:edit Tab:actions Esc:cancel`; K2 and F1 say action area, and hjkl within it
- color: a swatch — a cell whose content is a colour, such as the `███` of a colour value or kamonu's grid — keeps its
  own colour under a cursor block; the other text on it still turns Base

## v0.6.6 — 2026-10-15

From ccdrawu, which wants its drawer items put in order inside a popup: the panel's Drag mode, now in a dialog too.

- New input component `reorder`: a list without search whose value is the whole order. `D` picks up the cursor's
  item into the Drag mode, where `j|k` swap it with its neighbour, `Enter` drops it and `Esc` puts it back; holding
  nothing, `Enter` writes the order back and `Esc` cancels, first asking whether to discard a changed order. The hints
  are `Enter:apply D:drag Esc:cancel` and `Enter:drop Esc:cancel`; the popup is at least 35 cells wide
- The held item, on a panel as in the popup: drawn as the cursor in the mode colour (a Yellow background, Base bold)
  with `nf-md-swap_vertical` (U+F04E2) in the cell kept at the start of every row
- K12: the held item wraps at the ends too — the last one moved down goes to the top
- F1: reorder is the one list without search that is an input, not a menu; F3 and form's Cancel: a changed reorder
  asks before `Esc` discards it, as a form and a textarea do

## v0.6.5 — 2026-10-14

From ccdrawu's colour picker: its `Choose` button follows the form, but `Tab` had been left out.

- K2: every popup with an action row — a form, and an input popup with a button such as the colour picker — has
  `Tab|Shift-Tab` go back and forth between the field area and the action row, coming back to the item it left;
  input/README says so for every input popup with a button
- color-picker: `Tab|Shift-Tab` between the channels (R, G, B) and `Choose`; the hint is
  `Enter:edit Tab:actions Esc:cancel` on a channel and `Enter:choose Tab:fields Esc:cancel` on `Choose`, so the popup
  is 40 cells wide

## v0.6.4 — 2026-10-14

A gap found while ccdrawu gets a Windows build.

- E3 on Windows: `~` is `%USERPROFILE%` — config in `%USERPROFILE%\.config\<app>`, data under `%USERPROFILE%\.<app>\`,
  worked out as on macOS and Linux, not in `%APPDATA%`; the cache in the system's cache directory, `%LOCALAPPDATA%\<app>`

## v0.6.3 — 2026-10-14

From ccdrawu's sidebar with details beside it.

- K3: the one place `Enter` may change panels is details — on a panel listing items, `Enter` may move the focus to the
  panel showing that item's details. Whether to, and on which items, is up to the app; not using it is just as much
  within the spec. layout/panel "Details" says so too

## v0.6.2 — 2026-10-14

Gaps found while building ccdrawu's settings on the shared lib, a sidebar with details beside it.

- layout/panel, groups: a list split into groups starts each group with a title row — Blue, uppercase, not bold, no
  glyph, one cell from the frame — and its items two cells further in, with no blank row or separator between groups.
  The cursor skips group titles (`gg|G` go to the first and last item, `N of M` counts items, a group's title stays on
  screen with its first item), and a group with no items, filtered out or empty, has no title. components "Uppercase"
  lists group titles
- layout/panel, details: a panel showing the item under another panel's cursor switches at once as the cursor moves,
  label included when it names the item, with no `Enter`; the focus stays where it was (Rules K3)

## v0.6.1 — 2026-10-14

A gap found while building kamonu on the shared lib: a form's title that names the item it edits.

- layout/popup: when a title names what the popup acts on, the name follows after `: ` and keeps its case (`EDIT: filu`,
  as in the terminal's `ALTERM: myhost`); viewers and the file-picker keep their own form (`YAML — pod/nginx`,
  `IDENTITY FILE · ~/.ssh`). components "Uppercase" and dialog/form point to it

## v0.6.0 — 2026-10-14

Released together with the shared lib, terminu-go. A gap found while building kamonu, the family app that draws marks.

- S5: the spec no longer says how the tool that draws a mark splits its letters; it fixes only the svg — XML comments
  split the letters, the first is the U frame, and their order is the order of the reveal

## v0.5.9 — 2026-10-13

A gap the user found walking through the shared lib's showcase: a file's Tab pushed the rest of the row out of the frame.

- Viewers and the file-picker's preview draw a Tab as `input_tab_width` spaces (the textarea's setting), not aligned to
  tab stops; the `\r` of a CRLF line break is not drawn; any other control character is drawn by name in Red, as in a
  typing row. Copying takes the original characters

## v0.5.8 — 2026-10-13

A gap found while planning the tool that draws the family mark.

- S5: a mark's svg splits its letters with XML comments — a comment names a letter and the rects after it belong to it,
  the first comment is the U frame, and the order of the comments is the order of the reveal. The tool that draws a mark
  does not split letters; whoever develops the app adds the comments

## v0.5.7 — 2026-10-13

A gap found while following v0.5.6 in the shared lib.

- dialog/note: plain text in a viewer with no fixed format is a recommendation — an app that knows its content may colour
  it (the ERROR and WARN lines of a log, say); the lib adds no syntax colours there but keeps the app's

## v0.5.6 — 2026-10-13

The sixth round of gaps, from following v0.5.5 in the shared lib, and syntax colours in viewers, asked for by the user.

- S5: when only the splash text is drawn and a single word is wider than the terminal, it is cut into pieces by cells,
  each centred
- A viewer with tabs sizes its line numbers by the longest page seen so far: they widen on a longer page and never
  narrow again
- A viewer whose lines wrap scrolls one screen row at a time, as `less` does; `N-M of T` gives the lines of the top and
  bottom rows
- Viewers colour content with a known format (YAML, JSON, TOML, HTML, XML, Markdown…) as the file-picker's preview does —
  chroma's catppuccin-mocha, foreground only; content with no fixed format, such as an app log, stays plain Text
- The cursor on a pasted control character turns the whole character Red behind Base text

## v0.5.5 — 2026-10-13

The fifth round of gaps, from following v0.5.4 in the shared lib and the user's second walk through its showcase.

**Splash**

- The splash is centred on the screen
- When it does not fit, only the text is drawn, centred and wrapped at words; if it is still too tall, rows go from the
  bottom up, each group taking the blank row above it, and the name and version always stay
- The U frame grows from the centre of each row out, one mirrored pair a tick, both sides together
- No row of the text is wider than the mark (50 columns); the lib refuses a longer one when the splash is built

**Inputs**

- A grey suggestion, and the grey dots of an existing password, start under the cursor: the cursor sits on the first
  character (in the unlock look, on the first grey dot)
- In a textarea, `Home` and `End` go to the start and end of the whole text; the line's ends are `0|$` in "move"
- A textarea keeps pasted control characters in red as a single-line input does, and will not save while it has any; a
  lone `\r` there is a line break
- In the directory picker, the `.` row is not there while a filter or a wildcard is typed; wildcard results list only
  directories

**Forms and viewers**

- When the focus lands on a radio or checkbox field — the form opened at it, a submit held back, `e` from the error row —
  it stops on the first option with a value: the chosen radio, the first ticked box, else the first option
- Viewers (YAML, App Log, file contents) have line numbers, at least three digits wide: a viewer whose length is known
  when it opens never shifts, a streaming one widens only past 999 lines

## v0.5.4 — 2026-10-13

The fourth round of gaps: what the shared lib met while following v0.5.3, what the user found walking through its showcase,
and the splash, now specified in full.

**Splash**

- S5: the family mark is specified — a navy U frame (`#205090`), the same in every app, around the app's own letters in gold
  (`#f2b753`), 25 × 19 pixels, each pixel one `nf-fa-square` two columns wide, on a Surface0 sheet. tdp ships terminu's own
  mark, a gold T, as `principle/icon.svg`; the showcase draws it
- The splash takes the whole screen
- Under the mark: the app's command name (Blue, bold), its version (Blue), its one-line description (Text); `developed by`
  (Overlay0) and the author's e-mail (the mark's gold); `Press any key to close` (Overlay0)
- The reveal is specified, no longer up to the app: the sheet row by row from the top, the letters in order with their pixels
  scattered two a tick, then the U frame rising from the base; a 10 ms tick, 250 ms between stages; the name, version and
  description 400 ms after the mark, the rest 500 ms later

**Keys**

- confirm answers only with `Enter` and `Esc`; no `y` or `n`
- `Home` and `End` act only on a typing row
- After a lone `g`, a key that forms no combination runs as if `g` had not been pressed
- The form's `Tab|Shift-Tab` moves between the field area and the action row, coming back to the item it left; inside the
  fields, `j|k` go item by item. The hint reads `Tab:actions` on a field and `Tab:fields` on the button
- A checkbox option drawn on a form ticks with `Space` too (`Enter|Space:toggle`), as in the checkbox popup

**Inputs**

- Every single-line input popup starts its typing row with `nf-fa-angle_right` and a space, as the filters do; the
  unlock-style password does not
- The unlock-style password has a cursor where the next dot will go; on the last digit it sits on that dot
- Pasted control characters are all kept and drawn in red — `\r`, `\n`, `\t` by name, the rest as `\xNN` — and a value that
  will be used is held back on `Enter` while it has any
- A textarea's line numbers are at least two digits wide, so the text no longer jumps at line 10
- The file-picker can pick a directory: only directories are listed, and a `.` row (`nf-md-folder_move`) at the top chooses
  the directory you are in
- The file-picker's metadata for a symlink describes its target; a value that cannot be read is `—`

**Layout and colour**

- A popup that scrolls is wide enough for its whole hint and its scroll position, so `Esc:close` is never dropped
- A panel's loading icon takes the frame colour
- A key reference's section about another surface comes last
- Dimming and the layer colours round each channel half up; the third layer is `#84C5F1`, and the dimming examples are
  corrected

## v0.5.3 — 2026-10-13

A gap found while following v0.5.2 in the shared lib.

- input/file-picker: the hex preview is always 8 bytes a row, followed by ASCII (33 cells), not 16 (65 cells) — a
  side-by-side preview is at most 56 cells wide, so 16 bytes never fit beside the list

## v0.5.2 — 2026-10-12

The third round of gaps found while building the shared lib, from its Inputs, Dialogs and Terminal screens.

**Keys and hints**

- M5: keys that do the same thing are joined with `|`, not `/` (`j|k`, `Enter|Tab:list`, `Tab|1–N:panels`, `[h]|[l]`),
  and the `|` takes the description colour, not the key colour; `/` is itself a key, so `Tab//:filter` could not be read.
  Every hint, footer, key reference and sentence in the spec follows
- A finder's list hint shows both ways back to the typing row: `Tab|/:filter`
- A menu whose `Enter` opens the row in full (a jobs list) shows `Enter:detail`
- No panel hint while the focus is in a PTY inside the panel; its exit keys are in the footer

**Finders and the file-picker**

- Every typing row (finder, select, checkbox popup, file-picker, panel filter) starts with `nf-fa-angle_right` (U+F105):
  Overlay0 with the focus on the list, the layer colour (a panel filter: the frame colour) when typing; the count on its
  right is Overlay0
- A finder with a preview always takes the maximum height. 96 columns or more: side by side; under 96 with metadata:
  the list and an `INFO` box on top, the preview full width below (5 entries and 7 preview rows at 80×24)
- The file-picker previews in four parts — typing row, list, preview, metadata (`TYPE`, `SIZE`, `MODIFIED`, `MODE`,
  written for people) — and a finder previewing files does the same. Previews by kind as filu draws them: a three-level
  tree for directories and archives, syntax colours and line numbers for text, PDF text, image data URIs, hex for the rest
- `hide_secrets_in_preview` (off by default): when on, a private key shows only its first line and an owner-only file
  nothing, each with `(sensitive content not shown)`
- The file-picker lists `..`, directories, then files, by name; hidden files only when the filter starts with `.`
- In a checkbox popup, Green follows the tick on screen

**Other popups**

- Form options always run down, one a row; the form's scroll position counts fields only and is not shown while the
  focus is on the error row or the button
- The colour picker: R, G, B and a `Choose` button take the focus (new no longer does); the focused channel's name and
  hex are both drawn as the cursor, as wide as the swatch
- The textarea opens at the maximum size and scrolls; `Tab` inserts `input_tab_width` spaces (default 4) instead of
  leaving it to the app; the Move cursor is in the layer colour; the scroll position counts lines
- A viewer's selection mode: no cursor until `v`; the first `v` shows the cursor, the second starts selecting by
  characters; `y` copies and leaves, `Esc` leaves; the scroll position shows the cursor's line inside the mode. Only
  viewers have it
- A PTY draws the subprocess's cursor as a reversed Text block and ignores DECSCUSR

**Rules**

- E3: shared config keys `hide_secrets_in_preview` and `input_tab_width`, named the same in every app; E7: the README's
  settings section names them
- F7: popups whose height cannot be known when they open (a finder with a preview, a textarea) take the maximum
- K8, K12 follow the textarea's `Tab` and the viewer's selection mode

## v0.5.1 — 2026-10-12

The second round of gaps found while building the shared lib from the spec.

**Widths**

- E5: two kinds of glyph are measured separately — icons (the Private Use Area) and powerline symbols (U+E0A0–U+E0D7:
  capsule ends and joins, a popup title's round ends, the cursor's arrow). Each is taken from the app's variable, then
  the family's, then the probe; the new `<APP>__POWERLINE_WIDTH` and `TERMINU__POWERLINE_WIDTH` pair with the icon ones
  (E2), an app with a PTY sets both `TERMINU__` variables for its subprocess, and READMEs name all four (E7). The L4
  tests run with "icons two cells, powerline symbols one" and with "both two"
- E5's implementation reference: remove the "erase to end of line" that bubbletea v1's renderer appends to a line it
  measures as short — where icons take two cells it erases the right border
- The right padding beside a cursor across a whole row is as wide as its arrow (the powerline symbol width), so the arrow
  never covers text or pushes the frame out; menu descriptions sit against that padding
- layout/popup: the PIN example is 43 cells, not 27 — the frame was always at least as wide as the hint (its width + 6)

**Capsule chains**

- The ends and joins are coloured as in Powerline: the foreground is the fill on the left, the background the fill on
  the right, an unselected part counting as Base — colour appears only on the selected parts
- A panel's tabs: `[N]` is a part of its own and always lit, and only the current tab is lit; the first tab's name is the
  label, joined to `[N]` by a space while it is current, so it looks like a panel without tabs
- Tabs after a popup title keep one line segment away from the title
- The chip row in dialog/terminal is drawn as a chain

**Finder**

- The preview box is in the layer colour, never dimmed, with nothing on its bottom border: P6's "only the focused area is
  lit" means the areas the focus can rest on

## v0.5.0 — 2026-10-12

A new look for the family: sharper frames, slanted capsules and a fixed popup animation. The colours are unchanged
(catppuccin-mocha); only the shapes and the type change.

**Frames and capsules**

- A focused panel has a heavy frame `┏━┓` (Blue), an unfocused one a light square frame `┌─┐` (Surface2) — the same
  width, so switching still shifts nothing (L5); the rounded and double frames are gone
- Popups have heavy frames in the layer colour; mode-name junctions are `┫ ┣` on heavy frames and `┤ ├` on light ones
- Panel capsules, screen chips and tabs have slanted ends: U+E0BA (`nf-ple-lower_right_triangle`) and U+E0B0
  (`nf-pl-left_hard_divider`); the joins inside a chain are unchanged
- A popup's title is a capsule of its own, rounded at both ends (U+E0B6, U+E0B4), filled with the layer colour, Base bold,
  one line segment from the corner — the ends tell a floating popup from a panel
- The divider under the screen chip row is a heavy line `━`

**Lists and menus**

- A cursor across a whole row ends in an arrow: its rightmost cell (the right padding) holds U+E0B0 in the cursor's
  colour; the text does not move. A form's focus block that runs to the frame ends the same way; a button and one-cell
  cursors (calendar days, hours, minutes) do not
- Menu and key-reference section titles start with `nf-md-hexagon` (U+F02D8) and are in uppercase; the separator
  between menu sections is the double dash `╌` (U+254C)
- Hints and the footer are unchanged (`Enter:connect`)

**Uppercase** (new section in the components README)

- Panel capsules and tabs, screen chips, popup titles, table headers, the labels of a one-value panel and section titles
  are in uppercase; values, menu labels, hint words, key names, mode names and app content are not
- The letter in a hotkey marker keeps its case (`[m]ANAGE`), and names and paths in a title keep theirs
  (`ALTERM: myhost`)

**Animation**

- F2 and layout/popup: one form for the family — a heavy line in the layer colour grows from the popup's centre to its
  width (4 frames), holds for 1 frame, then the popup opens up and down from its middle (4 frames); closing runs the
  same frames backwards. 32ms a frame, about 288ms each way (was 8 × 16ms ≈ 128ms with the form left to the app)
- A popup takes no keys until its opening animation ends; what lies beneath is dimmed from the first frame

**Diagrams**

- Every diagram is redrawn in the new look; Nerd Font glyphs in diagrams are written with their real code points
  (components README, "Diagrams and spacing")

## v0.4.0 — 2026-10-12

Gaps found while building the shared lib (terminu-go) and its showcase strictly from the spec, settled one by one.

**How the spec reads**

- Diagrams are requirements: their structure (frames, glyph positions, spacing, alignment, the noted colours) is as
  drawn, the names and values in them are examples; the text wins over a diagram, and two diagrams that disagree are a
  bug in the spec. Numbers that are hard to count are written in the text; "indented N cells" means N cells from the
  frame (components README, "Diagrams and spacing")
- Two general spacing rules: two cells between columns, one cell between a glyph and its text
- The English "what is a requirement" now covers every form of example ("e.g.", "for example", "Example:", "such as")

**Rules**

- K1: the digits `1`–`9` are a core key on panels — jump to that panel of the current screen; each screen numbers its
  own panels from `[1]`; an app may not register a digit hotkey on a panel; digits are free inside popups, and a digit
  global hotkey works only inside the global operation popup (M4)
- K2: the form row reads "the error row (while it holds an error) and the action row"
- K6: a panel's key reference lists its movement keys and the core keys that work there; a popup's lists its hotkeys,
  `Enter`, `Esc` and movement
- K11: inside a mode only the mode's keys and the listed core keys work — panel and global hotkeys do nothing, silently;
  the digits may be suspended like `Tab`, and must respond if so. English: `Esc` goes "back to the state before it was
  entered"
- K12: stepping (`j`/`k`, `h`/`l`, arrows, `Tab`) wraps at the ends of every run of items — lists, forms, menus, tabs,
  picker columns; `u`/`d` stop at the ends; the calendar, the month and year, the two sides and text movement do not
  wrap. English: "Where you are not typing", "`h`/`l` switch tabs"
- F7: the toast's bottom border is always on the third row from the bottom; a terminal keeps the chip row's divider and
  has no padding on any side
- E8 (new): the shared lib and its example app — a table of which rules the lib covers and which stay with an app that
  uses it; the lib never departs from tdp, it reports a gap instead

**Components**

- color: the screen background is not painted — Base is only written where a background must be (text on blocks,
  capsule seams, the dimming target); the 16 colours are dimmed by the terminal's own palette, asked with OSC 4 at
  startup, falling back to xterm's
- layout/screen: with a popup open the footer stays the screen's own, dimmed with it (a sixth case); panels are
  numbered per screen; the chip row and its divider stay over a terminal popup
- layout/panel: text on a frame keeps one line segment from the corner (`3 of 40 ═╝`), only the capsule touches it
  (`╔([1] Kinds)═══╡Drag╞═╗`); the loading icon follows the whole capsule chain; no hint while typing in a panel filter;
  columns are numbers or text, which sets alignment and sorting; a one-value panel's label column is as wide as the
  longest label plus two cells; a panel filter's typing row lines up with the list
- layout/popup: text on a frame keeps one segment from the corner (`4 of 12 ─╯`); a list cursor runs from frame to frame
  and a form's focus block runs to the frame; the terminal has no padding on any side; the loading icon follows the
  whole row of tabs. English: whole *pairs* are dropped from a hint
- menu: at least two cells between label and description; section titles sit one cell from the frame; wrapping per K12,
  `u`/`d` stop
- form: two cells after the label column; the focus block runs to the frame; `u`/`d` move half a page; a table of the
  form's own keys (`e`, `u`/`d`, `g`, `?` bring up no note); the full error message from the error row is an error popup
- note: every error popup closes with `Enter` or `Esc`, however it was opened; the key reference has a `move` section
  (item → panel → move → core keys → app-wide), lists the core keys that really work, and keeps menu labels' case
- toast: always on the third row from the bottom, so a terminal's prompt row and exit key stay visible. English: "that",
  not ", which"
- terminal: the PTY touches the frame on every side; the chip row's divider stays (it is the progress bar)
- confirm (English): hotkeys of its own "must be listed in `?`"
- input/README: the grey suggestion is for single-line inputs; leading and trailing *whitespace* (every Unicode
  whitespace character) is trimmed
- textarea: opens with the old value, the cursor at its end, in Write
- finder: typing filters by *contains* — case-insensitive, each space-separated word must appear, the list keeps its
  order; the cursor runs from frame to frame and the typing row lines up with the list
- file-picker: matching as the finder; a typed path stays on the typing row, split at its last `/` into directory and
  filter; `..` is not supported in a path; wildcard results show paths relative to their starting point, without `..`;
  `/` has no `..`
- datetime-picker: the calendar is not indented; two cells between month and year and between hours and minutes; the
  unfocused time column is dimmed; hours and minutes wrap on their own
- color-picker: blocks 8×2 and 3×1, two cells between the five items; the four items wrap

## v0.3.0 — 2026-10-08

A from-scratch review of the whole spec, before the apps implement the components.

**How the spec reads**

- Everything in the Rules and the Components is a requirement, except four things: parts marked as left to the app,
  examples, the **Why** paragraphs, and blocks marked "implementation reference (not a requirement)". A fixed rule may
  mark a part "(concept)", and a concept rule a part "(fixed)"
- Dates, "decided by the user", first-person notes, the story of how a decision was reached, and each app's current
  state are gone from the spec; the reasons stay. App status moved to the per-app fix lists
- The Components count as the fixed zone: an app that departs from one writes why in its dev-remarks and reports it as
  a gap in tdp
- What used to be Family defaults is now required, not only colour: the footer, the screen chips, the narrow width, the
  128 ms animation, the toast's duration, the menu's look. Where the old numbers went:

  | Old number | Now |
  |---|---|
  | D1 footer, screen chips, narrow threshold, empty states | components/layout/screen |
  | D1 panel capsules, D3 mode name label | components/layout/panel |
  | D2 colour system | components/color |
  | D3 popup frame, animation, loading icon, cancelling and completing, implementation notes | components/layout/popup |
  | D3 confirm hint, toast, finder focus | components dialog/confirm, dialog/toast, input/finder |
  | D4 Menus | components/dialog/menu |
  | D5 navigation letters, text motions (`w/b/e`, `0/$`) | Rules K12 |
  | D5 `Alt-Esc` always confirms first | Rules K10 |
  | D5 the rest (hotkey table, case carrying scope, `x` deletes) | dropped: tdp does not assign hotkeys on panels (P5) |
  | D6 distribution and environment | Rules E2–E6 |
  | D7 documentation | Rules E7 |

**Principle**

- P4 covers the interface elements tdp defines; the colours and symbols of the content itself are the app's
- P5: what tdp leaves to apps is now hotkeys on panels and domain symbols and colours; keys and glyphs inside a
  component are part of the component
- P6 (new): the bright place is where the focus is — everything else is faded
- Terms: core keys include `q`; the input state is "typed text is the content"; popups listed by the seven F1 classes;
  a source/target example that K5 allows

**Rules**

- K1: `Enter` means "the obvious thing; on a value, confirm it"; a form is an exception for `q`
- K2: on a typing row `Tab` goes to its list; an input popup with one area takes a suggestion with `Tab`, otherwise
  `Tab` does nothing; a form's error row and action row are stops
- K3 rewritten: `Enter` acts on the focused part and **never moves the focus**; a value that did not change is not
  written back; a typing row's `Enter` moves to the list; a form submits only with its button
- K4: search is not a mode; `Esc` clears a panel filter
- K5: in a checkbox popup's list, `Space` toggles (the one exception)
- K8: the input state is a typing row with focus; lists, pickers, a textarea's move state and forms are not
- K9: `q` does nothing on a form
- K11: a mode names itself on its frame; the look moved to components
- K12: `g` only starts two-key combinations (`gg`, and hotkeys such as `[go]to`); in text, `w/b/e` and `0/$` move too
- M1: `Space` need not be shown in a mode; M2: the `Global operation` row has no hotkey; M3: a popup with only a typing
  row lists every action in its hint; M4: global hotkeys work directly on a panel (the panel's own key wins a clash);
  M5: the example has the single unheaded `Global operation` row, and the marker table covers mid-word, prefix and core
  keys; M6: disabled rows use the disabled colour and the cursor skips them; M7 rewritten; M9 is now fixed
- F1: a menu is a list without search, a list with search is a finder; an input enters or chooses one value; a toast is
  not a layer; a terminal also lets the app keep reserved keys
- F3 lists its exceptions (PTY, a textarea while writing, a changed form or textarea)
- F7: two widths — content known when it opens means content + 4, otherwise `min(width − 2, 120)`; at most the screen
  height − 2; the toast sits bottom-centre; the error row is for values only, a failed action opens an error popup; a
  terminal keeps the statusbar and covers the footer
- F8: the drawn screen is faded once; T1: a value popup that writes back to its form or picker keeps the source
- E: E3 gives the state and cache locations; E5 separates the requirements from the implementation reference

**Components**

- `input/README` (new) holds the rules every input shares; `input/search` is now `input/finder`, and select, the
  checkbox popup and file-picker are kinds of finder
- color: the layer colour is a gradient from Lavender to Sapphire; one meaning per colour (Blue focus, Surface2 not
  available, Green in effect, Yellow mode, Peach warning); Subtext1 for the panel cursor, Surface1 for the button
- layout/screen: the footer for a single panel, a mode, a panel filter and a PTY; the screen chips; the statusbar
- layout/panel: one capsule chain for panel titles, panel tabs and screen chips; list panels (cursor, header with sort
  arrows, `N of M`, marks, truncation, loading and errors); every panel has a hint on its bottom border
- layout/popup: a title glyph per class; the order of hint items; dividers do not touch the frame
- form: no `Ctrl-S` — submit with the button (`G` jumps to it); typing on a field opens a short note; at most five
  options drawn on the form
- menu: label Text, description Overlay0 on the right; hint `Enter:run Esc:close`
- confirm: shield glyph, the question last, warnings in Peach; note: closed with `Esc` (the error popup and the typing
  note also with `Enter`), the key reference's look; toast: Info, Warning and Error with their own glyphs, bottom-centre,
  centred text up to three lines; terminal: `Alt-Esc:exit` or `Alt-Esc:leave`
- checkbox: a filled tick; the popup toggles with `Space` and applies with `Enter`; datetime-picker: hours and minutes
  in two columns, a six-row calendar; select opens on its list; file-picker shows the directory in its title

## v0.2.0 — 2026-10-08

- **Components** (new, `components/`): the component specs under tdp, and they are required — an app picks only among
  the listed options, and a missing option is a gap in tdp. Three nouns: a *popup* is the floating frame
  (`layout/popup`), an *input* is a popup for one kind of value (`input/`), a *dialog* is any other popup
  (`dialog/`: form, menu, confirm, note, toast, terminal). Also `color`, `layout/screen` and `layout/panel`, and
  twelve inputs: text, password, number, textarea, search, select, radio, checkbox, slider, datetime-picker,
  color-picker, file-picker
- **Family defaults dissolved**: what the family must follow moved into the Rules or the Components, the rest went; the
  principle README maps D1–D7 to where they are now. Colour (former D2) is now set by tdp
- K2: a form switches fields with `Tab` and always has `Shift-Tab`; an input popup has one field, so `Tab` accepts a
  suggestion; a popup with two areas switches areas
- K3: in an input popup `Enter` submits the one value; in a form `Enter` acts on the focused item and the button or
  `Ctrl-S` submits
- K8: a form is not in the input state; `Tab` in the input state accepts a suggestion or switches areas
- K10: `Alt-Esc` always confirms first (from D5)
- K12 (new): `j k u d g G h l` are kept for movement; hjkl are the arrow keys — directions where there is a left-right
  structure, back and on in a one-dimensional list; `u`/`d` half a page, `gg`/`G` top and bottom
- F1: **form** is a seventh class (a form shows values and opens an input popup per field, so it is no longer an input);
  a typing row with a candidate list moves the focus to the list on `Enter`, and a second `Enter` submits
- F2: the animation length is the same across the family (components/layout/popup)
- F3: the exception — a changed form or textarea asks before discarding on `Esc`
- M5: the hint example lists no movement keys (hints never do)
- T2: unfocused panels are dimmed as in F8, streaming content excepted — now required
- E (new chapter, App and environment): E1 every app has `<app> version` and `<app> help`; E2–E6 from D6
  (environment variables, paths, Nerd Font and truecolor, icon width, releases); E7 from D7 (documents)

## v0.1.23 — 2026-09-29

- D7: a README names both `<APP>__ICON_WIDTH` and the family-wide `TERMINU__ICON_WIDTH` where it
  talks about the icon width, and names no font as always two cells wide

## v0.1.22 — 2026-09-29

- D6: an app with a PTY sets `TERMINU__ICON_WIDTH` for its child, and every app reads
  `<APP>__ICON_WIDTH`, then `TERMINU__ICON_WIDTH`, then probes — so the icon width is right in any
  family app running inside another's PTY
- D6: an overlay larger than the screen in both directions is clipped too; the edge-case tests
  point at filu's `TestD6CompositeDispOversized`

## v0.1.21 — 2026-09-29

- D5: a text-selection mode moves as vim does (`h/j/k/l`, `w/b/e`, `0/$`, `gg/G`, `u/d`)
- D6: environment variables are named `<APP>__<NAME>` with shared names for the config, state,
  data and cache directories and the icon width; variables meant for another program are the
  exception; renamed variables keep no old names
- D6: an overlaid popup larger than the screen starts at 0 and is clipped, never panics

## v0.1.20 — 2026-09-29

- K11, D3: the mode name sits between two border junctions (`╡Drag╞` on a double frame,
  `┤Visual├` on a single one), bold in the mode colour, one word if possible; the title is
  clipped first; a panel's capsule turns the mode colour with its frame
- D6: the icon width is how far the cursor actually moves (no font named as the example); the
  full reference from filu (`compositeDisp`, `centerDisp`, `joinH`/`joinV`), the
  `<APP>_ICON_WIDTH` override, unix-only detection, and what done looks like

## v0.1.19 — 2026-09-29

- L5: focus is not told by colour alone, since a mode recolours its frame (K11); the family
  default stays the double line for focus
- K10: while the subprocess is not ready, ordinary keys may be held back but `Ctrl-C` is still
  forwarded; in a PTY every key is the PTY's except the disclosed exit key and kept chords

## v0.1.18 — 2026-09-29

What the v0.1.17 migration of the five apps raised.

- F1, D3: which side of a finder has focus must show; the family look greys the filter row
  (Overlay0, not F8's fade) and gives the list's cursor row the layer colour
- K11, D2: a mode shows its name at the right of its frame's top border and turns the frame
  Yellow
- D2: hints on an unfocused panel's border use Overlay0 / Surface2, keeping Blue for focus
- D3: a bottom-border hint that doesn't fit drops whole items from the end
- D6: detect the icons' real cell width (CJK icon fonts draw them two wide) and measure every
  width with one display-width function; filu's `width.go` is the reference
- K10, K9: an app may hold keys back while the subprocess is not ready (still connecting);
  `q` and `Ctrl-C` belong to the subprocess in a PTY

## v0.1.17 — 2026-09-29

- M5: keys mentioned in the description column of a menu or the key reference count as a
  sentence (square brackets); the README marks keys in prose as Markdown code; another tool's own
  keys (tmux's `prefix l`) keep that tool's notation

## v0.1.16 — 2026-09-29

- D5: `Alt-Esc` always confirms when it would move focus out of the PTY or end the subprocess,
  since a busy app reads two `Esc` presses as `Alt-Esc` (measured with bubbletea v1.3.10); other
  Alt-chord exit keys confirm as the app decides
- M6: a separately titled key reference section describing another surface is shown at full
  brightness

## v0.1.15 — 2026-09-29

How keys are written, settled while preparing the v0.1.14 fix lists.

- M5: key names are the key-cap names in UpperCamelCase with no abbreviations of our own
  (`Esc`, `Backspace`, `PgUp`); letters in the case pressed, the letter after `Ctrl` upper case;
  alternatives joined with `/`, ranges with `–`. By place: labels keep the bracket marking,
  sentences put every key in square brackets (`[A]`, `[Space]`, `[!]`), hints and the footer
  write `key:description` separated by one space (`j/k:move Enter:run Esc:close`), and the key
  reference is two columns with bare keys
- D1, D2, D3, D4, D5: the footer, confirm and menu hint examples follow M5; keys in hints, the
  footer and the key reference are Blue, the colon and description in hints Overlay0, the key
  reference's descriptions Text; `Ctrl-U` `Ctrl-D`

## v0.1.14 — 2026-09-29

What kbu's migration raised.

- F1, F8, K11: a toast takes no key but `Esc`; in a mode, the first `Esc` closes the toast that
  answered `Tab` (wording only, behaviour unchanged)
- K10, D5: the family's PTY exit key is `Alt-Esc`; an exit key that ends the subprocess confirms
  first, since a fast double `Esc` in vim can arrive as `Alt-Esc`
- Terms: switching the layout (zoom) is not a mode, so `Esc` need not leave it
- M5: how keys are written covers the key reference and the README; brackets belong in labels,
  while hints, the footer and the key reference write "key + word"; modifiers are joined with `-`
  (`Alt-t`, `Ctrl-C`, `Shift-Tab`)
- M6: the key reference follows the same rule as menu rows (a key that can't run now is listed,
  dimmed); hints may list only what works now

## v0.1.13 — 2026-09-28

- F1: a menu's `Enter` may open the row in full (a list with a cursor and nothing else to do, e.g.
  sshu's jobs); a confirm may carry content to read before answering, scrolled with `j/k`, and is
  still just a confirm (sshu's host details above "Connect to X?", no longer a departure)

## v0.1.12 — 2026-09-28

What the v0.1.11 audits of filu, locku, webu and sshu raised.

- F7: a loading popup **always** shows the spinning icon after its title, whether or not its height
  changes; loading means the whole popup's content, while one streaming item is that item's loading,
  disclosed as the app decides. A height change caused by the user's own action is allowed, not
  required — what is disclosed must be correct
- D2: dimming never lightens a colour (each channel keeps the smaller of original and dimmed); output
  is always 24-bit
- D3: the loading icon spec (webu's circle slices, 90 ms, clock-driven, one cell, layer colour)
- D6: the family requires a truecolor terminal

## v0.1.11 — 2026-09-28

What filu, locku, webu and sshu taught while aligning to v0.1.8–v0.1.10.

- K3: when the panel is a content area with no item, `Enter` does the most obvious action to the
  whole panel, as the app decides
- F6: a choice made explicitly in a picker may count as the confirmation, as the app decides
- F7: the height fixed at opening may change in two cases only — while **loading** (disclosed by a
  spinning icon after the popup title) and when **the user's own action** changes the row count
- F8: dimming fades every colour, foreground and background, toward the base; never strip colours,
  drop backgrounds or collapse foregrounds to one dim colour (that broke powerline capsules)
- D2: the dim calculation, `c × 0.45 + base × 0.55`, with filu's `dim.go` as the reference

## v0.1.10 — 2026-09-28

- K11: inside a mode `Space` opens nothing — the mode's key list (runnable rows) is gone. `?` is
  the mode's key reference; the mode's keys are pressed directly and disclosed in `?` and the
  footer / hint. Also removes the v0.1.2 note about moving that list with the arrow keys

## v0.1.9 — 2026-09-28

- F1: a finder's `Tab` moves focus between typing and its list, `Esc` closes the whole finder; an
  input may carry a candidate list (arrows move, `j`/`k` stay characters, `Enter` submits the
  chosen one) and is still an input; each step of a multi-step flow is its own popup
- F7: only an input whose submit can fail reserves the error row; the terminal class takes the
  whole available area, no 120 cap
- F8: borders below the top are dimmed too, each in a dimmed version of its own layer colour

## v0.1.8 — 2026-09-28

- F1: popups come in **six classes** — menu, confirm, input, note, toast, terminal — each with fixed
  key meanings; a note may have its own hotkeys and modes; a popup may change class by phase (a
  finder: input, then menu) but is one class at a time
- F7 (new): every popup is `min(terminal width − 2, 120)` wide, centred; its height follows the
  content but is fixed when it opens, scrolling beyond the screen; the toast sits at the bottom;
  an input reserves one error row, where K3's failed submit writes its error
- F8 (new): with a popup open, everything below the topmost — popups and base screen, streaming
  content and warning colours included — is dimmed; a toast does not dim; border layer colours stay
- T2: a popup on top is the exception (F8). D4: the old "key reference as wide as its longest
  description" gives way to F7

## v0.1.7 — 2026-09-28

- M2: the Space menu's global row carries **no region header** — `global operation` over a single
  `Global operation` row only repeated itself; a divider still separates it. The item and panel
  regions keep their headers on a panel's Space menu

## v0.1.6 — 2026-09-27

- K2: in a single input box with a greyed-out suggestion, `Tab` **accepts** it (was: the app *may*);
  in an input group `Tab` only switches fields and the app picks another key for suggestions (e.g. `→`)

## v0.1.5 — 2026-09-27

- K8, K2: in the writing state of multi-line text `Tab` is a character (an indent), like `Enter`
  is a newline there (K3); leave the writing state to switch fields. `\t` or spaces is the app's call
  (webu's editor popup)

## v0.1.4 — 2026-09-27

- K10: a PTY needs **at least** one exit key; whether the app keeps other chords of its own in
  the PTY is up to the app, disclosed like the exit key (sshu's grid)

## v0.1.3 — 2026-09-27

- K3: `Enter` always submits — the whole input group or a single field, as the app decides.
  A failed group submit moves focus to the first invalid field and discloses the error; that is
  not `Tab`, which alone moves field by field
- K10: where focus lands after the PTY exit key is up to the app

## v0.1.2 — 2026-09-27

What sshu taught while being brought to tdp.

- **`?` only reads** (K6, M4): it opens the key reference of the frontmost surface — read-only,
  scrollable, nothing to run. The runnable global actions move to a **global operation popup**,
  opened from the Space menu's global region, which is now **always a single row** (M2), even with
  one global action; quitting lives there (K9)
- **PTY** (K10): in a PTY every key, core keys and all app hotkeys, belongs to the subprocess;
  only the exit key is the app's; app actions on a PTY are done after leaving it
- K2: the SSH-grid example is gone; `Tab` in a PTY belongs to the subprocess
- K4, F4: with popups stacked, `Esc` closes only the topmost and the stack below stays as it was
- K11: a mode whose keys overlap navigation moves its key list with the arrow keys only
- D3: the quit confirm is its own popup; "on top" is routing, `closeTop` and drawing alike.
  D4: key reference width follows its longest description

## v0.1.1 — 2026-09-27

What locku and webu taught while being brought to v0.1.0.

- **Modes** (new term, Rules K11): inside a mode `Space` lists the mode's keys, `?` is the mode's help,
  `Esc` leaves, `q` / `Ctrl-C` quit as K9, `Tab` may be suspended but must answer
- M2: a panel's Space menu always carries region headers (the global region is always there)
- D3: the `?` help is on top in routing and drawing; judge a layer by `owns()`, not `isActive()`
- D4: `key reference` rows are not selectable; a label that shows its key is not bracketed again

## v0.1.0 — 2026-09-26

First release of terminu design and the terminu design principle, grown out of VTP
(see [vtp/](vtp/), which also maps every VTP clause to its tdp ID).

- Principle P0–P5; Rules K1–K10, M1–M9, L1–L5, F1–F6, X1–X2, T1–T2, each marked
  `fixed` or `concept`; Family defaults D1–D7
- Three scopes of operation, with `global operation` in both the Space menu and the `?` menu
- `q` joins the core keys; `Ctrl-C` runs the same quit flow
- Minimum supported size 80×40
- The splash is the family easter egg and the one undisclosed thing (Rules S1–S5)
- Colour moves out of the rules into a colour system in the defaults (D2)
- Letter hotkeys and symbol vocabulary are left to each app (P5); D5 records the family's habits

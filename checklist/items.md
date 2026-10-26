# terminu checklist: items

**Language**: English · [繁體中文](items-zh_TW.md)

The items of tdp v0.10.1. What each column means and what an item applies to: [README.md](README.md).

## principle — P0–P6

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| P3-1 | P3 | An action on a batch of marked items is in panel operation | marks | Mark a few rows and press `Space`: the action is in the panel operation region |
| P3-2 | P3 | An action that concerns only another panel appears only in the Space menu of the panel it belongs to: it is not pushed into the focused panel, nor promoted to global | several panels | Look at each panel's Space menu and the global operation popup: none has an action that acts only on another panel |
| P3-3 | P3 | Switching screens is a global operation, listed in the global operation popup | several screens | `Space` → `Global operation`: it has a row switching to each screen |

## principle — Terms

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| terms-1 | terms.1 | Focus never rests on the always-on areas (footer, statusbar, screen chip row) | everyone | Press `Tab` and the digit keys again and again: focus moves only between panels |
| terms-2 | terms.8 | A layout switch (e.g. zoom) is restored by its own key | everyone | After switching, press its own key: the layout is back as it was |

## rules — Citing

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| references-1 | Citing | The app's files (the README, `CLAUDE.md`, code comments) cite a tdp clause as `tdp` plus the ID (e.g. `tdp K4`, `tdp panel.1`); `Rules K4` and a bare `K4` do not count | everyone | Read the files: wherever the README, `CLAUDE.md` and code comments mention a tdp clause |

## rules — K Core keys

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| K1-1 | K1 | `Tab` `Enter` `Esc` `Space` `?` `!` `q` `1`–`9` carry the meaning in the K1 table on every surface; the only exceptions are input state, PTY, modes, `q` on a form, and a form's typing note | everyone | Press these keys on every kind of panel and popup: nowhere uses them for something else |
| K1-2 | K1 | A core key the app designates keeps its meaning on every surface | everyone | Press that key on every kind of panel and popup: it does the same thing |
| K1-3 | K1 | No letter hotkey takes over a key in the K1 table | everyone | Read the code, or look at every menu and key reference: no hotkey uses `Tab` `Enter` `Esc` `Space` `?` `q` (a label marking the core key's own action, like `[Enter] Edit`, does not count; for digits see K1-7) |
| K1-4 | K1 | On a panel (with no popup open), `1`–`9` move focus to the panel marked `[N]` on its frame in the current screen | several panels | On a panel press `1`, `2`…; in an app with several screens, switch to another screen and press again: the jump goes to that screen's panels |
| K1-5 | K1 | Each screen numbers its own panels from `[1]` | everyone | Look at the numbers on each screen's panel frames: they start at `[1]` |
| K1-6 | K1 | A digit with no such panel on the screen does nothing | everyone | On a panel press a digit larger than the number of panels: nothing happens |
| K1-7 | K1 | The app registers no digit as a hotkey on a panel | everyone | Read the code, or look at the panels' Space menus and key references: no digit hotkeys |
| K1-8 | K1 | A global hotkey that is a digit can only be pressed inside the global operation popup; that digit on a panel jumps to a panel | everyone | On a panel that digit only jumps to a panel; only inside the global operation popup does it run |
| K1-9 | K1 | `!` on a panel opens the App Log | everyone | Press `!` on a panel |
| K2-1 | K2 | On a screen, `Tab` moves focus to the next panel of the same screen, wrapping from the last to the first, without crossing screens | several panels | Press `Tab` again and again on a panel: after a full round it is back at the first, and the screen does not change |
| K2-2 | K2 | In a popup with an action area (a form, an input popup with a button), `Tab` switches between the field area and the action area | form or color picker | Open a form and press `Tab`: focus goes back and forth between the field area and the action area |
| K2-3 | K2 | When `Tab` comes back to an area, it lands on the item it left | form or color picker | Move to the third field in the field area, `Tab` to the action area and `Tab` back: focus is on the third field |
| K2-4 | K2 | The items within the field area and within the action area move with hjkl | form or color picker | Press hjkl in each area: focus moves between the items of the same area |
| K2-5 | K2 | `Tab` does not leave the current popup | everyone | Press `Tab` on every kind of popup: focus never goes to the panel underneath |
| K2-6 | K2 | On a typing row (the typing row of a finder or a select, a panel filter), `Tab` goes to its list | panel filter or select or finder | Type a few characters on the typing row and press `Tab`: focus goes to the list |
| K2-7 | K2 | In an input popup with a single area and no grey suggestion (a password with an old password included: the grey dots are not a suggestion, and `Tab` does not take in the old password), `Tab` does nothing | input | Open an empty input popup and press `Tab`: nothing changes |
| K2-8 | K2 | A popup with an action area always has `Shift-Tab` (cycling backwards) | form or color picker | Press `Shift-Tab` on a form: focus switches the other way |
| K3-1 | K3 | `Enter` does the most intuitive action to the focused item | everyone | Press `Enter` on the items of every kind of panel; judge whether it is the most intuitive action for that kind of item |
| K3-2 | K3 | The same kind of item always gets the same `Enter` action within an app | everyone | Press `Enter` on the same kind of item in different panels and screens: it does the same thing |
| K3-3 | K3 | When the panel itself is a content area with no item to pick (e.g. a preview, a log), `Enter` does the most intuitive action to the whole panel | everyone | Press `Enter` on such a panel; judge whether it is the most intuitive action |
| K3-4 | K3 | After `Enter`, focus stays where it was as a rule (once a field's input popup is confirmed on a form or a one-value-per-row panel, focus is back on the same field / row; choosing a radio option or flipping a checkbox does not move it); position changes only in the three places built into the components (going into details, `Enter` on a typing row going to the list, a blocked submit on a form jumping to the first field with a problem), or on an app action the user expects to change it when pressing it | everyone | Press `Enter` on a panel, a form, a radio and a checkbox; see where focus rests; where it moved, judge whether the user expected the move when pressing the key |
| K3-5 | K3 | When `Enter` changes the panel or the screen, it lands where the user expected when pressing it (e.g. a detail's `Enter` going to the panel showing that item's details) | everyone | When `Enter` on a list changes the panel or the screen, judge whether the landing place is the one the user expected |
| K3-6 | K3 | In an input popup with focus on the value, `Enter` confirms the value: it is written back and the popup closes | input | Change the value and press `Enter`: the popup closes and the value is written back |
| K3-7 | K3 | With an invalid value (by the field's own rules: format, range, not empty), `Enter` does not write it back; the error goes in the reserved error row and the popup stays open; one opened from a form is also stopped at the input popup, not left to the form's submit. A field that opens empty and may not be empty is invalid too when `Enter` is pressed with nothing typed (with a suggested value, the suggested value is used) | input | Type an invalid value and press `Enter`; open an empty field that may not be empty and press `Enter` without typing |
| K3-8 | K3 | With the value the same as when the popup opened, and valid when it opened (e.g. an old value left unchanged), `Enter` writes nothing back and just closes (one opened from a form does not mark the form as changed) | input | Press `Enter` without changing the value: the popup closes; read the code: nothing is written back |
| K3-9 | K3 | Multi-line text: in the writing state `Enter` is a newline; only `Enter` after leaving the writing state (`Esc`) confirms | textarea | In the writing state press `Enter`: a newline; press `Esc` then `Enter`: the value is confirmed |
| K3-10 | K3 | On a typing row (the typing row of a finder or a select, a panel filter), `Enter` moves focus to the item under the cursor in the list, without running it; a second `Enter` on the list runs or picks it | panel filter or select or finder | Press `Enter` on the typing row: focus goes to the list and nothing runs; press it again to run |
| K3-11 | K3 | With no results on the typing row (including while results are listed as they are found and none has arrived yet), `Enter` does nothing | panel filter or select or finder | Type a string with no results and press `Enter` |
| K3-12 | K3 | On other parts of an input popup (e.g. a datetime picker's month, a color picker's R), `Enter` does the most intuitive thing | input | Press `Enter` on those parts; judge whether it is the most intuitive thing |
| K3-13 | K3 | Pressing the submit button checks every field; if any is invalid, nothing is submitted and focus moves to the first field with a problem | form | Leave two fields invalid and press the submit button |
| K3-14 | K3 | Things happening in the background (a load finishing, a task ending, a change from the remote side) never move the focus or change the screen | everyone | Let something happen in the background (a reload, a task ending, a remote change): the focus and the screen stay put |
| K3-15 | K3 | After adding an item (once New, Copy or Import is confirmed), the cursor moves to the new item, scrolled into view | everyone | Add an item: the cursor is on the new item |
| K4-1 | K4 | With no popup, `Esc` leaves the current mode or goes up one level (e.g. on a panel filter, `Esc` clears the filter whether focus is on the typing row or the list) | everyone | Enter a mode, or type a panel filter, and press `Esc` |
| K4-2 | K4 | `Esc` goes back one layer per press: with several popups stacked, one press closes only the topmost | everyone | Stack three layers (Space menu → global operation popup → confirm) and press `Esc` once: only the confirm closes |
| K4-3 | K4 | Once the top layer is closed, the popups underneath stay and are shown exactly as they were | everyone | As above: the two layers underneath are still there, with the cursor and content as before the confirm opened |
| K4-4 | K4 | `Esc` never leaves the app; at the top it does nothing | everyone | On a panel with no popup and no mode, press `Esc` again and again: the app does not close |
| K5-1 | K5 | With focus on any panel (including a panel with no items, and with the cursor on a checkbox row), `Space` opens the Space menu and does not flip the checkbox | everyone | Press `Space` on every panel |
| K5-2 | K5 | While the Space menu is open, `Space` closes it again | everyone | Open the Space menu and press `Space` again |
| K5-3 | K5 | On any popup other than the Space menu, `Space` does nothing (except for a mode inside it) | everyone | Press `Space` on the global operation popup, the key reference and a confirm: nothing happens |
| K5-4 | K5 | On checkbox options (a checkbox popup's list, the checkboxes drawn on a form), `Space` checks or unchecks | checkbox | Press `Space` on a checkbox option |
| K5-5 | K5 | A popup's own operations run by hotkey; no Space menu is stacked on top of a popup (except for a mode inside it) | everyone | No kind of popup offers a way to open a menu; every operation is by hotkey |
| K5-6 | K5 | In an app's own popup, when the focused cell has several values to cycle through, `Space` moves it to the next value | an app's own popup | Press `Space` again and again on such a cell: the values come in turn |
| K6-1 | K6 | `?` responds on any surface (input state and PTY follow K8 and K10; a textarea's moving state is not input state and opens the key reference as usual) | everyone | Press `?` in every kind of panel, popup and mode |
| K6-2 | K6 | While the key reference is open, `?` closes it again | everyone | Open the key reference and press `?` again |
| K6-3 | K6 | `?` opens the key reference of the frontmost surface | everyone | Press `?` on a popup: it lists that popup's keys, not those of the panel underneath |
| K6-4 | K6 | The key reference is read-only: no cursor, nothing to run | everyone | Open the key reference: there is no cursor row, and `Enter` runs nothing |
| K6-5 | K6 | A panel's key reference lists the keys that work on this panel, movement keys included | everyone | Press `?` on a panel |
| K6-6 | K6 | The key reference of a popup (the Space menu and the global operation popup included) lists only this popup's keys: its own hotkeys, `Enter`, `Esc`, the movement keys | everyone | Press `?` on the Space menu: no panel or global keys |
| K6-7 | K6 | The key reference lists every movement key that works, by K12: a one-dimensional list (a form, a one-value-per-row panel without tabs, a menu) gives `h\|k` back and `j\|l` forward | everyone | Press `?` on a form, a menu and a one-value-per-row panel without tabs, and look at `move` |
| K6-8 | K6, M6 | With the list empty (nothing to move over) or the content fitting whole (nothing to scroll), the key reference lists no movement or scrolling keys | everyone | Empty a list, and make some content fit, then press `?` on each |
| K6-9 | K6 | When a one-value-per-row panel's key reference has a "what each row is" section, it comes first: each row's name (in the ordinary text colour, not the key colour) and what it means, with the key sections after it | one value per row | Press `?` on a panel with this section; look at the order of the sections and the colour of the names |
| K7-1 | K7 | When a role is bound to several keys, every alias works the same on every surface | everyone | Press the alias on every kind of panel and popup: it does the same as the main key |
| K8-1 | K8 | In input state, every key that produces a character (letter hotkeys, the splash's `V`, `Space`, `?`, `q` included) is typed as a character and triggers no action | input or panel filter | On a typing row type `q`, `?`, a space and hotkey letters: they all become characters |
| K8-2 | K8 | In input state, `Esc` cancels the input | input or panel filter | Press `Esc` on a typing row |
| K8-3 | K8 | In input state, `Ctrl-C` starts the quit flow | input or panel filter | Press `Ctrl-C` on a typing row |
| K8-4 | K8 | The moment focus leaves the input surface, hotkeys work again | input or panel filter | Leave the typing row and press a hotkey at once |
| K8-5 | K8 | In the writing state of multi-line text, `Tab` inserts `input_tab_width` spaces (4 by default), not `\t` | textarea | In the writing state press `Tab` and count the spaces inserted; read the code: not `\t` |
| K9-1 | K9 | `q` and `Ctrl-C` do the same thing: start the app's quit flow | everyone | On a panel press `q`, then `Ctrl-C`: the same flow appears |
| K9-2 | K9 | `q` does not start the quit flow on a form or on a form's typing note (on a field that takes typing it brings up the typing note; elsewhere it does nothing) | form | On a form (not on a typing row) press `q`; on a field that takes typing, type a character to bring up the typing note, then press `q` |
| K9-3 | K9 | `Ctrl-C` still starts the quit flow on a form and on a form's typing note | form | Press `Ctrl-C` on a form and on its typing note |
| K9-4 | K9 | Pressing `Ctrl-C` again during the quit flow (e.g. while the confirm before quitting is open) quits at once, with no further questions (an app that quits straight away has it only with a popup open, K9-6) | everyone | Press `Ctrl-C`, and once the confirm appears press `Ctrl-C` again |
| K9-5 | K9 | Quitting is listed in the global operation popup | everyone | `Space` → `Global operation`: quitting is there |
| K9-6 | K9 | With a popup open, the first `q` or `Ctrl-C` never quits: a flow that would quit at once opens the quit confirm (`Quit <app>?`) instead, a flow whose first step already asks stays as it is; `Esc` goes back to the popup; on a panel the app's flow is unchanged | everyone | Open the Space menu and press `q`, then `Esc`; close the menu and press `q` on a panel |
| K9-7 | K9 | On an app's own popup that works like a form (with values to submit), `q` does not start the quit flow, while `Ctrl-C` still does | an app's own popup | Press `q` on such a popup, then `Ctrl-C` |
| K10-1 | K10 | With focus in a PTY (in a panel or a terminal popup), keys go to the subprocess: core keys and the app's hotkeys (the splash's `V` included) stop working, and only the exit key and the chords the app keeps (in an interactive terminal also `Alt-v` and `PgUp`) belong to the app; `Esc` goes to the subprocess too, so an open toast can only wait for its timer to go | PTY | In the PTY press `Space` `?` `q` `Tab` `Esc` `1` and the app's hotkeys: all go to the subprocess |
| K10-2 | K10 | At least one exit key moves focus out of the PTY | PTY | In the PTY, the exit key gets back to the app |
| K10-3 | K10 | The exit key is `Alt-Esc` | PTY | In the PTY press `Alt-Esc` |
| K10-4 | K10 | Whenever pressing `Alt-Esc` would move focus out of the PTY or end the subprocess, a confirm always comes first: `Enter` leaves, `Esc` returns to the PTY | PTY | In the PTY press `Alt-Esc`: a confirm appears; press `Esc`: back in the PTY; press `Alt-Esc` again and then `Enter`: it leaves |
| K10-5 | K10 | While the subprocess is not ready for keys yet, `Ctrl-C` is still forwarded to the subprocess | PTY | Press `Ctrl-C` while the subprocess is starting or connecting; read the code: it is forwarded |
| K10-6 | K10 | While the subprocess is not ready for keys yet, the exit key still works and is still disclosed | PTY | While the subprocess is starting or connecting, look at the footer and press the exit key |
| K11-1 | K11 | Inside a mode, `Space` opens the mode's Space menu, listing only what can be done in the mode | mode | Enter a mode and press `Space` |
| K11-2 | K11 | Inside a mode, `?` opens the mode's key reference: which keys work in the mode and what they do | mode | Enter a mode and press `?` |
| K11-3 | K11 | Inside a mode, `Esc` leaves the mode, back to the state before it was entered; in a mode with layers, back one layer at a time (`Visual>select` back to `Visual`) | mode | Enter a mode, do something and press `Esc`: the state is back to what it was before the mode |
| K11-4 | K11 | Inside a mode on a panel or in a popup, `q` and `Ctrl-C` run the quit flow, as K9 | mode | Enter a mode and press `q`, `Ctrl-C` |
| K11-5 | K11 | When a mode on a panel suspends `Tab` or the digit keys, pressing them must respond, saying to leave the mode with `Esc` first | mode (on a panel) | Enter a mode and press `Tab`, `2`: an explanation appears (e.g. a toast) |
| K11-6 | K11 | Inside a mode only the mode's own keys and the core keys in the K11 table work: panel hotkeys and global hotkeys do nothing | mode | Enter a mode and press panel hotkeys and global hotkeys: none does anything |
| K11-7 | K11 | Inside a mode, a hotkey that does nothing does so silently | mode | As above: no toast or any other notice |
| K11-8 | K11 | Inside a mode there is no list of keys to run | mode | Enter a mode: there is no list of keys to pick from and run |
| K11-9 | K11 | The mode's own keys are disclosed in the footer or the bottom-border hint | mode | Enter a mode and look at the footer (a mode on a panel) or the bottom-border hint (a mode in a popup) |
| K11-10 | K11 | Leaving the mode restores the mode name and the frame colour | mode | Press `Esc` to leave and look at that frame |
| K11-11 | K11 | With the mode in a popup, `Tab` and the digit keys do whatever they do in that popup (never switching panels), with no extra response; the footer stays as it is while a popup is open, not changing to the mode's words | mode (in a popup) | Enter a mode in a popup, press `Tab`, `2`, and look at the footer |
| K11-12 | K11 | With the mode on a PTY (a terminal's history or selection mode), any key other than the mode's own keys, `?` and `Esc` first leaves the mode, then goes to the subprocess; `q` and `Ctrl-C` too, never starting the quit flow | PTY | Enter the history mode on a PTY, type a character, press `q` and `Ctrl-C`: the mode is left first and the key lands in the subprocess |
| K11-13 | K11 | Inside a mode `!` does nothing | mode | Enter a mode and press `!` |
| K12-1 | K12 | Where you are not typing, no action takes `j` `k` `u` `d` `g` `G` `h` `l` (two-key chords starting with `g` excepted) | everyone | Read the code, or look at every menu and key reference: none of these letters is registered to an action |
| K12-2 | K12 | `h\|j\|k\|l` are `←\|↓\|↑\|→`: the arrow keys do the same | everyone | On a list, a menu and a form press hjkl and the arrow keys in turn: the same effect |
| K12-3 | K12 | With a left-right structure (tabs within one surface, two sides, a grid), `j\|k` go up and down and `h\|l` left and right (switching tabs, crossing to the other side) | everyone | On a panel with tabs press `h\|l` to switch tabs |
| K12-4 | K12 | In a plain one-dimensional list with no left-right structure (a form, a one-value-per-row panel without tabs, a menu), `h\|k` go back and `j\|l` go on | everyone | On the Space menu press `l` to go down and `h` to go up |
| K12-5 | K12 | A one-dimensional list in a panel with tabs: `h\|l` switch tabs, `j\|k` move in the list | panel tab | On a list panel with tabs press `h\|l` and `j\|k` |
| K12-6 | K12 | `u\|d` move half a page | everyone | On a list longer than a page press `u`, `d` |
| K12-7 | K12 | `gg\|G` go to the top and the bottom | everyone | On a list press `gg`, `G` |
| K12-8 | K12 | A single `g` does nothing | everyone | Press `g` and wait: the screen does not change |
| K12-9 | K12 | When the key after `g` is not a registered chord, it is as if `g` had not been pressed and that key works as usual | everyone | Press `g` then `j`: down a row |
| K12-10 | K12 | `Ctrl-U\|Ctrl-D` are not taken as aliases | everyone | On a list press `Ctrl-U`, `Ctrl-D`: no page turns |
| K12-11 | K12 | On a typing row, `Home` and `End` move the cursor to the start and the end | input or panel filter | Type a few characters on a typing row and press `Home`, `End` |
| K12-12 | K12 | On lists, menus, viewers and a textarea's moving state, `Home` and `End` do nothing | everyone | On a list and a menu press `Home`, `End`: the cursor does not move |
| K12-13 | K12 | Moving one step at a time (`j\|k`, `h\|l`, the arrow keys, `Tab`) along a run of items wraps at the ends: one step past the last goes to the first, and one step back from the first goes to the last (so do a panel's list, a menu, a form, a panel's tabs, `↑\|↓` on a finder's list and typing row, a reorder, a color picker's R → G → B, and a datetime picker's hour column (after 23 comes 00) and minute column (after 55 comes 00)) | everyone | On a panel's list, a menu, a form, a panel's tabs and the like, walk to each end and take one more step |
| K12-14 | K12 | While a Drag mode holds an item, `j\|k` move it, wrapping at the ends too: holding the last item, one step on takes it to the first and every other item moves down one; holding the first, one step back takes it to the last | Drag | Hold the last item and press `j` |
| K12-15 | K12 | `u\|d` stop at the first and the last item and do not wrap | everyone | Press `d` on one of the last few rows: it stops on the last row |
| K12-16 | K12 | What moves through space rather than along a run of items does not wrap: the days of a calendar, the month and the year, the two sides, moving within a piece of text (an input's typing-row cursor included) | everyone | Go on past the last day of a calendar, further right on the right side, or right from the last character of a typing row: it does not wrap |
| K12-17 | K12 | Two-dimensional content (several items on a row, e.g. the links on one line of a web page, the cells of a table) in a panel with tabs: `h\|l` switch tabs, `j\|k` walk item by item in reading order (left to right along a row, then the next row), wrapping at the ends | panel tab | On a panel with tabs and two-dimensional content, press `h\|l` and `j\|k` |

## rules — M Menus and disclosure

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| M1-1 | M1 | Every screen outside input state always shows `?`, `Space` and `!` (inside a mode `!` does nothing and may go unshown) | everyone | Look at the footer on every screen and in every mode |
| M1-2 | M1 | With the focus in a PTY, `?`, `Space` and `!` are not shown; what is always shown is the exit key and the keys the app keeps (in an interactive terminal also `Alt-v` and `PgUp`) | PTY | Go into a PTY and look at the footer or the terminal's bottom border |
| M2-1 | M2 | The Space menu is split into regions by what each acts on, in a fixed order: `item operation` → `panel operation` → the global row | everyone | Press `Space` on every panel |
| M2-2 | M2 | Each action is in the right place: one acting on the item under the cursor is in item operation, one acting on the current panel (or its tab) as a whole is in panel operation, and one belonging to no panel is in the global operation popup | everyone | Look at each panel's Space menu and the global operation popup, judging what each row acts on |
| M2-3 | M2 | The last row is always `Global operation`, with no hotkey | everyone | Look at the last row of the Space menu |
| M2-4 | M2 | `Enter` on the `Global operation` row opens the global operation popup | everyone | Move the cursor to that row and press `Enter` |
| M2-5 | M2 | With only one global action, it is still a single `Global operation` row that opens the global operation popup | everyone | Look at the last row of the Space menu: it is not the action itself |
| M2-6 | M2 | The region header strings are the English words `item operation` and `panel operation`, word for word | everyone | Look at the region headers of the Space menu |
| M2-7 | M2 | The global row carries no region header | everyone | Look at the Space menu: there is no header above the last row |
| M2-8 | M2 | Regions are separated by a divider line, the global row from the regions above it included | everyone | Look between the regions of the Space menu |
| M2-9 | M2 | No target, no region: on an empty list, item operation does not appear, header and all | everyone | Press `Space` when the list is empty |
| M2-10 | M2 | On a panel's Space menu, the item and panel regions always carry their headers, even when only one of them is left | everyone | Press `Space` where only one region is left (e.g. an empty list): the remaining region has its header |
| M3-1 | M3 | Every item operation and panel operation of every panel is in that panel's Space menu | everyone | Read the code to list each panel's actions, then find each one in the Space menu |
| M3-2 | M3 | Every global operation is in the global operation popup | everyone | Read the code to list the global actions, then find each one in the global operation popup |
| M3-3 | M3 | A popup's own operations are all in that popup's `?` key reference | everyone | Press `?` on every kind of popup and compare with the operations found by reading the code |
| M3-4 | M3 | The hint of a popup with only a typing row (text, password, number) lists every operation | text or password or number | Look at that popup's bottom-border hint and compare with the code |
| M3-5 | M3 | The hint of a popup with only a typing row fits in 80 columns | text or password or number | Set the terminal to 80 columns and open that popup: the hint is not cut |
| M3-6 | M3 | No action is triggered only by hotkey and found nowhere else: every letter hotkey is a shortcut to a row in some list | everyone | Read the code: every registered hotkey maps to a row of the Space menu, the global operation popup or another menu (for a popup's own keys see M3-3) |
| M4-1 | M4 | The row that switches to the current screen is disabled as M6 says | several screens | Open the global operation popup on a screen: the row switching to this screen is in the disabled colour, and the cursor skips it |
| M4-2 | M4 | With no popup open, the hotkeys in the global operation popup can also be pressed directly on a panel | everyone | Press a global hotkey directly on a panel |
| M4-3 | M4 | When a global hotkey clashes with a panel's own hotkey, the panel's wins | everyone | On that panel press the clashing key: the panel's action runs |
| M4-4 | M4 | The key reference of the panel with the clash does not list the global key it overrides | everyone | Press `?` on that panel |
| M5-1 | M5 | A hotkey letter that appears in the label (in either case) is bracketed in place, at its first occurrence (`[r]ename`, `[n]ew`, `D[e]lete`, `UR[L]`, `Ex[P]ort`) | everyone | Look at menu rows, statusbar chips and panel titles |
| M5-3 | M5 | A hotkey letter not in the label goes in front (`[x] Reset`) | everyone | As above |
| M5-4 | M5 | A hotkey with a modifier goes whole into the brackets (`[Alt-t]erm`) | everyone | As above |
| M5-5 | M5 | A hotkey of several characters goes whole into the brackets (`[go]to`) | everyone | As above |
| M5-6 | M5 | A digit hotkey always goes in front (`[3] Favorites`), never inside the word | everyone | As above |
| M5-7 | M5 | A core key marked on a label goes in front (`[Enter] Edit`) | everyone | As above |
| M5-8 | M5 | A label with no hotkey has no brackets | everyone | Look at the `Global operation` row and the other rows with no hotkey |
| M5-9 | M5 | The letters in brackets and in key names are in the case actually pressed (`[A]dd` is `Shift-A`; when the label's letter differs in case from the key, the brackets follow the key, e.g. `Export` with the hotkey `Shift-P` is written `Ex[P]ort`); in chips and titles turned uppercase they stay as they are (`[m]ANAGE`), and key names in hints, the footer and the key reference are not turned uppercase | everyone | Compare with the code: a row marked `[A]` is pressed with `Shift-A`, one marked `[a]` with `a` |
| M5-10 | M5 | A row whose label already spells out the key (`[/] Search`) is not bracketed again | everyone | Look at those rows: the key is marked only once |
| M5-11 | M5 | Hotkeys are marked explicitly, not hinted by colour or a glyph alone | everyone | Look at menus, the statusbar and panel titles: wherever there is a hotkey there is a bracket marking |
| M5-12 | M5 | On screen (the footer, hints, the key reference), key names are the names printed on the key cap, UpperCamelCase, no abbreviations of our own (`Esc` `Tab` `Enter` `Space` `Backspace` `Delete` `Home` `End` `PgUp` `PgDn`) | everyone | Look at the footer, hints and the key reference |
| M5-13 | M5 | On screen, arrow keys are written `↑` `↓` `←` `→` | everyone | Look at the footer, hints and the key reference |
| M5-14 | M5 | On screen, the letter after `Ctrl` is always upper case (`Ctrl-C`, `Ctrl-U`) | everyone | Look at the footer, hints and the key reference |
| M5-15 | M5 | On screen, modifiers are joined with `-` (`Alt-t`, `Shift-Tab`, `Alt-Esc`) | everyone | Look at the footer, hints and the key reference |
| M5-16 | M5 | On screen, `\|` joins several keys doing one thing (`h\|k`, `Enter\|Esc:close`) and a pair of opposite keys told with one verb (`j\|k:move`, `u\|d`, `gg\|G`), never `/` | everyone | Look at the footer, hints and the key reference |
| M5-17 | M5 | A range uses `–` (`1–9`) | everyone | Look at the footer and the key reference |
| M5-18 | M5 | Hotkeys on statusbar chips and panel titles also use the label's bracket marking | everyone | Look at the statusbar and panel titles |
| M5-19 | M5 | Every key mentioned in a sentence (empty states, toasts, error messages, and the description column of a menu or the key reference) is in square brackets (`Press [A] or [Space]`) | everyone | Look at empty states, toasts, error messages and description columns |
| M5-20 | M5 | Hints and the footer are written `key:description`, no space around the colon, one space between items | everyone | Look at the footer and each popup's bottom-border hint |
| M5-21 | M5 | The key reference has two columns, key and description; no brackets, no colon on the key | everyone | Press `?` and look |
| M5-22 | M5 | Keys in the README's prose are Markdown code, not square brackets | everyone | Read the file: the README |
| M5-23 | M5 | A label the README quotes from the screen is written as on screen (`[A]dd`) | everyone | Read the file: the README |
| M5-24 | M5 | Another tool's own keys are written the way that tool writes them (e.g. tmux's `prefix l`) | everyone | Read the files: the README, and the places on screen that mention another tool's keys |
| M5-25 | M5 | A label keeps its own case and is not rewritten for the hotkey (`Export`, never `ExPort`) | everyone | Look at menu rows, statusbar chips and panel titles |
| M5-26 | M5 | In the README, key names are the names printed on the key cap, UpperCamelCase, no abbreviations of our own (`Esc` `Tab` `Enter` `Space` `Backspace` `Delete` `Home` `End` `PgUp` `PgDn`) | everyone | Read the files: the README |
| M5-27 | M5 | In the README, arrow keys are written `↑` `↓` `←` `→` | everyone | Read the files: the README |
| M5-28 | M5 | In the README, the letter after `Ctrl` is always upper case (`Ctrl-C`, `Ctrl-U`) | everyone | Read the files: the README |
| M5-29 | M5 | In the README, modifiers are joined with `-` (`Alt-t`, `Shift-Tab`, `Alt-Esc`) | everyone | Read the files: the README |
| M5-30 | M5 | In the README, `\|` joins several keys doing one thing and a pair of opposite keys (`gg\|G`), never `/` | everyone | Read the files: the README |
| M6-1 | M6 | An action with no target: its row is not shown | everyone | Make the target go away (e.g. empty the list) and look at the menu |
| M6-2 | M6 | An action with a target that can't run right now: its row is still shown, in the disabled colour | disabled | Make an action unable to run for now and look at the menu |
| M6-3 | M6 | A disabled row keeps its usual description, with no reason added | disabled | As above, comparing the description before and after it is disabled |
| M6-4 | M6 | The cursor skips disabled rows | disabled | Move past a disabled row on the menu with `j\|k` |
| M6-5 | M6 | A disabled row's hotkey does nothing | disabled | Press that row's hotkey |
| M6-6 | M6 | The key reference does not list a key whose target does not exist | everyone | Press `?` |
| M6-7 | M6 | A section of the key reference with a title of its own describing another surface is shown as usual, not in the disabled colour | everyone | Press `?` and look at that section's colour |
| M6-8 | M6 | The section describing another surface comes last, after `app-wide` | everyone | Press `?` and look at the order of the sections |
| M7-1 | M7 | With the focus on a panel, `Space` always opens the Space menu: the global row is always there, so the menu is never empty | everyone | Press `Space` on every panel, empty and read-only ones included |
| M8-1 | M8 | When a menu other than the Space menu is grouped, the first group is the actions related to the current cursor | everyone | Open that menu and look at the first group |
| M8-2 | M8, M2 | Every group of a grouped menu (the first included) has a header naming its kind | everyone | Open that menu and look at each group: the first has a header too |
| M9-1 | M9 | When a hotkey does different things on different panels and both indicators are on screen at the same time, the one that fires when pressed on the current focus is bright, and the one that doesn't is dim | everyone | When the bottom-border hints of two panels both have the same key, look at the colours; switch focus and look again |

## rules — L Layout

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| L1-1 | L1 | At 80 columns × 40 rows, every core task can be completed | everyone | Open the terminal at 80 × 40 and go through every core task of the app |
| L1-2 | L1 | The app's minimum size is no larger than 80×40 (80×40 by default; the app may lower it) | everyone | Read the code: the minimum size set; set the terminal to 80×40 and check that the app draws as usual |
| L1-3 | L1 | Below the minimum size (too narrow or too short), the app's screen is not drawn; only the app's name (Blue bold) in the centre, with the hint `needs a terminal of at least <W>×<H>` (Overlay0, giving the app's minimum size) on the row below | everyone | Shrink the terminal below the minimum size (once only narrower, once only shorter) |
| L1-4 | L1 | When the two rows do not fit, the hint goes first and the name stays; shrinking all the way to 1×1 never crashes | everyone | Shrink all the way to 1×1 |
| L1-5 | L1 | Below the minimum size no key does anything (nothing goes to the app or into a PTY); `q` and a single `Ctrl-C` do nothing, and only `Ctrl-C` pressed twice quits at once | everyone | Once shrunk, press a few keys that would change something, `q` and one `Ctrl-C`; enlarge and see nothing changed; shrink again and press `Ctrl-C` twice |
| L1-6 | L1 | Once the window is back above the minimum size, the screen is as it was (the cursor, any open popup) | everyone | Move the cursor and open a popup, shrink, then enlarge again |
| L2-1 | L2 | Dynamic text in titles, the statusbar, chips and the like uses fixed-width slots or padding; its width does not change with the length of the content (the last dynamic slot in a row may go unpadded) | everyone | Make the dynamic text longer and shorter (switching tabs, progress, counts): the slot widths and the content beside them do not shift sideways |
| L3-1 | L3 | Permanent chrome has a fixed number of rows that does not change with the amount of content: the top row (in an app with several screens, the screen chip row plus the divider below it; in a single-screen app with a statusbar, one statusbar row) and one footer row | everyone | Make the content of the statusbar, chip row and footer grow and shrink, and resize the terminal: the top row (divider included) and the footer keep their number of rows |
| L3-2 | L3 | A panel's tabs are drawn on the panel's top border and take no row of their own | panel tab | Look at a panel with tabs: the tabs are in the string of capsules on the top border, with no other row of tabs outside the frame |
| L4-1 | L4 | Every line on screen is exactly the terminal width, no more, no less | everyone | Look at every line at several sizes, with icons taking one cell and two: the right border never wraps and no stale cells linger; or read the code: the screen tests run with icons and powerline symbols taking one cell and two (E5-11) |
| L5-1 | L5 | The focused surface is recognisable at a glance (in a mode too) | everyone | On every screen, one glance tells which panel or popup has focus |
| L5-2 | L5 | Moving focus shifts no content | several panels | Press `Tab` to switch panels and compare the screen before and after: text and frames stay in place |
| L5-3 | L5 | Focus is not told by colour alone: something besides colour differs (e.g. the line style) | several panels | Compare the frames of the focused and unfocused panels: something besides colour differs; in a mode it still shows which panel has focus |

## rules — F Popups

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| F1-1 | F1 | Every popup of the app is one of the eight classes: menu, confirm, input, form, note, toast, terminal, an app's own popup (the splash is not a popup; a box drawn by a panel's own content is content, not a popup) | everyone | Open every popup and class each one |
| F1-2 | F1 | A menu moves its cursor with `j\|k` | everyone | Open the Space menu and press `j`, `k`: the cursor moves up and down |
| F1-3 | F1 | A menu (the Space menu and the global operation popup included) runs a row with `Enter` or its hotkey | everyone | On the Space menu press `Enter` on one row and another row's hotkey: each runs its row |
| F1-4 | F1 | An input popup handles one value per popup | input | Open every input popup: each enters or picks only one value |
| F1-5 | F1 | A form has one value per row | form | Open every form: each row has only one field |
| F1-6 | F1 | A note is read-only | everyone | Open a note such as the `?` key reference: no key changes its content |
| F1-7 | F1 | While a toast is open, every key but `Esc` passes through it | toast | While a toast is up press `j`, `Space`: what is underneath reacts as usual, and the toast takes no key |
| F1-8 | F1 | A popup with a list of options to run with `Enter` is a menu, not a note | everyone | Look at every read-only popup with a list of options: each looks and works like a menu |
| F1-9 | F1 | When a menu's `Enter` opens the row in full (e.g. a jobs-list row with nothing to do on it), it opens a note showing the row's whole content | everyone | In such a menu press `Enter` on a row: a note stacks up showing the whole content |
| F1-10 | F1 | A confirm carrying content is one confirm, not split into two popups, a note plus a confirm | confirm | Trigger a confirm carrying details: only one layer of popup stacks up |
| F1-11 | F1 | A popup that changes class by phase belongs to one class at a time, and its keys follow that class | everyone | Press `j` and `Enter` on a finder's typing row and on its list: the keys mean what the class at that moment says |
| F1-12 | F1 | In a popup that changes class by phase, `Esc` closes the whole popup rather than going back a phase (whether focus is on the typing row or the list) | everyone | With focus on a finder's list press `Esc`: the whole finder closes |
| F1-13 | F1 | A list popup with search (a select, a checkbox popup, a file-picker and the like) works as a finder: the typing row is the input state, the list is for picking | finder | Open every searchable list popup: what is typed on the typing row is content, and the list is for picking |
| F1-14 | F1 | A list popup with no search works as a menu; the one exception is reorder, which is an input | everyone | Look at every list popup with no search: all but reorder look and work like a menu |
| F1-15 | F1 | A toast does not count toward the layer colours' levels | toast | With a toast up over a popup, open another popup: the new popup's layer colour is the same as without the toast |
| F1-16 | F1 | With a toast and a popup both open, `Esc` closes the toast first | toast | With a toast up over a popup press `Esc` once: only the toast closes |
| F1-17 | F1 | Each step of a multi-step flow is its own popup, stacked, not one box changing its content | everyone | Go through a multi-step flow (e.g. picking a column, then a direction): each step stacks a new layer |
| F1-18 | F1 | An app's own popup holds only content the seven classes cannot hold; what they can hold (a list, a confirmation, one value, a form of one value per row, read-only content, a short message, a subprocess) is done as that class | an app's own popup | Open every popup of the app's own: none of their content fits one of the seven classes |
| F1-19 | F1 | An app's own popup with values to submit works like a form: the action area below the content, `Tab` switching between the content and the action area, a button submitting | an app's own popup | Press `Tab` on such a popup, then a button |
| F1-20 | F1 | A box drawn by a panel's own content is not a layer: `Space` and `?` on it open the Space menu and key reference of the panel it is in, and `Esc` does what K4 says on a panel | panel content box | When the content draws a box, press `Space`, `?` and `Esc` |
| F2-1 | F2 | The animation is 32ms a frame, 9 frames each way for opening and closing (about 288ms) | everyone | Read the code, or count the frames in a recording: 32ms a frame, 9 frames each way |
| F2-2 | F2 | A popup takes no keys until its opening animation ends | everyone | Open a popup and press `j` at once: the cursor does not move before the animation ends |
| F2-3 | F2 | When several layers close together (an action closing the whole stack, T1 clearing two or more layers of source), every layer closes at once, each at its own size and layer colour, still about 288ms in all; not just the top layer animating | everyone | Read the code; or from two stacked popups run an action that clears the source, and step through the frames: both layers close together |
| F3-1 | F3 | Any visible popup (toasts included, without waiting for the countdown) starts closing at once on `Esc` (the only exceptions are those F3 lists: PTY, a textarea's writing state, a mode inside a popup, a form / textarea / reorder / app's own popup working like a form whose content changed) | everyone | Press `Esc` on every class of popup: the closing animation starts at once |
| F3-2 | F3 | A popup already running its closing animation ignores `Esc` and takes no other keys either | everyone | Press `Esc`, and while the closing animation is still playing press `j`, `Enter`: the closing layer does not react; press `Esc` again during the closing animation: it is the next layer that closes |
| F3-3 | F3 | In a textarea's writing state, `Esc` leaves the writing state for the moving state | textarea | While writing in a textarea press `Esc`: back in the moving state, with the popup still open |
| F3-4 | F3, K4 | While a popup is in a mode (e.g. a viewer's selection mode, a reorder's Drag mode), `Esc` leaves the mode first and the popup stays; the next press closes the popup | mode | In a viewer press `v` for the selection mode (or `D` in a reorder), then press `Esc`: the mode ends and the popup stays; only another `Esc` closes the popup |
| F3-5 | F3 | In a form whose content changed, `Esc` first opens a confirm asking whether to discard it | form | Change a field and press `Esc`: a discard confirm stacks up |
| F3-6 | F3 | In a textarea whose content changed, `Esc` to close first opens a confirm asking whether to discard it | textarea | Change the content, go back to the moving state and press `Esc`: a discard confirm stacks up |
| F3-7 | F3 | In a reorder whose order changed, `Esc` first opens a confirm asking whether to discard it | reorder | Move an item and press `Esc`: a discard confirm stacks up |
| F3-8 | F3 | In an app's own popup with values to submit whose content changed, `Esc` first opens a confirm asking whether to discard it | an app's own popup | Change something and press `Esc`: a discard confirm stacks up |
| F4-1 | F4 | When popup A opens popup B, A stays underneath | everyone | Open the global operation popup from the Space menu, then run one of the app's own actions from the Space menu that opens another popup: the (dimmed) Space menu is still visible underneath |
| F4-2 | F4 | Cancelling B returns to A | everyone | Press `Esc` on the global operation popup and on a popup opened by one of the app's own actions: back to the Space menu each time |
| F5-1 | F5 | Errors appear immediately (a toast or a popup) | everyone | Trigger an error (e.g. no network, no permission): a toast or a popup shows at once |
| F5-2 | F5 | Errors do not block the app | everyone | After an error appears, the app works as usual, and the user can go on to deal with the error itself |
| F5-3 | F5 | Errors also go into the App Log, to be looked up after the toast has gone | everyone | Cause an error, wait for the toast to go, press `!` |
| F6-1 | F6 | An action set to be confirmed is confirmed every time (a choice made explicitly in a picker may count as the confirmation) | confirm | Do the same action two or three times: a confirm every time |
| F6-2 | F6 | On a confirm, `Enter` accepts and `Esc` cancels | confirm | On a confirm press `Enter`, and `Esc` |
| F6-3 | F6 | A confirm's only answers are the two keys `Enter` and `Esc`; no `y` or `n` | confirm | On a confirm press `y`, `n`: nothing happens |
| F6-4 | F6 | A confirm's prompt says what accepting will do (verb and object), not an abstract OK | confirm | Read every confirm's question and its `Enter` hint |
| F6-5 | F6 | A confirm cannot be completed by accident (e.g. a mouse click must not accept it) | confirm | Click on a confirm and press keys other than the answers: none accepts it |
| F7-1 | F7 | A popup's width is fixed when it opens and does not change while it is open | everyone | In an open popup make the content longer and shorter (typing, filtering): the frame's width does not change |
| F7-2 | F7 | A popup whose content width is known is at most `min(terminal width − 2, 120)` wide | everyone | Open it once in a 200-column terminal and once in a very narrow one (e.g. a menu, a confirm, a select, a checkbox popup): the width never exceeds the cap |
| F7-3 | F7 | A popup whose content width is not known is `min(terminal width − 2, 120)` wide | everyone | Open it once at 80 columns and once at 200 (e.g. a URL, search results listed as they come, a form): the width is 78 and 120 |
| F7-4 | F7 | Popups are centred horizontally | everyone | Measure each popup's distance from the screen's left and right edges |
| F7-5 | F7 | A popup's height follows the content and is fixed when it opens, not resized with the content afterwards (changes during loading and changes the user made excepted) | everyone | With a popup open, let the data behind it update: the frame's height does not change |
| F7-6 | F7 | A popup is at most the screen height − 2: the screen chip row or the statusbar and the footer always stay in view (the divider under the chip row may be covered) | everyone | Open a popup with very long content: the screen chip row (or the statusbar) and the footer are not covered |
| F7-7 | F7 | Content beyond the maximum scrolls inside the box | everyone | Open a long list in a short terminal: scrolling inside the box shows all of it |
| F7-8 | F7 | When the user's action changes a popup's row count (removing a row, a row added, filtering as they type), what is disclosed is correct whether or not the height follows | everyone | In a popup remove a row or filter by typing: the box has no leftover, missing or misplaced rows |
| F7-9 | F7 | While the content of the whole popup is still loading, a spinning loading icon always sits after its title | loading | Open that popup where loading is slow: the icon after the title spins |
| F7-10 | F7 | When loading ends, the loading icon goes | loading | Wait for loading to finish: the icon after the title is gone |
| F7-11 | F7 | Popups are centred vertically (toasts excepted) | everyone | Measure each popup's distance from the screen's top and bottom edges |
| F7-12 | F7 | A popup whose value can be invalid (an input popup, a form) opens with one error row in its height, blank while there is no error | input | Open them: the box keeps one blank error row |
| F7-13 | F7 | An invalid value has its error written in the error row, and the box keeps its height | input | Enter an invalid value and press `Enter`: the error shows in that row, and the box does not grow |
| F7-14 | F7 | A terminal popup is `terminal width − 2` wide, with no 120-column cap | terminal popup | Open it in a 200-column terminal: the width is 198 |
| F7-15 | F7 | A terminal popup runs down to the last row of the screen, covering the footer | terminal popup | Open a terminal popup: its bottom border is on the last row, and the footer is gone |
| F7-16 | F7 | A terminal popup has no padding on any side inside its frame | terminal popup | The subprocess's content sits right against the frame lines on all four sides |
| F8-1 | F8 | While a popup is open, everything but the topmost popup (the popups beneath it and the whole base screen) is dimmed; only the topmost is bright | everyone | Open the global operation popup from the Space menu: the Space menu and the base screen underneath are both dim |
| F8-2 | F8 | Streaming content underneath (logs, remote sessions) and warning colours are dimmed too | streaming content | Open a popup over streaming content or warning colours: they dim too |
| F8-3 | F8 | Dimming fades the foreground and the background alike toward the base, without dropping backgrounds | everyone | Open a popup and look underneath: the bodies of powerline capsules, the cursor bar and selection highlights are still there, only darker |
| F8-4 | F8 | Every colour is faded on its own, never stripped and redrawn, never every foreground turned into one dim colour (the borders of the popups below are dimmed versions of their own layer colours, still showing which layer each is) | everyone | Open a popup and look underneath: layer colours, warning colours and streaming content are each a dimmed version of their own colour |
| F8-5 | F8 | The drawn screen is dimmed once: an unfocused panel gets a little darker again under a popup | several panels | Open a popup: the unfocused panel underneath is darker than the one that had focus before it opened |
| F8-6 | F8 | A toast does not trigger dimming | toast | When a toast pops up, the screen underneath does not dim |

## rules — X Mouse

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| X1-1 | X1 | The app is fully usable without a mouse | everyone | Without the mouse, go through every feature with the keyboard alone |
| X2-1 | X2 | Every mouse action maps to a keyboard action; nothing can be done by mouse alone | mouse | List every mouse action of the app and find the matching key for each |

## rules — T Time axis

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| T1-1 | T1 | For an action that opens one popup from another, whether the source stays after confirming follows the T1 table (by what happens once confirmed); for an action not in the table, a cleared source is one the user no longer wants once done with the target | everyone | Go through each of the app's actions run from a menu that opens another popup, and compare with the T1 table |
| T1-2 | T1 | A confirm before an action is only a gate: cancelling on the confirm always returns to the source (the menu) | confirm | Run an action that asks first from a menu, press `Esc` on the confirm: back on the menu |
| T1-3 | T1 | When what happens once confirmed is a value picked and written back (an input popup, a select writing back to a form or a picker), the source stays | form or input | Pick a field's value on a form: back on the form |
| T1-4 | T1 | When what happens once confirmed is opening a shell, the source is cleared | PTY | Open a shell from a menu; after leaving it, the menu is gone |
| T1-5 | T1 | When what happens once confirmed is a screen change (to another screen of the chip row) or a drill-down (e.g. into a directory, Deployment → Pods), the source is cleared | everyone | Change screen or drill down from a menu: the menu is gone |
| T1-6 | T1 | When the source is cleared, it closes while the target opens, both animations at once, without waiting for the source to finish closing; a source of several layers closes all its layers together (F2) | everyone | In a recording, the target's opening animation and the source's closing animation start together |
| T1-7 | T1 | When what happens once confirmed is opening something to look at (a YAML view, details, the full text), the source stays | everyone | Open something to look at from a menu; after closing it, you are back on the menu |
| T1-8 | T1 | When what happens once confirmed is editing the item in an editor (e.g. `kubectl edit`, `$EDITOR`), the source stays | everyone | Edit an item in an editor from a menu; after leaving the editor, you are back on the menu or the viewer |
| T1-9 | T1 | When what happens once confirmed makes the item go away (deleting, moving it elsewhere), the source is cleared | everyone | Delete an item from a menu: once confirmed, the menu is gone |
| T2-1 | T2 | An unfocused panel has its content (header, group titles, labels, cursor included) dimmed with the same fade as F8, and the cursor does not change to another colour | several panels | Press `Tab` to switch panels: the unfocused panel's content is dimmed, each colour a dimmed version of itself |
| T2-2 | T2 | Streaming content (logs, live output, remote sessions) is not dimmed on blur | streaming content | Move focus to another panel: the panel with streaming content does not dim |
| T2-3 | T2 | A streaming panel's content is not dimmed on blur, but the hint on its bottom border still is | streaming content | Move focus to another panel; the streaming panel's hint dims |

## rules — S Splash

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| S0-1 | Chapter S opening | The splash takes the whole screen; while it is open nothing of the screen beneath (chip row, panels, footer) is drawn | everyone | Press `V`: only the splash is on screen |
| S0-2 | Chapter S opening | Closing the splash brings the screen back | everyone | Close the splash: the screen is as it was before `V` |
| S1-1 | S1 | `V` on a panel opens the splash (a panel giving `V` to a panel operation excepted) | everyone | Press `V` on every panel |
| S1-2 | S1 | When some panel takes `V`, at least one panel in the app keeps `V` for the splash | everyone | Press `V` on every panel: at least one opens the splash |
| S2-1 | S2 | The splash does not appear in the Space menu, the global operation popup, the key reference, the footer or panel hints | everyone | Open these places: no `V` or splash to be found |
| S2-2 | S2 | The README, the CHANGELOG and the release notes do not mention the splash, entries already released included | everyone | Read the files: neither README nor the CHANGELOG (old versions' entries included) mentions the splash or the `V` easter egg; for an app that has released, no release's notes on GitHub do either |
| S3-1 | S3 | While the splash is open, any key only closes it, and the key does nothing else (`q`, `Ctrl-C`, `Esc`, `Space` and `?` included) | everyone | Open the splash and press each of these keys: each time it only closes the splash; `Ctrl-C` does not quit the app |
| S4-1 | S4 | The splash is not played at start-up | everyone | Start the app: it goes straight to the main screen |
| S4-2 | S4 | With a popup open, `V` does not summon the splash | everyone | Press `V` with the Space menu open |
| S5-1 | S5 | The splash draws the app's `docs/icon.svg`, cell for cell | everyone | Press `V` and compare it cell by cell with `docs/icon.svg` |
| S5-2 | S5 | The viewBox of `docs/icon.svg` is 250 × 250; each cell is one 10 × 10 rect; the background colour is `#000000` | everyone | Read the file: `docs/icon.svg` |
| S5-3 | S5 | The mark takes 25 × 19 cells (x 0–240, y 30–210), its leftmost and rightmost columns being background | everyone | Read the file: the range of the rects' coordinates |
| S5-4 | S5 | The U frame is `#205090`, the same in every family app, never changed | everyone | Read the file: the rects under `<!-- U -->` are the same as the U frame in tdp's `principle/icon.svg` |
| S5-5 | S5 | The letters in the frame are `#f2b753`, spelling the app's own name | everyone | Read the file and look at the splash: the gold letters spell the app's name |
| S5-6 | S5 | Letters are marked with XML comments: a comment starts a letter and holds only that letter, and the rects after it belong to it until the next comment; the first comment is `<!-- U -->` | everyone | Read the file: where the comments are and what they say |
| S5-7 | S5 | Each cell is one `nf-fa-square` (U+F0C8), two columns wide; where icons take one cell, a space follows it | everyone | Press `V` once with icons at one cell and once at two (`<APP>__ICON_WIDTH`): every cell is two columns wide |
| S5-8 | S5 | The background cells are squares in Surface0 `#313244` | everyone | Look at the splash's background |
| S5-9 | S5 | One more background row is drawn above the mark and one below, 21 rows in all, so the margin is the same on all four sides | everyone | Count the rows of the mark on the splash and the width of the background on all four sides |
| S5-10 | S5 | A blank row under the mark, then six rows of text (with a blank row between the tagline and `developed by`, and one between the e-mail address and the hint) | everyone | Count the rows under the mark |
| S5-11 | S5 | Each row of the text under it is centred within the mark's width | everyone | Look at the blank space left and right of each row |
| S5-12 | S5 | No row of the text under it is wider than the mark (50 columns) | everyone | Measure each row's width |
| S5-13 | S5 | Row 1 is the name: the app's command name, Blue, bold | everyone | Look at the splash's first row |
| S5-14 | S5 | Row 2 is the version, the same as `<app> version` prints, Blue | everyone | Compare the splash's version with `<app> version` |
| S5-15 | S5 | Row 3 is a one-line tagline, Text | everyone | Look at the splash's third row |
| S5-16 | S5 | Then `developed by`, Overlay0 | everyone | Look at the splash |
| S5-17 | S5 | Then the author's e-mail address, in the mark's gold `#f2b753`: a family member writes `vulcan.shen.2304@gmail.com`, an app made by tdp writes its own (the opening of chapter E) | everyone | Look at the splash |
| S5-18 | S5 | The last row is `Press any key to close`, Overlay0 | everyone | Look at the splash |
| S5-19 | S5 | The whole block (the mark, a blank row and the text, 30 rows × 50 columns) is centred on the screen, both ways | everyone | Press `V` in a large terminal and measure the blank space on all four sides |
| S5-20 | S5 | When the terminal is under 50 columns or 30 rows, the mark is not drawn, only the text under it, centred both ways | everyone | Shrink to 49 columns or fewer, or 29 rows or fewer, and press `V` |
| S5-21 | S5 | When the mark does not fit, the text still appears in two batches: the name, version and tagline 400ms after opening, the author and the hint 500ms later | everyone | Read the code: the timing of the two batches when the mark does not fit |
| S5-22 | S5 | When too narrow the text wraps, each wrapped row still centred (where it breaks follows the components' "Wrapping") | everyone | Shrink to narrower than the tagline and press `V` |
| S5-23 | S5 | A word wider than the terminal on its own is cut by cells into pieces, each centred, and nothing is lost | everyone | Shrink to narrower than the e-mail address (26 columns) and press `V` |
| S5-24 | S5 | Still too short: rows are cut from the bottom up — the hint goes first, then the two author rows, then the tagline | everyone | Shrink row by row and press `V`; look at the order in which rows go |
| S5-25 | S5 | The name and the version always show; with a single row, only the name | everyone | Shrink to the shortest and press `V`: the name and the version are still there; at one row, only the name is |
| S5-26 | S5 | When a group goes, the blank row above it goes with it, so no blank row is left at the bottom | everyone | Shrink and press `V`: the last row has text |
| S5-27 | S5 | The reveal animation is drawn in stages, in order (the background, the gold letters, the U frame, the text), a tick being 10ms; stages 1–3 (the background, the gold letters, the U frame) have a 250ms hold between one stage and the next | everyone | Read the code: the order of the stages, the 10ms tick, the 250ms between stages |
| S5-28 | S5 | The background: a whole row a tick, filled top to bottom | everyone | Read the code: the background a whole row a tick, top to bottom |
| S5-29 | S5 | The gold letters: one letter a stage, in the order of the comments in the svg; 2 cells a tick, the cells of a letter appearing scattered | everyone | Read the code: in the comments' order, 2 cells a tick, a letter's cells scattered |
| S5-30 | S5 | The U frame: rising from the bottom row by row; within a row from the middle outwards, one pair of mirrored cells a tick, the 13th cell on the centre line taking a tick of its own | everyone | Read the code: bottom to top, from the middle outwards within a row, a pair a tick, the 13th cell on the centre line a tick of its own |
| S5-31 | S5 | The text: 400ms after the last cell of the U frame appears (with no 250ms added), the name, version and tagline appear together; 500ms later, `developed by`, the e-mail address and the hint appear together | everyone | Read the code: 400ms from the last cell of the U frame, then 500ms |

## rules — E App and environment

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| E1-1 | E1 | `<app> version` prints the version | everyone | Run `<app> version` |
| E1-2 | E1 | `<app> help` prints the command-line usage (not the key reference) | everyone | Run `<app> help` |
| E2-1 | E2 | Every environment variable the app itself reads (including ones for tests and ones passed to its own subprocesses) is named `<APP IN CAPITALS>__<NAME>`: two underscores, the variable name in capitals with single underscores between words | everyone | Read the code: find every environment variable name read or written; all but those meant for another program follow this form |
| E2-2 | E2 | `<APP>__CONFIG` names the config directory (the config file lives in it), not the config file | stores settings or data | Start with `<APP>__CONFIG` set to a directory: the app reads the config file in that directory |
| E2-3 | E2 | Renamed environment variables do not keep their old names | everyone | Read the code: the old name is no longer read |
| E2-4 | E2 | Variables to be carried across ssh start with `LC_` (OpenSSH only forwards `LANG` and `LC_*` by default) | everyone | Read the code: every environment variable carried to the remote side starts with `LC_` (an app without ssh never has this case) |
| E3-1 | E3 | Config is in `$XDG_CONFIG_HOME/<app>` by default (falling back to `~/.config/<app>`) | stores settings or data | Read the code, or start with no environment variables set, and see where config is read and written |
| E3-2 | E3 | The config location can be overridden with `<APP>__CONFIG` | stores settings or data | Start with `<APP>__CONFIG` set: config moves there |
| E3-3 | E3 | State the app keeps separately is in the config directory by default | stores settings or data | Read the code, or start the app and see where the state file is |
| E3-4 | E3 | The state location can be overridden with `<APP>__STATE` | stores settings or data | Start with `<APP>__STATE` set: state is stored there instead |
| E3-5 | E3 | Data is under `~/.<app>/` by default | stores settings or data | Read the code, or start the app and see where the data is |
| E3-6 | E3 | The data location can be overridden with `<APP>__DATA` | stores settings or data | Start with `<APP>__DATA` set: data is stored there instead |
| E3-7 | E3 | The cache is in the system's cache directory (macOS `~/Library/Caches/<app>`; Linux `$XDG_CACHE_HOME/<app>`, falling back to `~/.cache/<app>`; Windows `%LOCALAPPDATA%\<app>\cache`) | stores settings or data | Read the code, or start the app and see where the cache is |
| E3-8 | E3 | The cache location can be overridden with `<APP>__CACHE` | stores settings or data | Start with `<APP>__CACHE` set: the cache is stored there instead |
| E3-9 | E3 | On Windows `~` is `%USERPROFILE%`: config in `%USERPROFILE%\.config\<app>`, data under `%USERPROFILE%\.<app>\`, not in `%APPDATA%` | Windows build | Read the code: how the paths are worked out on Windows |
| E3-10 | E3 | Hiding private keys and owner-only files in the previews of popups uses the config key `hide_secrets_in_preview` (in the app's config file), `false` by default: everything shown as usual | file preview | Read the code and the config file: the key's name and its default |
| E3-11 | E3 | (An app with only the App Log does not count.) How many spaces `Tab` inserts in the writing state, and how many cells a Tab is drawn as in content for reading (viewers, file previews, a log on a panel), uses the config key `input_tab_width`, `4` by default | textarea or viewer or streaming content or file preview | Read the code and the config file: the key's name and its default |
| E3-12 | E3 | The config file is `config.yaml` in the config directory | stores settings or data | Read the code, or start the app and look at the config file's name and format |
| E3-13 | E3 | Things go where "what happens if it is deleted" puts them: the app's own single options are settings; what only falls back to defaults is state; what cannot be got back and would be backed up (bookmarks, records, logs, lists the user writes for the app — even when they hold how the app works — and original values the app keeps for the user) is data; what the app rebuilds or fetches again is cache | stores settings or data | Read the code: where each kind of thing written to disk goes |
| E3-14 | E3 | After a release moves a location, the first start moves it item by item: an item missing at the new place is moved over, with a toast saying from where to where; the emptied old directory is then removed | stores settings or data | Read the code; or put things at the old place and start the new release (for an app that moved a location) |
| E3-15 | E3 | When the move fails, the old place is used as before, and an error popup gives both paths | stores settings or data | Read the code; or make the new place unwritable and start the app |
| E3-16 | E3 | An item already at the new place when moving: a cache's old copy is deleted; settings, state and data are not deleted but left at the old place, with an error popup giving both paths | stores settings or data | Read the code; or put the same item at both places and start the new release |
| E3-17 | E3 | When the app's own settings, state or data cannot be read, a confirm at start gives the path and the reason, with the hint `Enter:move Esc:quit` | stores settings or data | Damage the config file's format and start the app |
| E3-18 | E3 | `Enter` on that confirm renames the file to `.bak` and starts as on the first start | stores settings or data | As above, press `Enter`: the `.bak` is there and the app is as on its first start (a file the first start makes is made again) |
| E3-19 | E3 | With a `.bak` already there, `.bak.1`, `.bak.2`… are used, nothing overwritten; the question names the file really used | stores settings or data | Leave a `.bak` in place, damage the file and start the app |
| E3-20 | E3 | `Esc` on that confirm quits the app and writes the path and the reason to stderr | stores settings or data | As above, press `Esc`: the app ends and the terminal shows the message |
| E3-21 | E3 | A cache that cannot be read is thrown away and rebuilt, with no question | stores settings or data | Damage a cache file and start the app: no confirm |
| E3-22 | E3 | When the data is one record per file, `Enter` only renames the unreadable record to `.bak`, making nothing new, and the rest is read as usual; the question says `go on without it` | stores settings or data | Damage one record's file, start the app, press `Enter` |
| E3-23 | E3 | A settings, state or data file the app no longer uses is not deleted and gets no toast; while it is there, every start writes an INFO entry with its path to the App Log | a file no longer used | Put an old file the app no longer uses in place, start, look at the App Log and the disk; restart and look at the App Log again |
| E4-1 | E4 | PUA glyphs are written as code points in the source | everyone | Read the code: a scan of the source finds no PUA characters |
| E4-2 | E4 | The README's requirements say a Nerd Font is required | everyone | Read the prerequisites in both READMEs |
| E4-3 | E4 | The README's requirements say, next to the Nerd Font, that a truecolor terminal (24-bit colour) is required | everyone | Read the prerequisites in both READMEs |
| E5-1 | E5 | What is measured is how far the cursor actually moves (a glyph that spills into the next cell while the cursor moves one counts as one) | everyone | Open the app in a terminal where icons take two cells: the borders line up |
| E5-2 | E5 | Icons (PUA, the powerline symbols excepted) and powerline symbols (U+E0A0–U+E0D7) are measured each on its own and kept separately | everyone | Read the code: each kind has its own width; with "icons two cells, powerline symbols one" the borders line up |
| E5-3 | E5 | The app probes with CPR at startup: it prints an icon and asks for the cursor position, then prints a powerline symbol and asks again | everyone | Read the code: the probe at startup |
| E5-4 | E5 | Every width measurement (padding, clipping, centring, joining side by side, borders, overlaying popups) goes through one display-width function | everyone | Read the code: no call measures width bypassing the display-width function |
| E5-5 | E5 | The icon width is taken in the order `<APP>__ICON_WIDTH` → `TERMINU__ICON_WIDTH` → `LC_TERMINU_ICON_WIDTH` → the probe | everyone | Start once with all the variables set, once with only some, and once with none: see which value is used |
| E5-6 | E5 | The powerline symbol width is taken in the order `<APP>__POWERLINE_WIDTH` → `TERMINU__POWERLINE_WIDTH` → `LC_TERMINU_POWERLINE_WIDTH` → the probe | everyone | Start once with all the variables set, once with only some, and once with none: see which value is used |
| E5-7 | E5 | The probe runs on unix only; Windows defaults to one cell, overridden by the environment variables | Windows build | Read the code: no probe on Windows, one cell by default |
| E5-8 | E5 | When it starts a subprocess, the app sets `TERMINU__ICON_WIDTH` and `TERMINU__POWERLINE_WIDTH` (the cells it uses) in the subprocess's environment | PTY | In the PTY run `echo $TERMINU__ICON_WIDTH $TERMINU__POWERLINE_WIDTH` |
| E5-9 | E5 | An app with ssh puts the widths it uses in `LC_TERMINU_ICON_WIDTH` and `LC_TERMINU_POWERLINE_WIDTH` when it connects, carrying them to the remote side | PTY | Read the code: the two variables are sent when connecting; run a family app on the remote side: the borders line up |
| E5-10 | E5 | When an overlaid popup is wider or taller than the screen (or larger both ways), it starts at 0 and what falls off the screen is clipped, with no panic | everyone | Shrink the terminal below a popup's size and open the popup, and resize while it is open: the app does not crash |
| E5-11 | E5 | The app's L4 screen tests (its own layout with the popups it opens) run twice more: "icons take two cells, powerline symbols one" and "both take two cells" | everyone | Read the code: the tests |
| E5-12 | E5 | The tests above measure the whole screen with each popup overlaid; an app not on the library also measures each kind of popup's bare box (with the library, the bare boxes are the library's to test, E8) | everyone | Read the code: the tests |
| E5-13 | E5 | The edge cases of the tests above include the popup wider than the screen, taller than it and larger both ways, and sizes below L1's minimum size all the way down to 1×1 (e.g. 80×5, 1×1): no crash, and the name and the hint drawn | everyone | Read the code: the tests |
| E6-1 | E6 | A single static binary built with goreleaser | everyone | Read the file: `.goreleaser.yaml` (`CGO_ENABLED=0`); what is released is a single executable |
| E6-2 | E6 | There are `install.sh` and `uninstall.sh`, installing and removing with `curl \| sh`, with no sudo | everyone | Install and then remove with the README's commands: no sudo needed |
| E6-3 | E6 | Also published to a Homebrew tap: a family member to `vulcanshen/homebrew-tap`, an app made by tdp to its own tap | has released | The tap has a formula for this app's latest version |
| E6-4 | E6 | There are screen tests across sizes: with its own layout and the popups it opens, at several terminal sizes, every line is exactly the terminal width | everyone | Read the code: the tests |
| E6-5 | E6 | A test keeps the program's copy for the splash (a copy of the file under `internal/`, or the cells written into the code) identical to `docs/icon.svg` | everyone | Read the code: a test compares the two |
| E6-6 | E6 | Demo gifs are recorded with VHS, the scripts in `.local/demos/` | everyone | Read the files: `.local/demos/` has the tapes |
| E7-1 | E7 | There are a `README.md` (English) and a `README-zh_TW.md` (Traditional Chinese) | everyone | Read the files |
| E7-2 | E7 | The two READMEs stay in step | everyone | Read the files: compare the two section by section |
| E7-3 | E7 | The README covers only what users need to know | everyone | Read both READMEs: every section is something users need to know to use the tool |
| E7-4 | E7 | README section 1: title, badges, language switch (`English · 繁體中文`) | everyone | Read the opening of both READMEs |
| E7-5 | E7 | README section 2: a one-line positioning plus a paragraph on what it can do | everyone | Read both READMEs |
| E7-6 | E7 | README section 3 holds one representative demo gif, and only one | everyone | Read section 3 of both READMEs and count the gifs |
| E7-7 | E7 | README section 4: features, saying what users get, not how it is done | everyone | Read the features section of both READMEs |
| E7-8 | E7 | README section 5: installation, giving the prerequisites, how to install, what happens on first launch, and removal | everyone | Read the installation section of both READMEs: all four are there |
| E7-9 | E7 | README section 6: quick start | everyone | Read both READMEs |
| E7-10 | E7 | README section 7: usage and keys | everyone | Read both READMEs |
| E7-11 | E7 | README section 8: configuration and where data is stored | everyone | Read both READMEs |
| E7-12 | E7 | README section 9: limitations, written in the user's language | everyone | Read the limitations section of both READMEs |
| E7-13 | E7 | README section 10: related links, with the CHANGELOG | everyone | Read the related links of both READMEs |
| E7-14 | E7 | README section 11: terminu family — a family member says it follows terminu design and lists the other family members; an app made by tdp says it is made by terminu design, with a link, and lists no family members | everyone | Read both READMEs |
| E7-15 | E7 | README section 12: License | everyone | Read both READMEs |
| E7-16 | E7 | The README has all 12 sections, in the order 1–12 | everyone | Read the order of the sections in both READMEs |
| E7-17 | E7 | The README has no "status" section with a hard-coded version number | everyone | Read both READMEs |
| E7-18 | E7 | The README's settings section names the shared config keys of E3 the app uses, and their defaults | stores settings or data | Read the settings section of both READMEs |
| E7-19 | E7 | Where the README talks about the icon width, it names `<APP>__ICON_WIDTH`, `TERMINU__ICON_WIDTH`, `<APP>__POWERLINE_WIDTH` and `TERMINU__POWERLINE_WIDTH` | everyone | Read where both READMEs talk about the Nerd Font or the icon width |
| E7-20 | E7 | The README says the `TERMINU__` ones are shared by the whole family: set once and every family app reads them; inside a family app's PTY the outer app sets them | everyone | Read the same place in both READMEs |
| E7-21 | E7 | The README gives no font as an example of "always two cells" | everyone | Read where both READMEs talk about the icon width |
| E7-38 | E7 | What belongs to one of the 12 sections goes in that section as a subsection (e.g. updating goes under installation, beside removing) | everyone | Read the sections and subsections of both READMEs |
| E7-39 | E7 | Sections the app adds come only between section 4 (features) and section 9 (limits), after the section they relate to most; nothing comes between sections 1–3 or 10–12 | everyone | Read the order of the sections in both READMEs |
| E7-40 | E7 | A troubleshooting section, if any, comes right after "usage and keys" | everyone | Read both READMEs (an app with no troubleshooting section never has this case) |

## components (README)

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| components-1 | components.2 | Two cells between a label and its value (the statusbar's `label: value` is the exception, see components-25) | everyone | Count the spaces between label and value in forms and one-value-per-row panels |
| components-2 | components.2 | Two cells between the columns of a table | header | Count the spaces between columns in a list's header and rows |
| components-3 | components.2 | Two cells between items side by side | everyone | Count the spaces between items side by side (the statusbar's groups, chips, buttons side by side…) |
| components-4 | components.2 | One cell between a glyph and the text after it | everyone | Count the spaces after glyphs such as those of popup titles, menu section titles and marked rows |
| components-5 | components.3 | Text that wraps (a textarea, a viewer, a confirm, a note, a toast, an error popup, an empty-state sentence, the splash when too narrow) breaks between words: when the next word does not fit on the row, the whole word goes to the next row; what does not fit wraps, it is not cut | everyone | Put English text wider than the frame in a textarea, a viewer, a confirm, a toast and an error popup, narrow the terminal and press `V`; check that no English word is cut |
| components-6 | components.3 | A break may fall between any two wide characters (two cells, e.g. Chinese, Japanese) and between a wide character and the character before or after it, so a row is filled before going on | everyone | Put Chinese text, or Chinese mixed with English, wider than the frame; check that every row is filled before the next begins |
| components-7 | components.3 | Only a word wider than a row on its own (e.g. a long URL) is cut by cells; when the row already has text before it, it starts a new row first and is cut there | everyone | Put a URL wider than the frame after some text; check that it starts on a new row and is cut by cells into several pieces |
| components-8 | components.3 | When cutting by cells, a wide character is never cut in half: when a row has one cell left, that wide character goes whole to the next row | everyone | Put a long string containing Chinese; check that no row ends in half a wide character and the frame line is not skewed |
| components-9 | components.4 | A panel's `[N] label` capsule is uppercase | everyone | Look at the capsule at the top left of each panel |
| components-10 | components.4 | A panel's tabs are uppercase | panel tab | Look at each tab on the top border of a panel with tabs |
| components-11 | components.4 | Screen chips are uppercase | several screens | Look at each chip on the top row |
| components-12 | components.4 | Popup titles are uppercase | everyone | Open several kinds of popup and look at the text of the title capsule |
| components-13 | components.4 | Table headers are uppercase | header or one value per row | Look at the headers of lists and one-value-per-row panels |
| components-14 | components.4 | Group titles in lists are uppercase | grouped list | Look at each group title of a grouped list |
| components-15 | components.4 | The labels of a panel with one value per row are uppercase | one value per row | Look at the label column of a panel such as settings |
| components-16 | components.4 | Values keep their case (a color picker's hex always in upper case is how colours are written, not a change of value) | everyone | Check that values in forms and one-value-per-row panels keep their original case |
| components-17 | components.4 | Menu labels and descriptions keep their case | everyone | Press `Space`; check that no row's label or description is turned uppercase |
| components-18 | components.4 | The descriptions in hints and the footer keep their case | everyone | Look at the text after the colons in the footer and bottom-border hints |
| components-19 | components.4 | Mode names keep their case | mode | Enter a mode and look at the mode name at the right of the top border (`Drag`, not `DRAG`) |
| components-20 | components.4 | The app's own content (the statusbar, the data in lists) keeps its case | everyone | Check that the statusbar and the data in lists are as they are |
| components-21 | components.4 | Names and paths in a title keep their case (`EDIT: filu`, `IDENTITY FILE · ~/.ssh`) | everyone | Open a popup that acts on one thing; check that the name is not turned uppercase |
| components-22 | components.6 | A component's look is picked only from the options the components list, never invented inside the app | everyone | Compare against the options each component lists; check that the app always uses one of them |
| components-23 | components.3 | When a word fills a row exactly and a space follows, that space is drawn in the next row's first cell | textarea or viewer | Type in a textarea so that a word fills a row exactly, then a space; check that the space starts the next row and the text cursor can stop on it |
| components-24 | components.3 | Text that is only shown (a confirm, a note, a toast, an error popup, an empty state, the splash) does not draw the space it breaks at: the next row does not start with a blank cell | everyone | Make the text of a toast, a confirm or a too-narrow splash wrap right after a word; check that the next row starts with no blank and stays centred |
| components-25 | components.2 | A statusbar group is written `label: value`, one space after the colon; two cells between groups, with no separator symbol | statusbar | Look at each statusbar group and between groups |
| components-26 | components.4 | A name in a panel title keeps its case (`[2] PODS: nginx-7d4f`), and a label that is all name keeps it too (`[1] prod-web-01`) | everyone | Look at the capsules of panels whose label holds a name |
| components-27 | components.5 | In names and short text (values on forms and panels, list cells, menus, popup titles, toasts, confirms, error popups, options, explanation rows, empty states, the statusbar, tab names, finder items), every control character, a Tab, a `\n` and the ESC of a colour code included, is drawn by name in red; never dropped, turned into spaces or sent to the terminal as it is | everyone | Give a name that shows in these places (e.g. a file name, a web page title) a Tab or `\x1b[31m` and look at the list, the menu and the confirm; or read the code |
| components-28 | components.5 | A log on a panel is drawn as a terminal would draw it: `\n` is a line break, a Tab is spaces, colour codes colour the text, a `\r` within a line keeps only the last state, and any other control character or sequence that is not a colour code is drawn by name in red | streaming content | Feed the log a coloured line, a line `10%\r100%` and a line holding `\x1b[2J`, and look at the log panel |
| components-29 | components.5 | In a list column the app marks as "a line of text" (a line of source code or of a log), a Tab is drawn as `input_tab_width` spaces and other control characters stay red names | everyone | Put a line holding a Tab in that column and look at the indent; read the code: which columns are marked |
| components-30 | components.5 | The app's own names and short text carry no line breaks: walked with ordinary data (no tricky values), the screen shows no red `\n` | everyone | Walk every place that shows a message (error popup, toast, confirm) with ordinary data; or read the code: no `\n` in the app's strings |
| components-31 | components.5 | An error popup's message, a toast or a confirm's content with several rows: each starts a row of its own and wraps, with no blank row between them | everyone | Give a message two rows and look at the screen |
| components-32 | components.5 | Several lines from outside are not put whole into short text: the line saying why goes there, the whole into the App Log | everyone | Make an outside program fail with several lines of error; look at the toast or error popup and the App Log |

## color

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| color-1 | color.1 | Interface elements take only the colour codes of color (catppuccin-mocha) and the layer colours derived from the anchors; no colour is picked for a single element | everyone | Read the code: the colours of interface elements all refer to the colour code table and the layer colours; every interface colour on screen matches a code in the table |
| color-2 | color.1 | Each colour stands for one meaning; no other meaning uses the same colour | everyone | Compare each interface element with the colour code table (e.g. popup frames are not Lavender) |
| color-3 | color.1、color.3 | A layer-K popup's frame and title take the layer colour of layer K: the bottom popup is layer 1, layers 1, 2 and 3 are `#A4C0FA` `#94C3F5` `#84C5F1`, layer 4 and above stay at `#74c7ec`; the error popup is the exception, in Red | everyone | Open popups one on top of another (up to layer 5) and measure the colour of each layer's frame and title capsule |
| color-4 | color.1 | Errors in Red and warnings in Peach are the same colour on every layer, not changing with the layer | everyone | Bring up an error or a warning once in a layer-1 popup and once in a layer-2 popup, and compare the colours |
| color-5 | color.1 | Bold is used only for text on the cursor, popup titles, text in selected capsules, mode names, the loading icon after a popup title, the splash's name, and the app's name in the centre when the screen is below the minimum size | everyone | Look across the screens: headers, group titles, labels, hints, the footer, unselected capsules and the loading icon on a panel's top border are not bold |
| color-6 | color.2 | Keys in a popup's bottom-border hint are Blue (`#89b4fa`), the colon and description Overlay0 (`#6c7086`) | everyone | Open any popup and look at the hint on its bottom border |
| color-7 | color.2 | Disabled rows, labels and options are Surface2 (`#585b70`) | disabled | Make an action or option unavailable for now and look at its colour |
| color-8 | color.2 | The cursor block in a popup has the layer colour as its background, text Base (`#1e1e2e`) bold; the text's original colour is not kept | everyone | Press `Space` and look at the menu's cursor row |
| color-9 | color.2 | A panel's location row (the breadcrumbs) is Lavender | location row | Look at the location row |
| color-10 | color.2 | Live sessions are Green | PTY | Look at how a live session is shown |
| color-11 | color.2 | Work in progress and progress bars are Green (a single-screen app writes it in the work's own row) | long task | Start a long task and look at the progress bar and how the task is shown |
| color-12 | color.2 | What completed successfully is Green: a Success toast's text | toast | Complete an action and look at the Success toast's text |
| color-13 | color.2 | A mode's frame is Yellow (`#f9e2af`) | mode | Enter a mode and look at the frame's colour |
| color-14 | color.2 | The `\|` between keys (`j\|k`) is Overlay0, not the key colour | everyone | Look at a pair containing `\|` in the footer or a hint |
| color-15 | color.2 | An unfocused button (in a form's action area, a color picker's `Choose`) has a background too: Surface1, its text in Text | form or color picker | Look at an unfocused button in a form's action area |
| color-16 | color.2 | Cells whose content is a colour (the `███` of a colour value) keep their own colour on a cursor block, while the other text on the block still turns Base | color picker | Move the cursor to a colour value's row; check that the `███` keeps its colour and the other text is Base |
| color-17 | color.2 | The screen's background is not painted: cells with no background of their own are left to the terminal's own background | everyone | Set the terminal's background to a colour other than Base; check that the screen is not painted Base |
| color-18 | color.3 | A closing popup does not count toward K: when a target opens while its source closes, the target takes the layer colour of the layer it ends up on from its first frame, and does not change colour when the source is gone | everyone | Open a target from a source that is cleared, and look at the target's frame colour frame by frame |
| color-19 | color.4 | The dimming formula is `dim(c) = c × 0.45 + t × 0.55` (t `#0c0c13`, the step after Crust), each channel rounded half up (.5 goes up) | everyone | Open a popup and measure the colours beneath (e.g. Blue `#89b4fa` dims to `(68,88,123)`) |
| color-20 | color.4 | 256-colour codes 16–255 are turned into RGB by their standard values before dimming | everyone | Read the code: 256 colours are turned into RGB by the standard values |
| color-21 | color.4 | The 16 colours (0–15) are turned into RGB by the terminal's palette, asked with OSC 4 at startup (at the same time as the icon-width probe of Rules E5) | everyone | Read the code: the OSC 4 queries are sent at startup; in a terminal with a changed palette, check that 16-colour content keeps its hue when dimmed |
| color-22 | color.4 | With no answer about the palette, the xterm defaults are used | everyone | Read the code: the 16-colour values used when there is no answer are the xterm defaults |
| color-23 | color.4 | Dimming never lightens a colour: each channel takes the smaller of its original and dimmed value | everyone | Put text in `#000000` beneath and open a popup; check that it keeps its original colour |
| color-24 | color.4 | Dimmed output is always 24-bit (`38;2;…` / `48;2;…`) | everyone | Capture the output when a popup opens and look at the dimmed colour codes |
| color-25 | color.4 | Text with no foreground of its own gets `dim(Text #cdd6f4)` when dimmed | everyone | Capture the output and look at the dimmed colour code of text that had no foreground colour |
| color-26 | color.4 | Dimming leaves bold, reverse, cursor movement, the text and the layout untouched | everyone | Compare the text, positions and bold of the screen beneath before and after opening a popup |

## layout/screen

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| screen-1 | screen.1 | The top row of a multi-screen app is the screen chip row | several screens | Look at the top row of the screen |
| screen-2 | screen.1 | All the remaining height between the top row (in an app with several screens, the chip row and the divider under it, two rows) and the footer is the panel area | everyone | Check that the panels run from below the top row (below the divider under the chip row in an app with several screens; from the first row in a single-screen app with no top row) all the way to above the footer |
| screen-3 | screen.1 | The bottom row is the footer, one row only | everyone | Look at the bottom row of the screen |
| screen-4 | screen.2 | Keys in the footer are Blue, the colon and description Overlay0 | everyone | Look at the footer's colours |
| screen-5 | screen.2 | When the footer is too narrow, whole pairs are dropped from the end | everyone | Narrow the terminal; check that the footer loses whole `key:description` pairs from the end |
| screen-6 | screen.2 | On a screen with several panels, the footer is `Space:menu ?:help !:log Tab\|1–N:panels q:quit` | several panels | Look at the footer on a screen with several panels |
| screen-7 | screen.2 | On a screen with only one panel, the footer is `Space:menu ?:help !:log q:quit` | everyone | Look at the footer on a screen with only one panel (in a multi-screen app, on each screen) |
| screen-8 | screen.2 | With a mode on a panel, the footer is `Space:menu ?:help`, the mode's own keys, and last `Esc:<verb for leaving>` | mode (on a panel) | Enter a mode and look at the footer |
| screen-9 | screen.2 | While typing in a panel filter, the footer is `Enter\|Tab:list Esc:clear` | panel filter | Press `/` and look at the footer while typing |
| screen-10 | screen.2 | With the focus on a PTY in a panel, the footer has the exit key plus the keys the app keeps (in an interactive terminal also `Alt-v` and `PgUp`); no `?` or `Space` | PTY | Enter the PTY; check that the footer's first pair is the exit key |
| screen-11 | screen.2 | While a popup is open, the footer is as for the screen underneath, its words unchanged (a terminal popup is the exception: the footer is not drawn, terminal-13) | everyone | Compare the footer's words before and after opening a popup |
| screen-12 | screen.3 | One capsule per screen, drawn as the capsule chain | several screens | Look at the top row |
| screen-13 | screen.3 | The selected screen is filled with Blue, its text Base bold | several screens | Look at the current screen's chip |
| screen-14 | screen.3 | The unselected screens are filled with Mantle, their text Blue, not bold | several screens | Look at the other screens' chips |
| screen-15 | screen.3、screen.4 | A multi-screen app puts the statusbar's content on the right of the chip row, not on a row of its own | several screens + statusbar | Look at the right of the chip row |
| screen-16 | screen.3 | Below the chip row runs a full-width heavy line `━` in Overlay0 | several screens | Look at the second row |
| screen-17 | screen.3 | During a long task the separator fills with Green from the left as a progress bar | several screens + long task | Start a long task and look at the line below the chip row |
| screen-18 | screen.4 | A single-screen app puts the statusbar on the top row | statusbar | Look at the top row |
| screen-19 | screen.4 | Ordinary text on the statusbar is Overlay0 | statusbar | Look at the statusbar's colours |
| screen-20 | screen.4 | The "where you are now" values on the statusbar are Lavender | statusbar | Look at the values on the statusbar that show the current position |
| screen-21 | screen.4 | The count of errors on the statusbar is Red | statusbar | Cause an error and look at the error count on the statusbar |
| screen-22 | screen.4 | The count of warnings on the statusbar is Peach | statusbar | Cause a warning and look at the warning count on the statusbar |
| screen-23 | screen.4 | When the statusbar does not fit it is truncated, never wrapped | statusbar | Narrow the terminal; check that the statusbar stays one row |
| screen-24 | screen.5 | When not all panels fit, only the focused panel is drawn, at full width | several panels | Narrow the terminal below the narrow-width threshold (but above the minimum size) |
| screen-25 | screen.5 | At narrow widths `Tab` changes panels as usual, showing one at a time | several panels | Press `Tab` at a narrow width |
| screen-26 | screen.5 | The narrow-width threshold is not above 80 columns | several panels | Set the terminal to 80 columns; check that the panels are side by side as usual |
| screen-27 | screen.8 | An empty state is one fact plus a hint naming the key | everyone | Leave a panel with no data and look at its middle |
| screen-28 | screen.8 | An empty state is centred | everyone | As above, look at where the two lines are |
| screen-29 | screen.8 | Both lines of an empty state are Overlay0 | everyone | As above, look at the colours |
| screen-30 | screen.8 (diagram) | One blank row between the fact and the hint | everyone | Leave a panel with no data and look between the fact and the hint |
| screen-31 | screen.2 | While typing in a panel filter with no results, the footer is `Tab:list Esc:clear` (no `Enter`) | panel filter | Press `/` and type something that matches nothing; look at the footer |
| screen-32 | screen.3 | In a single-screen app, a long task's progress is written in that task's own row | long task | Start a long task in a single-screen app and look at the task's row |
| screen-33 | screen.6 | Zooming a panel, with no way of its own set, follows the default (only the focused panel drawn, filling the panel area; the panel reached with `Tab` or a digit is zoomed too; pressing the zoom key again restores) | zoom | Zoom, press `Tab` and a digit, then press the zoom key |
| screen-34 | screen.8 | An empty-state sentence too long for the panel wraps between words, each row centred, still one cell from the frame on each side; never cut | everyone | Narrow a panel with no data and look at the two sentences |
| screen-35 | screen.2 | With errors in the App Log not seen yet, the footer's `!:log` becomes `!:N errors` (Red), with only warnings `!:N warning` (Peach); after the App Log is opened it is `!:log` again | everyone | Cause an error and look at the footer; press `!`, then look again |

## layout/panel

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| panel-1 | panel.1 | A focused panel's frame is a Blue heavy line `┏━┓` | everyone | Look at the frame line of the focused panel |
| panel-2 | panel.1 | An unfocused panel's frame is a Surface2 light square line `┌─┐` | several panels | Press `Tab` to change panels and look at the frame of the one left |
| panel-3 | panel.1 | Each panel has a `[N] label` capsule at the left of its top border, right after the top-left corner | everyone | Look at the top-left corner of each panel; there is no line between the capsule and the corner |
| panel-4 | panel.1 | While a panel is loading, the loading icon sits after the whole capsule chain (tabs included), with one space on each side | loading | Reload a panel and look after the capsule chain on its top border |
| panel-5 | panel.3 | The mode name sits at the right of the top border of the frame the mode lives in (panel or popup), set between two border junctions | mode | Enter a mode and look at the right of the top border |
| panel-6 | panel.3 (diagram) | The mode name sits right against the two junctions, with no space between (`┫Drag┣`) | mode | Enter a mode and look between the junctions and the mode name |
| panel-7 | panel.3 | The mode name's junctions take the frame's colour | mode | Enter a mode and compare the colours of the junctions and the frame line |
| panel-8 | panel.3 | The junctions follow the frame's line style: `┫` `┣` on a heavy frame (a focused panel, a popup), `┤` `├` on a light one (an unfocused panel) | mode (on a panel) + several panels | In a mode, press `Tab` to move away; check that the junctions change from heavy to light |
| panel-9 | panel.3 | The mode name is bold in the mode colour | mode | Enter a mode and look at the mode name's colour and weight |
| panel-10 | panel.3 | The mode name is one word if possible | mode | Look at every mode name |
| panel-11 | panel.3 | When space runs out, the title is clipped first and the mode name stays | mode | In a mode, narrow the terminal; check that the title is clipped first and the mode name is still there |
| panel-12 | panel.3 | In a mode, the capsule turns the mode colour along with the frame | mode | Enter a mode and look at the capsule's colour |
| panel-13 | panel.1 | Every panel has a hint at the left of its bottom border; a panel with no key that does anything (e.g. a read-only panel, or an emptied list with no key for the whole panel) writes no hint, leaving only the border | everyone | Look at the bottom left of each panel; empty a list and look at a panel with no key that does anything |
| panel-14 | panel.1 | No hint while the focus is on a panel filter's typing row; it comes back when the focus returns to the list | panel filter | Press `/` and look at the bottom border, then press `Enter` to go back to the list and look again |
| panel-15 | panel.1 | No hint while the focus is in a PTY in the panel; it comes back on leaving the PTY | PTY | Enter the PTY and look at the bottom border, then press the exit key to leave and look again |
| panel-16 | panel.1 | Text on the frame keeps one line segment away from the corner: the hint starts with `┗━ `, the scroll position ends with ` ━┛`, the mode name is followed by `┣━┓`; only the `[N] label` capsule sits right after the top-left corner | everyone | Look at a panel's four corners |
| panel-17 | panel.1 | The hint is ordered like a popup's hint: `Enter` first, `h\|l:tab` next when there are tabs, then this panel's own keys | everyone | Look at each panel's bottom-border hint; `Enter` comes first (e.g. `Enter:logs .:helm`) |
| panel-18 | panel.1 | The hint holds this panel's own keys: what `Enter` does here, the common hotkeys | everyone | Look at each panel's hint |
| panel-19 | panel.1 | The hint leaves out movement keys, except `h\|l:tab` with two tabs or more | everyone | Check that no panel's hint has keys such as `j\|k`; a panel with tabs has `h\|l:tab` |
| panel-20 | panel.1 | The hint leaves out the core keys the footer already has | everyone | Compare the hint with the footer; no core key appears in both |
| panel-21 | panel.1 | When focused, the hint's keys are Blue and its descriptions Overlay0 | everyone | Look at the focused panel's hint |
| panel-22 | panel.1 | Unfocused, the hint stays and is dimmed with the panel | several panels | Press `Tab` to move away; check that the panel's hint is still there, dimmed |
| panel-23 | panel.1 | When the hint does not fit, whole pairs are dropped from the end, and the scroll position stays | everyone | Narrow the terminal; check that the hint loses whole pairs from the end and `N of M` is still there |
| panel-24 | panel.1 (diagram) | A panel's content is one cell from the left frame (a PTY is the exception: it sits against the frame) | everyone | Look between each panel's first character and its left frame |
| panel-25 | panel.1 (diagram) | A panel's content has no blank row above or below; the first row is right below the top border | everyone | Check that the row right below each panel's top border is content |
| panel-26 | panel.4 | The capsule chain's ends are slanted: U+E0BA on the left, U+E0B0 on the right | everyone | Look at the ends of a panel's title capsule; read the code to check the code points |
| panel-27 | panel.4 | A selected part is filled with the chain's colour, text Base bold | everyone | Look at a panel's `[N] label` capsule and the current tab |
| panel-28 | panel.4 | On a panel the chain's colour is the border colour, changing with focus, unfocus and mode | everyone | Press `Tab` to change panels and enter a mode; check that the capsule's colour follows the frame line |
| panel-29 | panel.4 | For the tabs after a popup title, the chain's colour is the layer colour | popup tab | Open a popup with tabs and look at the selected tab |
| panel-30 | panel.4 | The `[N] label` capsule counts as selected | everyone | Check that the `[N] label` capsule is filled |
| panel-31 | panel.4 | An unselected part is filled with Mantle, its text in the chain's colour, not bold | several screens or panel tab or popup tab | Look at an unselected tab; set the terminal's background to a colour other than Base and check that the unselected parts are still Mantle |
| panel-32 | panel.4 | Joins are always slants: a solid slant where the colour changes, a thin slant between two unselected parts | several screens or panel tab | Change tabs and look at the shape of the joins; read the code to check the code points |
| panel-33 | panel.4 | The join from selected to unselected is U+E0BC, foreground the chain's colour, background Mantle | several screens or panel tab | Look at the join on the right of the selected part |
| panel-34 | panel.4 | The join from unselected to selected is U+E0BA, foreground the chain's colour, background Mantle | several screens or panel tab | Look at the join on the left of the selected part |
| panel-35 | panel.4 | The join between two unselected parts is U+E0BB, foreground the chain's colour, background Mantle | several screens or panel tab | Look between two unselected parts side by side |
| panel-36 | panel.4 | Each end's foreground is the fill of the part beside it: the chain's colour beside a selected part, Mantle beside an unselected one; no background is painted outside | everyone | Look at the start and end of the capsule chain, then change tabs so that the last part is unselected; set the terminal's background to a colour other than Base or Mantle and check that there is no block outside the ends |
| panel-37 | panel.4 | Every end and join takes the width of one powerline symbol, so changing the selected part shifts no text | several screens or panel tab | Change tabs; check that no part's text moves |
| panel-137 | panel.4 | On an unfocused panel the unselected parts stay Mantle (the chain's colour turns to the unfocused border colour); covered, they dim with the whole screen and Mantle becomes Crust `#11111b` | several screens or panel tab or popup tab | Press `Tab` to another panel and check that the unselected parts on the unfocused panel keep their background; open a popup and measure the background of the unselected parts beneath |
| panel-138 | panel.9 | The compare key on a row enters a K11 mode and makes that row the anchor; the frame and mode name are Yellow | compare mode | Press the compare key; look at the frame and the mode name |
| panel-139 | panel.9 | Only text or content shown as text is compared; an item that is not `text` has no compare action | compare mode | Open the Space menu on an item that is not text; there is no compare |
| panel-140 | panel.9 | In the mode, the compare key and `Enter` are disabled while the cursor rests on the anchor or on an item that cannot be compared | compare mode | On the anchor press `?`: the compare key is in the disabled colour; pressing it does nothing |
| panel-141 | panel.9 | The anchor row is all Yellow, Base text, not bold, no arrow on the right; with the cursor on it, the cursor is drawn | compare mode | After entering, move the cursor away and look at the anchor, then move back |
| panel-142 | panel.9 | The compare key or `Enter` opens the comparison with the anchor; closing it goes back to the mode with the anchor kept | compare mode | Compare once, close it; the mode and the anchor are still there |
| panel-143 | panel.9 | When the two are identical nothing opens: an Info toast, and the mode stays | compare mode | Compare two identical items |
| panel-144 | panel.9 | `Esc` leaves the mode and drops the anchor; `Tab` and the number keys are paused | compare mode | In the mode press `Tab`, then `Esc` |
| panel-145 | panel.9 | When the anchor is gone the mode is left with a Warning toast | compare mode | In the mode, have the anchor's item deleted |
| panel-146 | panel.3 | Entering a mode, the mode name opens from its middle: the junctions start side by side and move apart, the name showing from its middle; leaving plays it backwards; the junctions take the first frame, then one more letter every 32ms frame | mode | Enter and leave a mode and watch the right of the top border |
| panel-147 | panel.3 | Switched again while the mode name is opening or closing, it turns around from where it is, without starting over | mode | Enter and leave a mode quickly several times (e.g. `D` `Esc` `D`) |
| panel-148 | panel.3 | The mode takes effect at once and the frame turns its colour at once; keys are taken while the mode name animates | mode | Enter a mode and press one of its keys at once; watch the frame colour |
| panel-149 | panel.3 | A mode with layers adds each layer to its name after a `>`, with no spaces (e.g. `Visual>select`) | mode | Press `v` a second time in a viewer's selection mode and look at the top right |
| panel-150 | panel.3 | A layer added grows from the tail, one letter every 32ms frame, the right end staying; going back a layer takes it off from the tail; switched again halfway it turns around; leaving the whole mode from a layer closes the whole tag from its middle | mode | In the selection mode press `v`, `Esc`, then `v`, `y`, watching the top right |
| panel-151 | panel.2 | When the cursor's row in a focused list stands for another panel on screen, that panel's frame is a Lavender light square line, not focused, its capsule chain turning with it | pointed panel | Move along the list and look at the matching panel's frame |
| panel-152 | panel.2 | The cursor moving to another row points at that row's panel; when that row's panel is not on screen, no panel is pointed | pointed panel | Move to a row whose panel is not on screen |
| panel-153 | panel.2 | It points only while the list has the focus: with the focus on the pointed panel it is drawn as focused, with the focus on another panel none is pointed; under a popup it dims with the rest | pointed panel | Switch panels with `Tab`; open a popup |
| panel-38 | panel.4 | No space before or after the text inside a capsule (`[1] TABS`) | everyone | Look between a capsule's text and its ends |
| panel-39 | panel.4 | On a panel with tabs, `[N]` is a part of its own and always selected | panel tab | Change to the second tab; check that `[N]` is still filled |
| panel-40 | panel.4 | Each tab after `[N]` is a part, and only the current tab is selected | panel tab | Change tabs; check that only the current tab is filled |
| panel-41 | panel.4 | A panel with tabs has no other name: the first tab's name is the label | panel tab | Check that the top border of a panel with tabs has no separate label |
| panel-42 | panel.4 | On the first tab, blank space joins `[N]` and the first tab, with no seam drawn; that space takes the width of a powerline symbol, as a seam does (two cells when a powerline symbol takes two) | panel tab | Change back to the first tab and look between `[N]` and the tab name; start with `TERMINU__POWERLINE_WIDTH=2` and check that the text does not shift when changing tabs |
| panel-43 | panel.4 | When it does not fit, the unselected ones first shrink to their first character or glyph | several screens or panel tab | Narrow the terminal and look at the unselected parts |
| panel-44 | panel.4 | If it still does not fit, unselected ones are folded away from the end and a `…` is drawn instead | several screens or panel tab | Narrow it further and look at the end of the chain |
| panel-45 | panel.4 | When it does not fit, the selected one always stays | several screens or panel tab | Narrow it as far as it goes; check that the selected part is still there |
| panel-46 | panel.4 | The capsule chain never stretches the frame wider | everyone | Narrow the terminal; check that the frame does not go past the terminal's width |
| panel-47 | panel.5 | The cursor is a Subtext1 background, Base bold | everyone | Look at the cursor row on a list panel |
| panel-48 | panel.5 | The cursor spans the whole inner width, from frame to frame | everyone | Look at the left and right ends of the cursor block |
| panel-49 | panel.5 | The whole cursor row is Base text; the columns' own colours are not kept | everyone | Move the cursor to a row with coloured columns |
| panel-50 | panel.5 | The cursor's right padding holds U+E0B0 in Subtext1 | everyone | Look at the far right of the cursor row |
| panel-51 | panel.5 | Every row's right padding is as wide as the arrow (two cells when a powerline symbol takes two), so the arrow fits and the text does not move | everyone | Start the app with `TERMINU__POWERLINE_WIDTH=2` and look at the right padding and the arrow on every row |
| panel-52 | panel.5 | An ordinary list with several columns always has a header (when the list is empty the header goes with it into the empty state, panel-132) | everyone | Check that every list panel with several columns has a header row at the top |
| panel-53 | panel.5 | An ordinary list's header is Blue | header | Look at the list's header |
| panel-54 | panel.5、panel.12 | The header is fixed at the top and never scrolled | header or one value per row | Scroll down; check that the header stays at the top |
| panel-55 | panel.5 (diagram) | The header's text lines up with the items' text (after the mark column, when there is one) | header | Look at where the header's first column and each row's first column start |
| panel-56 | panel.5 (diagram) | The data follow right below the header, with no blank row and no separator | header | Look at the row below the header |
| panel-57 | panel.5 | Number columns align right, text columns align left | header | Look at how number columns and text columns are aligned |
| panel-58 | panel.5 | Number columns sort by value (`9` before `10`), text columns sort as text | sorting | Sort on a number column; check that `9` comes before `10` |
| panel-59 | panel.6 | A column being sorted on gets U+F160 (ascending) or U+F161 (descending) after its title | sorting | Sort once ascending and once descending, and look at the glyph after the column name |
| panel-60 | panel.6 | When several columns sort together, the rank goes before the arrow (`Name (2)`) | sorting | Sort on two columns and look at the second column's name |
| panel-61 | panel.5 | When the content does not fit, the right of the bottom border reads `N of M` (which entry the cursor is on, how many in all) | everyone | Make the list longer than the panel, move the cursor and look at the bottom right |
| panel-62 | panel.5 | The scroll position is in the border colour | everyone | Check that `N of M` is the same colour as the frame line |
| panel-63 | panel.5 | No scroll position when everything fits | everyone | Make the list short enough to fit; check that there is no `N of M` at the bottom right |
| panel-64 | panel.5 | A panel without a cursor (a preview, a log) shows the visible lines, `N-M of T` | panel without a cursor | Look at the bottom right of a preview or log panel |
| panel-65 | panel.7 | Every row keeps a one-cell mark column at its very start | marks | Check that every row keeps one blank cell at its start even when nothing is marked |
| panel-66 | panel.7 | A marked row shows a Green U+F0132 | marks | Mark a row and look at the mark column |
| panel-67 | panel.7 | An unmarked row leaves it blank, the column width always kept, so rows never shift sideways when marked or unmarked | marks | Mark a row, then unmark it; check that the row's text does not move |
| panel-68 | panel.8 | The row held in a Drag is drawn as the cursor, with a Yellow background, Base bold | Drag | Enter the Drag and pick up a row |
| panel-69 | panel.8 | The arrow on the right of the held row is Yellow too | Drag | Pick up a row and look at the far right |
| panel-70 | panel.8 | The held row's mark column shows U+F04E2 | Drag | Pick up a row and look at the mark column |
| panel-71 | panel.8 | Once dropped, the row's own mark comes back | Drag | Mark a row, pick it up and drop it; check that the mark comes back |
| panel-72 | panel.8 | A panel with a Drag keeps the mark column on every row | Drag | Check that every row of a panel with a Drag keeps one blank cell at its start |
| panel-73 | panel.8 | While a row is held, `Enter` drops it | Drag | Pick up a row, move it and press `Enter` |
| panel-74 | panel.5 | Text too long is cut with `…`: at the end by default; at the front for paths, file names and the like whose end matters more; in the middle for values meaningful at both ends (e.g. a pod's name: `demo-app…66-gm72n`); where each column is cut, the app may decide for itself | everyone | Look at columns with long names |
| panel-75 | panel.15 | While the panel has no content yet, one loading line is written in the middle in the empty-state look | loading | Load a panel for the first time and look at its middle |
| panel-76 | panel.15 | On reload, the old content stays and is not cleared | loading | Reload; check that the old content is still there |
| panel-77 | panel.15 | When a panel cannot read its content (errors, a lost connection, no permission), two centred lines in the empty-state look, the fact in Red | everyone | Make a panel with no content fail to read and look at the first line in the middle |
| panel-78 | panel.15 | The other line when the content cannot be read is a hint, in Overlay0 | everyone | As above, look at the second line |
| panel-79 | panel.15 | When a load fails and the old content is still there, it stays | loading | With content in place, make a reload fail; check that the content is still there |
| panel-80 | panel.15 | With the old content still there, the error is reported in a toast | loading | As above, check that a toast pops up |
| panel-81 | panel.11 | Each group in a grouped list starts with a group title row | grouped list | Look at a grouped list |
| panel-82 | panel.11 | Group titles are Blue | grouped list | Look at the group titles' colour |
| panel-83 | panel.11 | Group titles have no glyph | grouped list | Look before the group titles |
| panel-84 | panel.11 | Group titles are one cell from the frame | grouped list | Look between a group title and the left frame |
| panel-85 | panel.11 | Items are two cells further in than the group title | grouped list | Compare where items and group titles start |
| panel-86 | panel.11 | When a grouped list has a mark column, the mark goes in the items' two extra cells: the mark one cell from the frame, a space, the text three cells from the frame | grouped list + marks | Mark an item in a grouped list and count how many cells the mark and the text are from the left frame |
| panel-87 | panel.11 | When a grouped list has a mark column, a group title row keeps no mark column | grouped list + marks | Check that with a mark column a group title still starts one cell from the frame, as without one |
| panel-88 | panel.11 | The cursor skips group titles: `j\|k` step over them | grouped list | Press `j\|k` past a group title |
| panel-89 | panel.11 | `gg\|G` go to the first and last item | grouped list | Press `gg` and `G`; check that the cursor stops on items |
| panel-90 | panel.11 | The `N of M` scroll position counts items only | grouped list | Check that the total in `N of M` equals the number of items |
| panel-91 | panel.11 | When scrolling puts the cursor on a group's first item, that group's title stays on screen too | grouped list | Make the terminal shorter and scroll to the first item of a group |
| panel-92 | panel.11 | No blank row and no separator between groups | grouped list | Look between two groups |
| panel-93 | panel.11 | A group with no items has no title | grouped list | Filter with the panel filter until a group has no items left; check that its title disappears |
| panel-94 | panel.12 | `Enter` opens the value's input popup | one value per row | Press `Enter` on a value |
| panel-95 | panel.12 | A value takes effect and is saved the moment it is confirmed in the input popup | one value per row | Change a value and confirm it, quit the app right away and reopen it; check that the value is still there |
| panel-96 | panel.12 | A switch or radio option takes effect and is saved the moment it is chosen in place | one value per row | Flip a switch, quit the app right away and reopen it; check that the value is still there |
| panel-97 | panel.12 | There is no action area | one value per row | Check that the panel has no buttons such as submit or cancel |
| panel-98 | panel.12 | There is no "ask first when changed" | one value per row | Change a value and leave the panel; check that nothing asks whether to save |
| panel-99 | panel.12 | The focus block is a Subtext1 background with Base bold text | one value per row | Look at the focused row |
| panel-100 | panel.12 | The focus block's right padding is the arrow | one value per row | Look at the far right of the focused row |
| panel-101 | panel.12 | The focus block runs from the value (from the option, for an option) to the panel's inner right edge | one value per row | Look at the left and right ends of the focus block |
| panel-102 | panel.12 | Labels are Blue normally | one value per row | Look at the label column |
| panel-103 | panel.12 | A label is Red when its value has an error, over any other colour | one value per row | Give a value an error and look at its label |
| panel-104 | panel.12 | The label column is as wide as the longest of the labels and the header's first column name | one value per row | Check that the value column starts two cells after the longest label (or the header's first column name, when that is longer) |
| panel-105 | panel.12 | When a one-value-per-row panel has a header, it takes Overlay0 | one value per row | Look at the header's colour |
| panel-106 | panel.12 (diagram) | When a one-value-per-row panel has a header, its column names line up with the label and value columns below | one value per row | Look at where the header's two column names start |
| panel-107 | panel.13 | When the other panel's cursor moves, the details switch to the new item straight away, with no `Enter` | detail panel | Press `j\|k` on the list and look at the details |
| panel-108 | panel.13 | When the details' label names the item, the label switches too | detail panel | As above, look at the details' capsule |
| panel-109 | panel.13 | As the cursor moves, the focus remains on the panel it was on | detail panel | As above, look at which frame has the focus |
| panel-110 | panel.14 | `/` brings up a typing row at the top of the panel | panel filter | Press `/` on a list |
| panel-111 | panel.14 | When the list has a header, the typing row is above it; with a location row, below that | header + panel filter | Press `/` on a list with a header; check that the typing row appears above the header |
| panel-112 | panel.14 | The panel filter opens no popup | panel filter | Press `/`; check that no popup opens |
| panel-113 | panel.14 | The typing row starts with U+F105, one cell from the frame | panel filter | Press `/` and look at the start of the typing row |
| panel-114 | panel.14 | U+F105 takes the panel's frame colour with the focus on the typing row, Overlay0 on the list | panel filter | Switch between the typing row and the list, and look at the glyph's colour |
| panel-115 | panel.14 | With the focus on the list, the typing row is drawn in Overlay0 | panel filter | Press `Enter` to go to the list and look at the typing row |
| panel-116 | panel.14 (diagram) | The typing row shows the filtered count `matches/total` (`2/5`) on its right, aligned right, one cell from the frame | panel filter | Type, and look at the right of the typing row |
| panel-117 | panel.14 | The count is Overlay0 | panel filter | Look at the count's colour |
| panel-118 | panel.14 (diagram) | The header follows right below the typing row (the list, when there is no header), with no blank row and no separator | panel filter | Look at the row below the typing row |
| panel-119 | panel.14 | `Tab` on the list goes to the next panel | panel filter | After filtering, go to the list and press `Tab` |
| panel-120 | panel.14 | After `Enter` on the list the panel filter does not close: the list keeps its filtered look and works as usual | panel filter | After filtering, go to the list and press `Enter`; check that the typing row and the filter are still there and the list works as usual |
| panel-121 | panel.14 | `/` on the list goes back to the typing row, continuing the old text | panel filter | After filtering, press `/` on the list |
| panel-122 | panel.14 | The filter stays when the focus leaves the panel, whichever way it leaves | panel filter | After filtering, leave with `Tab` and with a digit key, then come back |
| panel-123 | panel.14 | When the focus returns to a panel with a filter, it lands straight on the typing row | panel filter | After filtering, leave and come back; check that the focus is on the typing row |
| panel-124 | panel.1 | When the list has no items (a panel filter matched nothing, or it was empty to begin with), the hint drops `Enter` and the hotkeys on an item, keeping only those on the whole panel | everyone | Filter the list to nothing or empty it; check that the bottom-border hint has no `Enter` and no item hotkeys |
| panel-125 | panel.4 | When the selected segment is too long on its own, its text is cut at the end with `…`; both slants are still drawn, and a stretch of line stays between it and the corner | everyone | Narrow the terminal a lot and look at the capsule of a panel with a long label |
| panel-126 | panel.6 | Sort groups: the groups the app assigns rows to come in the app's order, sorting happens only within a group, and no title is drawn between groups (e.g. directories always before files) | sorting | Change the sorting of a list with groups: the groups keep their order |
| panel-127 | panel.5 | When the columns do not fit, the columns that may be cut short narrow to their least width first; only then do whole columns go: the least important one, by the order the app marks, is taken away (its header too), never the name column | header | Narrow the terminal: long columns are cut short first, then whole columns go, and the name column stays |
| panel-128 | panel.5 | When the terminal grows, the columns taken away come back in order | header | Narrow, then widen again: the columns taken away come back |
| panel-129 | panel.10 | The location row is the first row inside the panel, one cell from the frame; above the header when there is one, and above the panel filter's typing row when that appears; fixed at the top, never scrolled | location row | Look at where the location row is; scroll down, press `/` |
| panel-130 | panel.10 | A location row too long is cut at the front with `…`, keeping the end (where you are now) | location row | Go somewhere deep and look at the start of the location row |
| panel-131 | panel.10 | The location row is display only: it cannot be pressed, the cursor never rests on it, and the scroll position does not count it; it dims with the panel on blur | location row | Walk to the top with `j\|k`: the cursor does not rest on the location row; look at `N of M`; press `Tab` to move away |
| panel-132 | panel.5 | When the list is empty, the empty state takes the whole panel: the header is not drawn either, and the sentences are centred in the whole panel | everyone | Empty a list with a header: the header goes too, and the sentences sit in the middle of the panel |
| panel-133 | panel.5 | The list's order is fixed: the same data comes out in the same order every time it opens or is fetched again; data with no order of its own is sorted by the app first (by name by default, numbers by value) | everyone | Close and reopen, fetch again a few times: the order holds; read the code: data with no order (e.g. a map) is sorted first |
| panel-134 | panel.10 | When the list is empty, the location row stays; only the header and the list give way to the empty state | location row | Empty a list with a location row (e.g. open an empty directory): the location row is still there |
| panel-135 | panel.5 | The columns that may be cut short (names, URLs, a line of text) share the width left and are cut their own way; the other, short columns take their widest value and never shrink | header | Put a very long name in the list: the other columns stay whole and the name is cut short |
| panel-136 | panel.5 | A value in a cell (a file name or a name that came from a file or another program) holding control characters shows them as red escapes, as on the typing row (`\n`, `\t`, `\x1b`): never dropped, turned into spaces or sent to the terminal as they are | everyone | Put an item whose name holds a newline or `\x1b` in a list (e.g. a file name) and look at that cell; or read the code |

## layout/popup

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| popup-1 | popup.1 | A popup is always a heavy line `┏━┓`, also when covered and dimmed | everyone | Stack two popups and look at the frame of the one underneath |
| popup-2 | popup.1 | The title is glyph + text, made into a capsule after `┏━` on the top border | everyone | Look at the top border of any popup |
| popup-3 | popup.1 | The title capsule has rounded ends: U+E0B6 on the left, U+E0B4 on the right | everyone | Look at the ends of the title capsule; read the code to check the code points |
| popup-4 | popup.1 | The title capsule is filled with the layer colour (Red for the error popup), text Base bold | everyone | Look at the title capsule's fill and text |
| popup-5 | popup.1 | The title text says what this popup is for (`RENAME`, `NEW HOST`) | everyone | Open various popups and look at their titles |
| popup-6 | popup.1 | When the title names what the popup acts on, the name follows after `: ` (`EDIT: filu`) | everyone | Open a popup on one thing and look at the title |
| popup-7 | popup.1 | A title too long is cut at the end with `…` | everyone | Open a popup on something with a very long name, or narrow the terminal |
| popup-8 | popup.1 | Tabs after the title are drawn as the capsule chain | popup tab | Open a popup with tabs and look after the title |
| popup-9 | popup.1 | The tabs keep one line segment away from the rounded title (`┏━TITLE━CONSOLE…`) | popup tab | Look between the title capsule and the first tab |
| popup-10 | popup.1 | Hint order: `Enter` first → the `h\|l:tab` that switches tabs → this popup's own keys → the `Tab:…` that switches parts → `Esc` last | everyone | Open various popups and look at the order of their hints |
| popup-11 | popup.1 | The hint leaves out keys that move between items (`j\|k`, `↑\|↓`); with two tabs or more and `h\|l` switching them, `h\|l:tab` is written | everyone | Look at the hints of various popups; open the comparison viewer and find `h\|l:tab` |
| popup-12 | popup.1 | When the hint still does not fit at the widest frame, whole pairs are dropped working back from the one before `Esc`, never cut mid-pair; the final `Esc` always stays | everyone | Narrow the terminal a lot, open a popup at its full width and check that the bottom border keeps `Esc` |
| popup-13 | popup.1 | When pairs are dropped, the scroll position at the right of the bottom border stays | everyone | As above, with content that does not fit either, look at the bottom right |
| popup-14 | popup.1 | Text on the frame keeps one line segment away from the corner: `┏━TITLE`, `┗━ Enter:run`, `4 of 12 ━┛` | everyone | Look at a popup's four corners |
| popup-15 | popup.1 | One blank row above and below the content (viewers too) | everyone | Look at the row below the top border and the row above the bottom border of various popups |
| popup-16 | popup.1 | The content is one cell from the border on the left and right | everyone | Look between the content and the left and right borders |
| popup-17 | popup.1 | A list's cursor runs from frame to frame, covering the left and right padding | everyone | Press `Space` and look at the ends of the cursor block |
| popup-18 | popup.1 | The text on a cursor block still stays one cell from the frame | everyone | As above, look between the text on the block and the left frame |
| popup-19 | popup.1 | The right padding of a cursor across a whole row holds U+E0B0, in the block's colour | everyone | Press `Space` and look at the far right of the cursor row |
| popup-20 | popup.1 | In a popup with a cursor across a whole row (a form's focus block included), every row's right padding is as wide as the arrow (two cells when a powerline symbol takes two) | everyone | Start the app with `TERMINU__POWERLINE_WIDTH=2` and look at the right of every row of a menu and a form |
| popup-21 | popup.1 | Only a cursor across a whole row has the arrow; one-cell cursors (the days, hours and minutes of the datetime picker) do not | everyone | Check that a whole-row cursor has the arrow; with a datetime picker, check that there is no arrow beside the day, hour and minute cursor |
| popup-22 | popup.1 | A horizontal separator does not join the frame, leaving one blank cell at each end | everyone | Press `Space` and look at the ends of the separators between sections |
| popup-23 | popup.1 | A vertical separator is not drawn into the top and bottom padding | everyone | Look at the top and bottom ends of a vertical separator |
| popup-24 | popup.1 | Separators in a popup are Overlay0 | everyone | Look at the separators' colour |
| popup-25 | popup.2 | A popup whose content width is known when it opens is as wide as its widest row + 4 (where the right padding is as wide as the arrow, its real width) | everyone | Measure the frame width of a menu and a confirm |
| popup-26 | popup.2 | A popup with a known content width is at least wide enough for the title | everyone | Open a popup with narrow content and a longer title; check that the title is whole |
| popup-27 | popup.2 | A popup with a known content width is at least wide enough for the hint: the hint's width + 6 (`┗━ ` and ` ━┛`) | everyone | Open a popup with narrow content and a longer hint (e.g. a PIN) and measure the frame width |
| popup-28 | popup.2 | A popup that scrolls is also wide enough for the scroll position at its widest: the hint's width + the scroll position's widest width + 9 (`N of M` counted as `M of M`, `N-M of T` as `T-T of T`), so the frame does not change width while it scrolls | everyone | Open a long menu in a short terminal and scroll from top to bottom; check that the frame width does not change |
| popup-29 | popup.2 | Narrow content is aligned left, one cell from the frame | everyone | Open a confirm and look at where the content is |
| popup-30 | popup.3 | Opening part one, the line, 4 frames: on the popup's middle row, a heavy `━` line in the layer colour grows from the centre to both sides until it is as wide as the popup | everyone | Record a popup opening and step through it frame by frame |
| popup-31 | popup.3 | Part two, the hold, 1 frame: the full line stays for one frame | everyone | As above |
| popup-32 | popup.3 | Part three, the opening, 4 frames: the popup opens up and down from its middle row, each frame showing the rows at the very middle of the popup, the last frame the whole popup | everyone | As above |
| popup-33 | popup.3 | Closing is the same 9 frames backwards: pressed into a line at the middle, then the line shrinks to its centre | everyone | Record a popup closing and step through it frame by frame |
| popup-34 | popup.3 | From the first opening frame, what lies beneath is dimmed | everyone | Record the first opening frame; check that what lies beneath is already darker |
| popup-35 | popup.3 | Once closing starts, what lies beneath lights up again at once | everyone | Record the first closing frame; check that what lies beneath is already lit again |
| popup-36 | popup.3 | The half-closed source lies under the target, dimmed as F8 says | everyone | Open a target from a source that is cleared, record it, and check that the half-closed source is dimmed |
| popup-37 | popup.3 | Toasts and terminal popups animate the same way too | terminal popup or toast | Record a toast and a terminal popup opening and closing |
| popup-38 | popup.4 | When tabs follow the title, the loading icon sits after the whole row of tabs | popup tab | Open a popup with tabs that loads |
| popup-39 | popup.4 | A popup's loading icon has one space on each side | loading | Look at both sides of the icon |
| popup-40 | popup.4 | The loading icon is U+F0A9E–U+F0AA5 (`nf-md-circle_slice_1` to `_8`), eight frames, a circle filling slice by slice, then starting over once full | loading | Record the icon through one turn; read the code to check the code points |
| popup-41 | popup.4 | The loading icon takes 90ms a frame | loading | Read the code: the time per frame |
| popup-42 | popup.4 | The frame comes from the clock (`frames[(now / 90ms) % 8]`), not a counter | loading | Read the code: how the frame is picked |
| popup-43 | popup.4 | The loading tick is only rescheduled while something is loading | loading | Read the code: no tick is scheduled while nothing is loading |
| popup-44 | popup.4 | The loading icon is one cell wide, the same as the static glyph it replaces, so swapping it in and out shifts nothing | loading | Check that the text beside it does not move when loading starts and ends |
| popup-45 | popup.4 | Braille dots are not used as the loading icon | loading | Look at the loading icon's shape |
| popup-46 | popup.4 | The loading icon is the same colour as the text beside it | loading | Look at the colour of the icon in the loading line in the middle of a panel |
| popup-47 | popup.4 | A loading icon after a popup title takes that layer's layer colour, bold | loading | Look at the colour of the icon after the title |
| popup-48 | popup.4 | A loading icon on a panel's top border takes the border colour (Blue with focus, Surface2 without), not bold, dimmed along with the frame | loading | While a panel is loading, press `Tab` to move away and look at the icon's colour |
| popup-49 | popup.6 | Only the content area scrolls; the top and bottom padding, the error row and the top and bottom borders stay put | everyone | Scroll in a popup whose content does not fit; check that the padding and the error row do not move |
| popup-50 | popup.6 | It scrolls with the focus, by as little as needed for the unit holding the focus to be fully visible; the focus is not pinned to the middle | everyone | In a menu that does not fit, keep moving down; check that it starts scrolling only when the cursor reaches the bottom |
| popup-51 | popup.6 | While the content does not fit, the right of the bottom border shows the scroll position | everyone | Look at the bottom right of a popup whose content does not fit |
| popup-52 | popup.6 | A popup's scroll position is in the layer colour | everyone | Look at the colour of the scroll position at the bottom right |
| popup-53 | popup.6 | With a cursor or a text cursor it reads `N of M` (the position of the unit holding the focus, and the total) | everyone | Move the cursor in a menu that does not fit and look at the bottom right |
| popup-54 | popup.6 | Without a cursor or a text cursor (a note, a viewer outside the selection mode) it reads the visible lines, `N-M of T` | everyone | Open a key reference that does not fit and look at the bottom right |
| popup-55 | popup.6 | Nothing is shown when everything fits | everyone | Open a popup whose content fits and look at the bottom right |
| popup-56 | popup.6 | A form and a one-value-per-row panel count fields: the label and value rows of a stacked field, or the options of a radio, make one field; M counts fields only, not the error row or the button | form or one value per row | Move around a form or a one-value-per-row panel that does not fit and look at `N of M` |
| popup-57 | popup.6 | A text cursor in a stretch of text (a textarea, a viewer in the selection mode) counts lines: the cursor's line and the number of lines, the same numbers as the line numbers | viewer or textarea | Move the text cursor in a long textarea; check that `N of M` matches the line numbers |
| popup-58 | popup.6 (diagram) | Below the error row comes one row of bottom padding, then the bottom border | input | Open an input popup and look between the error row and the bottom border |
| popup-59 | popup.7 | The error row sits below the content area, fixed, never scrolling | input | Open an input popup, make it show an error, and look at where the error row is |
| popup-60 | popup.7 | One blank row between the error row and the content | input | As above, look between the error row and the content |
| popup-61 | popup.7 | Only popups whose values can be invalid reserve an error row | everyone | Open a confirm and a menu; check that there is no reserved blank row |
| popup-62 | popup.7 | The error row holds value errors only (format, range, a required field, a duplicate name), with a short message, and the countdown while taking values is paused after too many wrong ones | input | Give an invalid value and look at the message in the error row |
| popup-63 | popup.7 | The error row is Red text | input | Look at the error row's colour |
| popup-64 | popup.7 | The error row shares the content's left edge; when the content is centred, it is centred too | input | Look at where the error row starts |
| popup-65 | popup.7 | With an error, the frame and title do not change colour and keep the layer colour | input | Give an invalid value and look at the colours of the frame and title |
| popup-66 | popup.7 | The error row keeps to one row; when too long it is cut at the end with `…` | input | Bring up a very long error; check that it takes one row only |
| popup-67 | popup.7 | In an input popup the error row never takes the focus | input | Make an input popup show an error and press keys; check that the focus never goes to the error row |
| popup-68 | popup.7 | An input popup checks on `Enter` | input | Type an invalid value; check that the error appears only on `Enter` |
| popup-69 | popup.7 | When the action itself fails (a write failing, the remote refusing, the file changed underneath), it is not written in the error row: an error popup opens over the current popup | everyone | Make a submitted action fail; check that an error popup pops up |
| popup-70 | popup.7 | While taking values is paused after too many wrong ones, the countdown goes in the error row (Red, updated every second, cleared when done); during the pause every key but `Esc` is swallowed, none reaching the typing row | input | Get it wrong until it pauses: the error row counts down every second; typing during the pause leaves the typing row unchanged; when done the error row clears (an app that never pauses has no such case) |
| popup-71 | popup.8 | An app's own popup takes the frame, title, hint, width, opening and closing animation, loading, layer colours and dimming of a popup | an app's own popup | Open it and look at the frame, title, hint and the opening and closing; open another popup on top |
| popup-72 | popup.8 | Hotkeys on an app's own popup's content are disclosed in that popup's `?` | an app's own popup | Press `?` on such a popup |
| popup-73 | popup.8 | In an app's own popup the focus is visible, and movement follows K12 (hjkl are the arrow keys) | an app's own popup | Press hjkl on the content and watch the focus |

## dialog/form

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| form-1 | form.1 | A form is used only for several values submitted together: a single value uses an input popup, not a form | form | Look at every form: each has more than one field |
| form-2 | form.1 | Values that take effect when changed, with nothing to submit, go in a panel with one value per row, not in a form | form | Look at every form: every value in it takes effect only on submit |
| form-3 | form.1 | Nothing is typed into a form itself: a field that takes typing (text, password…) opens that field's input popup on `Enter`, and the value is entered there | form | With the focus on a field that takes typing, press `Enter`: an input popup opens; typing straight into the form does not change the value |
| form-4 | form.1 | A field with more options than fit (select, date, colour, file) opens that field's input popup on `Enter` | form | With the focus on a field such as a select, press `Enter`: its popup opens |
| form-5 | form.3 | The title does not name the type (`number`, `path`, `email`) | form | Read the title text |
| form-6 | form.4 | Each field takes one of the two arrangements, stacked or side by side | form | Look at how each field of the form is arranged |
| form-7 | form.4 | Stacked: the label on one row, the value on the next, the value using the full inner width | form | Look at the two rows of a stacked field |
| form-8 | form.4 | Side by side: one row, the label in a left column, the value to its right | form | Look at a side-by-side field |
| form-9 | form.4 | No blank row between fields | form | Look between two adjacent fields in the field area: no blank row |
| form-10 | form.4 | No blank row between a stacked label and its value | form | Look at the label and the value of a stacked field |
| form-11 | form.4 | In a stacked field, the label, the value and the error share the same left edge | form | After a refused submit, look at a stacked field: the value, the error row and the label start in the same column |
| form-12 | form.4 | The label column of side-by-side fields is as wide as the longest label among the side-by-side fields; stacked labels do not count | form | Look at the side-by-side values: all start in the same column, after the longest side-by-side label |
| form-13 | form.5 | Options drawn in a form or on a one-value-per-row panel always run down, one a row | radio or checkbox | Look at the options: none run across |
| form-14 | form.9 (diagram) | Options of a side-by-side field in a form or on a one-value-per-row panel: the first option on the label's row, each of the rest on a row of its own below, its left edge at the value's, the label column blank (a checkbox group's options two cells further in than `Select all`) | radio or checkbox | Look at the second and later options of a radio field: their left edge lines up with the first option's |
| form-15 | form.6 | A field's focus block runs from the value all the way to the frame, covering the right padding | form | With the focus on a field, look at the block: from the value's left edge to the right border |
| form-16 | form.6 | In a form and on a one-value-per-row panel, an option's focus block runs from that option's glyph all the way to the frame | radio or checkbox | With the focus on an option, look at the block |
| form-17 | form.6 | A field with an empty value is still a full block of background when it has the focus | form | With the focus on an empty field, look at the block |
| form-18 | form.6 | A button's focus block is the button itself, with no arrow | form | `Tab` to a button: the block is the button only |
| form-19 | form.6 | In a form and on a one-value-per-row panel, the label does not change colour with the focus | form or one value per row | Move the focus into and out of a field: the label's colour stays the same |
| form-20 | form.6 | A normal label is in the layer colour (the same as the title capsule and the border) | form | Compare the label's colour with the border's |
| form-21 | form.6 | The label of a field whose value has an error is Red, over any other colour | form | After a refused submit, look at the label with a problem |
| form-22 | form.6 | In a form and on a one-value-per-row panel, a disabled field stays in place, neither removed nor changing the height | form or one value per row | Make a field disabled: the form's layout does not change |
| form-23 | form.6 | In a form and on a one-value-per-row panel, a value never shares its label's colour, in any state | form or one value per row | Look at the label and the value when normal, focused, disabled and in error |
| form-24 | form.7 | A button is its text with one blank cell on each side, on a block of background | form | Look at the buttons in the action area |
| form-25 | form.7 | A button says what pressing it does (`Save`, `Connect`) | form | Read the button text |
| form-26 | form.7 | A button is not drawn in square brackets (`[ Save ]`) | form | Look at the buttons |
| form-27 | form.7 | A button is not drawn as a capsule | form | Look at both ends of the buttons |
| form-28 | form.7 | From top to bottom: the field area → a blank row → the error row (blank when there is no error) → a separator → the action area | form | Look at the rows of the lower half of the form |
| form-29 | form.7 (diagram) | No blank row between the error row, the separator and each row of buttons | form | Look from the error row to the last row of buttons: no blank row |
| form-30 | form.7 | Every row of buttons sits on the right, the rightmost button one cell from the border | form | Count the cells between the rightmost button's block and the right border |
| form-31 | form.7 (diagram) | The separator above the action area is a solid line `─` (U+2500) | form | Look at the character the separator uses |
| form-32 | form.7 | The error row, the separator and the action area never scroll; when the fields do not fit, only the field area scrolls | form | Make the terminal too short for the fields; while scrolling, the error row and the buttons do not move |
| form-33 | form.7 | With the focus on the error row or a button, no scroll position is shown; it comes back once the focus is on a field | form | With fields that do not fit, `Tab` to a button and back, looking at the right of the bottom border |
| form-34 | form.7 | There is always one main submit, in the bottom-right corner of the action area (with one button, that is it) | form | Check the rightmost button on the last row is the main submit |
| form-35 | form.7 | One cell between the buttons of a row | form | Count the cells between the blocks of two buttons on a row |
| form-36 | form.7 | An action that keeps the form open, when pressed, checks only the fields this action needs | form | Leave a field it does not need empty and press that button: it is not refused |
| form-37 | form.7 | When the check of an action that keeps the form open fails, it shows as a refused submit does: the labels with a problem turn Red, the error row gives the first problem, and the focus jumps to that field | form | Leave a field it needs empty and press that button |
| form-38 | form.7 | An action that keeps the form open shows a toast of one sentence on success | form | Make the action succeed and look at the toast at the bottom |
| form-39 | form.7 | When an action's result is content to read, a note opens | form | Press that button: the result opens in a note |
| form-40 | form.7 | An action that keeps the form open and takes a while, and a submit that takes a while (e.g. `Connect`), put the loading icon after the title while they run | form | Press it: a spinning loading icon sits after the title, gone once it is done |
| form-41 | form.7 | While the action runs, `Enter` with the focus on that button does nothing | form | Press it, then right away `Enter` again: nothing is sent a second time |
| form-42 | form.7 | While the action runs, the hint drops that button's `Enter`, and puts it back once it is done | form | Press it and look at the hint on the bottom border, then again once it is done |
| form-43 | form.7 | A submit that takes a while (`Connect`) does the same while it runs: `Enter` does nothing, and the hint drops its `Enter` | form | Press the submit, then right away `Enter` again; look at the hint |
| form-44 | form.7 | The form closed before the action is done (`Esc`, or another submit): the action is cancelled, stopped if it can be | form | Press it, then right away `Esc`; read the code: the action is stopped |
| form-45 | form.7 | Once the form is closed, the action's result is not shown (no toast, note or error popup) | form | Press it, then right away `Esc`; wait a moment: no result shows |
| form-46 | form.7 | After an action that keeps the form open is done, the focus stays on the button | form | After the action succeeds, look at the focus |
| form-47 | form.7 | When an action writes a value into a field, that field counts as changed | form | Let the action write into a field, then press `Esc`: a confirm comes first |
| form-48 | form.7 | No cancel button in the action area | form | Look at the action area: no `Cancel` or similar button |
| form-49 | form.9 | In a form and on a one-value-per-row panel, the focus moves by item: a field that takes typing or opens a popup is one item, each option of a radio or checkbox field is one, a checkbox group's `Select all` is one, each button is one | form or one value per row | Walk through with `j`, counting the stops |
| form-50 | form.9 | The error row, while it holds an error, is an item too, after the last field; with no error the focus does not stop on it | form | Walk past the last field with `j` before and after a refused submit |
| form-51 | form.9 | In a form and on a one-value-per-row panel, going on from a field's last option enters the next field; going back from its first option returns to the previous field | radio or checkbox | Press `j` on a radio field's last option and `k` on its first |
| form-52 | form.9 | The action area runs in reading order: along a row from left to right, then on to the next row | form | Press `j` in the action area through every button |
| form-53 | form.9 | `gg\|G` go to the first and the last item of the area | form | Press `gg` and `G` in the field area and in the action area |
| form-54 | form.9 | `u\|d` move half a page, counted in items, and stop at the ends | form | On a form with many fields, press `d` to the bottom and once more: it does not wrap |
| form-55 | form.9 | The first time in the action area, the focus lands on the main submit (the bottom-right corner) | form | Open the form and press `Tab` for the first time |
| form-56 | form.9 | The error row belongs to the field area: `j\|k` and `e` reach it, and `Tab` on it goes to the action area | form | After a refused submit, walk to the error row with `j`, then press `Tab` |
| form-57 | form.9 | Each area wraps at its own ends: past the last item of the field area (the error row, when it holds an error) comes the first field again; past the last button comes the first button | form | Press `j` on the last item of the field area and on the last button |
| form-58 | form.9 | In a form and on a one-value-per-row panel, disabled fields and options are skipped: `j\|k` do not stop on them | form or one value per row | Walk past a disabled field with `j` |
| form-59 | form.9 | On opening, the focus is on the first item it can stop on (disabled ones skipped, and a checkbox group's `Select all` too, for its first option), for a new entry and an edit alike | form | Open a new-entry form and an edit form, looking at the focus in each |
| form-60 | form.9 | When the app opens the form from one field, the focus is on that field | form | Open an edit form from a row of a panel and look at the focus |
| form-61 | form.9 | On opening, no field's input popup opens by itself: what opens is always the form itself, left with one `Esc` | form | Open a new-entry form and press `Esc` once: back where it was opened from |
| form-62 | form.9 | Landing on a radio or checkbox field (the app opening the form at that field, a blocked submit, `e` on the error row), the focus stops on the first option with a value: a radio on the chosen option, a checkbox on the first ticked option; with no value, on the first option (`Select all` does not count) | form | Give the radio field an error and submit; look at which option the focus stops on |
| form-63 | form.10 | `Enter` on a button presses it: submitting, or doing that button's action | form | `Tab` to a button and press `Enter` |
| form-64 | form.11 | There is one way only to submit: `Enter` with the focus on a submit button (no letter hotkey or other way to submit) | form | Press `s` and other letters on a field: none of them submits |
| form-65 | form.12 | With the focus on a field that takes typing (text, password, number, textarea), a printable character that is not one of the form's keys (digits and `q` included) brings up a note to explain | form | Type `s`, `1` and `q` on a text field |
| form-66 | form.12 | The explanation note's title is the field's name | form | Read the title of the note that pops up |
| form-67 | form.12 (diagram) | The explanation note tells the user to press `[Enter]` to edit the field | form | Read the note's text |
| form-68 | form.12 | Both `Enter` and `Esc` close the explanation note, back to the form with the focus unmoved | form | Bring up the note and close it with `Enter`, then again with `Esc` |
| form-69 | form.12 (diagram) | The explanation note's hint is `Enter\|Esc:close` | form | Look at the note's bottom border |
| form-70 | form.12 | The form's own keys (`j` `k` `h` `l`, the arrow keys, `Tab\|Shift-Tab`, `u\|d`, `g`, `G`, `e`, `Enter`, `Esc`, `Space`, `?`) bring up no note on a field that takes typing | form | Press each of these keys on a text field |
| form-71 | form.12 | `e` acts only on a field with a problem and on the error row, and does nothing elsewhere | form | Press `e` with no error |
| form-72 | form.12 | On a field that opens another input popup (select, slider, date, colour, file, reorder, checkbox popup), a printable character brings up no note and does nothing | form | With the focus on a field such as a select, type `s`, `1` and `q`: no note, and nothing changes |
| form-73 | form.12 | Other printable characters on options, buttons and the error row bring up no note and do nothing | form | With the focus on a button, type `s` |
| form-74 | form.13 | With the focus on a field that opens an input popup, the hint reads `Enter:edit` | form | Look at the hint on the bottom border |
| form-75 | form.13 | In a form and on a one-value-per-row panel, with the focus on a radio option, the hint reads `Enter:choose` | radio | Look at the hint on the bottom border |
| form-76 | form.13 | On a form, with the focus on a checkbox option, the hint reads `Enter\|Space:toggle` | form + checkbox | Look at the hint on the bottom border |
| form-77 | form.13 | With the focus on a button, the hint gives the button's word: its verb in lower case, names and paths as they are (`Save` → `Enter:save`, `Save As` → `Enter:save as`) | form | `Tab` to each button and look at the hint |
| form-78 | form.13 | With the focus on a field with a problem, `e:error` is added (`Enter:edit e:error Tab:actions Esc:cancel`) | form | After a refused submit, look at the hint |
| form-79 | form.13 | With the focus on the error row, the hint is `Enter:show e:edit Tab:actions Esc:cancel` | form | After a refused submit, walk to the error row and look at the hint |
| form-80 | form.13 | `Tab` names the area it goes to: `Tab:actions` in the field area (the error row too), `Tab:fields` on a button; never `Tab:save` | form | Look at the hint once on a field and once on a button |
| form-81 | form.13 | `Esc` reads `Esc:cancel`, not `close` | form | Look at the hint on the bottom border |
| form-82 | form.15 | `Esc` on a form with no changes closes it at once | form | Open a form, change nothing, and press `Esc` |
| form-83 | form.15 | On the confirm asking whether to discard, `Enter` discards and closes the form; `Esc` closes the confirm and returns to the form with every value still there | form | On that confirm press `Enter`, and on another try `Esc` |
| form-84 | form.15 | A value written back to the form counts as a change: an input popup confirming a value different from the one it opened with (a checkbox popup writing the whole group back on `Enter` included), a radio option chosen, a checkbox flipped | form | Do each once, then press `Esc`: each time a confirm comes first |
| form-85 | form.15 | The "changed" flag, once set, is never cleared: changing a value and then changing it back still counts as a change | form | Change a field, change it back, and press `Esc`: a confirm still comes first |
| form-86 | form.15 | Only forms, the textarea and reorder ask whether to discard: other input popups close at once on `Esc`, without asking | input | Type something in a text input popup, then press `Esc` |
| form-87 | form.16 | Rules involving the whole form (a required field, a field required because of another, a duplicate name) are checked only when the button is pressed to submit | form | Walking past an empty required field does not turn it Red; only pressing the submit refuses it |
| form-88 | form.16 | A failed check: nothing is saved; the form stays open with every value | form | Leave a required field empty and submit |
| form-89 | form.16 | On a failed check, the label of every field with a problem (not just the first) turns Red | form | Give two fields an error and submit |
| form-90 | form.16 | The error row gives the first problem in field order | form | Give two fields an error, submit, and read the error row |
| form-91 | form.16 | `e` on a field with a problem: the focus moves to the error row, which switches to that field's message | form | With two fields in error, press `e` on the second |
| form-92 | form.16 | `Enter` on the error row opens an error popup with the whole message, its title the field's name, closed with `Enter` or `Esc` | form | Press `Enter` on the error row and read the title; close it with `Enter`, then again with `Esc` |
| form-93 | form.16 | `e` on the error row: the focus returns to the field the message belongs to | form | Press `e` on the error row |
| form-94 | form.16 | Errors follow the check: a form's Red labels and error row stay even when values change, until the next check (a submit, or pressing an action that keeps the form open) changes or clears them | form | After a refused submit, fix that field: the label is still Red, and only the next submit clears it |
| form-95 | form.12 | The typing note takes only `Enter` and `Esc`: any other typable character (`q` and `?` included) does nothing and does not pass through | form | On a text field type `a` to bring up the note, then type `q`, `?`, `j`: the note stays and nothing happens |
| form-96 | form.16 | An input popup's error row stays even when the value changes, until the next `Enter` changes or clears it | input | Give an input popup an error, change the value: the error stays; only the next `Enter` changes it |

## dialog/menu

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| menu-1 | menu.1 | A menu is used only for a list without search, choosing a row to run it: a list that needs search is a finder, choosing a value to be written back is a select, putting items in order is a reorder | everyone | Look at every menu: choosing a row runs that row |
| menu-2 | menu.2 | Each row's label is in Text | everyone | Press `Space` and look at the menu's rows |
| menu-3 | menu.2 | The hotkey mark `[x]` is in the label's colour | everyone | Look at a row with a hotkey |
| menu-4 | menu.2 | Descriptions are in Overlay0 | everyone | Look at the descriptions' colour |
| menu-5 | menu.2 | Each row: the action's name on the left; the description right-aligned, against the right padding (normally one cell from the right border) | everyone | Look at the right edge of each row's description |
| menu-6 | menu.2 | A description too long (with the frame already at its widest) is cut at the end with `…`, keeping to one row | everyone | Narrow the window and look at a long description |
| menu-7 | menu.2 | At least two cells between the label and the description | everyone | Look at the widest row |
| menu-8 | menu.2 | A section title: an `nf-md-hexagon` (U+F02D8), one space, then the title | everyone | Look at the Space menu's section titles |
| menu-9 | menu.2 | Section titles are in uppercase | everyone | Look at the section titles |
| menu-10 | menu.2 | Section titles are in Overlay0, not bold | everyone | Look at the section titles |
| menu-11 | menu.2 | Section titles are indented one cell (one cell from the frame, in the same column as the rows' text) | everyone | Look at the left edge of the section titles |
| menu-12 | menu.2 | The cursor skips section titles | everyone | Move past a section title with `j\|k` |
| menu-13 | menu.2 | Separators between sections are the double dash `╌` (U+254C) | everyone | Look at the character the separators use |
| menu-14 | menu.2 | The cursor skips separators | everyone | Move past a separator with `j\|k` |
| menu-15 | menu.2 (diagram) | No blank row between section titles, rows and separators | everyone | Look at the Space menu: no blank row |
| menu-16 | menu.2 | The title is `nf-fa-bars` (U+F0C9) plus text, drawn as the title capsule | everyone | Look at each menu's title |
| menu-17 | menu.2 | The Space menu's title shows the focused panel's `[N] label` | everyone | Press `Space` on different panels and read the title |
| menu-18 | menu.2 | The `Global operation` row's description is always `actions for the whole app` | everyone | Look at the Space menu's last row |
| menu-19 | menu.3 | The hint is `Enter:run Esc:close`, with no movement keys | everyone | Look at the menu's bottom border |
| menu-20 | menu.3 | On a jobs-list row with nothing to do on it, `Enter` opens the row's full text and the hint is `Enter:detail Esc:close` | jobs list | Move the cursor to a row with nothing to do on it and look at the bottom border |
| menu-21 | menu.5 | On a jobs-list row something can be done to (e.g. a running transfer that can be cancelled), `Enter` opens a confirm holding the row's full text, and the hint names that action (e.g. `Enter:cancel Esc:close`) | jobs list | Move the cursor to a row something can be done to, read the hint, then press `Enter` |
| menu-22 | menu.5 | While a jobs list is open, its rows follow the work (a row changes as soon as the progress or the state changes), with no closing and reopening | jobs list | Open the jobs list while work runs and watch a row's progress change |
| menu-23 | menu.4 | The mode's Space menu has two sections, `ITEM OPERATION` and `<mode name> MODE`; no panel, item or global actions | mode | Enter a mode and press `Space` |
| menu-24 | menu.4 | Item operations run like any row, picking one being the same as pressing its key; what cannot be done now is disabled | mode | Run one from the menu; open the menu with the cursor where it cannot be done |
| menu-25 | menu.4 | Movement keys are only shown: the key in Blue, the description in Overlay0, skipped by the cursor, `Enter` doing nothing | mode | Move the cursor in the menu |
| menu-26 | menu.4 | Leaving the mode (named with the verb of `Esc` in the mode's hint, e.g. `[Esc] Leave`) runs from the menu; `Esc` in the menu only closes it, back to the mode | mode | Pick Leave; open the menu again and press `Esc` |
| menu-27 | menu.4 | The title is where the mode lives: the panel's `[N] label`, or the popup's title | mode | Open it in a mode on a panel and in one in a popup |

## dialog/confirm

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| confirm-1 | confirm.2 | The title glyph is `nf-md-shield_alert` (U+F0ECC) | confirm | Open a confirm (e.g. quitting) and look at the title |
| confirm-2 | confirm.2 | The title text is the action's name (`DELETE`, `QUIT`, `CONNECT`) | confirm | Read the title text |
| confirm-3 | confirm.2 | The question comes last, with the hint right below it (only the bottom padding between them) | confirm | Look between the question and the bottom border |
| confirm-4 | confirm.2 | What to read before answering sits above the question | confirm | Look at a confirm with content |
| confirm-5 | confirm.2 | A blank row between the content and the question | confirm | Look between the content and the question |
| confirm-6 | confirm.2 | With nothing to read, there is only the question | confirm | Look at a confirm with no content |
| confirm-7 | confirm.2 | The question is in Text, not bold | confirm | Look at the question |
| confirm-8 | confirm.2 | The content is in Overlay0 | confirm | Look at the content's colour |
| confirm-9 | confirm.2 | The warning sentence in the content is in Peach | confirm | Look at the warning sentence |
| confirm-10 | confirm.2 | A question or content too long wraps, never cut | confirm | Narrow the window and look at a long question or content |
| confirm-11 | confirm.2 | When the content is long, only the content scrolls with `j\|k`; the question stays fixed at the end | confirm | Press `j\|k`: the question does not move |
| confirm-12 | confirm.3 | The hint is `Enter:<verb> Esc:cancel`, the verb saying what accepting does (`Enter:delete Esc:cancel`) | confirm | Look at each confirm's bottom border |

## dialog/note

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| note-1 | note.2 | The title is a glyph plus what is shown, drawn as the title capsule | everyone | Look at the titles of the key reference and of a viewer |
| note-2 | note.2 | A viewer's title: the kind in uppercase; to say which one is shown, ` — ` and then the name, the name as it is (e.g. `YAML — pod/nginx`) | viewer | Look at the viewer's title |
| note-3 | note.2 | When a viewer wraps, N is the line of the top row, M the line of the bottom row and T the number of lines | viewer | Narrow the window until the content wraps; compare the scroll position with the line numbers |
| note-4 | note.2 | A viewer wraps by default: a line wider than the frame continues on the next row; for content to keep aligned, the app may keep it unwrapped, the part past the frame cut with `…` at the end of the line | viewer | Open content with a long line: it wraps onto the next row, or ends in `…` |
| note-6 | note.2 | The first row of each line carries its number, right-aligned, with a space after it | viewer | Look at the gutter |
| note-7 | note.2 | A wrapped row leaves the gutter blank | viewer | Look at the wrapped rows |
| note-8 | note.2 (diagram) | The gutter comes right after the left padding (one cell from the frame), with no separator drawn between the numbers and the content | viewer | Look at where the gutter is |
| note-9 | note.2 (diagram) | A wrapped row starts at the left edge of the content column, not following the line's indent | viewer | Look at the wrapped rows of a deeply indented line |
| note-10 | note.2 | Line numbers are in Overlay0 | viewer | Look at the line numbers' colour |
| note-11 | note.2 | In the selection mode, the cursor's line has its number in Text | viewer | Press `v` and look at the number of the cursor's line |
| note-12 | note.2 | Copying leaves the numbers out | viewer | Select a stretch, copy it, and paste it to look |
| note-13 | note.2 | The gutter is at least three digits: where the line count is known on opening, it is max(3, the digits of the line count) and stays so | viewer | Open content of under 100 lines and of over 1000 lines; look at the gutter's width |
| note-14 | note.2 | A streaming viewer (App Log) starts its gutter at three digits and widens it only past 999 lines | viewer | Look at the gutter before and after the stream reaches 1000 lines |
| note-15 | note.2 | In a viewer with tabs, the gutter follows the widest of the pages seen so far, and only ever widens, never narrows (a streaming page likewise) | viewer | Switch to a page with more lines and back: the gutter does not narrow again |
| note-16 | note.2 | A viewer whose content has a fixed format (YAML, JSON, TOML, HTML, XML, Markdown…) is coloured as a text file in the file-picker preview: chroma's catppuccin-mocha, foreground only; file content goes by the file name | viewer | Open a YAML view and the content of a `.json` file: the syntax colours match the preview, with no background colour |
| note-17 | note.2 | No syntax colours inside the selection | viewer | Select a stretch of text with syntax colours and look at the characters in the selection |
| note-18 | note.2 | A Tab in a viewer is drawn as `input_tab_width` spaces, not aligned to tab stops | viewer | Open a file with Tabs |
| note-19 | note.2 | A `\r` before a line break (CRLF) is not drawn | viewer | Open a CRLF file |
| note-20 | note.2 | Any other control character is drawn by name (`\x07`), in Red | viewer | Open content with control characters |
| note-21 | note.2 | Copying takes the original characters: the original Tabs and control characters, not the spaces or names drawn | viewer | Select a stretch with a Tab, copy it, and paste it to look |
| note-22 | note.3 | `j\|k`, `u\|d`, `gg\|G` scroll | everyone | Press these keys on a key reference that does not fit |
| note-23 | note.3 | A wrapping viewer scrolls by rows as drawn: `j\|k` one row at a time, `u\|d` half a page counted in rows | viewer | While it wraps, press `j`: it scrolls one row only |
| note-24 | note.3 | `Enter` does not close a note (the error popup and a form's typing explanation aside) | everyone | Press `Enter` on the key reference and on a viewer |
| note-25 | note.4 | Only viewers have the selection mode: on the key reference, the error popup and the typing explanation, `v` does nothing and `j\|k` only scroll | everyone | Press `v` on the key reference |
| note-26 | note.4 | A viewer has no cursor by default; `j\|k`, `u\|d`, `gg\|G` scroll the view | viewer | Open a viewer and press `j` |
| note-27 | note.4 | A viewer with tabs switches tabs with `h\|l` by default | viewer | Press `h` and `l` |
| note-28 | note.4 | The first `v` enters the selection mode: the frame and the mode name turn the mode colour Yellow | viewer | Press `v` and look at the frame and the mode name |
| note-29 | note.4 | On entering the selection mode, the cursor is at the start of the first visible line, with nothing selected yet | viewer | Press `v` and look at where the cursor is |
| note-30 | note.4 | In the selection mode, `h\|j\|k\|l` (in a viewer with tabs too, where `h\|l` do not switch tabs), `w\|b\|e`, `0\|$`, `u\|d`, `gg\|G` move the cursor, and the view scrolls when it reaches the edge | viewer | Press `v`, then each of these keys, moving to the bottom edge |
| note-31 | note.4 | With nothing selected yet, the hint is `v:select Esc:cancel` | viewer | Press `v` once and look at the bottom border |
| note-32 | note.4 | The second `v` starts the selection where the cursor is; moving the cursor stretches it | viewer | Press `v` a second time, then move the cursor |
| note-33 | note.4 | The selection runs by characters: from the start to the cursor, the cursor's character included | viewer | Select a stretch, copy it, and check both ends |
| note-34 | note.4 | Once selecting, the mode name is `Visual>select` and the hint `y:copy Esc:unselect` | viewer | Press `v` a second time and look at the bottom border |
| note-35 | note.4 | Once selecting, `v` does nothing (it is not an alias for leaving) | viewer | Press `v` once selecting |
| note-36 | note.4 | `y` copies the selection and leaves the mode; the selection and the cursor disappear, and a Success toast says it is copied | viewer | Select a stretch and press `y` |
| note-37 | note.4 | `Esc` goes back one layer at a time: once selecting, the selection disappears and it is back to `Visual`, the cursor where it is; before selecting, it leaves the whole mode and the cursor disappears; neither copies | viewer | Press `Esc` while selecting, then again |
| note-38 | note.4 | The cursor is one cell of the layer colour background with Base text | viewer | Press `v` and look at the cursor |
| note-39 | note.4 | The selection has a Yellow background with Base text, the cursor's cell keeping the layer colour | viewer | Select a stretch and look at the selection and the cursor |
| note-40 | note.4 | An empty line inside the selection shows one cell | viewer | Select a stretch across an empty line |
| note-41 | note.5 | The title glyph is `nf-fa-question_circle` (U+F059) | everyone | Press `?` and look at the title |
| note-42 | note.5 | The title text is `<surface> keys` (`[2] HOSTS KEYS`, `SPACE MENU KEYS`) | everyone | Press `?` on a panel and on the Space menu, reading the title each time |
| note-43 | note.5 | One key per row, indented two cells (the key starting in the third cell inside the border) | everyone | Look at the left edge of the keys |
| note-44 | note.5 | The key is padded to the width of the widest key, then two blank cells, then the description | everyone | Check every description starts in the same column |
| note-45 | note.5 | A description too long (with the frame already at its widest) is cut at the end with `…`, never wrapped | everyone | Narrow the window and look at a long description |
| note-46 | note.5 | Rows from a menu: the description reads `label — description` | everyone | Compare with the Space menu's rows |
| note-47 | note.5 | Rows from a menu: the label loses its hotkey marks and keeps its case (`[E]dit` becomes `Edit`) | everyone | Compare with the Space menu's rows |
| note-48 | note.5 | Section titles as in a menu: `nf-md-hexagon`, uppercase, Overlay0, indented one cell, not bold | everyone | Look at the section titles |
| note-49 | note.5 (diagram) | No separator and no blank row between sections: a section title comes right below the previous section's last row | everyone | Look between two sections |
| note-50 | note.5 | On a panel the sections are, in order, (`what each row is`, when a one-value-per-row panel has it,) `item operation`, `panel operation`, `move`, `core keys`, `app-wide` | everyone | Press `?` on a panel and look at the order of the sections |
| note-51 | note.5 | `item operation` and `panel operation` hold the same as the Space menu | everyone | Compare with the same panel's Space menu |
| note-52 | note.5 | `move` lists only the movement keys that really work here | everyone | Press each key in `move` on this panel: each does something |
| note-53 | note.5 | `core keys` lists the core keys that work on this panel: `Space`, `?`, `Tab`, `1–N`, `q\|Ctrl-C` | everyone | Look at the `core keys` section |
| note-54 | note.5 | `1–N` is listed in `core keys` only with several panels | everyone | Check a screen with only one panel has no `1–N` |
| note-55 | note.5 | `Esc` is listed in `core keys` only where it does something here (e.g. a filter to clear) | everyone | Press `?` with a filter and without one |
| note-56 | note.5 | `Enter` is not listed in `core keys` (`item operation` already has it) | everyone | Check `core keys` has no `Enter` |
| note-57 | note.5 | A panel's key reference lists the global hotkeys in the `app-wide` section; quitting's `q` is already in `core keys` and is not repeated | everyone | Compare with the global operation popup's hotkeys |
| note-58 | note.5 | A key that can be pressed now is in Blue, not bold (for one that cannot, see note-60) | everyone | Look at the colour of the key column |
| note-59 | note.5 | Descriptions are in Text | everyone | Look at the descriptions' colour |
| note-60 | note.5 | A key that cannot be pressed right now (its target exists) is still listed, both key and description in Surface2 | disabled | Make an action disabled and press `?` |
| note-61 | note.5 | The hint is `?\|Esc:close` | everyone | Look at the key reference's bottom border |
| note-62 | note.6 | Frame and text are in Red | error popup | Look at the error popup's frame and message |
| note-63 | note.6 | The title capsule is filled Red, with Base bold text | error popup | Look at the title capsule |
| note-64 | note.6 | The title glyph is `nf-md-fire` (U+F0238) | error popup | Look at the title |
| note-65 | note.6 | The message wraps inside the frame; when too long it scrolls with `j\|k` | error popup | Bring up a long message and press `j\|k` |
| note-66 | note.6 | The title says what failed (`RENAME FAILED`, `SAVE FAILED`); one opened from a form's error row gives that field's name (form-92) | error popup | Read the title text |
| note-67 | note.6 | Both `Enter` and `Esc` close it | error popup | Close it with `Enter`, then again with `Esc` |
| note-68 | note.6 | The hint is `Enter\|Esc:close` | error popup | Look at the bottom border |
| note-69 | note.6 | After the error popup closes, it is back to the popup underneath, the focus where it was (when a form's submit or an action that keeps the form open fails, the focus is on that button, and one more `Enter` retries), every value still there | error popup | Close it and look at the popup underneath |
| note-70 | note.4 | Every viewer has the selection mode (`v` to select, `y` to copy) | viewer | Press `v` on every viewer |
| note-71 | note.2 | A viewer's search: every match underlined, keeping its colour; the current match drawn as the cursor block; no Yellow | viewer | In a viewer with `/`, search for a word that appears several times; look at the underlines and the current match (a viewer with no search never has this case) |
| note-72 | note.2 | In an unwrapped viewer, when the selection cursor walks into the cut part, the view scrolls sideways to show it, with `…` at the start of lines cut on the left; the cut text can be selected and copied | viewer | In an unwrapped viewer, enter the selection mode and walk the cursor right into the cut part |
| note-73 | note.5 | A long explanation in the "Each row" section wraps in the right column with the name column kept, instead of being cut; the sections of keys stay one key per row, cut when too long | one value per row | Give a row an explanation wider than the frame and press `?`: it wraps |
| note-74 | note.2 | In a viewer, a line the app hands over that holds a `\n` is split in two | viewer | Hand the viewer a line holding a `\n` (e.g. an error message over several lines) and check that it shows as two lines |
| note-75 | note.2 | In a viewer, colour codes (SGR) colour the text, a `\r` within a line keeps only the last state, and a sequence that is not a colour code is drawn by name in red | viewer | Open content with colour codes, `10%\r100%` and `\x1b[2J` |
| note-76 | note.7 | Every app has an App Log, a viewer with the newest entry last, where new entries keep arriving while it is open | everyone | Press `!`, do a few things, and watch new entries arrive |
| note-77 | note.7 | It records what the user did and how it ended, every toast, and what the app did in the background | everyone | Do something, get a toast, press `!`; read the code |
| note-78 | note.7 | Each entry: the time `HH:MM:SS` (Overlay0), the level (`INFO` Text, `OK` Green, `WARN` Peach, `ERR` Red, four cells wide, left-aligned), and what happened, capitalised like a toast | everyone | Look at the App Log's levels |
| note-79 | note.7 | Kept in memory only, emptied when the app quits; the number of entries has a limit, and the oldest goes when it is full | everyone | Read the code; or quit and start again: the App Log is empty |
| note-80 | note.8 | Title glyph `nf-md-compare` (U+F018A), `DIFF — <anchor> ↔ <the other>`, followed by two tabs, `UNIFIED` and `SPLIT`, switched with `h\|l` | compare mode | Open a comparison and press `h\|l`; read the code to check the code point |
| note-81 | note.8 | Only the parts that differ, with 3 unchanged lines before and after, an Overlay0 separator between parts | compare mode | Compare two long items that differ in two places |
| note-82 | note.8 | UNIFIED: removed lines `-` in Red, added lines `+` in Green, unchanged in Text; the anchor is the removed side; two line-number columns in Overlay0 | compare mode | Look at UNIFIED |
| note-83 | note.8 | SPLIT: the anchor on the left, the other on the right, each with its line numbers; removed in Red on the left, added in Green on the right, a blank row where there is no counterpart; not wrapped, cut with `…` | compare mode | Look at SPLIT |
| note-84 | note.8 | The last chosen tab is remembered (state) | compare mode | Switch to SPLIT, quit, start again, compare again |
| note-85 | note.8 | Narrower than 96 it is always UNIFIED and `SPLIT` is disabled | compare mode | Shrink the terminal below 96 and compare |

## dialog/terminal

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| terminal-1 | terminal.1 | A PTY placed in a panel is not a popup: its frame follows the panel's | PTY | Look at the frame of the panel holding the PTY |
| terminal-2 | terminal.2 | Above, the statusbar or the screen chip row stays (with the divider under the chip row); the frame starts on the row below the divider | terminal popup | Open it and look at the top rows |
| terminal-3 | terminal.2 | In an app without a statusbar, the frame starts from the first row | terminal popup | Check the top border is on the screen's first row |
| terminal-4 | terminal.2 | The title glyph is `nf-md-console` (U+F018D) | terminal popup | Look at the title |
| terminal-5 | terminal.2 | The title text says what is running (`SHELL`, `ALTERM: myhost`), names and paths keeping their case | terminal popup | Read the title text |
| terminal-6 | terminal.2 | The real cursor is hidden; a block of one cell, Text background with Base text, is drawn where the subprocess's cursor is | PTY | Look at the cursor in a shell |
| terminal-7 | terminal.2 | The cursor shape the subprocess asks for with DECSCUSR (underline, bar) is ignored | PTY | Send `printf '\e[6 q'` in a shell: the cursor is still a block |
| terminal-8 | terminal.3 | The exit key always comes first in the hint | terminal popup | Look at the hint on the bottom border |
| terminal-9 | terminal.3 | When the hint does not fit, the exit key is the last to be dropped | terminal popup | Narrow the terminal and look at the hint |
| terminal-10 | terminal.3 | The exit key's verb says what pressing it really does: `Alt-Esc:exit` when it ends the subprocess, `Alt-Esc:leave` when it leaves with the subprocess still running | terminal popup | Read the hint, then press the exit key and compare with what happens |
| terminal-11 | terminal.3 | The exit key never reads `close` | terminal popup | Look at the hint |
| terminal-12 | terminal.3 | After the exit key come the key combinations the app keeps (`Alt-t:hide`, `PgUp:history`) | terminal popup | Look at the order in the hint |
| terminal-13 | terminal.2 | While a terminal popup is open the footer is not drawn: both ends of the last row are blank, with no footer text showing | terminal popup | Open a terminal popup and look at both ends of the last row |
| terminal-14 | terminal.2 | A PTY in a panel has no padding either: the panel's frame is drawn as usual, with the PTY against it | PTY | Look between the first character and the frame in a panel holding a PTY |
| terminal-15 | terminal.5 | `PgUp` on a PTY scrolls up into the history mode: the frame and the mode name take the mode colour, the mode name being `History` | interactive terminal | Press `PgUp` on a PTY and look at the frame and the right of the top border |
| terminal-16 | terminal.5 | In the history mode, `j\|k`, `u\|d`, `gg\|G` and `PgUp\|PgDn` all scroll the history and are not sent to the subprocess | interactive terminal | In the history mode press these keys: the history scrolls and the shell receives nothing |
| terminal-17 | terminal.5 | In the history mode, `Esc` leaves the mode, back to the live screen | interactive terminal | In the history mode press `Esc` |
| terminal-18 | terminal.6 | An interactive terminal's selection mode is entered with `Alt-v` (the family's `v`, with `Alt` to get out of the subprocess in a PTY), always shown like the kept keys | interactive terminal | Check that the footer or the terminal's bottom border shows `Alt-v:select`, and press it |
| terminal-19 | terminal.6 | Entering a PTY's selection mode freezes the screen: later output from the subprocess is not drawn yet, and the cursor can go up into the history; leaving returns to the live screen | interactive terminal | Enter the selection mode while the shell keeps printing: the screen holds still and the cursor can go up |
| terminal-20 | terminal.6 | A PTY's selection mode follows the note's selection mode: the same keys, colours, scroll position and toast after copying | interactive terminal | Select and copy a stretch in a PTY's selection mode and compare with a viewer's selection mode |
| terminal-21 | terminal.4 | A PTY the app opens to run a program for one job (an editor, sudo asking for a password) has no history or selection mode; every key goes to that program, `PgUp` included | PTY | In a PTY running an editor press `PgUp`: the editor pages up itself and the frame does not take the mode colour |
| terminal-22 | terminal.4 | While the subprocess takes the whole screen (vim, less, htop), `PgUp` goes to it and the bottom border has no `PgUp:history`; once it is back on the normal screen, `PgUp` enters the history mode again | interactive terminal | Run `less` in the shell and press `PgUp`: less pages up and the bottom border has no `PgUp:history`; quit less and press `PgUp` again |
| terminal-23 | terminal.4 | While the user gives every key to the subprocess (e.g. a locked cell in sshu), the selection mode steps aside and `PgUp\|PgDn` go straight in; the key that unlocks is always shown, and both modes come back after unlocking | interactive terminal | In an app with such a state: enter it, press `Alt-v` and `PgUp` and check that both reach the subprocess and the bottom border shows the unlocking key; unlock and press them again |
| terminal-24 | terminal.7 | When privileges are raised, the app neither asks for the password nor handles it: it first tries without one, and when one is needed the system's tool asks in a terminal popup that closes itself when done | raising privileges | Do something that needs privileges on a machine that asks for a password; read the code: the password never passes through the app |

## dialog/toast

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| toast-1 | toast.2 | The frame is a popup's frame, always in the layer colour of layer 1 | toast | Bring up a toast with popups stacked and look at the frame's colour |
| toast-2 | toast.2 | A toast is not dimmed | toast | Open a popup while a toast is up: the toast is not dimmed |
| toast-3 | toast.2 | The bottom border is always on the third row from the bottom, so the two bottom rows always stay in sight (normally the panel's bottom border and the footer; with a terminal popup open, the PTY's last row and the terminal's bottom border; the same on a screen without panels) | toast | Bring up a toast once on an ordinary screen and once in a terminal popup; look at which row the bottom border is on |
| toast-4 | toast.2 | The text is centred | toast | Look at where the message sits |
| toast-5 | toast.2 | When too long it wraps, every row centred | toast | Bring up a long toast |
| toast-6 | toast.2 | How many rows at most, the app may decide for itself; when the app sets a limit and a message runs past it, the last row ends with `…` | toast | Bring up a very long toast and look at the rows and the end |
| toast-7 | toast.2 | When the app sets a row limit, the full text of a message that would be cut goes to an error popup or the app's log | toast | Read the code: a long message's full text is also written to an error popup or the log |
| toast-8 | toast.2 | Info: title `nf-fa-flag` (U+F024) `INFO`, text in Text | toast | Bring up an Info toast |
| toast-9 | toast.2 | Warning: title `nf-md-alarm_light` (U+F078F) `WARNING`, text in Peach | toast | Bring up a Warning toast |
| toast-10 | toast.2 | Error: title `nf-md-fire` (U+F0238) `ERROR`, text in Red | toast | Bring up an Error toast |
| toast-11 | toast.2 | Success and Info show for 2200 ms | toast | Time how long a Success and an Info toast stay |
| toast-12 | toast.2 | Warning and Error show for 4400 ms | toast | Time how long a Warning and an Error toast stay |
| toast-13 | toast.2 | A second toast replaces the first at once, and the timer starts over | toast | Bring up two toasts one after the other |
| toast-14 | toast.3 | The hint is `Esc:close` | toast | Look at the toast's bottom border |
| toast-15 | toast.2 | Success: title `nf-md-check_circle` (U+F05E0) `SUCCESS`, text in Green | toast | Bring up a Success toast |
| toast-16 | toast.2 | Whether something finished is told with Success or Info, the app may decide for itself; a failure is always an Error | toast | Complete an action: the toast is a Success or an Info; make an action fail: it is an Error |
| toast-17 | toast.1 | A failure tied to a popup's action, which the user must read before deciding, uses an error popup, not a toast | toast | Make an action in a popup fail: an error popup comes up |
| toast-18 | toast.2 | Done, or still usable, but with something worth noticing uses Warning (e.g. `3 files skipped`) | toast | Run an action that skips part of its work: the toast is a Warning |
| toast-19 | toast.2 | A failed action is always an Error, never a Warning | toast | Make an action fail: the toast is an Error (or an error popup comes up) |

## input/README

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| input-1 | input.1 | opened from a field of a form or a one-value-per-row panel, an error that names the value uses the field's name, not the title; one that can point straight at what is wrong does so | form or one value per row | make the value invalid and press `Enter`; the error row names the field or the wrong part, never the title |
| input-2 | input.1 | an input opened on its own (its title saying what it does, e.g. `RENAME`, `SAVE AS`): an error names the value by the name the app gives besides (e.g. `Name`), never by the title | input | on a popup such as `SAVE AS`, paste a control character and press `Enter`; the error says `Name can't …`, not `Save as can't …` |
| input-3 | input.1 | `Esc`: closes, the value unchanged | input | change the value and press `Esc`; the field keeps the old value |
| input-4 | input.1 | an input popup with a button: the hint says `Tab:actions` on a field and `Tab:fields` on a button | input | look at the hint on the bottom border in both places |
| input-5 | input.2 | there is an explanation row: one sentence saying what to enter, in Overlay0 (a password's unlock look is the exception, see password-24) | text or password or number | open a text, number or password popup and look at the sentence above the typing row |
| input-6 | input.2 (diagram) | the explanation row is above the typing row | text or password or number | look at the order of the rows |
| input-7 | input.2 | there is a blank row between the explanation row and the typing row | text or password or number | count the blank rows between the two |
| input-8 | input.2 | what is being changed goes into the explanation row's sentence (e.g. `New name for assets`) | text or password or number | open a popup such as rename; the explanation row names what is being changed |
| input-78 | input.2 | A long explanation wraps and the popup grows; when it still does not fit at the tallest, the last row ends with `…` | text, password, number | Give the explanation more than the frame's width (e.g. a web page's long prompt): it wraps |
| input-9 | input.2 | the typing row starts with `nf-fa-angle_right` (U+F105), one cell from the border (except a password's unlock option) | text or password or number | look at the typing row's first character and its distance from the left border |
| input-10 | input.2 | a one-line input popup's `nf-fa-angle_right` is always the layer colour | text or password or number | look at the glyph's colour once on opening and once while typing |
| input-11 | input.2 | the value is Lavender | text or password or number | type a few characters and look at the colour |
| input-12 | input.2 | the cursor is one cell, Lavender background with Base text | text or password or number | move the cursor onto a character and look |
| input-13 | input.2 | the hint is `Enter:<verb> Esc:cancel`, the verb saying what pressing it does (rename, create, save) | text or password or number | look at the hint on the bottom border |
| input-14 | input.3 | when the value is longer than the box, the box shows the stretch around the cursor | text or password or number | type a string longer than the box |
| input-15 | input.3 | the side that is cut gets `…` | text or password or number | type a long value, press `Home`, and look at both ends |
| input-16 | input.3 | the cursor is always in sight | text or password or number | in a long value, press `Home`, `End`, `←` and `→` |
| input-17 | input.3 | moving the cursor scrolls by just enough, never pinning the cursor to the middle | text or password or number | in a long value, press `←` all the way from the end and watch the scrolling |
| input-18 | input.3 | cutting counts display width (a CJK character is 2 cells) | text or password or number | type a long CJK value; the border stays straight |
| input-19 | input.3 | cutting never splits a character in two, nor a red `\n` or `\x1b` | text or password or number | paste a long value holding `\x1b` and watch the edges while scrolling |
| input-20 | input.4 | characters and `Space` insert at the cursor (not a password) | input or panel filter | move the cursor to the middle and type |
| input-21 | input.4 | `←\|→` move the cursor one character left / right (not a password) | input or panel filter | press `←` and `→` |
| input-22 | input.4 | `Backspace` deletes the character before the cursor (not a password) | input or panel filter | press `Backspace` with the cursor in the middle |
| input-23 | input.4 | `Delete` deletes the character under the cursor (not a password) | input or panel filter | press `Delete` with the cursor in the middle |
| input-24 | input.4 | a character is what looks like one: a CJK character and an emoji count as one each, and a combining mark counts as one together with the character before it (not a password) | input or panel filter | type CJK, an emoji and a combining mark, then press `←` and `Backspace` |
| input-25 | input.4 | a pasted control character counts as one character each (`←\|→` and `Delete` cross or delete a whole `\x1b` at once) (not a password) | input or panel filter | paste text holding `\x1b` and press `←` and `Delete` |
| input-26 | input.4 | `Ctrl-U` and `Ctrl-W` are not taken | input or panel filter | type, then press `Ctrl-U` and `Ctrl-W`; the value does not change |
| input-27 | input.4 | other `Ctrl-` and `Alt-` combinations do nothing on the typing row and type nothing | input or panel filter | press `Ctrl-A` and `Alt-b`; the value does not change |
| input-28 | input.5 | the grey suggestion is for text and number only (a password shows grey dots, a textarea opens with the old value already in) | input | open a text and a number that have old values: they have a grey suggestion; open a textarea and a password that have old values: neither has one |
| input-29 | input.5 | changing an existing value, the box opens empty and the old value is shown in grey (Overlay0) | text or number | open a field that has an old value |
| input-30 | input.5 | the grey text starts at the cursor's cell: the cursor sits on its first character (Lavender background, Base character), the grey text after it | text or number | on opening, look where the cursor and the grey text are |
| input-31 | input.5 | when the old value's first character is a control character, the cursor's cell is drawn as a control character (Red background, Base text) | text or number | open a field whose old value starts with `\x1b` |
| input-32 | input.5 | `Tab` takes the old value into the box, the cursor at its end | text or number | with grey text, press `Tab`, then change it with `←` |
| input-33 | input.5 | typing straight away: a new value is typed and the grey text hides | text or number | with grey text, type a character |
| input-34 | input.5 | deleting all that was typed brings the grey text back | text or number | type, then delete it all with `Backspace` |
| input-35 | input.5 | `Backspace` on an empty box: the grey text goes (not this value) | text or number | open it and press `Backspace` straight away |
| input-36 | input.5 | once the grey text has gone, `Enter` saves the value empty (where the field cannot be empty, it is handled as an error) | text or number | press `Backspace`, then `Enter`; the field turns empty or an error shows |
| input-37 | input.5 | `Enter` with grey text and nothing touched: the old value is kept and it closes (not saved empty) | text or number | open it and press `Enter` straight away |
| input-38 | input.5 | with grey text the hint adds `Tab:edit Backspace:clear` (e.g. `Enter:rename Tab:edit Backspace:clear Esc:cancel`) | text or number | look at the hint on the bottom border while there is grey text |
| input-39 | input.5 | a grey suggestion has only two sources: the old value, and the suggested value the app gives when there is no old value (no suggestions from history, completion and the like) | input or panel filter | type a few characters and look for any other grey text |
| input-40 | input.7 | an input popup has no placeholder (an empty typing row has no grey explanation) | input | open an input with no old value; the typing row has nothing but the glyph |
| input-41 | input.7 | the `nf-fa-angle_right` before a typing row is not text: it is never taken into the value, and it stays while typing | input or panel filter | type on an empty typing row; the glyph stays |
| input-42 | input.8 | only pasted text counts: pressed `Tab`, `Enter` and `Ctrl-J` keep their own roles and type no control character | input or panel filter | press `Ctrl-J` on the typing row; no `\n` is added to the value |
| input-43 | input.8 | no pasted control character is dropped or turned into a space; they stay in the value | input or panel filter | paste several lines of text |
| input-44 | input.8 | control characters are drawn as they are, in red (Red), never split (not a password) | input or panel filter | paste several lines of text and look at the colour |
| input-45 | input.8 | `\r`, `\n` and `\t` are written by name (2 cells) (not a password) | input or panel filter | paste text holding line breaks and tabs |
| input-46 | input.8 | every other C0, DEL and C1 is written as `\xNN` (4 cells, e.g. `\x1b`, `\x7f`, `\x85`) (not a password) | input or panel filter | paste coloured text copied from a terminal |
| input-47 | input.8 | `\r\n` is drawn as it is, as the two `\r\n` (not a password) | input or panel filter | paste text with CRLF line breaks |
| input-48 | input.8 | in a row drawn grey as a whole (a typing row without the focus, a suggestion), control characters are grey too (not a password) | input or panel filter | with a `\n` on the typing row, move the focus to the list; or look at the grey text of an old value holding a control character |
| input-49 | input.8 | the cursor resting on a control character: the whole control character is drawn with a Red background and Base text (other characters keep the Lavender background) (not a password) | input or panel filter | press `←` onto a `\x1b` |
| input-50 | input.8 | `Backspace` deletes a whole control character at once (not a password) | input or panel filter | with the cursor after a `\x1b`, press `Backspace` once |
| input-51 | input.8 | masked values stay masked (a password with pasted control characters draws only the mask) | password | paste text holding `\n` into a password |
| input-52 | input.8 | values the user did not type (the original name, a value from a file or another program, a value filled back from a list, a default from the start directory, a suggestion…) go through the same filter | input or panel filter | bring in an old value holding `\x1b`: it is drawn in red and refused on confirming; or read the code |
| input-53 | input.8 | a value that is used (submitted, saved, run, handed to another program) is refused on `Enter` while it holds a control character | input | paste several lines and press `Enter`; the popup stays open |
| input-54 | input.8 | when refused, the error row gives the reason and names the value (e.g. `Name can't have control characters`) | input | look at the error row when it is refused |
| input-55 | input.8 | the control character check comes before trimming leading and trailing whitespace (`Icon\r` is caught too) | input | paste `Icon\r` and press `Enter`; it is refused |
| input-56 | input.8 | search and filter typing rows only draw control characters, never refuse | panel filter or finder | paste text holding `\n` on a finder's typing row; it still filters and draws it in red |
| input-57 | input.9 | a one-line value has leading and trailing whitespace trimmed when confirmed (not for a password) | text or number | type `  x ` and confirm; it is saved as `x` |
| input-58 | input.9 | the trim covers every Unicode whitespace character (the ordinary space, the ideographic space U+3000, NBSP…) | text or number | type an ideographic space, `x` and an NBSP, and confirm; it is saved as `x` |
| input-59 | input.10 | a value's colour is Text | form or input | look at a value in a form or on a panel |
| input-60 | input.10 | an empty value is grey text (Overlay0) saying what empty means (e.g. `not set`), not a blank | form or input | clear a field and look |
| input-61 | input.10 | the grey text of an empty value does not teach keys (e.g. no `enter to browse ~/.ssh`) | form or input | look at the text of every empty value |
| input-62 | input.10 | a value too long is cut from the end, with `…` | form or input | fill in a very long value |
| input-63 | input.10 | a path too long is cut from the start (`…/.ssh/id_ed25519`) | file-picker | fill in a very long path |
| input-64 | input.10 | a text shows the value itself; a number shows the value itself, with its unit after a space when it has one, written in full (`10 seconds`) | text or number | look at the value in a form or on a panel |
| input-65 | input.10 | a set password is always 8 `•`; not set, it shows as an empty value | password | look at one password field that is set and one that is not |
| input-66 | input.10 | a textarea shows the first line, with `…` when more follows | textarea | fill in several lines and look at the field |
| input-67 | input.10 | a select shows the chosen option's text | select | look at the field |
| input-68 | input.10 | a checkbox popup's value is the chosen items joined with `, `, with `…` when too long | checkbox | tick a few and look at the field |
| input-69 | input.10 | a reorder's value is the items in their current order joined with `, `, with `…` when too long | reorder | reorder the items and look at the field |
| input-70 | input.10 | a radio or checkbox drawn in a form shows the options themselves | radio or checkbox | look at the form |
| input-71 | input.10 | a date or datetime picker shows the formatted date (and time) | datetime picker | look at the field |
| input-72 | input.10 | a color picker's value shows as a swatch 3 cells wide (`███`), a space, and the hex (`███ #2A2A3C`, the hex always in upper case) | color picker | look at the field |
| input-73 | input.10 | a file-picker shows the path, the home directory written as `~` | file-picker | choose a file under the home directory and look at the field |
| input-74 | input.6 | with no old value and a value suggested by the app, the suggested value shows as a grey suggestion (its look, `Tab`, typing over it, `Backspace` and the hint all as with an old value) | text or number | open a field for something new that has a suggested value (an app with no suggested values never has this case) |
| input-75 | input.6 | with a suggested value, `Enter` with nothing touched uses it: written back and checked as usual (a field that may not be empty does not complain it is empty) | text or number | open a field with a suggested value and press `Enter` at once |
| input-76 | input.10 | a value holding control characters shows them on forms and panels as on the typing row, as red escapes (`\n`, `\t`, `\x1b`), never dropped or turned into spaces | input | give a field a value holding a Tab or `\x1b` and look at it on the form or panel |
| input-77 | input.2 | the typing row's `nf-fa-angle_right` is followed by one space before the value | text or password or number | look between the typing row's glyph and the value |

## input/text

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| text-1 | text.1 | several lines of text use a textarea, not a text | text or textarea | find the fields that take several lines; they open a textarea |
| text-2 | text.1 | a digits-only value uses a number, not a text | text or number | find fields such as a port or seconds; they open a number |
| text-3 | text.1 | a value not shown (a password, a PIN, a passphrase) uses a password | text or password | find the password-like fields; they open a password |

## input/password

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| password-1 | password.2 | the mask option is picked by use: plain for passwords in forms and ordinary password boxes; unlock where the whole box exists to enter this one value (unlocking a screen, PINs, verification codes) | password | compare each password's use with its option |
| password-2 | password.2 | plain option: one `•` per character, left-aligned | password | type a few characters and look |
| password-3 | password.2 | unlock option: one `●` per character, with a space between dots | password | type a few digits and look |
| password-4 | password.2 | unlock option: the dots are centred and grow both ways | password | type one digit at a time; the dots grow both ways |
| password-5 | password.2 | the mask takes the value's colour (Lavender) | password | type a few characters and look at the colour |
| password-6 | password.2 | the 8 grey dots of "a password is already set" use the same option's glyph (plain `•`, unlock `●`) | password | open a field with an old password |
| password-7 | password.2 | when the mask does not fit the box, "When the value is longer than the box" applies, the cursor's end in sight | password | type until the mask is longer than the box |
| password-8 | password.2 | the unlock option's cursor is where the next `●` will appear (a space after the last dot) | password | type 3 digits and look at the cursor |
| password-9 | password.2 | once the last digit is typed, the cursor rests on the last dot (Lavender background, a Base `●`), with no extra cell | password | type up to the limit |
| password-10 | password.2 | centring counts the cursor: n digits typed (not full) take 2n + 1 cells, all N digits 2N − 1 cells | password | measure whether the space left and right is equal |
| password-11 | password.2 | the unlock option has no `nf-fa-angle_right` | password | look at the start of the typing row |
| password-12 | password.3 | with an old password, the box opens empty and always draws 8 grey dots, not the real length | password | open a field whose old password is not 8 characters long |
| password-13 | password.3 | the grey dots start at the cursor's cell: the cursor sits on the first (Lavender background, a Base dot), the other 7 in Overlay0 | password | open a field with an old password and look at the first dot |
| password-14 | password.3 | in the unlock option, the 8 grey dots are a space apart and centred (15 cells) | password | open a box with an old PIN |
| password-15 | password.3 | with nothing typed, `Enter` and `Esc` both keep the old password | password | open it and press `Enter` straight away, then check that the old password still works |
| password-16 | password.3 | typing straight away: it is replaced with a new password, and the dots hide | password | with grey dots, type a character |
| password-17 | password.3 | the hint has no `Tab` | password | look at the hint on the bottom border |
| password-18 | password.4 | with something typed, `Backspace` clears all of it at once, back to the dots (the old password kept) | password | type a few characters and press `Backspace` once |
| password-19 | password.4 | on an empty box, `Backspace` clears the old password and the dots go | password | open it and press `Backspace` straight away |
| password-20 | password.4 | once the dots have gone, `Enter` saves no password | password | press `Backspace`, then `Enter`; the field becomes an empty value |
| password-21 | password.4 | the hint adds `Backspace:clear` | password | look at the hint on the bottom border |
| password-22 | password.4 | characters always go at the end | password | while typing, press `←` and type again; the character still goes at the end |
| password-23 | password.4 | `←\|→`, `Home\|End` and `Delete` do nothing | password | type, then press these keys |
| password-24 | password.2 | the unlock option has no explanation row; the title says what to enter (e.g. `UNLOCK`, `CURRENT PIN`, `NEW PIN`, `CONFIRM PIN`) | password | open a box in the unlock option and look at the explanation row and the title (an app with no unlock option never has this case) |
| password-25 | password.2 (diagram) | inside an unlock-option box: two blank rows, the typing row, a blank row, the error row, 7 rows with the frame | password | count the rows of an unlock-option box |

## input/number

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| number-1 | number.1 | a value with a small range, quicker to pick than to type, uses a slider, not a number | number or slider | find the number fields with a small range; they use a slider |
| number-2 | number.2 | the explanation row gives the range (e.g. `Port, 1-65535`) | number | look at the explanation row |
| number-3 | number.3 | only digits are taken as typed; other keys do nothing | number | type letters and symbols |
| number-4 | number.3 | `-` is taken only if the field allows negatives | number | type `-` in a field that does not allow negatives |
| number-5 | number.3 | `.` is taken only if the field allows decimals | number | type `.` in an integer field |
| number-6 | number.3 | pasting keeps only the characters that are taken | number | paste `a1b2` |
| number-7 | number.3 | no `↑\|↓` stepping | number | press `↑` and `↓`; the value does not change |
| number-8 | number.4 | a range mistake is written in the error row, naming the value (e.g. `Port must be 1-65535`) | number | type a number out of range and press `Enter` |
| number-9 | number.4 | when the field may be empty, an empty value skips the range check and is saved empty | number | clear a number field that may be empty and press `Enter` (an app with no such field never has this case) |
| number-10 | number.2 | with a unit, a unit row sits below the typing row: the word in full (`seconds`, not `s`), Overlay0, lined up with the value's first cell, not moving as you type | number | open a number field with a unit and type a few digits, watching the unit row (an app with no units never has this case) |
| number-11 | number.2 | with a unit row, the width counts the unit row among the widest rows | number | measure the frame of a number field with a unit |

## input/select

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| select-1 | select.2 | the finder's skeleton, without a preview | select | open a select |
| select-2 | select.2 | the typing row is always shown, even for a short list | select | open a select with few options |
| select-3 | select.3 | it opens with the focus on the list | select | open it; the hint is the list's hint |
| select-4 | select.3 | it opens with the cursor on the current value | select | open a field that has a value |
| select-5 | select.3 | the list's hint is `Enter:choose Tab\|/:filter Esc:cancel` | select | look at the hint on the bottom border |

## input/radio

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| radio-1 | radio.1 | one of five options or fewer is drawn straight in the form or the panel (radio) | radio or select | find the single-choice fields with five options or fewer |
| radio-2 | radio.1 | one of more than five options uses a select | radio or select | find the single-choice fields with more than five options |
| radio-3 | radio.2 | chosen `nf-md-radiobox_marked` (U+F043E), not chosen `nf-md-radiobox_blank` (U+F043D) | radio | look at the glyph before each option |
| radio-4 | radio.2 | the chosen one's text is Green, the others Text | radio | look at the options' colours |
| radio-5 | radio.2 | always down, one option a row | radio | look at how the options are laid out |
| radio-6 | radio.2 (diagram) | the second option on starts in the same column as the first (the glyphs line up) | radio | look at the options' left edges |
| radio-7 | radio.3 | each option is an item; `j\|k` (or `h\|l`) move between the options | radio | press `j` and `k` on the options |
| radio-8 | radio.3 | `Enter` chooses it; the focus stays | radio | press `Enter` on an option not chosen |
| radio-9 | radio.3 | a choice takes effect at once, with no separate confirming | radio | press `Enter` and look at the effect |

## input/checkbox

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| checkbox-1 | checkbox.1 | a switch and a group of five or fewer are drawn straight in the form or the panel and flip in place | checkbox | find the switches and the multi-choice fields with five options or fewer |
| checkbox-2 | checkbox.1 | more than five to tick open a checkbox popup | checkbox | find the multi-choice fields with more than five options |
| checkbox-3 | checkbox.2 | ticked `nf-md-checkbox_marked` (U+F0132), not ticked `nf-md-checkbox_blank_outline` (U+F0131); the same in a form, on a panel and on every row of a checkbox popup | checkbox | look at the glyph before each option |
| checkbox-4 | checkbox.2 | a ticked one's text is Green | checkbox | look at the colour of ticked options |
| checkbox-5 | checkbox.2 | an option not available is drawn in its place, not hidden (an option not available is not a disabled one) | checkbox | check that options not available are still in the list |
| checkbox-6 | checkbox.2 | an option not available is Surface2 all along the row, the tick too (not Green even when ticked) (an option not available is not a disabled one) | checkbox | look at options not available, ticked and not ticked |
| checkbox-7 | checkbox.2 | under the cursor, an option not available is drawn as the cursor block, like any other row (an option not available is not a disabled one) | checkbox | move onto an option not available |
| checkbox-8 | checkbox.2 | the checkbox popup is the finder's skeleton, without a preview | checkbox | open a checkbox popup |
| checkbox-9 | checkbox.4 | in a form or a panel, `Enter` flips it in place; the focus stays | checkbox | press `Enter` on a checkbox |
| checkbox-10 | checkbox.4 | in a form or a panel, a flip takes effect at once | checkbox | flip it and look at the effect |
| checkbox-11 | checkbox.4 | the checkbox popup opens with the focus on the list | checkbox | open it; the hint is the list's hint |
| checkbox-12 | checkbox.4 | it opens with the cursor on the option the app names, the first option when none is named (not `Select all`) | checkbox | open it and look at the cursor; or read the code |
| checkbox-13 | checkbox.4 | `Space` changes only the tick on screen; nothing is written back and nothing takes effect | checkbox | press `Space`; the screen underneath does not change |
| checkbox-14 | checkbox.4 | `Enter` writes back the whole set currently ticked at once and closes the popup; only then does it take effect | checkbox | tick two options and press `Enter` |
| checkbox-15 | checkbox.4 | opened on its own, it applies only on `Enter` | checkbox | look at what it applies to before and after `Enter` |
| checkbox-16 | checkbox.4 | `Esc` cancels: none of the ticks count, and the value stays as it was when opened | checkbox | change the ticks, press `Esc`, then open it again and look |
| checkbox-17 | checkbox.4 | the cursor stops on an option not available (an option not available is not a disabled one) | checkbox | move past an option not available with `j\|k` |
| checkbox-18 | checkbox.4 | an option not available can still be ticked or unticked (`Space` in a popup, `Enter` in a form or a panel) (an option not available is not a disabled one) | checkbox | flip an option not available |
| checkbox-19 | checkbox.4 | `Enter` in a popup writes back the ticks on screen, options not available included (an option not available is not a disabled one) | checkbox | tick an option not available, press `Enter`, and look at the value |
| checkbox-20 | checkbox.4 | when filtering, options not available are listed in the results too (an option not available is not a disabled one) | checkbox | type to filter down to an option not available |
| checkbox-21 | checkbox.4 | the list's hint is `Enter:apply Space:toggle Tab\|/:filter Esc:cancel` | checkbox | look at the hint on the bottom border |
| checkbox-22 | checkbox.4 | filtered down to no results, `Enter` on the list still writes back the whole set ticked (ticks filtered out count too) | checkbox | tick two options, type until there are no results, go to the list and press `Enter`; both are written back |
| checkbox-23 | checkbox.4 | filtered down to no results, the list's hint drops `Space`: `Enter:apply Tab\|/:filter Esc:cancel` | checkbox | type until there are no results, go to the list and look at the bottom border |
| checkbox-24 | checkbox.4 | `Enter` in a checkbox popup with nothing changed: no change, and it closes | checkbox | Open a checkbox popup and press `Enter` without changing anything |
| checkbox-25 | checkbox.4 | On a one-value-per-row panel with the focus on a checkbox, the hint is `Enter:toggle` (`Space` on a panel opens the Space menu and does not flip it) | one value per row + checkbox | Look at the panel's bottom-border hint |
| checkbox-26 | checkbox.3 | A group of options (in a form, on a panel and in a checkbox popup) has `Select all` as its first row, drawn with the options' glyphs and colours, the focus and the cursor stopping on it; a switch has none | checkbox | Look at every group's first row and move onto it |
| checkbox-27 | checkbox.3 | `Select all` is not an option: not part of the value, not counted towards the five; the app has no option of its own standing for all | checkbox | Tick them all and write back, `Select all` is not in the value; look for an "All"-like option |
| checkbox-28 | checkbox.3 | Ticking `Select all` ticks every option, unticking it unticks them all, options not available included; it takes effect when an option would (in a popup only on `Enter`) | checkbox | Flip `Select all` twice and look at every row |
| checkbox-29 | checkbox.3 | `Select all` is ticked only while every option is: unticking one unticks it, ticking them all one by one ticks it, and it opens ticked when all are | checkbox | Tick all, untick one row, tick it back |
| checkbox-30 | checkbox.3 | While the checkbox popup's typing row holds text, `Select all` is not drawn; it comes back when the text is cleared | checkbox | Type a letter and look at the first row, then clear it |
| checkbox-31 | checkbox.3 | The options sit two cells further in than `Select all`; while a filter hides it, they stay where they are | checkbox | Look at the options' left edge; type a letter and see they do not move |
| checkbox-32 | checkbox.3 | Disabled options are not flipped by `Select all` and not counted in "every option ticked"; with every option disabled, it is disabled too | checkbox | Flip `Select all` with a disabled option in the group |
| checkbox-33 | checkbox.3 | The focus and the cursor never start on `Select all`: a form opening, a popup with no option named and landing on the field all stop on an option | checkbox | Open a form whose first field is a checkbox group and a checkbox popup, looking at where they start |

## input/slider

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| slider-1 | slider.1 | a value that needs an exact number typed uses a number, not a slider | number or slider | find the fields that need an exact number; they use a number |
| slider-2 | slider.2 | in a form or a panel, a slider is drawn as a track and the number | slider | look at the field |
| slider-3 | slider.2 | the track is a heavy line `━` | slider | look at the track's character |
| slider-4 | slider.2 | `●` is drawn where the value is (on the track, further right for a larger value) | slider | change the value and watch the `●` move |
| slider-5 | slider.2 (diagram) | the number follows the track after a space | slider | look between the track and the number |
| slider-6 | slider.3 | `Enter` opens a select whose options are the numbers from bottom to top, one per step | slider | press `Enter` on a slider; look at the list's first and last options and the gap between them |
| slider-7 | slider.3 | no keys drag it in place: `h\|l` and `←\|→` do not change the value | slider | press `h` and `l` on a slider |
| slider-8 | slider.4 | every slider has three attributes, bottom, top and step | slider | read the code |
| slider-9 | slider.4 | an unset step is `(top − bottom) / 10` | slider | read the code; or open the select of a slider with no step set and count the options |

## input/textarea

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| textarea-1 | textarea.1 | content where a line is a line, such as code and config files, goes to the user's `$EDITOR`, not to a textarea | textarea | find where such content is edited; it opens `$EDITOR` |
| textarea-2 | textarea.2 | a line wider than the box wraps onto the next row, never scrolling sideways | textarea | type a line wider than the box |
| textarea-3 | textarea.2 | wrapping is only on screen; no line break is added to the value | textarea | save and look at the value; or read the code |
| textarea-4 | textarea.2 | wrapping counts display width (a wide character is 2 cells) | textarea | type a long line of CJK text; no row runs past the box and the border stays straight |
| textarea-5 | textarea.2 | the first row of each line carries its line number | textarea | type a few lines and look at the left |
| textarea-6 | textarea.2 | line numbers are right-aligned, followed by a space | textarea | type up to line 10 and look at the alignment |
| textarea-7 | textarea.2 | wrapped rows leave the number column blank | textarea | look at the second row of a wrapped line |
| textarea-8 | textarea.2 | line numbers are Overlay0, the cursor's line number Text | textarea | move the cursor and look at the line numbers' colours |
| textarea-9 | textarea.2 | the number column is max(2, the digits of the largest number) wide: lines 1–99 never shift | textarea | type up to line 10; the content does not move right |
| textarea-10 | textarea.2 | there is no limit on the number of lines | textarea | paste many lines; or read the code |
| textarea-11 | textarea.2 | the box's height takes the maximum of Rules F7 (the screen height − 2), even with a short old value | textarea | open a field whose old value is one line and measure the box's height |
| textarea-12 | textarea.2 | content taller than the box scrolls inside it, the cursor always in view | textarea | paste content taller than the box and move up and down |
| textarea-13 | textarea.2 | in Write, the cursor is one cell of Lavender background with Base text | textarea | open it and look at the cursor |
| textarea-14 | textarea.2 | in Move, the cursor is one cell of the layer colour background with Base text | textarea | press `Esc` and look at the cursor |
| textarea-15 | textarea.2 | the value's text is Lavender in both states | textarea | look at the content's colour |
| textarea-16 | textarea.2 | in either state, the cursor resting on a control character draws the whole control character with a Red background and Base text | textarea | paste `\x1b`, then move onto it once in Write and once in Move |
| textarea-17 | textarea.2 | a `\t` in the value is drawn as `input_tab_width` spaces, not aligned to any column | textarea | paste text holding a `\t` |
| textarea-18 | textarea.3 | it opens in Write | textarea | open it and type straight away |
| textarea-19 | textarea.3 | the hint in Write is `Esc:move` | textarea | look at the hint on the bottom border |
| textarea-20 | textarea.3 | in Move, `i` starts writing before the cursor, `a` after the cursor, and `o` opens a new line below and writes there (as in vim) | textarea | press each once in Move |
| textarea-21 | textarea.3 | the hint in Move is `Enter:save i:write Esc:cancel` | textarea | look at the hint on the bottom border |
| textarea-22 | textarea.3 | it opens with the old value already in, the cursor at its end | textarea | open a field that has an old value |
| textarea-23 | textarea.3 | `Esc` in Move closes it | textarea | with the content unchanged, press `Esc` in Move |
| textarea-24 | textarea.3 | in Write, `↑\|↓` go to the row above or below (rows as drawn, a wrapped row counting as one) | textarea | press `↓` on a wrapped line |
| textarea-25 | textarea.3 | in Write, `←\|→` at the start or end of a line cross to the previous or next line | textarea | press `→` at the end of a line |
| textarea-26 | textarea.3 | `Backspace` at the start of a line joins it to the line above | textarea | press `Backspace` at the start of the second line |
| textarea-27 | textarea.3 | in Write, `Home` and `End` go to the start and the end of the whole text | textarea | press `Home` and `End` on a line in the middle |
| textarea-28 | textarea.3 | a pasted `\n`, `\r\n` or lone `\r` is a real line break | textarea | paste text with each of the three line breaks |
| textarea-29 | textarea.3 | other pasted control characters are kept in the value and drawn in red | textarea | paste coloured text from a terminal |
| textarea-30 | textarea.3 | `Backspace` deletes a whole control character at once | textarea | press `Backspace` once after a `\x1b` |
| textarea-31 | textarea.3 | while the value holds a control character, confirming (`Enter` in Move) is held back and nothing is saved | textarea | paste `\x1b`, then press `Enter` in Move |
| textarea-32 | textarea.3 | when held back, the error row names the value (e.g. `Notes can't have control characters`) | textarea | look at the error row when it is held back |
| textarea-33 | textarea.3 | line breaks and `\t` do not count as control characters and are not held back | textarea | paste several lines holding a `\t` and confirm; it saves |
| textarea-34 | textarea.3 | `Backspace` removes the spaces `Tab` inserted one at a time | textarea | press `Tab`, then `Backspace` once |
| textarea-35 | textarea.3 | a pasted `\t` is kept as it is, not turned into spaces | textarea | paste text holding a `\t`, save, and look at the value |
| textarea-36 | textarea.3 | movement in Move follows Rules K12: `h\|j\|k\|l`, `w\|b\|e`, `0\|$`, `u\|d`, `gg\|G` | textarea | press each in Move |

## input/color-picker

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| color-picker-1 | color-picker.2 | One row, left to right: old, new, R, G, B | color picker | Open a color picker |
| color-picker-2 | color-picker.2 | The old and new swatches are 8 cells wide and 2 rows tall | color picker | Measure the swatches |
| color-picker-3 | color-picker.2 | old is the colour it opened with, never changing | color picker | Change R, then look at old |
| color-picker-4 | color-picker.2 | new follows R, G and B as they change | color picker | Change R, then look at new |
| color-picker-5 | color-picker.2 | Under old and new: `old`, `new` and each one's hex | color picker | Look at the two rows under the swatches |
| color-picker-6 | color-picker.2 | R, G and B are small swatches (3 cells wide, 1 row tall), not sliders | color picker | Measure the swatches |
| color-picker-7 | color-picker.2 | Each R, G and B swatch is drawn in its channel's own colour (R is `#RR0000`) | color picker | Look at the colours of the three small swatches |
| color-picker-8 | color-picker.2 | Under R, G and B, its value, always in hex | color picker | Look at the values under the channels |
| color-picker-9 | color-picker.2 (diagram) | The R, G and B swatches are on the same row as the second row of the old and new swatches (bottom edges aligned) | color picker | Look at which row the small swatches are on |
| color-picker-10 | color-picker.2 (diagram) | Under the swatches, a row of names and a row of hex, each aligned with its own swatch's left edge | color picker | Look at the left edges of the names and the hex |
| color-picker-11 | color-picker.2 | The action area: a separator under the content, and one button on the right, `Choose` | color picker | Look at the lower part of the box |
| color-picker-12 | color-picker.2 (diagram) | One blank row between the hex row and the separator | color picker | Count the blank rows between the hex row and the separator |
| color-picker-13 | color-picker.2 | `Choose` is on the right, one cell from the border | color picker | Look at the distance between the button and the right border |
| color-picker-14 | color-picker.3 | The four items R, G, B and `Choose` take the focus | color picker | Go through with `Tab` and hjkl; the focus stops only on these four |
| color-picker-15 | color-picker.3 | hjkl move only among R, G and B: `h\|l` left and right, `j\|k` back and on too | color picker | Press `h`, `l`, `j`, `k` on R, G, B |
| color-picker-16 | color-picker.3 | `Choose` is reached only with `Tab`: hjkl never move to `Choose` | color picker | Press `l` on B: it goes back to R, not to `Choose`; only `Tab` reaches `Choose` |
| color-picker-17 | color-picker.3 | It opens with the focus on R | color picker | Look after opening |
| color-picker-18 | color-picker.3 | With the focus on a channel, both rows under it, the name and the hex, are drawn as a cursor (layer colour background, Base bold) | color picker | Look with the focus on G |
| color-picker-19 | color-picker.3 | A channel's cursor is as wide as the swatch above (3 cells × 2 rows) | color picker | Measure the cursor block |
| color-picker-20 | color-picker.3 | `Enter` on R, G or B opens a select of numbers: 00–FF, step 1, the cursor on the current value | color picker | Press `Enter` on R |
| color-picker-21 | color-picker.3 | Every row of that select is in hex, with the decimal in brackets (`2A (42)`) | color picker | Look at the rows of the list |
| color-picker-22 | color-picker.3 | Typing filters by hex or decimal alike | color picker | Type `2A`, then type `42` |
| color-picker-23 | color-picker.3 | Back from choosing, new changes with it | color picker | Choose a value, then look at new |
| color-picker-24 | color-picker.3 | Back from choosing, the focus stays on that channel | color picker | Choose a value, then look at the focus |
| color-picker-25 | color-picker.3 | `Enter` on `Choose`: confirms, writes back and closes | color picker | Press `Enter` on `Choose` |
| color-picker-26 | color-picker.3 | The hint on R, G, B is `Enter:edit Tab:actions Esc:cancel` | color picker | Look at the hint on the bottom border |
| color-picker-27 | color-picker.3 | The hint on `Choose` is `Enter:choose Tab:fields Esc:cancel` | color picker | Look at the hint on the bottom border |
| color-picker-28 | color-picker.2 | With no value to begin with, old has no swatch and reads `none` (Overlay0); new starts at `#000000` | color picker | Open a colour field that is unset (an app whose colours are always set never has this case) |
| color-picker-29 | color-picker.3 | With no value to begin with, `Choose` always counts as a change: written back even when new is `#000000` | color picker | Open an unset colour field and press `Choose` without changing anything: the value becomes `#000000` |
| color-picker-30 | color-picker.4 | Hex is always written in upper case, however the file stores it: in the color picker, on forms and on panels | color picker | Store a lower-case hex in the config file and look at the hex in the color picker and on the panel |

## input/datetime-picker

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| datetime-picker-1 | datetime-picker.2 (the date) (diagram) | The month and year row is at the top, the weekday row right under it, then the calendar right under that, with no blank rows between | datetime picker | Look at the order of the content rows |
| datetime-picker-2 | datetime-picker.2 (the date) (diagram) | The weekday row is in Overlay0 | datetime picker | Look at the weekdays' colour |
| datetime-picker-3 | datetime-picker.2 (the date) | The calendar is aligned left, one cell from the border, with no indent of its own | datetime picker | Look at the distance between the calendar's left edge and the border |
| datetime-picker-4 | datetime-picker.2 (the date) | Each day takes 4 cells: the date in 2 (aligned right) plus a gap of 2 | datetime picker | Look at how one-digit and two-digit dates line up |
| datetime-picker-5 | datetime-picker.2 (the date) | The weekdays follow the same 4-cell grid | datetime picker | Look at the weekdays lining up with the dates under them |
| datetime-picker-6 | datetime-picker.2 (the date) | The calendar always draws 6 rows, keeping the unused rows all the same | datetime picker | Turn to a month that spans only 4 or 5 weeks; the box's height does not change |
| datetime-picker-7 | datetime-picker.2 (the date) | The day under the cursor is the day to be written back (there is no "chosen but not yet confirmed" state) | datetime picker | Move to a day and confirm; that day is what is written back |
| datetime-picker-8 | datetime-picker.2 (the date) | The field's original value is in Green | datetime picker | Open a field with a value, move the cursor away and look at the original day |
| datetime-picker-9 | datetime-picker.2 (the date) | The cursor opens on the original value, or on today when there is no value | datetime picker | Open a field with a value and a field without one |
| datetime-picker-10 | datetime-picker.2 (the date) | Today is underlined, with no colour of its own | datetime picker | Look at today |
| datetime-picker-11 | datetime-picker.2 (the date) | Weekends get no colour of their own | datetime picker | Look at Saturday and Sunday |
| datetime-picker-12 | datetime-picker.2 (the date) | Days outside the range are in Surface2 | datetime picker | Turn to a month at the edge of the range |
| datetime-picker-13 | datetime-picker.2 (date and time) | Date and time: a vertical separator on the right sets off an area for the time | datetime picker | Open a datetime picker |
| datetime-picker-14 | datetime-picker.2 (date and time) | A date-only picker has no time area | datetime picker | Open a date picker |
| datetime-picker-15 | datetime-picker.2 (date and time) | Two blank cells on each side of the separator | datetime picker | Count the blank cells on both sides of the separator |
| datetime-picker-16 | datetime-picker.2 (date and time) | The time is split into two columns, hour and minute | datetime picker | Look at the time area |
| datetime-picker-17 | datetime-picker.2 (date and time) | Hours are 00–23 | datetime picker | Go round the hour column once |
| datetime-picker-18 | datetime-picker.2 (date and time) | Minutes are one step every 5 minutes (00–55) | datetime picker | Go round the minute column once |
| datetime-picker-19 | datetime-picker.2 (date and time) | The time area has no search (it is not a finder) | datetime picker | Type digits in the time area; nothing is filtered |
| datetime-picker-20 | datetime-picker.2 (date and time) | The current hour and minute are in Green | datetime picker | Open a field with a value and look |
| datetime-picker-21 | datetime-picker.2 (date and time) (diagram) | The two time columns are as tall as the left side (from the month and year row to the calendar's 6th row), scrolling beyond | datetime picker | Look at the first and last rows of the time columns |
| datetime-picker-22 | datetime-picker.2 (date and time) (diagram) | The hour and minute columns each scroll on their own: when it opens, each scrolls by as little as needed for the current value to show (e.g. 10:05 shows hours 03–10 and minutes 00–35); a column is not drawn as a ring (00 does not follow 55) | datetime picker | Open a field whose value is 10:05, and look at the first and last rows of both columns |
| datetime-picker-23 | datetime-picker.2 (date and time) | When the current value falls between steps (10:07), the cursor opens on the nearest step before it (10:05) | datetime picker | Open a field whose value is 10:07 |
| datetime-picker-24 | datetime-picker.2 (date and time) | In the area holding the focus the cursor has the layer colour background; in the area without the focus, the cursor is the layer colour cursor, dimmed once more | datetime picker | `Tab` between the calendar and the time, and look at both areas' cursors |
| datetime-picker-25 | datetime-picker.2 (date and time) | Within the time area, the cursor of the column without the focus is dimmed once more too (the whole picker has one lit cursor) | datetime picker | Press `h`, `l` in the time area, and look at both columns' cursors |
| datetime-picker-26 | datetime-picker.3 | What can take the focus: month, year, calendar, time (no time in a date-only picker) | datetime picker | Go round once with `Tab` |
| datetime-picker-27 | datetime-picker.3 | The picker's own operations use only `Tab`, hjkl (the arrow keys), `Enter`, `Esc` and `t`, with no keys of their own for changing the month or the year (core keys `?`, `q` / `Ctrl-C` follow input/README) | datetime picker | Press `p`, `n` and other letters; the month does not change, and nothing else happens |
| datetime-picker-28 | datetime-picker.3 | `Tab` moves the focus in screen order: month → year → calendar → time → back to month | datetime picker | Press `Tab` again and again from the calendar |
| datetime-picker-29 | datetime-picker.3 | It opens with the focus on the calendar | datetime picker | Look at the hint after opening |
| datetime-picker-30 | datetime-picker.3 | On the month or the year, `h\|l` (`←\|→`) go to the previous or next month or year | datetime picker | Press `l` on the month |
| datetime-picker-31 | datetime-picker.3 | When the month or the year changes, the calendar turns with it, the cursor on the same day; on the last day when that month has no such day | datetime picker | Change to February while on the 31st |
| datetime-picker-32 | datetime-picker.3 | On the calendar, `h\|l` go a day back or on, `j\|k` a week back or on | datetime picker | Press `h`, `l`, `j`, `k` on the calendar |
| datetime-picker-33 | datetime-picker.3 | On the calendar, crossing the month's end goes into the next month naturally | datetime picker | Press `l` at the end of the month |
| datetime-picker-34 | datetime-picker.3 | Days outside the range are skipped, stopping on the next day within the range in that direction | datetime picker | Move in a direction with days outside the range in between |
| datetime-picker-35 | datetime-picker.3 | When there is no day within the range left in that direction, it does not move | datetime picker | Press `l` on the latest day |
| datetime-picker-36 | datetime-picker.3 | On the time, `j\|k` move within a column, `h\|l` switch between the hour and minute columns | datetime picker | Press `j`, `l` in the time area |
| datetime-picker-37 | datetime-picker.3 | Each column wraps on its own: minutes wrapping do not move the hour, and hours wrapping do not move the date | datetime picker | Press `j` with the minute on 55 and look at the hour; press `j` with the hour on 23 and look at the date |
| datetime-picker-38 | datetime-picker.3 | `Enter` on the month or the year: moves the focus to the calendar, choosing nothing | datetime picker | Press `Enter` on the month |
| datetime-picker-39 | datetime-picker.3 | In a date-only picker, `Enter` on the calendar confirms (writes back and closes) | datetime picker | Press `Enter` on the calendar |
| datetime-picker-40 | datetime-picker.3 | In a datetime picker, `Enter` on the calendar moves the focus to the time | datetime picker | Press `Enter` on the calendar |
| datetime-picker-41 | datetime-picker.3 | `Enter` on the time: confirms, writing back the day under the calendar's cursor plus the step under the time's cursor, and closes | datetime picker | Press `Enter` on the time and look at the value written back |
| datetime-picker-42 | datetime-picker.3 | `t` jumps the date to today, from any area | datetime picker | Press `t` once each on the month, the year and the calendar |
| datetime-picker-43 | datetime-picker.3 | `t` pressed on the time also jumps the time's cursor to now (the minute rounded down to the nearest 5) | datetime picker | Press `t` on the time |
| datetime-picker-44 | datetime-picker.3 | The hint on the calendar (datetime) is `Enter:time t:today Tab:time Esc:cancel` | datetime picker | Look at the hint on the bottom border |
| datetime-picker-45 | datetime-picker.3 | The hint on the calendar (date only) is `Enter:choose t:today Tab:month Esc:cancel` | datetime picker | Look at the hint on the bottom border |
| datetime-picker-46 | datetime-picker.3 | The hint on the month is `Enter:days h\|l:month t:today Tab:year Esc:cancel` | datetime picker | Look at the hint on the bottom border |
| datetime-picker-47 | datetime-picker.3 | The hint on the year is `Enter:days h\|l:year t:today Tab:days Esc:cancel` | datetime picker | Look at the hint on the bottom border |
| datetime-picker-48 | datetime-picker.3 | The hint on the time is `Enter:choose t:today Tab:month Esc:cancel` | datetime picker | Look at the hint on the bottom border |

## input/finder

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| finder-1 | finder.2 | The typing row on top, the list below | finder | Open a finder |
| finder-2 | finder.2 | A separator between the typing row and the list, not joining the border | finder | Look at both ends of the separator |
| finder-3 | finder.2 (diagram) | The typing row, the separator and the list follow one another, with no blank rows between | finder | Look at the order of the content rows |
| finder-4 | finder.2 | The typing row starts with `nf-fa-angle_right` (U+F105), one cell from the border | finder | Look at the first character of the typing row |
| finder-5 | finder.2 | The glyph's colour: Overlay0 with the focus on the list, the layer colour with the focus on the typing row | finder | Press `Tab` back and forth and look at the glyph |
| finder-6 | finder.2 | The filtered count `matches/total` (`3/41`) sits on the right of the typing row | finder | Look after typing to filter |
| finder-7 | finder.2 | The count is in Overlay0 | finder | With the focus on the typing row, look at the count's colour |
| finder-8 | finder.2 (diagram) | The count is on the right, one cell from the border | finder | Look at the distance between the count and the right border |
| finder-9 | finder.2 | A plain finder always has a preview | finder with a preview | Open a plain finder |
| finder-10 | finder.2 | The preview follows the entry under the cursor | finder with a preview | Move the cursor; the preview changes |
| finder-11 | finder.2 | When it previews something other than a file or a directory, there is no metadata | finder with a preview | Look at the preview box |
| finder-12 | finder.2 | The list and the preview together take one popup's width (the maximum of Rules F7) | finder with a preview | Measure the width of the two boxes together |
| finder-13 | finder.2 | Terminal width 96 or more: the list and the preview side by side, half each | finder with a preview | Open it at 96 columns or more |
| finder-14 | finder.2 | Terminal width 96 or more, with metadata: the right box is "preview / separator / metadata" | finder with a preview | Open it at 96 columns or more |
| finder-15 | finder.2 (diagram) | In the right box the preview takes the height left at the top; the separator and the four metadata rows are at the bottom | finder with a preview | Look at the order of the rows in the right box |
| finder-16 | finder.2 | Under 96, with metadata: the top row is the list box and the metadata box, half each | finder with a preview | Open it at 80 columns |
| finder-17 | finder.2 | Under 96, with metadata: below them the preview box takes the full width | finder with a preview | Open it at 80 columns |
| finder-18 | finder.2 | Under 96, with metadata: top and bottom take half the height each | finder with a preview | Measure the heights of the top and bottom rows of boxes |
| finder-19 | finder.2 | When the metadata has a box of its own, it is titled `INFO` | finder with a preview | Open it at 80 columns and look at the title |
| finder-20 | finder.2 (diagram) | The `INFO` box's bottom border carries no text | finder with a preview | Open it at 80 columns and look at the bottom border of `INFO` |
| finder-21 | finder.2 | At 80×24 the list shows 5 entries and the preview 7 rows | finder with a preview | Open it at 80×24 and count the rows |
| finder-22 | finder.2 | Under 96, without metadata: stacked, the list on top and the preview below, half each | finder with a preview | Open it at 80 columns |
| finder-23 | finder.2 (diagram) | One blank cell between the two boxes side by side | finder with a preview | Look between the two boxes |
| finder-24 | finder.2 (diagram) | When the width does not split evenly side by side, the right box gets one cell more (96 wide: 46 + 1 + 47; 80 wide: 38 + 1 + 39) | finder with a preview | Measure the widths of the two boxes |
| finder-25 | finder.2 (diagram) | No blank row between the top and bottom rows of stacked boxes | finder with a preview | Open it at 80 columns and look between top and bottom |
| finder-26 | finder.2 | The preview box's title is the chosen entry's name (or where it is) | finder with a preview | Look at the preview box's title |
| finder-27 | finder.2 | The preview takes no focus | finder with a preview | Press `Tab` back and forth; the focus never reaches the preview |
| finder-28 | finder.2 | The preview box's border and title capsule are in the layer colour | finder with a preview | Look at the preview box's colours |
| finder-29 | finder.2 | The preview's content is not dimmed | finder with a preview | Look at the preview's content with the focus on the typing row and on the list |
| finder-30 | finder.2 | The preview box's bottom border carries no text (no hint, no scroll position) | finder with a preview | Look at the preview box's bottom border |
| finder-31 | finder.2 | Listed while searching: results are listed as they arrive | finder | Open it on a large search scope |
| finder-32 | finder.2 | While it is still searching, a loading icon after the title | finder | Look at the title during a search |
| finder-33 | finder.2 | While none has arrived it reads `(indexing…)` | finder | Look at the list just after opening |
| finder-34 | finder.2 | A finder with a preview always takes the maximum height of Rules F7 (the screen height − 2); a short list leaves space below | finder with a preview | Measure the box's height when there are few results |
| finder-35 | finder.3 | Every row of a select starts with a radio glyph: chosen U+F043E, not chosen U+F043D | select | Look at the start of every row in the list |
| finder-36 | finder.3 | The current value's text is in Green | select or checkbox | Look at the current value's row |
| finder-37 | finder.3 | Every row's text lines up | select or checkbox | Look at the left edge of each row's text |
| finder-38 | finder.3 | With the cursor on the current value, the background is the cursor's and the text the cursor's Base | select or checkbox | Move the cursor onto the current value |
| finder-39 | finder.3 | In a checkbox popup Green follows the tick on screen: Green as soon as `Space` ticks it, not Green once unticked, before `Enter` as well | checkbox | Press `Space` and look at the text colour |
| finder-40 | finder.4 | With the focus on the typing row, the typing row is drawn as an input's typing row: the value Lavender, with a cursor | finder | Look with the focus on the typing row |
| finder-41 | finder.4 | With the focus on the typing row, the list's cursor is the layer colour cursor, dimmed once more | finder | With the focus on the typing row, look at the list |
| finder-42 | finder.4 | With the focus on the list, the whole typing row is Overlay0 (the count included), with no cursor | finder | With the focus on the list, look at the typing row |
| finder-43 | finder.5 | A plain finder opens with the focus on the typing row | finder with a preview | Open a plain finder and type straight away; the text goes into the typing row |
| finder-44 | finder.6 | Typing filters the list at once | panel filter or finder | Type and look at the list |
| finder-45 | finder.6 | On the typing row, `↑\|↓` move the cursor between results | panel filter or finder | Press `↓` on the typing row |
| finder-46 | finder.7 | Matching is case-insensitive | panel filter or finder | Type `READ`; `README` is found |
| finder-47 | finder.7 | What is typed must appear unbroken in the item (merely holding those letters in order does not count) | panel filter or finder | Type `prod`; `db-replica-tokyo-ap-northeast-1` is not in the results |
| finder-48 | finder.7 | Each word separated by spaces must appear, in any order | panel filter or finder | Type `me read` |
| finder-49 | finder.7 | The results keep the list's own order and are not reordered | panel filter or finder | Type, then check that the results are in the list's order |
| finder-50 | finder.7 | In the list's order, numbers sort by value (`9` before `10`), text as text | panel filter or finder | Look at the order of a list with numbers in it (a list with no numbers never has this case) |
| finder-51 | finder.8 | `Enter` in the list: goes there (a select chooses, a checkbox popup applies, a file-picker chooses the file or goes into the directory) | finder | Press `Enter` in the list |
| finder-52 | finder.8 | With no results (a search still listing as it goes, before the first result arrives, included), `Enter` in the list does nothing (a checkbox popup excepted) | select or finder or file-picker | Type until there are no results, `Tab` to the list and press `Enter`; nothing happens |
| finder-53 | finder.8 | `Tab\|/` in the list: back to the typing row | finder | Press `Tab` and `/` in the list |
| finder-54 | finder.8 | Back on the typing row, typing goes on after the old text (it is not cleared) | finder | Filter, go to the list, then press `/` and type |
| finder-55 | finder.9 | The typing row's hint is `Enter\|Tab:list Esc:cancel` | finder | With the focus on the typing row, look at the bottom border |
| finder-56 | finder.9 | The list's hint is `Enter:<the verb for going there> Tab\|/:filter Esc:cancel` | finder | With the focus on the list, look at the bottom border |
| finder-57 | finder.9 | With no results (a search still listing as it goes, before the first result arrives, included), the typing row's hint drops `Enter`: `Tab:list Esc:cancel`, and puts it back once there are results | select or checkbox or finder or file-picker | Type until there are no results and look at the bottom border; delete text until there are results and look again |
| finder-58 | finder.9 | With no results, the list's hint drops `Enter`: `Tab\|/:filter Esc:cancel` | select or finder or file-picker | Type until there are no results, `Tab` to the list and look at the bottom border |
| finder-59 | finder.2 | The typing row's `nf-fa-angle_right` is followed by one space before what is typed | finder | Type a few characters and look between the glyph and the text |
| finder-60 | finder.2 | A select's and a checkbox popup's width follows its options (known when it opens); only a finder listing results as they come, waiting on a search, uses F7's limit | select or checkbox | Open a select and a checkbox popup on a very wide terminal and measure the frame |
| finder-61 | finder.7 | When searching takes time (reading every file, handing it to a search tool or a remote side), results are listed as they come: the loading icon after the title, results arriving one by one, the typing row taking keys as usual | finder | Keep typing in a slow search: typing does not stall and results keep arriving (an app whose searches are all quick never has this case) |
| finder-62 | finder.2 | A preview starting at a given line (e.g. a file found by its content, shown from the line found): that line sits on the preview's third row, with two lines of context above, not otherwise marked; line numbers are the file's | finder with a preview | Find a file by its content and look at the preview (an app with no such preview never has this case) |

## input/file-picker

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| file-picker-1 | file-picker.1 | A field whose value is a directory uses the file-picker's "choosing a directory" | file-picker | Find a field whose value is a directory, and check that what opens is choosing a directory |
| file-picker-2 | file-picker.2 | Always four parts: the typing row, the list, the preview and the metadata | file-picker | Open a file-picker |
| file-picker-3 | file-picker.2 | When it opens, the list shows the root directory the app gives | file-picker | Look at the title and the list after opening |
| file-picker-4 | file-picker.2 | The root directory is only a start: the top row of the list is `..`, to go up | file-picker | Press `Enter` on `..` |
| file-picker-5 | file-picker.2 | At `/` there is no `..` | file-picker | Go to `/` and look at the list |
| file-picker-6 | file-picker.2 | The current directory is written in the title: the field's name (uppercase), then ` · `, then the directory (`IDENTITY FILE · ~/.ssh`) | file-picker | Look at the title |
| file-picker-7 | file-picker.2 | A path too long for the title is cut from the start (`…/sideproj/terminu`) | file-picker | Go into a deep directory and look at the title |
| file-picker-8 | file-picker.2 | It opens with the focus on the list | file-picker | After opening, check that the hint is the list's hint (`Enter:… Tab\|/:filter Esc:cancel`) |
| file-picker-9 | file-picker.2 | The typing row is empty when it opens | file-picker | Open a field with a value and look at the typing row |
| file-picker-10 | file-picker.2 | The list's order: `..` → directories → files | file-picker | Look at the list |
| file-picker-11 | file-picker.2 | Directories and files are each sorted by name, case-insensitive | file-picker | Look at names in mixed case |
| file-picker-12 | file-picker.2 | Hidden files (starting with `.`) are not listed by default | file-picker | Open the home directory |
| file-picker-13 | file-picker.2 | Hidden files are listed only when the filter (the last segment of a path) starts with `.` (`.ss` and `~/.ss` bring up `.ssh`) | file-picker | Type `.ss` |
| file-picker-14 | file-picker.2 | In a wildcard, `*` does not match hidden files and `**` does not go into hidden directories, unless the pattern starts with `.` | file-picker | Type `~/*` in the home directory |
| file-picker-15 | file-picker.2 | An icon before every row: `nf-md-folder` (U+F024B) for directories, `nf-md-file` (U+F0214) for files | file-picker | Look at the start of every row in the list; read the code to check the code points |
| file-picker-16 | file-picker.2 | When the field already has a value, the cursor opens on that file | file-picker | Open a field with a value |
| file-picker-17 | file-picker.2 | The field's original value is in Green | file-picker | Open a field with a value, move the cursor away and look |
| file-picker-18 | file-picker.3 | At most 64 KB is read for the preview | file preview | Read the code; or preview a large file and look at its end |
| file-picker-19 | file-picker.3 | A directory is previewed as a tree | file preview | Move the cursor onto a directory |
| file-picker-20 | file-picker.3 | An archive (zip, tar, tar.gz, tar.bz2) shows its contents as a directory tree | file preview | Move the cursor onto an archive |
| file-picker-21 | file-picker.3 | A text file shows its content, with syntax colours (chroma's catppuccin-mocha, foreground only) | file preview | Move the cursor onto a source file |
| file-picker-22 | file-picker.3 | A text file has line numbers: Overlay0, right-aligned, one space after | file preview | Look at the left of a text file's preview |
| file-picker-23 | file-picker.3 | In a text file a Tab is drawn as `input_tab_width` spaces | file preview | Preview a file with Tabs in it |
| file-picker-24 | file-picker.3 | In a text file the `\r` of a CRLF is not drawn | file preview | Preview a file with CRLF line endings |
| file-picker-25 | file-picker.3 | In a text file any other control character is drawn by name in Red | file preview | Preview a file with `\x1b` in it |
| file-picker-26 | file-picker.3 | PDF: a grey first row with the page count (`12 pages`), a blank row, then the text of the first 20 pages (at most 128 KB) | file preview | Preview a PDF |
| file-picker-27 | file-picker.3 | A PDF with no extractable text reads `(no extractable text)` | file preview | Preview a scanned PDF |
| file-picker-28 | file-picker.3 | Image (png, jpg, gif, bmp, webp, tiff, ico, avif, heic): a grey first row `data:image/png · 12.4 KB`, a blank row, then the base64 data URI wrapped at the preview's width | file preview | Preview a small image |
| file-picker-29 | file-picker.3 | An image over 1 MB shows only `(1.4 MB — too large to inline as a data URI)` | file preview | Preview an image over 1 MB |
| file-picker-30 | file-picker.3 | Any other file is shown in hexadecimal: always 8 bytes a row, followed by ASCII (`89 50 4e 47 0d 0a 1a 0a  .PNG....`, 33 cells) | file preview | Preview a binary file, once side by side and once stacked |
| file-picker-31 | file-picker.3 | An unreadable file reads `(unreadable)` | file preview | Preview a file without read permission |
| file-picker-32 | file-picker.3 | A directory's tree has at most three levels | file preview | Preview a deep directory |
| file-picker-33 | file-picker.3 | The tree's first level has no branches; from the second on, `├─`, `└─` and `│` join them | file preview | Look at the tree |
| file-picker-34 | file-picker.3 | The branches are in Overlay0 | file preview | Look at the branches' colour |
| file-picker-35 | file-picker.3 (diagram) | The second level's branches start at the column of the first level's names (indented 2 cells); each level deeper is indented 3 cells more (`│  ` or 3 blank cells) | file preview | Look at a three-level tree |
| file-picker-36 | file-picker.3 (diagram) | One space after a branch, then the icon | file preview | Look between a branch and its icon |
| file-picker-37 | file-picker.3 | Each entry in the tree has the same icon, colour and order as in the list | file preview | Compare the tree with the list after going in |
| file-picker-38 | file-picker.3 | The tree does not list hidden files | file preview | Preview a directory with hidden files |
| file-picker-39 | file-picker.3 | The tree cannot scroll: it is drawn until the preview area is full, with `…` on the last row | file preview | Preview a large directory |
| file-picker-40 | file-picker.3 | An empty directory reads `(empty)`, in grey | file preview | Preview an empty directory |
| file-picker-41 | file-picker.3 | An unreadable directory reads `(permission denied)`, in grey | file preview | Preview a directory without read permission |
| file-picker-42 | file-picker.3 | A subdirectory is expanded to the bottom before the next one | file preview | Preview a directory with several subdirectories |
| file-picker-43 | file-picker.4 | Always four rows (`TYPE`, `SIZE`, `MODIFIED`, `MODE`), for files and directories alike | file preview | Move between files and directories; the preview area's height does not jump |
| file-picker-44 | file-picker.4 | Labels in uppercase and the layer colour | file preview | Look at the labels |
| file-picker-45 | file-picker.4 | Values in Text | file preview | Look at the values' colour |
| file-picker-46 | file-picker.4 | The label column is as wide as the longest label, two cells before the value | file preview | Look at the values' left edge |
| file-picker-47 | file-picker.4 | A file's `TYPE` is the preview's kind: `text`, `private key`, `image`, `PDF`, `archive`, `binary` | file preview | Look at one file of each kind |
| file-picker-48 | file-picker.4 | A symlink's `TYPE` is `link → <target>` | file preview | Move the cursor onto a symlink |
| file-picker-49 | file-picker.4 | A directory's `TYPE` is `directory` | file preview | Move the cursor onto a directory |
| file-picker-50 | file-picker.4 | A file's `SIZE` reads `411 B`, `4.2 KB`, `3.4 MB` (powers of 1024, one decimal) | file preview | Look at a few files of different sizes |
| file-picker-51 | file-picker.4 | A directory's `SIZE` reads `12 items`, and `1 item` for one (hidden files not counted) | file preview | Look at a directory with hidden files and one with a single item |
| file-picker-52 | file-picker.4 | `MODIFIED` reads `2026-09-30 14:02` (local time, to the minute) | file preview | Compare with `ls -l` |
| file-picker-53 | file-picker.4 | `MODE` is written as `ls -l` does (`-rw-------`, `drwx------`) | file preview | Compare with `ls -l` |
| file-picker-54 | file-picker.4 | A file whose first line is a private key's header has the `TYPE` `private key`, whether `hide_secrets_in_preview` is on or not | file preview | Look at a private key with the setting on and with it off |
| file-picker-55 | file-picker.4 | A symlink's `SIZE`, `MODIFIED` and `MODE` are the target's | file preview | Look at a link such as `/etc/localtime` |
| file-picker-56 | file-picker.4 | An unreadable directory's `SIZE` is `—`; the time modified and the permissions are written as usual | file preview | Look at a directory without read permission |
| file-picker-57 | file-picker.4 | A broken link's `SIZE`, `MODIFIED` and `MODE` are `—` | file preview | Look at a broken link |
| file-picker-58 | file-picker.4 | When a value cannot be read, the four rows stay: no row is left out, and it is not written as `0 items` | file preview | Look at a broken link and an unreadable directory |
| file-picker-59 | file-picker.4 | No path, owner, or access and creation times | file preview | Check that the metadata has only four rows |
| file-picker-60 | file-picker.5 | When it is on, a file whose first line is a private key's header (starting with `-----BEGIN` and containing `PRIVATE KEY`, or starting with `PuTTY-User-Key-File-`) shows only its first line, then the grey line `(sensitive content not shown)` | file preview | With the setting on, preview a renamed private key |
| file-picker-61 | file-picker.5 | When it is on, a file readable by its owner only (no read permission for group or other) shows not a single line, only that grey line, whatever its kind | file preview | With the setting on, preview a `600` text file |
| file-picker-62 | file-picker.5 | Directories do not count (a `700` directory is previewed as usual) | file preview | With the setting on, preview `~/.ssh` |
| file-picker-63 | file-picker.5 | Any other file is previewed as usual | file preview | With the setting on, preview a `644` text file |
| file-picker-64 | file-picker.5 | The metadata shows as usual either way | file preview | With the setting on, look at a private key's metadata |
| file-picker-65 | file-picker.6 | `Enter` in the list on a directory: goes in | file-picker | Press `Enter` on a directory |
| file-picker-66 | file-picker.6 | Going into a directory clears the typed filter | file-picker | Filter, then press `Enter` on a directory |
| file-picker-67 | file-picker.6 | After going into a directory, the focus stays on the list and the cursor rests on the first item below `..` | file-picker | Look at the cursor after going into a directory |
| file-picker-68 | file-picker.6 | `Enter` on a file: chooses it, writes back and closes | file-picker | Press `Enter` on a file |
| file-picker-69 | file-picker.6 | When choosing a file, a directory is never chosen | file-picker | Try to choose a directory in every way |
| file-picker-70 | file-picker.6 | Plain text typed in the typing row filters the current level, as "Matching" in finder says | file-picker | Type `ed25` |
| file-picker-71 | file-picker.6 | When a path is typed (starting with `/` or `~/`), the path stays on the typing row | file-picker | Type `~/.ssh/` and look at the typing row |
| file-picker-72 | file-picker.6 | The path is split at its last `/`: before it the directory (the list shows it, the title names it), after it the filter text | file-picker | Type `~/.ssh/id_` |
| file-picker-73 | file-picker.6 | A half-typed path already works, and typing and pasting give the same result | file-picker | Type a string one character at a time and compare with pasting the same string |
| file-picker-74 | file-picker.6 | When the path's directory does not exist, the list is empty, as with no results | file-picker | Type `~/nope/x` |
| file-picker-75 | file-picker.6 | A `..` segment in a path is not resolved upwards; the list is empty | file-picker | Type `~/../x` |
| file-picker-76 | file-picker.6 | With `*` or `?` it is a wildcard: `*` matches within one level, `**` goes down every subdirectory | file-picker | Type `~/Downloads/*.png` and `~/.ssh/**/*.pem` |
| file-picker-77 | file-picker.6 | Each row of the wildcard results shows the path relative to the starting point (the directory before the first `*` or `?`) | file-picker | Type a path with `**` and look at the results |
| file-picker-78 | file-picker.6 | With a wildcard, the title names the starting point | file-picker | Type a wildcard and look at the title |
| file-picker-79 | file-picker.6 | Wildcard results have no `..` | file-picker | Type a wildcard and look at the first row of the list |
| file-picker-80 | file-picker.6 | The hint on the list, on a directory, is `Enter:into Tab\|/:filter Esc:cancel` | file-picker | With the cursor on a directory, look at the bottom border |
| file-picker-81 | file-picker.6 | The hint on the list, on a file, is `Enter:choose Tab\|/:filter Esc:cancel` | file-picker | With the cursor on a file, look at the bottom border |
| file-picker-82 | file-picker.7 | The list shows directories only, no files | file-picker | Open a file-picker choosing a directory |
| file-picker-83 | file-picker.7 | The order is `.` → `..` → directories | file-picker | Look at the list |
| file-picker-84 | file-picker.7 | The first row is `.`, written `. (this directory)` | file-picker | Look at the first row of the list |
| file-picker-85 | file-picker.7 | The icon of `.` is `nf-md-folder_move` (U+F0252) | file-picker | Look at the icon before `.` |
| file-picker-86 | file-picker.7 | `Enter` on `.` chooses the current directory, writes it back and closes | file-picker | Press `Enter` on `.` |
| file-picker-87 | file-picker.7 | `Enter` on another directory goes in | file-picker | Press `Enter` on a directory |
| file-picker-88 | file-picker.7 | While the typing row holds a filter or a wildcard, there is no `.` row | file-picker | Type a filter and look at the list |
| file-picker-89 | file-picker.7 | Wildcard results list directories only | file-picker | Type `~/*` |
| file-picker-90 | file-picker.7 | The hint on `.` is `Enter:choose Tab\|/:filter Esc:cancel` | file-picker | With the cursor on `.`, look at the bottom border |
| file-picker-91 | file-picker.4 | A file gone after being listed (deleted, moved), writes `—` in every row it cannot get | file preview | Delete a file elsewhere after it is listed, move the cursor to it and look at the metadata |
| file-picker-92 | file-picker.3 | The preview and the metadata are read in the background: typing and moving the cursor never wait; while reading, the preview frame has the loading icon after its title, reads `(loading…)` in grey, and the metadata values stay empty; what has been read is kept by path and not read again | file preview | Move the cursor fast on a slow (e.g. remote) file system: typing never stalls, and the reading state looks as described; read the code: files are not read while drawing |
| file-picker-93 | file-picker.3 | In a text file, colour codes colour the text and a `\r` within a line keeps only the last state | file preview | Preview a file with colour codes and `10%\r100%` in it |

## input/reorder

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| reorder-1 | reorder.1 | No typing row, no search | reorder | Open a reorder |
| reorder-2 | reorder.2 | Each row: one cell at the start for a glyph, a space, then the item | reorder | Look at the start of each row |
| reorder-3 | reorder.2 | Items are in Text | reorder | Look at a row without the cursor |
| reorder-4 | reorder.2 | Only the held item draws the glyph; the other rows leave that cell blank | reorder | Look at the starts of the rows before and after pressing `D` |
| reorder-5 | reorder.2 | The glyph's cell is always kept, so text never shifts when an item is picked up or dropped | reorder | Press `D`, then `Enter`; the text stays in place |
| reorder-6 | reorder.2 | The held item has a Yellow background, Base bold, the arrow Yellow too | reorder | Look after pressing `D` |
| reorder-7 | reorder.2 | The held item's first cell shows `nf-md-swap_vertical` (U+F04E2) | reorder | Look at the row's start after pressing `D` |
| reorder-8 | reorder.3 | It opens with the focus on the list, holding nothing | reorder | Look at the hint after opening |
| reorder-9 | reorder.3 | `D` picks up the cursor's item and enters the Drag mode | reorder | Press `D` |
| reorder-10 | reorder.3 | `Enter` holding nothing: writes the whole order back and closes the popup; only then does it take effect | reorder | Move items, then press `Enter` |
| reorder-11 | reorder.3 | `Esc` holding nothing, with the order unchanged: it closes at once | reorder | Open it and press `Esc` straight away |
| reorder-12 | reorder.3 | `Enter` on the discard confirm: discards and closes the popup | reorder | Press `Enter` on the confirm |
| reorder-13 | reorder.3 | `Esc` on the discard confirm: closes the confirm and returns to the list, the order still there | reorder | Press `Esc` on the confirm |
| reorder-14 | reorder.3 | "Changed": an item dropped somewhere other than where it was picked up, never cleared after that (moving one away and back still counts) | reorder | Move an item away and back, then press `Esc`; it still asks first |
| reorder-15 | reorder.3 | Holding nothing, the hint is `Enter:apply D:drag Esc:cancel` | reorder | Look at the hint on the bottom border |
| reorder-16 | reorder.3 | While holding, `j\|l` swap the item with the next one and `h\|k` with the previous one, the cursor going with it | reorder | Press `k` and `l` while holding |
| reorder-17 | reorder.3 | `Enter` while holding: drops it and leaves the Drag mode; the cursor stays on it | reorder | Press `Enter` while holding |
| reorder-18 | reorder.3 | `Esc` while holding: puts it back where it was picked up and leaves the Drag mode (the popup does not close) | reorder | While holding, move it two places, then press `Esc` |
| reorder-19 | reorder.3 | While holding, `Space` opens the Drag mode's Space menu and other keys do nothing; `D` is not an alias for dropping | reorder | Press `Space` and `D` while holding |
| reorder-20 | reorder.3 | While holding, the hint is `Enter:drop Esc:cancel` | reorder | Look at the hint on the bottom border while holding |

## project

| ID | Source | What to check | Applies to | How to check |
|---|---|---|---|---|
| project-1 | project.2 | `family.mk` is copied from the template as it is to `family.mk`, unchanged | everyone | Read the file: a diff against `project/family.mk` of the tdp version the app follows shows no difference |
| project-2 | project.2 | `release.yml` is copied from the template to `.github/workflows/release.yml`; the only change is `windows-latest` added to the test matrix, with a Windows build | everyone | Read the file: a diff against the template of the same version differs only by `windows-latest` in the matrix (with a Windows build) |
| project-3 | project.2 | `goreleaser.yaml` is copied from the template to `.goreleaser.yaml`, changing only `<app>` and the lines marked `app:`, and, with a Windows build, opening the comments marked `Windows` | everyone | Read the file: put `<app>` back in place of the app's name and diff against the template of the same version; only these places differ |
| project-4 | project.2 | `install.sh` is copied from the template, changing only `<app>`, `WINDOWS` and the blocks marked `app's own` | everyone | Read the file: put `<app>` back in place of the app's name and diff against the template of the same version; only these places differ |
| project-5 | project.2 | `uninstall.sh` is copied from the template, changing only `<app>` and the blocks marked `app's own` | everyone | Read the file: put `<app>` back in place of the app's name and diff against the template of the same version; only these places differ |
| project-6 | project.2 | `version.go` is copied from the template to `internal/version/version.go`, changing only `<app>` | everyone | Read the file: put `<app>` back in place of the app's name and diff against the template of the same version; nothing else differs |
| project-7 | project.2 | `gitignore` is copied from the template to `.gitignore`, changing only `<app>`, with the app's own lines after the last one | everyone | Read the file: put `<app>` back in place of the app's name and diff against the template of the same version; only the lines added at the end differ |
| project-8 | project.2 | With a Windows build, `windows-latest` is added to the test matrix of `release.yml` | Windows build | Read the file: the matrix in `.github/workflows/release.yml` |
| project-9 | project.2 | With a Windows build, the comments marked `Windows` in `.goreleaser.yaml` are all opened | Windows build | Read the file: `.goreleaser.yaml` |
| project-10 | project.2 | With a Windows build, `WINDOWS` in `install.sh` is set to `yes` (as the template's comment says) | Windows build | Read the file: `WINDOWS` in `install.sh` |
| project-11 | project.3 | The app's own Go code lives only in `cmd/<app>/` and `internal/`; development tools may go in a top-level `tools/` | everyone | Read the files: every `.go` file outside `tools/` is under these two directories |
| project-12 | project.3 (diagram) | The main package is in `cmd/<app>/main.go` | everyone | Read the files |
| project-13 | project.3 | `go install github.com/<account>/<app>/cmd/<app>@latest` installs it (a family member's account is `vulcanshen`, an app made by tdp uses its own) | everyone | Read the files: the module in `go.mod` is `github.com/<account>/<app>`, and `cmd/<app>` is the main package |
| project-14 | project.3 (diagram) | The README's demo gif is in `docs/` | everyone | Read the files: the gif the README refers to is under `docs/` |
| project-15 | project.3 (diagram) | `go.mod` and `go.sum` are at the root | everyone | Read the files |
| project-16 | project.3 (diagram) | `LICENSE` is at the root | everyone | Read the files |
| project-18 | project.3 | The family mark's original is `docs/icon.svg`; the copy the splash uses lives in the code (a copy of the file under `internal/`, or the cells written out) | everyone | Read the files: `docs/icon.svg` exists; read the code: the splash draws the copy under `internal/` or the cells written out |
| project-19 | project.3 | An app with a Windows build also has `install.ps1` and `uninstall.ps1` | Windows build | Read the files |
| project-20 | project.4 | `<app> version` and the splash's version print `Display()` of `internal/version` | everyone | Read the code: both places call `Display()` |
| project-21 | project.4 | A release's version is the tag injected without its v, and printed with the v (e.g. tag `v0.2.0` prints `v0.2.0`) | everyone | Read the files: `.goreleaser.yaml` injects the tag without its v and `internal/version` prints it with the v; for an app that has released, install a release and run `<app> version`: it prints the same as the tag |
| project-22 | project.4 | A local `make build` or `go build` injects no version; the version is `dev` | everyone | After a local `make build`, run `./<app> version`; it prints `dev` |
| project-23 | project.5 | `Makefile` only sets variables and does `include family.mk`; the app's own targets all go in the last section, `##@ <app> 自己的` | everyone | Read the file; run `make help`: the family's sections in family.mk's order, the app's own section last |
| project-24 | project.5 | The variables are set before `include family.mk` | everyone | Read the file |
| project-25 | project.5 | `BINARY` is set to the app's name, which is also the name of the directory under `cmd/` | everyone | Read the file |
| project-26 | project.5 | The two comment lines at the start of the Makefile are the template's (`<app> — build / run / test / package（家族共用的 target 在 family.mk）` and 「跑 make（或 make help）列出所有指令。」) | everyone | Read the start of the file |
| project-27 | project.5 | The app's own targets have names that are not family.mk's | everyone | Read the files: compare the target names on both sides |
| project-28 | project.6 | `CHANGELOG.md` starts as in the template: `# Changelog`, then `Each release names the version of terminu design (tdp) it follows.` | everyone | Read the start of the file |
| project-29 | project.6 | Each release's heading is the tag pushed (with its v), then ` — tdp <version>` | has released | Read the file: the heading of every release made after tdp v0.7.0 |
| project-30 | project.6 | Changes not yet released are written in `## Unreleased` at the top | everyone | Read the file and the commits after the latest tag: every change is recorded in `## Unreleased` at the top |
| project-31 | project.6 | Releases made before tdp v0.7.0 keep the headings they were written with | has released | Read the file: in `git log -p CHANGELOG.md`, the old releases' headings have not been rewritten |
| project-32 | project.6 | The CHANGELOG is written in English | everyone | Read the file |
| project-33 | project.6 | A GitHub release's notes are that release's section of the CHANGELOG | has released | Compare `gh release view <tag>` with that section of the CHANGELOG |
| project-34 | project.7 | A release's tag is `vX.Y.Z` | has released | Run `git tag` |
| project-35 | project.7 | `make check` passes on the repo as it is now | everyone | Run `make check` on the repo as it is now |
| project-36 | project.7 | A release with a Windows build also pushes to the scoop bucket | Windows build | Check that the scoop bucket has this release |

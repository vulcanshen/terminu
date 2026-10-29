# terminu design principle (tdp)

**Language**: English · [繁體中文](README-zh_TW.md)

tdp is the detailed specification behind [terminu design](../README.md), in four layers:

| Layer | Document | Nature |
|---|---|---|
| **Principle** | this document | The spirit: what it aims for, and why |
| **Rules** | [rules.md](rules.md) | Must hold, each with its reason; what is left to the app is left explicitly (P5) |
| **Components** | [components](../components/README.md) | Component specs: the colour scheme, frames, dialogs, and how each kind of input looks and works; required, choosing only among the listed options |
| **Project** | [project](../project/README.md) | The project spec: a family app repo's directories, Makefile, version, CHANGELOG and release; the template files are copied as they are; binds family members only |

The [checklist](../checklist/README.md) breaks the requirements of these four layers into items that can each be
checked, for checking whether an app does what tdp asks; it is not a requirement itself, and where it disagrees with the
spec, the spec wins.

tdp answers one question: **what makes a terminal UI usable without reading the docs?**

---

## P0 Rules serve the UX, not the other way round

tdp is what past UX decisions crystallised into, not a cage for future ones. **When a rule conflicts with the UX it was
meant to serve, the UX wins — extend the rule, don't flatten the UX.**

To decide whether to hold a rule or extend it:

1. **Recall the rule's origin UX**: what user-facing problem was it solving?
2. **Check the conflict in front of you**: does that problem still exist here, or are two different goals just landing on
   the same screen?
3. **If it doesn't apply, extend**: write down the exception and its reason instead of cutting the UX.

Watch the reverse too: when a new situation happens to fit an existing rule, ask "**is this real UX alignment, or
luck?**" A rule is a shortcut for reasoning, not a replacement for it.

## P1 Usable without the docs

Users **need not read documentation or memorise hotkeys in advance**. A set of **core keys whose meaning never changes
across screens or apps** is enough to use the whole app. Learn it once and it holds everywhere in the app — and moving to
another app of the family needs no relearning.

## P2 Disclosure is the only mechanism

There is only one way to achieve P1: **disclose what the user can do, so they find it without learning it first.** Both
of these must hold:

| | Question | If it fails |
|---|---|---|
| **The entry point is disclosed** | Does the user know there is a key to press? | The entry point might as well not exist |
| **The actions are all listed** | Once pressed, is everything they can do in there? | Unlisted actions can only be learned beforehand |

**Visible is not the same as disclosed.** What is disclosed must be a **list of actions you can run directly**, not
documentation:

| Form | From seeing to running | Disclosure? |
|---|---|---|
| Interactive menu (`j\|k` to pick, `Enter` to run) | 1 step | ✓ |
| Permanent hint (see the key on the footer, press it) | 1 step | ✓ |
| Explanatory text (read → find → remember → type) | several steps, needs memory | ✗ |

Moving the documentation into the app does not turn it into disclosure — the user is still reading documentation.

The one thing deliberately left undisclosed is the family easter egg, the splash (Rules, chapter S).

## P3 Three scopes of operation

Every action the user meets in an app belongs to one scope, decided by **what it acts on**:

| Scope | Acts on | Examples |
|---|---|---|
| **item operation** | the **one** item under the cursor | open, rename, delete this row |
| **panel operation** | the focused panel (or its tab) **as a whole** | search, sort, add, refresh, act on everything marked |
| **global operation** | no panel — the app as a whole | switch screen, open settings, switch context, quit |

The test is always **what it acts on**, never how important the action is. A small convenience that acts on the cursor is
an item operation; a crucial global toggle belongs to no panel and is a global operation.

Edge cases:

- **Acting on a batch of marked items** is a panel operation — it acts on "the batch marked in this panel", not the one
  item under the cursor. E.g. filu copying the marks into the current directory, sshu's transfer all.
- **An action that concerns only another panel** appears only in the menu of **the panel it belongs to**; it is not pushed
  into the current focus, nor promoted to global. The user finds it by pressing `Tab` over there. E.g. with filu's focus
  on `[1]`, "clear marks" belongs only to `[3]`; but "paste the marks here" acts on the directory in `[1]`, so it is a
  panel operation of `[1]`.
- **Switching screens** is a global operation. E.g. sshu's `[M]anage` / `[F]ile transfer` / `[S]SH`, webu's `[W]eb` /
  `[B]ookmarks` / `[H]istory`.

Each scope has a definite place (Rules, chapter M): `Space` opens what the current panel can do, ordered item → panel →
global, the global region being one row that opens the global operation popup; `?` only lists which keys work here,
read-only.

## P4 One element, one meaning

Once any visual or interactive element — a colour, a symbol, a key, a border style, a fixed slot — is given a meaning, it
is **dedicated** to it, and no other meaning may borrow it.

- If a colour means "the user's footprint", popup borders may not use the same colour, however good it looks
- If `Esc` means "cancel", no screen may use it to "confirm"
- If a slot on a label says "what kind of screen this is", it may not double as decoration

The cost of double duty is that the user has to learn two sets of rules, which contradicts P1 directly. This is also the
litmus test for whether a new rule holds up.

P4 governs the interface elements tdp defines (frames, cursors, hints, labels, capsules…). The colours and symbols of the
content itself (file types, pod states, log levels, syntax highlighting) belong to the domain, and the app may decide for itself (P5).

## P5 Leaving it to the app explicitly

tdp is the universe: every decision an app makes has its ground in tdp — it follows a requirement, or it lies within
what tdp explicitly leaves to the app. Wherever nothing is explicitly left to the app, the requirement is followed.

**How it is written**: always "the app may decide for itself", with the scope stated. Inside that scope the app may
handle the UI/UX itself, and may also do without terminu-go (Rules E8); the requirements that still hold inside the
scope are written beside it. Where tdp says "the app may…", it offers an option: whether to use it, the app may decide for
itself; once used, it is followed as written there.

Take core keys as an example:

- `Space` is not left to the app: pressing `Space` always opens / closes the Space menu of the current focus; in input
  state it is a space character, and that exception is fixed by tdp too.
- `Enter` leaves the how to the app: tdp specifies that it is "the most obvious action on the focused item", and what that
  action is, the app may decide for itself — in filu it enters a directory, in sshu it connects, in locku it flips a
  setting; inside that scope, the same kind of item always gets the same action within an app (Rules K3).

**When a fixed part does not fit**: it is reported as a gap in tdp, and tdp adds a solution or leaves it to the app
explicitly. Doing it any other way, outside what is left to the app, is a violation.

**tdp's scope:**

- **The function logic, the app may decide for itself**: how data is handled, file formats, whether an entered value is
  valid, which external commands to call. tdp governs the screens and operation the user sees, plus the app's command
  line, environment variables, where config and data live, the README, the repo and releases (chapter E of the Rules,
  [project](../project/README.md)); how an invalid value is shown follows the components.
- **The screen requirements cover only the TUI screens the app draws itself**: on a screen that is not part of the TUI
  (Rules K1, e.g. locku's screensaver and PIN box while locked) and on output printed for another program to show (e.g.
  ccdrawu's `statusline` printed for Claude Code's status line), the app may decide for itself.
- **Developer documents are outside tdp's scope**: design records and notes on developing and releasing — whether to
  write them, how and where, tdp does not govern.

**The larger openings:**

- **Domain hotkeys on a panel, the app may decide for itself**: which letter does what, whether case carries meaning,
  whether to use chords or `Alt`, whether to cycle backwards with `Shift-Tab` (popups with an action area excepted, Rules
  K2). Inside that scope they **must appear in a menu, marked with `[]`**, they **may not take over a core key**, and
  they **may not take over the movement letters** (Rules K12). Keys inside a component (e.g. a form's `e`, a datetime
  picker's `t`, a textarea's `i|a|o`) are part of the component spec, not left to the app.
- **Domain symbols and colours, the app may decide for itself**: file-type icons, status glyphs, the colours of the
  content itself. Inside that scope, other rules still constrain how symbols are used (P4 dedication, stable width,
  explicitly marked hotkeys); the family requires a Nerd Font (Rules E4). The glyphs of the components (radio, checkbox,
  the loading icon, borders, the titles of each class of popup) and the colour scheme are part of the component spec,
  not left to the app.

**Why**: only what is written counts, so an app and whoever checks it look in one place only: a requirement to follow, or
the sentence "the app may decide for itself". Letting every app write exceptions of its own, with enough of them
the family stops being one way of working; what does not fit goes back to tdp, which adds a solution every other app
gains from too. Hotkeys and domain symbols are bound to the concrete domain (in kbu `S` is shell, in filu `S` is sort)
and are not on the no-prior-learning path — everything the user looks for is in `Space` and `?` — so they are left to the
app; the function logic is the app itself, unseen by the user, and not tdp's to govern (the user, 2026-10-25).

## P6 What is lit is what has the focus

On screen, only the part where the user's keys go right now is lit; everything else is dimmed:

- The top popup is lit, everything under it dimmed (Rules F8).
- The focused panel is lit, unfocused ones dimmed (Rules T2).
- In a finder, the part with the focus is lit, the other part dimmed (Rules F1).
- When one hotkey has two indicators, the one that fires is lit (Rules M9).
- The cursor on a part without the focus is dimmed along with it.

Without reading a word, the user knows where the keys go by seeing what is lit. Dimming is not hiding: what is underneath
stays visible; it only says "not here right now".

---

## Terms

### terms.1 Surface

A UI container that can take focus and that the user interacts with directly; there are two kinds, **panel** and
**popup**. Always-on areas (footer, statusbar, screen chip row) are not surfaces — focus never rests on them.

### terms.2 Screen

A set of panels shown at the same time. Some apps have a single screen, some have several, switched by a global
operation.

- Single screen: kbu, filu, locku
- Several screens: sshu's `[M]anage` / `[F]ile transfer` / `[S]SH`; webu's `[W]eb` / `[B]ookmarks` / `[H]istory` /
  `[D]ownloads` / `[S]ettings`

### terms.3 Panel

A permanent area of the screen with its own cursor and content, numbered `[N]`.

- kbu: `[1]` resource kind sidebar, `[2]` resource list, `[3]` details
- filu: `[1]` file list, `[2]` preview, `[3]` Marks / Tasks / Favorites
- locku: `[1]` sidebar (Profiles, Savers, Integration, Settings), `[2]` property table of the item under the cursor

### terms.4 Panel tab

Several pages of content that can be switched within one panel. Switching panel tabs changes neither the panel nor the
screen.

- kbu `[3]`'s Logs / Events / Conditions / Relatives / History
- filu `[1]`'s up to 5 directory tabs; `[3]`'s Marks / Tasks / Favorites

### terms.5 Popup

A transient surface laid over the panels; closing it returns to what is underneath. There are eight classes (Rules F1):

- menu: the Space menu, kbu's sort picker
- confirm: filu's confirmation before deleting
- input: filu's rename, locku's PIN entry, a select choosing one value
- form: sshu's Host form
- note: kbu's YAML view, the key reference
- toast: a short message when an operation completes or fails
- terminal: kbu's Alterm, filu's shell — a subprocess (PTY) running inside a popup
- an app's own popup: kamonu's popup for drawing cells — content the seven classes cannot hold

### terms.6 Focus

Where the user's keys go right now, on two levels:

1. **Surface level**: which panel or popup. E.g. kbu's `[2]`, or the Space menu laid over it
2. **Position level**: the row under the cursor in that surface, the selected panel tab. E.g. the pod under the cursor in
   kbu's `[2]`

"The target is within focus" means the target is the current surface itself, or the item at its position level.

### terms.7 Input state

When typed text is the content: focus is on a typing row, and what is typed becomes that row's content. E.g. filu's
rename box, webu's address box (`o`), locku's PIN entry, the typing row of a panel filter or of a finder. The list of a
select or a picker, and a form itself, are not input state. See Rules K8.

### terms.8 Mode

A temporary state inside a panel or popup: once in it, some keys take on the mode's own meaning, and `Esc` leaves it.
E.g. webu's visual mode (selecting text), kbu's drag mode (reordering pins), sshu's `Alt-v` selection mode, the selection
in filu's yank viewport. A mode is not input state — keys do not become characters. Switching the layout (e.g. zoom,
which fills the screen with one panel) is not a mode either: no key changes meaning, `Esc` need not leave it, and its own
key restores it. See Rules K11.

### terms.9 Core key

A key whose meaning is specified by tdp and never changes on any surface: `Tab`, `Enter`, `Esc`, `Space`, `?`, `q`,
`1`–`9` (Rules, chapter K).

### terms.10 Letter hotkey

A key the app assigns to run a row of a menu directly. E.g. filu's `[r]ename`, kbu's `[C]ompare`, sshu's `[t]ransfer`
and `[T]ransfer all`. It is a shortcut, not an extra feature (Rules M3).

### terms.11 Source and target

When popup A opens popup B, A is the source and B is the target. E.g. opening the global operation popup from the global
row of the Space menu — the Space menu is the source, the global operation popup the target.

### terms.12 Streaming content

Content with new information continuously flowing in. E.g. kbu `[3]`'s Logs, sshu's SSH session, filu's search results
appearing one by one.

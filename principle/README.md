# terminu design principle (tdp)

**Language**: English · [繁體中文](README-zh_TW.md)

tdp is the detailed specification behind [terminu design](../README.md), in three layers:

| Layer | Document | Nature |
|---|---|---|
| **Principle** | this document | The spirit: what it aims for, and why |
| **Rules** | [rules.md](rules.md) | Must hold, each with its reason; split into a fixed zone and a concept zone (P5) |
| **Family defaults** | [defaults.md](defaults.md) | Family default recommendations: the concrete values, colour system and habits the terminu family shares. Using them is the easy path; not using them is not a violation |

tdp answers one question: **what makes a terminal UI usable without reading the docs?**

---

## P0 Rules serve the UX, not the other way round

tdp is what past UX decisions crystallised into, not a cage for future ones. **When a
rule conflicts with the UX it was meant to serve, the UX wins — extend the rule, don't
flatten the UX.**

To decide whether to hold a rule or extend it:

1. **Recall the rule's origin UX**: what user-facing problem was it solving?
2. **Check the conflict in front of you**: does that problem still exist here, or are two
   different goals just landing on the same screen?
3. **If it doesn't apply, extend**: write down the exception and its reason instead of
   cutting the UX.

Watch the reverse too: when a new situation happens to fit an existing rule, ask
"**is this real UX alignment, or luck?**" A rule is a shortcut for reasoning, not a
replacement for it.

## P1 Usable without the docs

Users **need not read documentation or memorise hotkeys in advance**. A set of **core
keys whose meaning never changes across screens or apps** is enough to use the whole app.
Learn it once and it holds everywhere in the app — and moving to another app of the
family needs no relearning.

## P2 Disclosure is the only mechanism

There is only one way to achieve P1: **disclose what the user can do, so they find it
without learning it first.** Both of these must hold:

| | Question | If it fails |
|---|---|---|
| **The entry point is disclosed** | Does the user know there is a key to press? | The entry point might as well not exist |
| **The actions are all listed** | Once pressed, is everything they can do in there? | Unlisted actions can only be learned beforehand |

**Visible is not the same as disclosed.** What is disclosed must be a **list of actions
you can run directly**, not documentation:

| Form | From seeing to running | Disclosure? |
|---|---|---|
| Interactive menu (`j/k` to pick, `Enter` to run) | 1 step | ✓ |
| Permanent hint (see the key on the footer, press it) | 1 step | ✓ |
| Explanatory text (read → find → remember → type) | several steps, needs memory | ✗ |

Moving the documentation into the app does not turn it into disclosure — the user is
still reading documentation.

The one thing deliberately left undisclosed is the family easter egg, the splash (Rules,
chapter S).

## P3 Three scopes of operation

Every action the user meets in an app belongs to one scope, decided by **what it acts on**:

| Scope | Acts on | Examples |
|---|---|---|
| **item operation** | the **one** item under the cursor | open, rename, delete this row |
| **panel operation** | the focused panel (or its tab) **as a whole** | search, sort, add, refresh, act on everything marked |
| **global operation** | no panel — the app as a whole | switch screen, open settings, switch context, quit |

The test is always **what it acts on**, never how important the action is. A small
convenience that acts on the cursor is an item operation; a crucial global toggle belongs
to no panel and is a global operation.

Edge cases:

- **Acting on a batch of marked items** is a panel operation — it acts on "the batch
  marked in this panel", not the one item under the cursor. E.g. filu copying the marks
  into the current directory, sshu's transfer all.
- **An action that concerns only another panel** appears only in the menu of **the panel
  it belongs to**; it is not pushed into the current focus, nor promoted to global. The
  user finds it by pressing `Tab` over there. E.g. with filu's focus on `[1]`,
  "clear marks" belongs only to `[3]`; but "paste the marks here" acts on the
  directory in `[1]`, so it is a panel operation of `[1]`.
- **Switching screens** is a global operation. E.g. sshu's `[M]anage` /
  `[F]ile transfer` / `[S]SH`, webu's `[W]eb` / `[B]ookmarks` / `[H]istory`.

Each scope has a definite place (Rules, chapter M): `Space` opens what the current panel
can do, ordered item → panel → global, the global region being one row that opens the
global operation popup; `?` only lists which keys work here, read-only.

## P4 One element, one meaning

Once any visual or interactive element — a colour, a lightness band, a symbol, a key, a
border style, a fixed slot — is given a meaning, it is **dedicated** to it, and no other
meaning may borrow it.

- If a colour means "the user's footprint", popup borders may not use the same
  lightness, however good it looks
- If `Esc` means "cancel", no screen may use it to "confirm"
- If a slot on a label says "what kind of screen this is", it may not double as
  decoration

The cost of double duty is that the user has to learn two sets of rules, which
contradicts P1 directly. This is also the litmus test for whether a new rule holds up.

## P5 Fixed zone and concept zone

Every rule belongs to one of two zones:

| Zone | What tdp specifies | What the app may do |
|---|---|---|
| **Fixed zone** | the behaviour itself | Follow it. When the app's nature genuinely doesn't fit, it may depart, but must write down why |
| **Concept zone** | the semantics — what this is meant to achieve | Decide for itself how to implement it. There is no "departure" here: breaking the semantics is breaking the fixed part |

Take core keys as an example:

- `Space` is in the **fixed zone**: pressing `Space` always opens / closes the Space menu
  of the current focus; in input state it is a space character, and that exception is
  fixed by tdp too.
- `Enter` is in the **concept zone**: tdp specifies that it is "the most obvious action
  on the focused item", not what that action is — in filu it enters a directory, in sshu
  it connects, in locku it flips a setting.

**What tdp does not specify:**

- **Letter hotkeys.** Which letter does what, whether case carries meaning, whether to use
  chords or `Alt`, whether to cycle backwards with `Shift-Tab` — all up to each app.
  Hotkeys depend on the domain (in kbu `S` is shell, in filu `S` is sort), and they are
  not on the no-prior-learning path — everything the user looks for is in `Space` and
  `?`. tdp governs only two things about hotkeys: they **must appear in a menu, marked
  with `[]`**, and they **may not take over a core key**.
- **Colour.** tdp provides a complete set of presentation rules, calculations and colour
  codes in [Family defaults D2](defaults.md#d2-colour-system), which an app that doesn't
  want to deal with colour can adopt as is; whether to follow it, and whether meaning may
  rely on colour alone, is up to each app.
- **Symbol vocabulary.** Which icon font, which glyphs, how many cells they take in which
  terminal and CJK font — all bound to concrete environments and left to each app. Other
  rules still constrain how symbols are used (P4 dedication, stable width, explicitly
  marked hotkeys).

---

## Terms

### Surface

A UI container that can take focus and that the user interacts with directly; there are
two kinds, **panel** and **popup**. Always-on areas (footer, statusbar, tab row) are not
surfaces — focus never rests on them.

### Screen

A set of panels shown at the same time. Some apps have a single screen, some have
several, switched by a global operation.

- Single screen: kbu, filu, locku
- Several screens: sshu's `[M]anage` / `[F]ile transfer` / `[S]SH`; webu's `[W]eb` /
  `[B]ookmarks` / `[H]istory` / `[D]ownloads` / `[S]ettings`

### Panel

A permanent area of the screen with its own cursor and content, numbered `[N]`.

- kbu: `[1]` resource kind sidebar, `[2]` resource list, `[3]` details
- filu: `[1]` file list, `[2]` preview, `[3]` Marks / Tasks / Favorites
- locku: `[1]` sidebar (Profiles, Savers, Integration, Settings), `[2]` property table
  of the item under the cursor

### Panel tab

Several pages of content that can be switched within one panel. Switching panel tabs
changes neither the panel nor the screen.

- kbu `[3]`'s Logs / Events / Conditions / Relatives / History
- filu `[1]`'s up to 5 directory tabs; `[3]`'s Marks / Tasks / Favorites

### Popup

A transient surface laid over the panels; closing it returns to what is underneath. E.g.:

- menu: the Space menu, kbu's sort picker
- confirm: filu's confirmation before deleting
- input: filu's rename, locku's PIN entry
- viewport: kbu's YAML view, the Compare of two resources
- toast: a short message when an operation completes or fails
- PTY: kbu's Alterm, filu's shell — a subprocess running inside a popup

### Focus

Where the user's keys go right now, on two levels:

1. **Surface level**: which panel or popup. E.g. kbu's `[2]`, or the Space menu laid
   over it
2. **Position level**: the row under the cursor in that surface, the selected panel tab.
   E.g. the pod under the cursor in kbu's `[2]`

"The target is within focus" means the target is the current surface itself, or the item
at its position level.

### Input state

While the user is typing: focus is on a field that takes keys as characters. E.g. filu's
rename box, sshu's host form, webu's address bar (`L`), locku's PIN entry, any `/`
search line.

### Mode

A temporary state inside a panel or popup: once in it, some keys take on the mode's own
meaning, and `Esc` leaves it. E.g. webu's visual mode (selecting text), kbu's drag mode
(reordering pins), sshu's `Alt-v` selection mode, the selection in filu's yank viewport.
A mode is not input state — keys do not become characters. Switching the layout (e.g. zoom,
which fills the screen with one panel) is not a mode either: no key changes meaning, `Esc`
need not leave it, and its own key restores it. See Rules K11.

### Core key

A key whose meaning is specified by tdp and never changes on any surface: `Tab`,
`Enter`, `Esc`, `Space`, `?` (Rules, chapter K).

### Letter hotkey

A key the app assigns to run a row of a menu directly. E.g. filu's `[r]ename`, kbu's
`[C]ompare`, sshu's `[t]ransfer` and `[T]ransfer all`. It is a shortcut, not an extra
feature (Rules M3).

### Source and target

When popup A opens popup B, A is the source and B is the target. E.g. in kbu, pressing
`Space` on the Compare viewport opens the layout menu — Compare is the source, the menu
is the target.

### Streaming content

Content with new information continuously flowing in. E.g. kbu `[3]`'s Logs, sshu's SSH
session, filu's search results appearing one by one.

### Departure and violation

- **Departure**: an app deliberately not following the fixed part of a rule, writing down
  which rule, where, and why in the "偏離 tdp" (departures from tdp) section of its own
  `docs/dev-remarks.md`. E.g. locku's lock screen shows no footer (M1), because its only
  action is pressing any key to bring up the PIN entry.
- **Violation**: not following the fixed part without a written reason. Listed for fixing
  in that app's `docs/<app>-terminu-fix.md`.

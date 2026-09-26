# terminu design principle (tdp)

**Language**: English · [繁體中文](README-zh_TW.md)

tdp is the detailed specification behind [terminu design](../README.md), in three layers:

| Layer | Document | Nature |
|---|---|---|
| **Principle** | this document | The spirit: what it aims for, and why |
| **Rules** | [rules.md](rules.md) | Must hold. Each comes with its reason; an app may depart from one when its nature calls for it, as long as the reason is written down |
| **Family defaults** | [defaults.md](defaults.md) | The concrete values and habits the terminu family shares. Using them is the easy path; departing from them is not a violation |

tdp answers one question: **what makes a terminal UI usable without reading the docs?**

---

## P0 Rules serve the UX, not the other way round

tdp is what past UX decisions crystallised into, not a cage for future ones. **When a
rule conflicts with the UX it was meant to serve, the UX wins — extend the rule, don't
flatten the UX.**

To decide whether to hold a rule or extend it:

1. **Recall the rule's origin UX**: what user-facing problem was it solving?
2. **Check the conflict in front of you**: does that problem exist here, or are two
   different goals just landing on the same screen?
3. **If it doesn't apply, extend**: write down the exception and its reason instead of
   cutting the UX.

Watch the reverse too: when a new situation happens to fit an existing rule, ask
"**is this real UX alignment, or luck?**" A rule is a shortcut for reasoning, not a
replacement for it.

## P1 Usable without the docs

Users **need not read documentation or memorise hotkeys in advance**. A small set of
**core keys whose meaning never changes across screens or apps** is enough to use the
whole app. Learn it once and it holds everywhere in the app — and in every other app of
the family.

This promise covers one dimension only: **no prior learning**. It says nothing about
whether hotkeys are easy to reach, how fast you are once you have learned them, or
whether they compose — that is hotkey ergonomics, a separate dimension (see P5).
**Following tdp does not make a good app, and not following it does not make a bad
one.** Choosing another path on purpose (as vim does) is a legitimate design decision;
tdp is for designers who want this one.

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
| Ambient cheatsheet (see the key, press it) | 1 step | ✓ |
| In-app documentation (read → find → remember → type) | several steps, needs memory | ✗ |

vim's `:help` is the classic counter-example: it lives inside the app and the start
screen mentions it, but it is documentation, not a list of actions.

**Disclosure can be a layer on top.** The same vim core, with which-key on top (as
LazyVim ships it), goes from almost no disclosure to almost complete disclosure — without
a single change to the core. Disclosure and app core are separable; when judging an app,
be clear whether you mean its default state or the state with a disclosure layer added.

## P3 Three scopes of operation

Every action the user meets in an app belongs to one scope, decided by **what it acts on**:

| Scope | Acts on | Examples |
|---|---|---|
| **item operation** | the **one** item under the cursor | open, rename, delete this row |
| **panel operation** | the focused panel (or its tab) **as a whole** | search, sort, add, refresh, act on everything marked |
| **global operation** | nothing in focus — the app itself | switch context, open settings, switch screen, quit |

The test is always **what it acts on**, never how important it is. A small convenience
that acts on the cursor row is an item operation and must be listed; a crucial global
toggle belongs to no focus and is a global operation.

Each scope has a definite place (Rules, chapter M): `Space` opens what the current focus
can do, ordered item → panel → global; `?` opens what the whole app can do, with global
operations runnable right there.

## P4 One element, one meaning

Once any visual or interactive element — a colour, a lightness band, a symbol, a key, a
border style, a fixed slot — is given a meaning, it is **dedicated** to it, and no other
meaning may borrow it.

- If a colour means "the user's footprint", popup borders may not use the same
  lightness, however good it looks
- If `Esc` means "cancel", no screen may use it to "confirm"
- If a slot on a label says "what kind of surface this is", it may not double as
  decoration

The cost of double duty is that the user has to learn two sets of rules, which
contradicts P1 directly. This is also the litmus test for any new rule.

## P5 Out of scope: letter hotkeys

tdp **defines what core keys mean** and **defines no letter hotkey**. Which letter does
what, whether delete is `D` or `x`, whether case carries meaning, whether to use chords,
`Alt`, or `Shift-Tab` to cycle backwards — all of it is up to each app.

**Why it is left undefined:**

- **Hotkeys depend on the domain.** In kbu `S` is shell, in filu `S` is sort; in sshu
  `D` duplicates a row, in kbu `D` drags. Every app has different verbs; forcing one
  table on them only yields rules that some app has to break (P0).
- **Hotkeys are not on the no-prior-learning path.** Everything the user looks for is in
  `Space` and `?`; hotkeys are speed-ups for those who already know (Rules M3). Whether
  they are well chosen affects ergonomics, not P1.
- **A shared hotkey table would compete with P2.** If moving between apps relied on a
  family-wide hotkey table, we would be back to learning in advance. What stays the same
  across apps is the **role of each core key**, not the letters.

tdp still governs two things about hotkeys: they **must appear in a menu, marked with
`[]`** (Rules M3, M5), and they **may not take over a core key** (Rules, chapter K). The
family's common hotkey habits are collected in the defaults, for reference.

**Symbol vocabulary** is out of scope too: which icon font, which glyphs, how many cells
they take in which terminal and CJK font — all bound to concrete environments and left to
each app. Other rules still constrain how symbols are used (P4 one meaning, Rules L2
stable width, M5 explicit hotkey marks).

## P6 UI you can see standing still, UX that exists only over time

UI rules show up in a screenshot and can be planned early; some UX rules only exist in
the flow of use (Rules, chapter T) and surface once an app is complete enough. Any
"UI/UX guide finished at v0.1" is missing the latter — tdp keeps being revised as the
apps grow.

---

## Terms

**Surface** — a UI container that can take focus and that the user interacts with
directly: mainly **panels** and **popups**. Always-on areas such as the statusbar or
footer are not surfaces.

**Focus** — where the user can act right now, on two levels: the **surface** (which
panel or popup) and the **position** within it (the row under the cursor, the selected
tab).

**Popup** — a transient surface over the panels: menu, confirm, input, viewport, toast,
PTY and so on.

**Input state** — while the user is typing: a form field, an input box, a search line.

**Departure** — an app deliberately not following a rule, with the reason written in its
own `docs/dev-remarks.md`. Not following a rule without a written reason is a
**violation**, listed for fixing in that app's `docs/<app>-terminu-fix.md`.

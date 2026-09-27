# terminu design

**Language**: English · [繁體中文](README-zh_TW.md)

**Terminal UIs you can use without reading the docs.**

terminu design is a design language for terminal UIs: a handful of keys that mean the
same thing on every screen of every app, plus two entry points that are always there —
`Space` tells you what you can do here, `?` tells you what you can do anywhere in the
app. Learn it once and every app in the family works the same way.

---

## Six keys

| Key | Meaning |
|---|---|
| `Tab` | Move to the next thing on the same level: between panels, between form fields |
| `Enter` | Do the obvious thing to what is selected; in a form, submit |
| `Esc` | Cancel, close the top layer — one layer at a time, never closes the app |
| `Space` | What can I do here? |
| `?` | Which keys work here? (read-only) |
| `q` | Quit the app (so does `Ctrl-C`) |

When in doubt, press `Space`.

## The spirit

- **Disclosure, not documentation.** Everything you can do is in a list you can open
  with one key and run straight from.
- **Three scopes of operation.** On this item, on this panel, on the whole app — menus
  are always ordered that way.
- **One element, one meaning.** A colour, a key, a border style each stand for exactly
  one thing.
- **Rules serve the UX.** When a rule gets in the way of good UX, the rule is extended,
  not the UX sacrificed.
- **What is fixed, and what is left to the app, is spelled out.** Core-key behaviour is
  fixed; everything else states what must be achieved and leaves the how to each app;
  colour and hotkeys are family defaults an app can adopt as they are.

The details are in the **[terminu design principle (tdp)](principle/)**:

| | |
|---|---|
| [Principle](principle/README.md) | The spirit: what it aims for and why |
| [Rules](principle/rules.md) | What must hold, each with its reason, split into a fixed and a concept zone |
| [Family defaults](principle/defaults.md) | Family default recommendations: colour system, popups, menus, hotkey reference, document skeletons |

## The terminu family

| App | What it is |
|---|---|
| [kbu](https://github.com/vulcanshen/kbu) | A Kubernetes TUI dashboard |
| [filu](https://github.com/vulcanshen/filu) | A terminal file manager you don't have to learn |
| [sshu](https://github.com/vulcanshen/sshu) | A terminal front end for ssh and sftp |
| [webu](https://github.com/vulcanshen/webu) | A terminal browser that reads a web page as a document |
| [locku](https://github.com/vulcanshen/locku) | A screensaver with a PIN lock, for the terminal |

## History

terminu design grew out of VTP, a TUI design principle that started inside kbu and was
later extracted. How it turned into what it is now is recorded (in Traditional Chinese)
in [vtp/](vtp/).

## License

[CC BY 4.0](LICENSE)

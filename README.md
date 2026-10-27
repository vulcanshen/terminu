# terminu design

**Language**: English · [繁體中文](README-zh_TW.md)

**Terminal UIs you can use without reading the docs.**

terminu design is a design language for terminal UIs: a handful of keys that mean the
same thing on every screen of every app, plus two entry points that are always there —
`Space` tells you what you can do here, `?` tells you which keys work here. Learn it once and every app in the family works the same way.

---

## Seven keys

| Key | Meaning |
|---|---|
| `Tab` | Move to the next thing on the same level: between panels, between form fields |
| `1`–`9` | Jump to panel N on this screen |
| `Enter` | Do the obvious thing to what is selected; in an input popup, confirm the value |
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
- **What is not left to the app is followed.** Whatever is left to the app says so
  explicitly, "the app may decide for itself" — hotkeys on panels, the domain's symbols
  and colours, the function logic; colour and how components look are set by the
  components.

The details are in the **[terminu design principle (tdp)](principle/)**:

| | |
|---|---|
| [Principle](principle/README.md) | The spirit: what it aims for and why |
| [Rules](principle/rules.md) | What must hold, each with its reason |
| [Components](components/README.md) | Component specs: colour, frames, dialogs, and how each kind of input looks and works |
| [Project](project/README.md) | The project spec: a family app repo's directories, Makefile, version, CHANGELOG and release |
| [Checklist](checklist/README.md) | The item list: the requirements broken into items that can be checked, for checking whether an app does what tdp asks |

## terminu-go

[terminu-go](https://github.com/vulcanshen/terminu-go) is tdp written as a Go library. An app registers its panels and
actions; terminu-go draws the screen from that and handles the core keys — the `Space` menu, `?`, the hints, confirms,
`Esc` closing one layer at a time — so a new app follows tdp without implementing it again. Its showcase app shows
every component on fake data; to see tdp at work, run it (Go required):

```sh
go run github.com/vulcanshen/terminu-go/examples/showcase@latest
```

Every app in the family is built on it. What an app needs that tdp does not say yet comes back here: the spec is
patched first, then the library follows.

## The terminu family

| App | What it is |
|---|---|
| [kbu](https://github.com/vulcanshen/kbu) | A Kubernetes TUI dashboard |
| [filu](https://github.com/vulcanshen/filu) | A terminal file manager you don't have to learn |
| [sshu](https://github.com/vulcanshen/sshu) | A terminal front end for ssh and sftp |
| [webu](https://github.com/vulcanshen/webu) | A terminal browser that reads a web page as a document |
| [locku](https://github.com/vulcanshen/locku) | A screensaver with a PIN lock, for the terminal |
| [kamonu](https://github.com/vulcanshen/kamonu) | A terminal editor for the family's marks (kamon), drawn letter by letter |
| [ccdrawu](https://github.com/vulcanshen/ccdrawu) | A sidebar for Claude Code: usage, context, cost and git beside the transcript |
| [hostu](https://github.com/vulcanshen/hostu) | Switch the hosts file between profiles, in the terminal |

## History

terminu design grew out of VTP, a TUI design principle that started inside kbu and was
later extracted. How it turned into what it is now is recorded (in Traditional Chinese)
in [vtp/](vtp/).

## License

[CC BY 4.0](LICENSE)

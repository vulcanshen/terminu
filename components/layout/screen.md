# screen: The whole screen

**Language**: English · [繁體中文](screen-zh_TW.md)

The skeleton of the whole screen: the footer, the screen chips of a multi-screen app, what a narrow terminal draws, empty
states. Moved here from Family defaults D1 on 2026-10-07 (from a default to a requirement). A panel's frame is in
[`panel`](panel.md), a floating frame in [`popup`](popup.md).

- **A one-row footer**, always reading:

  ```
  Space:menu ?:help Tab/1–N:panels q:quit
  ```

  Written like a hint (Rules M5); when too narrow, whole pairs are dropped from the end; keys
  Blue, colon and description Overlay0 (components/color).
- **Apps with several screens**: a row of screen chips on top (`[W]eb ╱ [B]ookmarks …`),
  then a full-width divider that doubles as a progress bar during long work.
- **Narrow threshold**: below 72 columns (60 for apps with a narrower sidebar) only the
  focused side is drawn.
- **Empty states**: one centred fact, plus a hint naming the key (e.g. "No hosts — press
  `[A]` or `[Space]`").

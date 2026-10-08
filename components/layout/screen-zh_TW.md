# screen：整個畫面

**Language**: [English](screen.md) · 繁體中文

整個畫面的骨架：footer、多畫面的 chip 列、窄寬時怎麼畫、空狀態。2026-10-07 從 Family defaults D1 搬來（從 defaults 升成規定）。
panel 的框見 [`panel`](panel-zh_TW.md)，浮在上面的框見 [`popup`](popup-zh_TW.md)。

- **footer 一列**，內容固定為：

  ```
  Space:menu ?:help Tab/1–N:panels q:quit
  ```

  寫法照 Rules M5 的 hint；寬度不夠時從尾端整組捨棄；鍵 Blue、冒號與說明 Overlay0（components/color）。
- **多畫面的 app**：上方一列畫面 chip（`[W]eb ╱ [B]ookmarks …`），下方一條全寬分隔線，
  長時間工作時兼當進度條。
- **窄寬門檻**：寬度 < 72 欄（側欄較窄的 app 用 60 欄）時只畫 focus 那一側。
- **空狀態**：置中寫一句事實，加上一句點名按鍵的提示（例如「沒有 host —— 按 `[A]` 或 `[Space]`」）。

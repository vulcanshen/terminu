# menu（從清單選一列執行）

**Language**: [English](menu.md) · 繁體中文

## 用途

沒有搜尋的清單，選一列執行（Rules F1）：Space menu、global operation popup、排序選擇器、工作清單（`Enter` 打開那一列的全文）。
清單需要搜尋時是 finder（[`input/finder`](../input/finder-zh_TW.md)）；選的是一個值、要寫回去時是 select（[`input/select`](../input/select-zh_TW.md)）；
自己搬動項目、排出順序的是 reorder（[`input/reorder`](../input/reorder-zh_TW.md)）。

## 長相

```
┏━ [2] HOSTS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                               ┃
┃ 󰋘 ITEM OPERATION                              ┃  ← 區塊標題
┃▓[Enter] Connect▓▓▓▓▓▓▓▓▓▓▓what it is, then in┃  ← cursor
┃ [E]dit                       change this host ┃
┃ [X] Delete             remove from hosts.yaml ┃
┃ ╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌ ┃  ← 分隔線
┃ 󰋘 PANEL OPERATION                             ┃
┃ [A]dd                              a new host ┃
┃ [/] Search          name, user, host, port, … ┃  ← 說明太長（框已經到最寬時）
┃ ╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌ ┃
┃ Global operation    actions for the whole app ┃
┃                                               ┃
┗━ Enter:run Esc:close ━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

（區塊標題前面的是 `nf-md-hexagon`。）

- **每一列**：label 用 Text，`[x]` 跟 label 同色；熱鍵怎麼標見 Rules M5。說明用 Overlay0，靠右，貼著右邊的留白（一般是離右框一格）；太長從尾端截，
  加 `…`（M5：單行）。label 與說明之間最少兩格：它決定最寬的那一列，也就決定 popup 的寬度。
- **區塊標題**：前面一個 `nf-md-hexagon`（U+F02D8），空一格，再寫標題；標題大寫（[components](../README-zh_TW.md) 的「大寫」）。
  Overlay0、縮一格（離框一格，跟各列的字同一欄）、不加粗；cursor 跳過。
- **分隔線**：區塊之間用兩段虛線 `╌`（U+254C）；其他照 [`layout/popup`](../layout/popup-zh_TW.md) 的分隔線（不接框、Overlay0）；
  cursor 跳過。
- **cursor**：層色底、Base 粗體，從框貼到框（蓋住左右的留白），字照樣離框一格；整列都是 Base 字。右邊的留白是箭頭
  U+E0B0，層色（[`layout/popup`](../layout/popup-zh_TW.md) 的 cursor 色塊）。
- **停用的列**：整列 Surface2，cursor 跳過，按熱鍵不作用（Rules M6）。
- **標題**：`nf-fa-bars` 加文字，畫成標題膠囊（[`layout/popup`](../layout/popup-zh_TW.md)）。Space menu 寫 focus panel 的 `[N] label`
  （它列的就是那個 panel 能做的事）；其他 menu 寫它做什麼（`GLOBAL OPERATION`、`SORT BY`）。
- **`Global operation` 那一列**（Rules M2）：沒有熱鍵，說明一律是 `actions for the whole app`。
- **寬度**：每一列打開時就確定，照 [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」。

**為什麼**：說明靠右，名稱與說明各成一欄，眼睛往下掃名稱時不會被說明打斷。cursor 用層色底：在家族的 popup 裡，層色底的那一塊
就是 `Enter` 會作用的地方（表單也一樣）。區塊標題有六角形、又是大寫，一眼就跟能執行的列分開；區塊之間用虛線，比實線輕，
只把清單分段，不會看起來像另一個框。

## 按鍵

- `j|k` 移動，到頭尾繞回；`u|d` 半頁（到頭尾停住）、`gg|G` 頭尾（Rules K12）。
- `Enter` 執行 cursor 那一列，熱鍵直接執行那一列。
- `Esc` 關掉（global operation popup 回到 Space menu，Rules F4）；Space menu 也可以再按 `Space` 關（Rules K5）。
- **hint**：`Enter:run Esc:close`（不寫移動鍵，見 [`layout/popup`](../layout/popup-zh_TW.md) 的 hint）。`Enter` 打開那一列全文的 menu
  （Rules F1，例：工作清單）寫 `Enter:detail Esc:close`：hint 寫按下去會發生什麼（Rules M5），那裡的 `Enter` 不執行任何東西。

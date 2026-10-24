# menu（從清單選一列執行）

**Language**: [English](menu.md) · 繁體中文

## 用途

沒有搜尋的清單，選一列執行（Rules F1）：Space menu、global operation popup、排序選擇器、工作清單（見下面的「工作清單」）。
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
- **工作清單的列跟著工作更新**：進度、狀態一變，menu 開著時那一列就跟著變，不用關掉重開。

**為什麼**：說明靠右，名稱與說明各成一欄，眼睛往下掃名稱時不會被說明打斷。cursor 用層色底：在家族的 popup 裡，層色底的那一塊
就是 `Enter` 會作用的地方（表單也一樣）。區塊標題有六角形、又是大寫，一眼就跟能執行的列分開；區塊之間用虛線，比實線輕，
只把清單分段，不會看起來像另一個框。

## 按鍵

- menu 是一維清單：`j|l|↓|→` 往後、`h|k|↑|←` 往前，到頭尾繞回；`u|d` 半頁（到頭尾停住）、`gg|G` 頭尾（Rules K12）。
- `Enter` 執行 cursor 那一列，熱鍵直接執行那一列。
- **執行之後**：menu 留不留照 Rules T1 的表，看確定之後做的事（打開來看、寫回一個值、用編輯器改那一項的保留；讓那一項不在、
  開 shell、換畫面、drill-down 的清掉）。動作前先問的 confirm 按 `Esc` 取消時，一律回到 menu（Rules F4）。
- `Esc` 關掉（global operation popup 回到 Space menu，Rules F4）；Space menu 也可以再按 `Space` 關（Rules K5）。
- **hint**：`Enter:run Esc:close`（不寫移動鍵，見 [`layout/popup`](../layout/popup-zh_TW.md) 的 hint）。工作清單的 hint 見下面。

## 模式裡

模式裡按 `Space`（Rules K11）打開的 Space menu，只列模式裡能做的事：

- **標題**：跟平常一樣寫模式所在的地方 —— panel 上寫 focus panel 的 `[N] label`，popup 裡寫那個 popup 的標題。
- **`ITEM OPERATION`**：現在對 cursor 上那一項（或選起來的範圍）能做的事，跟平常的列一樣能執行，選了就等於按那個鍵（例：Compare
  模式的 `[C]ompare`，說明 `with <anchor>`；選取模式還沒開始選時的 `[v] Select`、開始選之後的 `[y] Copy`）。現在不能做的照 M6 停用
  （例：cursor 在 anchor 上）。
- **`<模式名> MODE`**（例：`COMPARE MODE`；有好幾層時寫整個名字，例：`VISUAL>SELECT MODE`）：模式本身的鍵。移動鍵只顯示 —— 鍵寫在 label 的位置、Blue（跟 key reference 一樣是
  「現在按得了的鍵」），說明 Overlay0；cursor 跳過，`Enter` 不作用。真的做事的跟一般的列一樣能執行：離開模式，
  字用模式 hint 裡 `Esc` 的動詞（Compare 模式是 `[Esc] Leave`，hint 寫 `Esc:cancel` 的是 `[Esc] Cancel`）。
- panel、item、global 的動作與 `Global operation` 那一列一律不列。
- menu 裡按 `Esc` 照舊是關掉 menu（K4）、回到模式；離開那一列的 `[Esc]` 是在模式裡按的鍵，跟 `[Enter] Connect` 一樣。

**為什麼**：「不知道怎麼辦就按 `Space`」在模式裡也要有回應。對眼前這一項的事跟平常的 Space menu 一樣能直接執行；移動鍵從清單
執行沒有意義，只告訴使用者能按什麼，所以 cursor 跳過、鍵用 Blue。

## 工作清單

列出 app 正在跑或跑過的工作（例：sshu 的 Jobs）。

- **列跟著工作更新**（見「長相」）。
- **`Enter` 對 cursor 那一列**：
  - 可以對那一列做事的（例：進行中的傳輸可以取消）：`Enter` 打開一個 confirm，內容是那一列的全文，問句問要不要做那件事
    （[`dialog/confirm`](confirm-zh_TW.md)）。hint 寫那個動作：`Enter:cancel Esc:close`。
  - 沒有動作可做的：`Enter` 打開那一列的全文（Rules F1），hint `Enter:detail Esc:close`。那裡的 `Enter` 不執行任何東西。
  - hint 跟著 cursor 那一列換，寫按下去會發生什麼（Rules M5）。

**為什麼**：工作清單是用來看工作進行到哪裡的，列不動就要一直關掉重開。`Enter` 永遠是「對這一列」：能做事的先看全文、再確定，
不會一按就把傳到一半的東西取消掉。

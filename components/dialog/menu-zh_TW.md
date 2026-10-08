# menu（從清單選一列執行）

**Language**: [English](menu.md) · 繁體中文

## 用途

沒有搜尋的清單，選一列執行（Rules F1）：Space menu、global operation popup、排序選擇器、工作清單（`Enter` 打開那一列的全文）。
清單需要搜尋時是 finder（[`input/finder`](../input/finder-zh_TW.md)）；選的是一個值、要寫回去時是 select（[`input/select`](../input/select-zh_TW.md)）。

## 長相

```
╭─ ≡ [2] Hosts ─────────────────────────────────╮
│                                               │
│ item operation                                │  ← 區塊標題
│▓[Enter] Connect▓▓▓▓▓▓▓▓▓▓▓what it is, then in▓│  ← cursor
│ [E]dit                       change this host │
│ [X] Delete             remove from hosts.yaml │
│ ───────────────────────────────────────────── │  ← 分隔線
│ panel operation                               │
│ [A]dd                              a new host │
│ [/] Search          name, user, host, port, … │  ← 說明太長
│ ───────────────────────────────────────────── │
│ Global operation    actions for the whole app │
│                                               │
╰─ Enter:run Esc:close ─────────────────────────╯
```

（`≡` 代表 `nf-fa-bars`。）

- **每一列**：label 用 Text，`[x]` 跟 label 同色；熱鍵怎麼標見 Rules M5。說明用 Overlay0，靠右，離右框一格；太長從尾端截，
  加 `…`（M5：單行）。
- **區塊標題**：Overlay0、縮一格、不加粗；cursor 跳過。
- **分隔線**：照 [`layout/popup`](../layout/popup-zh_TW.md) 的分隔線（不接框、Overlay0）；cursor 跳過。
- **cursor**：層色底、Base 粗體，佔滿整個內寬，整列都是 Base 字。
- **停用的列**：整列 Surface2，cursor 跳過，按熱鍵不作用（Rules M6）。
- **標題**：`nf-fa-bars` 加文字。Space menu 寫 focus panel 的 `[N] label`（它列的就是那個 panel 能做的事）；其他 menu 寫它做什麼
  （`Global operation`、`Sort by`）。
- **`Global operation` 那一列**（Rules M2）：沒有熱鍵，說明一律是 `actions for the whole app`。
- **寬度**：每一列打開時就確定，照 [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」。

**為什麼**：說明靠右，名稱與說明各成一欄，眼睛往下掃名稱時不會被說明打斷。cursor 用層色底：在家族的 popup 裡，層色底的那一塊
就是 `Enter` 會作用的地方（表單也一樣）。

## 按鍵

- `j/k` 移動，頭尾相接；`u/d` 半頁、`gg/G` 頭尾（Rules K12）。
- `Enter` 執行 cursor 那一列，熱鍵直接執行那一列。
- `Esc` 關掉（global operation popup 回到 Space menu，Rules F4）；Space menu 也可以再按 `Space` 關（Rules K5）。
- **hint**：`Enter:run Esc:close`（不寫移動鍵，見 [`layout/popup`](../layout/popup-zh_TW.md) 的 hint）。

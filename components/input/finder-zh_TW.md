# finder（清單加搜尋）

**Language**: [English](finder.md) · 繁體中文

## 用途

清單加搜尋的 popup：上面打字篩選，下面清單選。一般的 finder 是「到那裡」（filu 的 Search、Find、Goto，webu 的 `/`）。

這些都是 finder 的一種，各自只寫跟這裡不同的地方：

| 種類 | 做什麼 |
|---|---|
| [`select`](select-zh_TW.md) | 選一個值（slider 的數字清單、color picker 的 00–FF 也是） |
| [`checkbox`](checkbox-zh_TW.md) 的 popup | 選好幾個值 |
| [`file-picker`](file-picker-zh_TW.md) | 選一個檔 |

沒有搜尋的清單是 menu（[`dialog/menu`](../dialog/menu-zh_TW.md)）。panel 上直接打字的篩選是 panel filter（[`layout/panel`](../layout/panel-zh_TW.md)），
打字列的按鍵跟這裡一樣。

## 長相

```
╭─ Search ────────────────────────────╮ ╭─ README.md ───────────────────────╮
│                                     │ │                                   │
│  read                          3/41 │ │ # terminu                         │
│ ─────────────────────────────────── │ │                                   │
│ ▓README.md▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ │ │ The terminal UI you can use…      │
│  README-zh_TW.md                    │ │                                   │
│  docs/readme-notes.md               │ │                                   │
│                                     │ │                                   │
╰─ Enter/Tab:list Esc:cancel ─────────╯ ╰───────────────────────────────────╯
```

- **兩塊**：上面是打字列，右邊寫篩選的筆數 `符合/總數`（`3/41`）；一條分隔線（不接框，[`layout/popup`](../layout/popup-zh_TW.md)）；下面是清單。
- **預覽**：一般的 finder 一定有（select、checkbox popup 沒有：值沒有內容可以預覽）。選中的那一筆在旁邊預覽。
  - 清單框與預覽框加起來是一個 popup 的寬（Rules F7 的上限）。terminal 寬 ≥ 96 時左右並排、各佔一半；不夠時上下疊，預覽在下面。
  - 預覽框的標題是選中那一筆的名字（或它在哪裡）；預覽不拿 focus。預覽的內容由 app 決定（檔案內容、目錄樹、網頁的那一段）。
- **邊找邊列**：結果陸續到時照樣列出，標題後面放 loading icon；一筆都還沒到時寫 `(indexing…)`。
- **大小**：高度打開時定好（Rules F7）；寬度不確定，用 F7 的上限。

### 清單的標記

select 與 checkbox popup 的每一列，最前面放一個標記：

| | 每一列前面 | 目前的值 |
|---|---|---|
| **select（單選）** | radio glyph：選中 `nf-md-radiobox_marked`（U+F043E）、沒選 `nf-md-radiobox_blank`（U+F043D） | 字是 Green |
| **checkbox popup（多選）** | checkbox glyph：勾了 `nf-md-checkbox_marked`（U+F0132）、沒勾 `nf-md-checkbox_blank_outline`（U+F0131） | 字是 Green |

- 標記在左邊，眼睛往下掃就看得到；所有列的字對齊；目前的值有顏色（[`color`](../color-zh_TW.md) 的 Green 是「生效中」）。cursor 停在
  目前的值上時，底色照 cursor、字照 cursor 的 Base。
- 單選用 radio glyph，多選用 checkbox glyph：看 glyph 就知道是單選還是多選，畫在表單上還是 popup 裡都一樣。

## 狀態

只有有 focus 的那一塊是亮的（Principle P6、Rules F1）：

| focus 在 | 打字列 | 清單的 cursor |
|---|---|---|
| 打字列 | 照 input 的打字列畫：值 Lavender、有游標 | 層色 cursor 再淡化一次 |
| 清單 | 整列用灰色（Overlay0）畫，沒有游標 | 層色底、Base 粗體（跟 menu 的 cursor 一樣） |

## 按鍵

### 打字列

panel filter 也用這一張表。

| 鍵 | 作用 |
|---|---|
| 字元 | 打進去，清單即時篩選（輸入態，Rules K8；編輯鍵照 [`input/README`](README-zh_TW.md)） |
| `↑`/`↓` | 在結果之間移 cursor（方向鍵打不出字，不衝突） |
| `Enter` | focus 移到 cursor 那一項，不執行；沒有結果時不作用 |
| `Tab` | focus 移到清單 |
| `Esc` | 關掉整個 finder（Rules F1：階段不是一層）；panel filter 是清掉篩選 |

### 清單

| 鍵 | 作用 |
|---|---|
| `j`/`k` 等 | 移動（Rules K12） |
| `Enter` | 去那裡（select 選定、checkbox popup 套用、file-picker 選檔或進目錄） |
| `Tab` | 回打字列 |
| `/` | 回打字列，接著舊的字打 |
| `Esc` | 關掉整個 finder |

### hint

| focus 在 | hint |
|---|---|
| 打字列 | `Enter/Tab:list Esc:cancel` |
| 清單 | `Enter:<去那裡的動詞> Tab:filter Esc:cancel`（例：`Enter:open`） |

**為什麼**：打字列上的 `Enter` 先 focus 到那一項、再按一次才執行：從打字列回到清單時，不會順手打開東西。代價是多按一下
`Enter`；fzf、VS Code 快速開檔那種「打字時 `Enter` 直接去」不採用 —— finder 的打字列與 panel filter 是同一種打字列，同一個鍵在兩處
次數不同，使用者記不住。

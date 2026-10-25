# finder（清單加搜尋）

**Language**: [English](finder.md) · 繁體中文

## finder.1 用途

清單加搜尋的 popup：上面打字篩選，下面清單選。一般的 finder 是「到那裡」（filu 的 Search、Find、Goto，webu 的 `/`）。

這些都是 finder 的一種，各自只寫跟這裡不同的地方：

| 種類 | 做什麼 |
|---|---|
| [`select`](select-zh_TW.md) | 選一個值（slider 的數字清單、color picker 的 00–FF 也是） |
| [`checkbox`](checkbox-zh_TW.md) 的 popup | 選好幾個值 |
| [`file-picker`](file-picker-zh_TW.md) | 選一個檔 |

沒有搜尋的清單是 menu（[`dialog/menu`](../dialog/menu-zh_TW.md)），排順序的是 reorder（[`reorder`](reorder-zh_TW.md)）。panel 上直接打字的篩選是 panel filter（[`layout/panel`](../layout/panel-zh_TW.md)），
打字列的按鍵跟這裡一樣。

## finder.2 長相

terminal 寬 ≥ 96（例：96×24）：

```
┏━SEARCH━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ ┏━README.md━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                            ┃ ┃                                             ┃
┃  read                                3/41 ┃ ┃  1 # terminu                                ┃
┃ ────────────────────────────────────────── ┃ ┃  2                                          ┃
┃▓README.md▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃ ┃  3 The terminal UI you can use without      ┃
┃ README-zh_TW.md                            ┃ ┃  4 reading a manual first.                  ┃
┃ docs/readme-notes.md                       ┃ ┃  5                                          ┃
┃                                            ┃ ┃  6 ## Principle                             ┃
┃                                            ┃ ┃  7                                          ┃
┃                                            ┃ ┃  8 Every action can be found from the menu. ┃
┃                                            ┃ ┃  9                                          ┃
┃                                            ┃ ┃ 10 ## Components                            ┃
┃                                            ┃ ┃ 11                                          ┃
┃                                            ┃ ┃ 12 Frames, popups, inputs and dialogs.      ┃
┃                                            ┃ ┃ 13                                          ┃
┃                                            ┃ ┃ ─────────────────────────────────────────── ┃
┃                                            ┃ ┃ TYPE      text                              ┃
┃                                            ┃ ┃ SIZE      4.2 KB                            ┃
┃                                            ┃ ┃ MODIFIED  2026-10-10 09:12                  ┃
┃                                            ┃ ┃ MODE      -rw-r--r--                        ┃
┃                                            ┃ ┃                                             ┃
┗━ Enter|Tab:list Esc:cancel ━━━━━━━━━━━━━━━━┛ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

terminal 寬不到 96（例：80×24）：

```
┏━SEARCH━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ ┏━INFO━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                    ┃ ┃                                     ┃
┃  read                        3/41 ┃ ┃ TYPE      text                      ┃
┃ ────────────────────────────────── ┃ ┃ SIZE      4.2 KB                    ┃
┃▓README.md▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃ ┃ MODIFIED  2026-10-10 09:12          ┃
┃ README-zh_TW.md                    ┃ ┃ MODE      -rw-r--r--                ┃
┃ docs/readme-notes.md               ┃ ┃                                     ┃
┃                                    ┃ ┃                                     ┃
┃                                    ┃ ┃                                     ┃
┃                                    ┃ ┃                                     ┃
┗━ Enter|Tab:list Esc:cancel ━━━━━━━━┛ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
┏━README.md━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                                            ┃
┃  1 # terminu                                                               ┃
┃  2                                                                         ┃
┃  3 The terminal UI you can use without                                     ┃
┃  4 reading a manual first.                                                 ┃
┃  5                                                                         ┃
┃  6 ## Principle                                                            ┃
┃  7                                                                         ┃
┃                                                                            ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **兩塊**：上面是打字列，下面是清單，中間一條分隔線（不接框，[`layout/popup`](../layout/popup-zh_TW.md)）。
  - 打字列最前面是 `nf-fa-angle_right`（U+F105），離框一格，後面空一格才接打的字（寬度照 Rules E5 的 icon 寬）：一看就知道這一列是
    打字篩選的地方；打開時 focus 在清單上的（select、checkbox popup、file-picker），還沒打字也不會是一片空白。它是 glyph，
    不是 placeholder（[`input/README`](README-zh_TW.md)）。
    顏色跟著打字列的亮暗：focus 在清單時跟整列一樣是 Overlay0，focus 在打字列時是該層的層色。
  - 打字列右邊寫篩選的筆數 `符合/總數`（`3/41`），Overlay0：它是輔助資訊，不跟打的字搶；focus 在清單時整列本來就是 Overlay0，
    數字不用變色。
- **預覽**：一般的 finder 一定有（select、checkbox popup 沒有：值沒有內容可以預覽）。選中的那一筆在旁邊預覽。
  - **預覽的是檔案或目錄時**（例：filu 的 Search、Find、Goto），照 [`file-picker`](file-picker-zh_TW.md) 的預覽：內容、metadata 四列、
    `hide_secrets_in_preview` 都一樣。其他的預覽（例：網頁的那一段）內容由 app 給，沒有 metadata。
  - **排法**：清單與預覽加起來是一個 popup 的寬（Rules F7 的上限）。
    - terminal 寬 ≥ 96：左右並排、各佔一半。有 metadata 時，右框是「預覽／分隔線／metadata」。
    - 不到 96、有 metadata：上面一列是清單框與 metadata 框，左右各一半（跟並排時一樣寬）；下面是整條寬的預覽框；上下各一半高。
      metadata 自己一個框，標題 `INFO`。80×24 時清單 5 筆、預覽 7 列。
    - 不到 96、沒有 metadata：上下疊，清單在上、預覽在下，各一半。
  - 預覽框的標題是選中那一筆的名字（或它在哪裡）；預覽不拿 focus。
  - 預覽框的框線與標題膠囊用該層的層色（跟清單框一樣）；內容不淡化（預覽是拿來看的，暗了難讀）；下框不寫字（沒有 hint，也沒有捲動位置）。
  - **從某一行開始的預覽**（例：用內容找到的檔，從找到的那一行看起）：那一行放在預覽的第三列，上面留兩行前文，不另外標；行號照
    檔案真實的行號。整個檔放得下預覽時從第 1 行畫，不用捲。
- **邊找邊列**：結果陸續到時照樣列出，標題後面放 loading icon；一筆都還沒到時寫 `(indexing…)`。
- **大小**：有預覽的 finder 一律取 Rules F7 的最高（畫面高度 − 2）：預覽每一筆長度不一樣，打開時不知道要多高，取最高換哪一筆框都
  不跳，預覽的空間也最大；清單短時下面空著。沒有預覽的（select、checkbox popup）高度打開時定好（F7）。
- **寬度**：有預覽的照上面的「排法」，是 F7 的上限。選項打開時就知道的（select、checkbox popup）寬度照選項確定（[`layout/popup`](../layout/popup-zh_TW.md)
  的「內容的寬度打開時就確定」）；邊找邊列、結果要等搜尋的才不確定，用 F7 的上限。

### finder.3 清單的標記

select 與 checkbox popup 的每一列，最前面放一個標記：

| | 每一列前面 | 目前的值 |
|---|---|---|
| **select（單選）** | radio glyph：選中 `nf-md-radiobox_marked`（U+F043E）、沒選 `nf-md-radiobox_blank`（U+F043D） | 字是 Green |
| **checkbox popup（多選）** | checkbox glyph：勾了 `nf-md-checkbox_marked`（U+F0132）、沒勾 `nf-md-checkbox_blank_outline`（U+F0131） | 字是 Green |

- 標記在左邊，眼睛往下掃就看得到；所有列的字對齊；目前的值有顏色（[`color`](../color-zh_TW.md) 的 Green 是「生效中」）。cursor 停在
  目前的值上時，底色照 cursor、字照 cursor 的 Base。
- **Green 跟著畫面上的勾與點**：checkbox popup 裡按 `Space` 勾了就是 Green、取消就不是，還沒按 `Enter` 也一樣。popup 裡的 Green
  讀成「按 `Enter` 就是這個值」：勾與顏色永遠一致，使用者不用讀兩種訊號；要回到原本的值按 `Esc`。
- 單選用 radio glyph，多選用 checkbox glyph：看 glyph 就知道是單選還是多選，畫在表單上還是 popup 裡都一樣。

## finder.4 狀態

只有有 focus 的那一塊是亮的（Principle P6、Rules F1）。這裡講的是 focus 會停的兩塊（打字列與清單）；預覽拿不到 focus，
不在其中，一直照上面的「預覽」畫：

| focus 在 | 打字列 | 清單的 cursor |
|---|---|---|
| 打字列 | 照 input 的打字列畫：值 Lavender、有游標；前面的 icon 用層色 | 層色 cursor 再淡化一次 |
| 清單 | 整列用灰色（Overlay0）畫（含前面的 icon 與筆數），沒有游標 | 層色底、Base 粗體，右邊的留白是箭頭（跟 menu 的 cursor 一樣） |

## finder.5 按鍵

一般的 finder 打開時 focus 在打字列：它是「到那裡」的搜尋，打開就是要打字（select、checkbox popup、file-picker 打開時在清單上，
見各自的檔）。

### finder.6 打字列

panel filter 也用這一張表。

| 鍵 | 作用 |
|---|---|
| 字元 | 打進去，清單即時篩選（輸入態，Rules K8；編輯鍵照 [`input/README`](README-zh_TW.md)） |
| `↑\|↓` | 在結果之間移 cursor，到頭尾繞回（方向鍵打不出字，不衝突） |
| `Enter` | focus 移到 cursor 那一項，不執行；沒有結果時不作用 |
| `Tab` | focus 移到清單 |
| `Esc` | 關掉整個 finder（Rules F1：階段不是一層）；panel filter 是清掉篩選 |

### finder.7 比對

打字列上打的字怎麼篩選。一般的 finder、select、checkbox popup、file-picker 打的一般的字、panel filter 都一樣：

- **包含**：不分大小寫，打的字要連續出現在那一項裡。例：`prod` 符合 `Prod-Web-01`；只是依序含有 p、r、o、d 的
  `db-replica-tokyo-ap-northeast-1` 不符合。
- **好幾個詞**：用空白分開的每個詞都要出現，順序不拘。例：`prod 22` 找得到 port 22 的 `prod-web-01`（panel 上可以跨欄）。
- **順序**：結果保持清單本來的順序，不重排；清單本來的順序是固定的（資料沒有順序時 app 先排好，[`layout/panel`](../layout/panel-zh_TW.md)）。數字照數值排（`9` 在 `10` 前面），文字照文字排（[`layout/panel`](../layout/panel-zh_TW.md)
  的表頭）。
- **比對的對象，app 可以自行決定**：預設是每一項顯示的字；也可以是項目的其他內容（例：filu 用檔案的內容找檔，打的字比對的是檔案裡的字）。
- **搜尋要花時間時**（例：讀每個檔的內容、交給搜尋工具或遠端一次找一批）：照上面的「邊找邊列」，標題後面放 loading icon，結果陸續
  列出；打字列照常能打，不等搜尋做完。

**為什麼**：字要連續出現才有過濾的效果；只要依序出現就算的比對，會留下一大堆不相干的項目，只能靠分數重排把要的推到前面。
保持原本的順序，清單的排序（panel 表頭的排序標示）一直是對的；數字與文字也用同一種比對：打 `20`，剩下 20、120、200–209，
照大小排（[`slider`](slider-zh_TW.md)）。

### finder.8 清單

| 鍵 | 作用 |
|---|---|
| `j\|k` 等 | 移動（Rules K12：一步一步的移動到頭尾繞回） |
| `Enter` | 去那裡（select 選定、checkbox popup 套用、file-picker 選檔或進目錄）；沒有結果時不作用（checkbox popup 例外，見下） |
| `Tab\|/` | 回打字列，接著舊的字打 |
| `Esc` | 關掉整個 finder |

### finder.9 hint

| focus 在 | hint |
|---|---|
| 打字列 | `Enter\|Tab:list Esc:cancel` |
| 清單 | `Enter:<去那裡的動詞> Tab\|/:filter Esc:cancel`（例：`Enter:open`） |
| 打字列，沒有結果 | `Tab:list Esc:cancel` |
| 清單，沒有結果 | `Tab\|/:filter Esc:cancel` |

沒有結果時（包括邊找邊列、一筆都還沒到時）兩處的 `Enter` 都不作用，hint 拿掉 `Enter`，有結果時再放回來 —— 跟 [`dialog/form`](../dialog/form-zh_TW.md) 的按鈕還在跑時
一樣，hint 只寫按得動的鍵。select、file-picker 也一樣。checkbox popup 清單上的 `Enter` 是寫回勾好的整組，沒有結果時照樣作用
（[`checkbox`](checkbox-zh_TW.md)）。

**為什麼**：打字列上的 `Enter` 先 focus 到那一項、再按一次才執行：從打字列回到清單時，不會順手打開東西。代價是多按一下
`Enter`；fzf、VS Code 快速開檔那種「打字時 `Enter` 直接去」不採用 —— finder 的打字列與 panel filter 是同一種打字列，同一個鍵在兩處
次數不同，使用者記不住。

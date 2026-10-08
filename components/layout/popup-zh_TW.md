# popup（浮在畫面上的框）

**Language**: [English](popup.md) · 繁體中文

popup 是浮在畫面上的框。這個檔只定框本身，不定框裡放什麼：輸入或選出一個值的是 input（[`input/`](../README-zh_TW.md#input)），
其他的是 dialog（[`dialog/`](../README-zh_TW.md#dialog)）。popup 的分類、尺寸、層疊淡化見 Rules F1–F8。

## 外框

```
╭─ Title ─────────────────────────────────────╮
│                                             │   ← 留白
│ content                                     │
│ content                                     │
│                                             │   ← 留白
╰─ Enter:run Esc:close ────────────── 4 of 12 ╯
```

- **線型**：圓角 `╭─╮`，層色（[`color`](../color-zh_TW.md)）。popup 一律圓角：最上層的 popup 有 focus，靠亮暗分辨（Rules F8、
  Principle P6），不靠線型 —— 圓角在 popup 上不代表失焦。
- **標題**：glyph + 文字，放在上框 `╭─ ` 後面，層色、粗體。文字寫這個 popup 是做什麼的（`Rename`、`New host`、
  `Add bookmark`）；太長從尾端截，加 `…`。glyph：

  | popup | glyph |
  |---|---|
  | menu | `nf-fa-bars`（U+F0C9） |
  | key reference | `nf-fa-question_circle`（U+F059） |
  | confirm | `nf-md-shield_alert`（U+F0ECC） |
  | toast | 依種類，見 [`dialog/toast`](../dialog/toast-zh_TW.md) |
  | terminal | `nf-md-console`（U+F018D） |
  | input、表單、note | 由 app 選：它編輯或顯示的東西（例：Rename 用一支筆）；避開太細的 outline glyph |

- **hint**：放在下框 `╰─ ` 後面，寫法照 Rules M5。
  - **順序**：`Enter` 第一 → 這個 popup 自己的鍵 → 換塊的 `Tab:…` → `Esc` 最後。terminal 例外：出口鍵第一（[`dialog/terminal`](../dialog/terminal-zh_TW.md)）。
  - **不寫在項目之間移動的鍵**（`j/k`、`↑/↓`、表單換欄的 `Tab`），只寫動作與離開：使用者操作一下就知道。切換塊的鍵不算移動，
    照寫（例：finder 的 `Tab:list`）。
  - **放不下時從尾端整組捨棄**，不截在項目中間；下框右邊的捲動位置留著。
  - **只有打字列的 popup**（text、password、number）：`?` 在那裡是字元，hint 要列出全部操作，而且 80 欄放得下（Rules M3）。
- **下框右邊**：內容放不下時的捲動位置（見下面的「內容放不下時」）。
- **留白**：內容上下各留一列空白，左右離框一格。每一種 popup 都有，viewer 也一樣；只有 terminal 例外
  （[`dialog/terminal`](../dialog/terminal-zh_TW.md)）。
- **分隔線**：popup 裡的分隔線不接框 —— 橫的左右各留一格空白，直的不畫進上下的留白。顏色 Overlay0。

**為什麼**：標題、hint、留白的位置固定，每一個 popup 一打開，使用者的眼睛就知道去哪裡找「這是什麼」「能按什麼」。
分隔線不接框：接上框的線看起來像把一個框切成兩個框，而它只是把內容分段。

## 寬度

Rules F7 的兩種寬度，打開時定好，開著時不變：

| | 寬度 | 例 |
|---|---|---|
| **內容的寬度打開時就確定** | 最寬的那一列 + 4（左右各一格框、一格留白），至少放得下標題與 hint，最寬 `min(terminal 寬 − 2, 120)` | 有長度上限的輸入（PIN 最多 12 碼：12 + 11 個空格 + 4 = 27 格）、confirm、menu、key reference、toast、error popup、datetime picker、color picker |
| **內容的寬度不確定** | `min(terminal 寬 − 2, 120)` | 自由打字的 text、網址、串流內容、搜尋結果、表單 |

「確定」指的是打開那一刻就知道最寬會有多寬，不是看現在打了幾個字：PIN 打第一碼時框就是 27 格，不會跟著長。

窄的內容靠左，離框一格（例：confirm、datetime picker、color picker）；toast 的文字與 password 的解鎖遮罩置中。

## 開關動畫

Rules F2：打開與關閉都要有動畫。長度全家族一樣：8 格 × 16ms ≈ 128ms，開啟與關閉對稱。動畫的形式由 app 決定。

**為什麼**：128ms 看得出框疊上來、退下去，又短到連續開關幾層也不用等。

## loading

Rules F7：popup 在 loading 時，標題後面一定放一個輪轉的 loading icon。panel 在 loading 時放在膠囊後面
（[`panel`](panel-zh_TW.md)）。規格：

- 字形：`nf-md-circle_slice_1` 到 `nf-md-circle_slice_8`（U+F0A9E–U+F0AA5）八格，一個圓一片一片填滿，滿了再從頭。
- 速度：一格 90ms，一圈 720ms。
- 哪一格由時鐘決定：`frames[(now / 90ms) % 8]`，不是計數；tick 只在有東西 loading 時續排。
- 寬度：一格；跟它取代的靜止 glyph 同寬，換上換下不位移。braille 點字的形狀與寬度不合，不用。
- 顏色：跟旁邊的字同色；放在 popup 標題後面時用該層的層色（粗體）。

## 取消與完成

取消回到 source（Rules F4）；完成之後 source 留不留，照 Rules T1。

## 內容放不下時

Rules F7：打開時定高、最高是畫面高度 − 2，超過就在框裡捲動。

- 只有內容區捲動；上下留白、錯誤列、上下框固定不動。
- 跟著 focus 捲，捲最少的量，讓 focus 所在的那一個整個看得到。不把 focus 固定在中間。
- 放不下時，下框右邊寫捲動位置，層色：有 cursor 的寫 `N of M`（focus 所在的那一個是第幾個、總數）；沒有 cursor 的
  （note）寫看得到的行 `N-M of T`。全放得下時不寫。
- 以什麼為單位由各種類定（例：表單以欄位為單位，上下式的 label 與值兩列、radio 的幾個選項都算同一欄）。

```
╭─ Title ────────────────────────────────────────╮
│                                                │   ← 留白
│ content                                        │   ← 內容區：只有這一段捲動
│ content                                        │
│ content                                        │
│                                                │
│ error                                          │   ← 錯誤列：固定不動
│                                                │
╰─ hint ──────────────────────────────── 4 of 12 ╯
```

## 錯誤列

- **位置**：內容區下面、固定不捲的一列，跟內容之間空一列。種類可以在它下面再加固定的列（例：表單的分隔線與動作列）。
- **只有值可能不合格的 popup 才預留**（Rules F7）：沒有錯誤時空白，高度不變。
- **只放值的錯**：值不合規則 —— 格式、範圍、必填、名字重複，訊息由 app 寫、很短。
- **樣子**：Red 字，左緣跟內容對齊（內容置中時錯誤列也置中）。框與標題不變色、維持層色：層色說的是「第幾層」，換成 Red
  這個資訊就沒了；而且這個 popup 本身不是錯誤，只是裡面有一個值不合格（表單上還有 Red 的 label）。
- **太長**：只佔一列，從尾端截斷加 `…`。表單上，錯誤列有錯誤時是一個可以 focus 的項目，`Enter` 打開完整的訊息
  （[`dialog/form`](../dialog/form-zh_TW.md)）。input popup 裡錯誤列不拿 focus：那裡是打字的地方（Rules K8）。
- **什麼時候改**：跟著檢查走 —— 只在檢查的時候改：檢查到錯就寫上這次的錯，沒錯就清掉；兩次檢查之間不動，值改了也一樣。
  表單在送出時檢查，input popup 在 `Enter` 時檢查。

**動作本身失敗**（寫檔失敗、遠端拒絕、檔案在底下被改了）不寫錯誤列，直接開一個 error popup 蓋在當前的 popup 上
（[`dialog/note`](../dialog/note-zh_TW.md)）；關掉後回到原本的 popup，值都還在（Rules F4、F5）。

**為什麼**：值的錯跟某一欄有關，寫在框裡，使用者修正時一直看得到。動作的失敗跟哪一欄都無關，訊息要完整顯示，使用者看完
才能決定下一步 —— 重試、改值、或放棄。

> **實作參考（不是規定）**：做對 Rules F3、F8 時踩過的坑，給用 Go 與 Bubble Tea 寫的 app 參考。
>
> - 一個 popup 一個檔、一個 animator。
> - `Esc` 只在一個地方處理（`closeTop`）。
> - 離開的 confirm 用自己的 popup，疊在整疊最上面：`Ctrl-C` 可能在另一個 confirm 開著時按下，借用同一個會蓋掉使用者正在回答的問題。
> - 「放在最上層」要同時改三處：按鍵路由、`closeTop`、繪製順序。
> - `?` 的 key reference 疊在其他 popup 上時，按鍵路由與繪製都把它放在最上層；confirm、options 等框排在底下的 menu 之前拿鍵。
> - 判斷一層「還在不在」用開啟中或已開（`owns()`），不用含關閉中的 `isActive()`（Rules F3）。

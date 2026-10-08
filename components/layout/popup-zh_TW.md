# popup：浮在畫面上的框

**Language**: [English](popup.md) · 繁體中文

popup 是浮在畫面上的框。這個檔只定框本身的樣子，不定框裡放什麼：框裡放什麼由種類決定，輸入一個值的是 input
（[`input/`](../README-zh_TW.md#input)），其他的是 dialog（[`dialog/`](../README-zh_TW.md#dialog)）。popup 的分類、寬度、
開的時候就定高、預留錯誤列、層疊淡化見 rules F1–F8，這裡不重寫。

## 外框

- **標題**：寫這個 popup 是做什麼的（`Rename`、`New host`、`Add bookmark`），glyph + 文字，放在上框。
- **hint**：放在下框。放不下時從尾端整組捨棄（跟 [`screen`](screen-zh_TW.md) 的 footer 一樣），不截在項目中間。**不寫在項目之間移動的鍵**（`j/k`、
  `↑/↓`、表單換欄的 `Tab`），只寫動作與離開：使用者操作一下就知道（user 2026-10-07）。切換階段的鍵不算移動，照寫（例：
  finder 的 `Tab:list`）。
- **留白**：內容上下各留一列空白，左右離框一格。

（標題、hint、留白與 hint 的捨棄 2026-10-07 從 defaults D3 搬來。）

## 開關動畫

Rules F2：打開與關閉都要有動畫。長度全家族統一：8 格 × 16ms ≈ 128ms，開啟與關閉對稱（2026-10-07 從 defaults D3 搬來，
user 定為統一）。動畫的形式由 app 決定。

## loading

Rules F7：popup 在 loading 時，標題後面一定放一個輪轉的 loading icon。規格（2026-10-07 從 defaults D3 搬來；出自 webu 載入網址時的
icon）：

- 字形：Nerd Font `nf-md-circle_slice_1` 到 `_8`（U+F0A9E–U+F0AA5）八格，一個圓一片一片填滿，滿了再從頭。
- 速度：一格 90ms，一圈 720ms。
- 哪一格由時鐘決定：`frames[(now / 90ms) % 8]`，不是計數；tick 只在有東西 loading 時續排。
- 寬度：一格；跟它取代的靜止 glyph 同寬，換上換下不位移（braille 點字的形狀與寬度不合，不用）。
- 顏色：跟旁邊的字同色；放在 popup 標題後面時用該層的層色（bold）。

## 取消與完成

取消回到 source；完成動作清掉整個 stack（T1 的常見答案）。（2026-10-07 從 defaults D3 搬來。）

## 內容放不下時

F7：打開時定高、上限是畫面高度，超過就在框裡捲動。

- 只有內容區捲動；上下留白、錯誤列、上下框固定不動。
- 跟著 focus 捲，捲最少的量，讓 focus 所在的那一個整個看得到。不把 focus 固定在中間。
- 放不下時，下框右側寫 `N of M`：N 是 focus 所在的那一個是第幾個，M 是總數，層色。全放得下時不寫。下框空間不夠時照
  hint 的規則從尾端整組捨，`N of M` 保留。
- 以什麼為單位由各種類定（例：表單以欄位為單位，上下式的 label 與值兩列、radio 的幾個選項都算同一欄）。

```
╭─ Title ────────────────────────────────────────╮
│                                                │   ← 留白
│ content                                        │   ← 內容區：只有這一段捲動
│ content                                        │
│ content                                        │
│                                                │
│ error                                          │   ← 錯誤列（F7 預留）：固定不動
│                                                │
╰─ hint ──────────────────────────────── 4 of 12 ╯
```

## 錯誤列

user 2026-10-07 定。

- **位置**：內容區的最後一列，跟內容之間空一列；固定不捲。種類可以在它下面再加固定的列（例：表單的分隔線與動作列）。
- **只有會失敗的 popup 才預留**（F7）：沒有錯誤時空白，高度不變。
- **樣子**：Red 字，左緣跟內容對齊（內容置中時錯誤列也置中）。框與標題不變色、維持層色：層色說的是「第幾層」（[`color`](../color-zh_TW.md)、F8），
  換成 Red 這個資訊就沒了；錯誤已經有 Red 的錯誤列（表單裡還有 Red 的 label）。
- **只放 input 的錯**（user 2026-10-07）：錯誤列寫的是值不合規則 —— 格式、範圍、必填、名字重複，訊息由 app 寫、很短。
  popup 的動作本身失敗（submit error：改名時檔案系統出錯、寫檔失敗、遠端拒絕、檔案在底下被改了）**不寫在錯誤列**，直接開一個
  **error popup** 蓋在當前的 popup 上：一個 note（F1），框與文字都是 Red，寫完整的訊息；關掉後回到原本的 popup，值都還在
  （F4、F5）。細節見 [`dialog/note`](../dialog/note-zh_TW.md) 的 error popup。
- **太長**：只佔一列，從尾端截斷加 `…`。表單上，錯誤列有錯誤時是一個可以 focus 的項目，`Enter` 打開跟 error popup 一樣的
  note 顯示完整的訊息（user；怎麼走到見 [`dialog/form`](../dialog/form-zh_TW.md)）。input popup 裡錯誤列不拿 focus：那裡是打字
  的地方（K8），而錯誤列只放 app 寫的短訊息。
- **什麼時候改**：跟著檢查走（user）—— 只在檢查的時候改：檢查到錯就寫上這次的錯，沒錯就清掉；兩次檢查之間不動，值改了也
  一樣。表單在送出時檢查，input popup 在 `Enter` 時檢查。

## 實作提醒

2026-10-07 從 Family defaults D3 搬來：做對 F3、F8 時踩過的坑，給用 Go 與 Bubble Tea 寫的 app 參考。

- 一個 popup 一個檔、一個 animator。
- `Esc` 只在一個地方處理（`closeTop`）。
- 離開的 confirm 用自己的 popup，疊在整疊最上面：`Ctrl-C` 可能在另一個 confirm 開著時按下，借用同一個會蓋掉使用者正在回答的問題。
- 「放在最上層」要同時改三處：按鍵路由、`closeTop`、繪製順序。
- `?` 的 key reference 疊在其他 popup 上時，按鍵路由與繪製都把它放在最上層；confirm、options 等框排在底下的 menu 之前拿鍵。
- 判斷一層「還在不在」用開啟中或已開（`owns()`），不用含關閉中的 `isActive()`（Rules F3）。

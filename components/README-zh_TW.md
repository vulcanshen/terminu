# terminu components

**Language**: [English](README.md) · 繁體中文

terminu components 是 [tdp](../principle/README-zh_TW.md) 之下的元件規格：浮在畫面上的框、框裡的每一種內容、panel 上的值，
各長什麼樣、怎麼操作。principle 講原則與規則，components 講具體的元件；terminu family 的 app 照這裡做，做不到的寫進 app 的
dev-remarks「偏離 tdp」。版號、CHANGELOG 跟 tdp 一起走。

## 三個名詞

| 名詞 | 是什麼 | 檔 |
|---|---|---|
| **popup** | 浮在畫面上的框：標題、hint、留白、內容區、捲動、錯誤列的位置。只定框的樣子，不定框裡放什麼 | `layout/popup` |
| **input** | 一種 popup：顯示一個值正在輸入的狀態（輸入態，K8）。一種值一個檔 | `input/` |
| **dialog** | 一種 popup：不是輸入一個值，而是 app 跟使用者對話 —— 表單、清單、確認、唯讀內容、訊息、子程序 | `dialog/` |

- 表單（`dialog/form`）上不打字：要打字或選項放不下的欄位，按 `Enter` 打開那個值的 input popup；選項少的 radio、checkbox，
  選項直接畫在表單上、在原地選。panel 上的值與 panel 裡的搜尋列，談 panel 時再定。
- rules F1 的七類：input 類對 `input/`，其他六類對 `dialog/`，各一個檔（form 是 2026-10-07 加的第七類）。
- 叫 dialog 不叫 modal：modal 講的是「開著時擋住底下」的行為，除了 toast 每個 popup 都會擋，分不出 input 和 dialog；
  dialog 講的是內容 —— app 在跟你對話。

## 在方案裡選

欄位的性質不同（值長或短、欄位多或少），適合的樣子就不同，所以 components 不把每件事寫死成一種，而是列出**幾種方案**，
app 依欄位的性質自己挑。挑的範圍只限列出的方案：方案都不合用時，那是 tdp 的缺漏，回報後補一個方案，不在 app 裡自己發明。

## color

| 檔 | 是什麼 |
|---|---|
| [`color`](color-zh_TW.md) | 配色：呈現規則、計算方式、色碼（2026-10-07 從 defaults D2 搬來） |

## layout

| 檔 | 是什麼 |
|---|---|
| [`screen`](layout/screen-zh_TW.md) | 整個畫面：footer、多畫面的 chip 列、窄寬、空狀態 |
| [`panel`](layout/panel-zh_TW.md) | panel 上的值與輸入 |
| [`popup`](layout/popup-zh_TW.md) | 浮在畫面上的框 |

## dialog

| 檔 | 是什麼 |
|---|---|
| [`form`](dialog/form-zh_TW.md) | 表單：好幾個值填好後一起送出 |
| [`menu`](dialog/menu-zh_TW.md) | 從清單選一列執行 |
| [`confirm`](dialog/confirm-zh_TW.md) | 問一句，`Enter` 接受、`Esc` 取消 |
| [`note`](dialog/note-zh_TW.md) | 唯讀內容 |
| [`toast`](dialog/toast-zh_TW.md) | 從下方彈出的一行訊息 |
| [`terminal`](dialog/terminal-zh_TW.md) | 框裡跑子程序 |

## input

每一種都是一個 popup，顯示那種值正在輸入的狀態。

| 檔 | 是什麼 |
|---|---|
| [`text`](input/text-zh_TW.md) | 一行文字 |
| [`password`](input/password-zh_TW.md) | 遮蔽輸入 |
| [`number`](input/number-zh_TW.md) | 數字 |
| [`textarea`](input/textarea-zh_TW.md) | 多行文字 |
| [`search`](input/search-zh_TW.md) | 搜尋與篩選 |
| [`select`](input/select-zh_TW.md) | 從清單選 |
| [`radio`](input/radio-zh_TW.md) | 幾個選一個 |
| [`checkbox`](input/checkbox-zh_TW.md) | 開關 |
| [`slider`](input/slider-zh_TW.md) | 範圍內的數值 |
| [`datetime-picker`](input/datetime-picker-zh_TW.md) | 日期與時間 |
| [`color-picker`](input/color-picker-zh_TW.md) | 顏色 |
| [`file-picker`](input/file-picker-zh_TW.md) | 選檔（finder 的一種） |

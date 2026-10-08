# terminu components

**Language**: [English](README.md) · 繁體中文

terminu components 是 [tdp](../principle/README-zh_TW.md) 之下的元件規格：配色、畫面、panel、浮在畫面上的框、框裡的每一種內容，
各長什麼樣、怎麼操作。principle 講原則與規則，components 講具體的元件；版號、CHANGELOG 跟 tdp 一起走。

## 什麼是規定

這裡的敘述都是規定。不是規定的只有四種：寫明「由 app 決定」的部分、標成「例」的例子、「為什麼」、標成「實作參考（不是規定）」
的段落。

components 全部算固定區（[Rules 開頭的「偏離」](../principle/rules-zh_TW.md)）：做不到的寫進 app 的 dev-remarks「偏離 tdp」，
寫明原因，同時回報成 tdp 的缺漏。

## 在方案裡選

欄位的性質不同（值長或短、選項多或少），適合的樣子就不同，所以 components 不把每件事寫死成一種，而是列出**幾種方案**，
app 依性質自己挑。挑的範圍只限列出的方案：方案都不合用時，那是 tdp 的缺漏，回報後補一個方案，不在 app 裡自己發明。

## 怎麼讀

依序讀 **color → layout（screen、panel、popup）→ dialog → input**。color 與 layout 是共同的底：每一個元件都用到配色，都畫在
畫面、panel 或框裡；dialog 與 input 是框裡放的東西。

## 三個名詞

| 名詞 | 是什麼 | 檔 |
|---|---|---|
| **popup** | 浮在畫面上的框：標題、hint、留白、內容區、捲動、錯誤列的位置。只定框的樣子，不定框裡放什麼 | `layout/popup` |
| **input** | 一種 popup：輸入或選出一個值，確定後寫回去。一種值一個檔 | `input/` |
| **dialog** | 一種 popup：不是輸入一個值，而是 app 跟使用者對話 —— 表單、清單、確認、唯讀內容、訊息、子程序 | `dialog/` |

- rules F1 的七類：input 類對 `input/`，其他六類對 `dialog/`，各一個檔。
- 表單（`dialog/form`）上不打字：要打字或選項放不下的欄位，按 `Enter` 打開那個值的 input popup；選項少的 radio、checkbox，
  選項直接畫在表單上、在原地選。
- 清單加搜尋就是 finder：一般的 finder、select、checkbox popup、file-picker 都是 finder 的一種（`input/finder`）。沒有搜尋的
  清單是 menu（`dialog/menu`）。
- 叫 dialog 不叫 modal：modal 講的是「開著時擋住底下」的行為，除了 toast 每個 popup 都會擋，分不出 input 和 dialog；
  dialog 講的是內容 —— app 在跟你對話。

## color

| 檔 | 是什麼 |
|---|---|
| [`color`](color-zh_TW.md) | 配色：呈現規則、計算方式、色碼 |

## layout

| 檔 | 是什麼 |
|---|---|
| [`screen`](layout/screen-zh_TW.md) | 整個畫面：footer、畫面 chip 列、statusbar、窄寬、空狀態 |
| [`panel`](layout/panel-zh_TW.md) | panel：框、清單、一列一個值、panel filter |
| [`popup`](layout/popup-zh_TW.md) | 浮在畫面上的框 |

## dialog

| 檔 | 是什麼 |
|---|---|
| [`form`](dialog/form-zh_TW.md) | 表單：好幾個值填好後一起送出 |
| [`menu`](dialog/menu-zh_TW.md) | 從清單選一列執行 |
| [`confirm`](dialog/confirm-zh_TW.md) | 問一句，`Enter` 接受、`Esc` 取消 |
| [`note`](dialog/note-zh_TW.md) | 唯讀內容：key reference、viewer、error popup |
| [`toast`](dialog/toast-zh_TW.md) | 從下方彈出的短訊息 |
| [`terminal`](dialog/terminal-zh_TW.md) | 框裡跑子程序 |

## input

每一種都是一個 popup，輸入或選出那種值。

| 檔 | 是什麼 |
|---|---|
| [`README`](input/README-zh_TW.md) | 所有 input 共用的規則 |
| [`text`](input/text-zh_TW.md) | 一行文字 |
| [`password`](input/password-zh_TW.md) | 遮蔽輸入 |
| [`number`](input/number-zh_TW.md) | 數字 |
| [`textarea`](input/textarea-zh_TW.md) | 多行文字 |
| [`finder`](input/finder-zh_TW.md) | 清單加搜尋；select、checkbox popup、file-picker 都是它的一種 |
| [`select`](input/select-zh_TW.md) | 從清單選一個值 |
| [`radio`](input/radio-zh_TW.md) | 幾個選一個，畫在表單上 |
| [`checkbox`](input/checkbox-zh_TW.md) | 開關，或勾好幾個 |
| [`slider`](input/slider-zh_TW.md) | 範圍內的數值 |
| [`datetime-picker`](input/datetime-picker-zh_TW.md) | 日期與時間 |
| [`color-picker`](input/color-picker-zh_TW.md) | 顏色 |
| [`file-picker`](input/file-picker-zh_TW.md) | 選檔 |

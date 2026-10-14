# terminu components

**Language**: [English](README.md) · 繁體中文

terminu components 是 [tdp](../principle/README-zh_TW.md) 之下的元件規格：配色、畫面、panel、浮在畫面上的框、框裡的每一種內容，
各長什麼樣、怎麼操作。principle 講原則與規則，components 講具體的元件；版號、CHANGELOG 跟 tdp 一起走。

## 什麼是規定

這裡的敘述都是規定。不是規定的只有四種：寫明「由 app 決定」的部分、標成「例」的例子、「為什麼」、標成「實作參考（不是規定）」
的段落。

components 全部算固定區（[Rules 開頭的「偏離」](../principle/rules-zh_TW.md)）：做不到的寫進 app 的 dev-remarks「偏離 tdp」，
寫明原因，同時回報成 tdp 的缺漏。

## 圖與間距

- **圖的結構是規定，圖裡的資料是例**：框、glyph 的位置、間距、對齊、旁邊標的顏色照圖；名稱、數值、說明文字是例。
- **文字跟圖衝突時以文字為準**；兩張圖互相不一致是規範的錯，發現就回報、修掉。
- **數不出來或很難數的數字寫在文字裡**（例：menu 的 label 與說明之間最少幾格，它決定 popup 的寬度）。
- **「縮 N 格」是離框 N 格**：從框線往內數，框線本身不算（例：key reference「每一列縮兩格」，字從框線內第三格開始）。
- **圖裡的 Nerd Font glyph 照實際的 code point 畫**（膠囊的兩端、cursor 尾端的箭頭、區塊標題的六角形、loading icon 等），每一個的
  code point 都寫在文字裡；沒有 Nerd Font 的地方看到的是方塊。底色畫不出來：`▓` 代表 cursor 的色塊，膠囊的底色見文字。
- **兩條通則**，文字沒另外寫時照這兩條：
  - **欄與欄之間兩格**：label 與值、label 與說明、表格的欄、並排的項目。
  - **glyph 與它後面的字之間一格**（例：`󰈔 id_ed25519`、radio 的 `󰐾 password`）。

**為什麼**：間距是使用者看得到的；交給實作，同一種東西在家族裡就會差一兩格，規範也不再是唯一的依據。兩條通則記得住，
新元件照用：兩格就分得開兩欄（label 與值本來就不同色）；glyph 只空一格，看起來跟它後面的字是一組。

## 大寫

- **要大寫的**：panel 的膠囊（`[N] label` 與 tab）、畫面 chip、popup 的標題、表頭、清單的分組標題、一列一個值的 panel 的 label、
  menu 與 key reference 的區塊標題。
- **不改的**：值、menu 的 label 與說明、hint 與 footer 的說明、按鍵名、模式名、app 自己的內容（statusbar、清單裡的資料）。
- **熱鍵標記裡的字母照原樣**：括號裡印的就是要按的鍵，大小寫算數（Rules M5）—— `[M]anage` 寫成 `[M]ANAGE`，`[m]anage` 寫成
  `[m]ANAGE`。
- **標題裡的名稱、路徑是內容，照原樣**：`EDIT: filu`、`ALTERM: myhost`、`IDENTITY FILE · ~/.ssh`（名稱前用什麼隔開見
  [`layout/popup`](layout/popup-zh_TW.md) 的「標題」）。

**為什麼**：大寫的是「這是什麼」—— 名稱、標題、欄名 —— 一眼就跟要讀、要改的內容分開。按鍵名與熱鍵標記不改：`q` 與 `Q` 是
不同的鍵；內容不改：使用者要認得的是它本來的樣子。

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
| [`file-picker`](input/file-picker-zh_TW.md) | 選檔；也有選目錄的一種 |

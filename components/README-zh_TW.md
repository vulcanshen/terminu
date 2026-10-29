# terminu components

**Language**: [English](README.md) · 繁體中文

terminu components 是 [tdp](../principle/README-zh_TW.md) 之下的元件規格：配色、畫面、panel、浮在畫面上的框、框裡的每一種內容，
各長什麼樣、怎麼操作。principle 講原則與規則，components 講具體的元件；版號、CHANGELOG 跟 tdp 一起走。

## components.1 什麼是規定

這裡的敘述都是規定。不是規定的只有三種：標成「例」的例子、「為什麼」、標成「實作參考（不是規定）」的段落。寫「app 可以自行
決定」的地方是明文放行，範圍內還要守的規定寫在旁邊（[Principle P5](../principle/README-zh_TW.md#p5-明文放行)）。

元件的方案不合用時，回報成 tdp 的缺漏，由 tdp 加方案或明文放行（[Rules 開頭的「放行」](../principle/rules-zh_TW.md)）。

## components.2 圖與間距

- **圖的結構是規定，圖裡的資料是例**：框、glyph 的位置、間距、對齊、旁邊標的顏色照圖；名稱、數值、說明文字是例。
- **文字跟圖衝突時以文字為準**；兩張圖互相不一致是規範的錯，發現就回報、修掉。
- **數不出來或很難數的數字寫在文字裡**（例：menu 的 label 與說明之間最少幾格，它決定 popup 的寬度）。
- **「縮 N 格」是離框 N 格**：從框線往內數，框線本身不算（例：key reference「每一列縮兩格」，字從框線內第三格開始）。
- **圖裡的 Nerd Font glyph 照實際的 code point 畫**（膠囊的兩端、cursor 尾端的箭頭、區塊標題的六角形、loading icon 等），每一個的
  code point 都寫在文字裡；沒有 Nerd Font 的地方看到的是方塊。底色畫不出來：`▓` 代表 cursor 的色塊，膠囊的底色見文字。
  標題 glyph app 可以自行決定的 popup（[`layout/popup`](layout/popup-zh_TW.md) 的 glyph 表），圖裡不畫 glyph；實際上 glyph 在標題文字前面，
  空一格。
- **兩條通則**，文字沒另外寫時照這兩條：
  - **欄與欄之間兩格**：label 與值、label 與說明、表格的欄、並排的項目。
  - **glyph 與它後面的字之間一格**（例：`󰈔 id_ed25519`、radio 的 `󰐾 password`）。
- **statusbar 的 `label: 值` 不套用兩格通則**：它是句子式的寫法，冒號後面空一格（`[C]ontext: prod  [N]amespace: default`）；組與組之間兩格，不另外加分隔符號
  （[`layout/screen`](layout/screen-zh_TW.md) 的 statusbar）。

**為什麼**：間距是使用者看得到的；交給實作，同一種東西在家族裡就會差一兩格，規範也不再是唯一的依據。兩條通則記得住，
新元件照用：兩格就分得開兩欄（label 與值本來就不同色）；glyph 只空一格，看起來跟它後面的字是一組。statusbar 的 `label: 值`
是一句話，冒號已經把 label 和值分開，再空兩格反而讀起來斷成兩截；組與組之間的兩格就夠分開，不用再畫一個符號。

## components.3 折行

文字要折行的地方 —— textarea、viewer、confirm、note（例：表單的打字說明）、toast、error popup、空狀態的句子、Rules S5 的 splash
太窄時 —— 都照同一套，放不下就折行、不截斷：

- **在空白處斷**：一列放不下下一個字時，整個字接到下一列（例：英文的一個單字整個走）。
- **寬字（佔兩格的字，例：中文、日文）每個字之間都可以斷**：寬字跟它前後的字之間也算可以斷的地方，一列填滿再換列。
- **一個字本身就比一列還長**（例：很長的網址），才照格子切；這一列前面已經有字時，先換到新的一列再切，不接在後面切。
- **寬字不切成兩半**：照格子切到一列只剩一格時，那個寬字整個接到下一列。
- **斷在空白處時，那個空白**：textarea 與 viewer 的每個字元都要畫出來（游標、選取模式會停在上面），一個字剛好填滿一列、後面接著
  空白時，那個空白畫在下一列的第一格；其他只是顯示的文字（confirm、note、toast、error popup、空狀態、splash），斷在空白處的那個
  空白不畫。

```
see                     ← 一列 20 格：網址放不下，先換列
https://example.com/    ← 從新的一列開頭照格子切
very/long/path/abc
```

**為什麼**：在字的中間斷開，一段文字就讀不下去；splash 本來就這樣斷（Rules S5）。同一套規則，在家族哪裡折行都一樣。長的字先換列
再切，跟「放不下就整個字移到下一列」是同一件事：網址從新的一列開頭，認得出、也好複製，不會一半接在前面的字後面。

## components.4 大寫

- **要大寫的**：panel 的膠囊（`[N] label` 與 tab）、畫面 chip、popup 的標題、表頭、清單的分組標題、一列一個值的 panel 的 label、
  menu 與 key reference 的區塊標題。
- **不改的**：值、menu 的 label 與說明、hint 與 footer 的說明、按鍵名、模式名、app 自己的內容（statusbar、清單裡的資料）。
- **熱鍵標記裡的字母照原樣**：括號裡印的就是要按的鍵，大小寫算數（Rules M5）—— `[M]anage` 寫成 `[M]ANAGE`，`[m]anage` 寫成
  `[m]ANAGE`。
- **名稱、路徑是內容，標題與 hint 裡都照原樣**：標題 `EDIT: filu`、`ALTERM: myhost`、`IDENTITY FILE · ~/.ssh`（名稱前用什麼隔開見
  [`layout/popup`](layout/popup-zh_TW.md) 的「標題」）；表單按鈕的 hint 只有動詞小寫，`Overwrite KBU.svg` → `Enter:overwrite KBU.svg`
  （[`dialog/form`](dialog/form-zh_TW.md) 的 hint）。
- **panel 的標題也一樣**：label 分成「這是什麼」（大寫）與名稱（照原樣），中間的寫法跟 popup 的標題一樣 —— `[2] PODS: nginx-7d4f`；
  整個 label 就是名稱時照原樣 —— `[1] prod-web-01`（[`layout/panel`](layout/panel-zh_TW.md) 的膠囊串）。

**為什麼**：大寫的是「這是什麼」—— 名稱、標題、欄名 —— 一眼就跟要讀、要改的內容分開。按鍵名與熱鍵標記不改：`q` 與 `Q` 是
不同的鍵；內容不改：使用者要認得的是它本來的樣子。

## components.5 控制字元

app 交給畫面的字常常來自外面（檔名、網頁標題、設定檔、程式的輸出），可能帶著控制字元。不論在哪裡，都不原樣送給終端機，照它在
哪一群畫：

- **打字的地方**（輸入框、textarea）：照 [`input`](input/README-zh_TW.md) 的「貼上的控制字元」與 [`input/textarea`](input/textarea-zh_TW.md)。
- **拿來讀的內容**（viewer、panel 上的 log、檔案預覽）：照終端機會畫的樣子（細節見 [`dialog/note`](dialog/note-zh_TW.md) 的 viewer）——
  - `\n` 是換行：app 一行一行交來的內容，一行裡夾著 `\n` 也拆成兩行；換行前面的 `\r`（CRLF）不畫。
  - Tab 畫成 `input_tab_width` 格空白（Rules E3）。
  - 顏色碼（SGR，例：`\x1b[32m`）照著上色；一行裡的 `\r`（進度列）只留最後的狀態。
  - 其他控制字元與不是顏色碼的序列（例：清畫面的 `\x1b[2J`）畫成紅色的名字。
- **名字與短字**（表單與 panel 上的值、清單的格子、menu 的 label 與說明、popup 的標題、toast、confirm、error popup、選項、說明列、
  空狀態、statusbar、tab 的名稱、finder 的項目）：照表單上的值，什麼都不解讀 —— 每個控制字元，連 Tab、`\n`、顏色碼的 ESC，都畫成
  紅色的名字（`\t`、`\n`、`\x1b`，寫法照 input 的「貼上的控制字元」），不丟、不換成空白。
  - 例外：app 把清單的一欄標成「一行文字」（例：原始碼的一行、log 的一行）時，那一欄的 Tab 畫成 `input_tab_width` 格空白，其他控制字元
    照舊。那樣的一欄是拿來讀的，Tab 是排版，不是名字裡的怪東西。
  - **app 自己寫的字不帶換行字元**：要好幾列的地方（error popup 的訊息、toast、confirm 的內容），app 一列一列給，每一列另起
    一列、太長照「折行」折，列跟列之間不空列。所以畫面上的 `\n` 一定是從外面來的（使用者打的、檔名、程式的輸出），照上面畫成名字。
  - 外面來的好幾行字（例：ssh 的 stderr）不整段放進短字：放說原因的那一行，全文寫進 App Log（Rules F5、[`dialog/note`](dialog/note-zh_TW.md) 的 App Log）。

**為什麼**：原樣送出去，`\r` 把那一列從頭蓋掉、`\x1b[2J` 清掉整個畫面，列寬也量不準（Rules L4）。名字與短字是使用者接著要操作的
東西：丟掉或換成空白，兩個不同的名字會看起來一樣（`a b.txt` 與中間是 Tab 的 `a⇥b.txt`）；清單、confirm、改名的輸入框三處要看到
一樣的東西。app 自己寫的字不帶換行：app 的 `\n` 跟名字裡的 `\n` 在畫面上分不出來，以前 lib 會把 app 的 `\n` 換行，改成照名字畫
之後，app 的 `\n` 默默變成紅字，編譯、測試都看不出來（來自 sshu）；app 一列一列給，畫面上的紅色 `\n` 就一定說的是外面的東西
（user 2026-10-24）。拿來讀的內容不一樣：程式的輸出本來就是要在終端機裡長那個樣子，照終端機畫才是它真的樣子，紅字反而把內容遮住。

## components.6 在方案裡選

欄位的性質不同（值長或短、選項多或少），適合的樣子就不同，所以 components 不把每件事寫死成一種，而是列出**幾種方案**，
選哪一種，app 可以自行決定，依性質挑；範圍只限列出的方案：方案都不合用時，那是 tdp 的缺漏，回報後補一個方案，不在 app 裡自己發明。

## components.7 怎麼讀

依序讀 **color → layout（screen、panel、popup）→ dialog → input**。color 與 layout 是共同的底：每一個元件都用到配色，都畫在
畫面、panel 或框裡；dialog 與 input 是框裡放的東西。

## components.8 三個名詞

| 名詞 | 是什麼 | 檔 |
|---|---|---|
| **popup** | 浮在畫面上的框：標題、hint、留白、內容區、捲動、錯誤列的位置。只定框的樣子，不定框裡放什麼 | `layout/popup` |
| **input** | 一種 popup：輸入或選出一個值，確定後寫回去。一種值一個檔 | `input/` |
| **dialog** | 一種 popup：不是輸入一個值，而是 app 跟使用者對話 —— 表單、清單、確認、唯讀內容、訊息、子程序 | `dialog/` |

- rules F1 的八類：input 類對 `input/`，menu、confirm、form、note、toast、terminal 對 `dialog/`，各一個檔；app 自己的 popup
  寫在 `layout/popup`。
- 表單（`dialog/form`）上不打字：要打字或選項放不下的欄位，按 `Enter` 打開那個值的 input popup；選項少的 radio、checkbox，
  選項直接畫在表單上、在原地選。
- 清單加搜尋就是 finder：一般的 finder、select、checkbox popup、file-picker 都是 finder 的一種（`input/finder`）。沒有搜尋的
  清單是 menu（`dialog/menu`），排順序的 reorder 除外（`input/reorder`）。
- 叫 dialog 不叫 modal：modal 講的是「開著時擋住底下」的行為，除了 toast 每個 popup 都會擋，分不出 input 和 dialog；
  dialog 講的是內容 —— app 在跟你對話。

## components.9 color

| 檔 | 是什麼 |
|---|---|
| [`color`](color-zh_TW.md) | 配色：呈現規則、計算方式、色碼 |

## components.10 layout

| 檔 | 是什麼 |
|---|---|
| [`screen`](layout/screen-zh_TW.md) | 整個畫面：footer、畫面 chip 列、statusbar、窄寬、zoom、比最低尺寸小時、空狀態 |
| [`panel`](layout/panel-zh_TW.md) | panel：框、清單、位置列、一列一個值、panel filter |
| [`popup`](layout/popup-zh_TW.md) | 浮在畫面上的框 |

## components.11 dialog

| 檔 | 是什麼 |
|---|---|
| [`form`](dialog/form-zh_TW.md) | 表單：好幾個值填好後一起送出 |
| [`menu`](dialog/menu-zh_TW.md) | 從清單選一列執行 |
| [`confirm`](dialog/confirm-zh_TW.md) | 問一句，`Enter` 接受、`Esc` 取消 |
| [`note`](dialog/note-zh_TW.md) | 唯讀內容：key reference、viewer、error popup |
| [`toast`](dialog/toast-zh_TW.md) | 從下方彈出的短訊息 |
| [`terminal`](dialog/terminal-zh_TW.md) | 框裡跑子程序 |

## components.12 input

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
| [`reorder`](input/reorder-zh_TW.md) | 自己搬動項目，排出順序 |

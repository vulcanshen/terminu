# input（共用的規則）

**Language**: [English](README.md) · 繁體中文

所有 input popup 共用的規則；各 input 檔只寫跟這裡不同的地方。

## 什麼是 input

一種 popup：輸入或選出一個值，確定後寫回去；一個 popup 一個值（Rules F1）。

- **打字列上是輸入態**（Rules K8）：字母、`Space`、`?`、`q` 都是字元。不打字的部分（select 的清單、picker）不是輸入態，core key
  照 Rules K1：`?` 打開 key reference，`q|Ctrl-C` 進離開流程，`Space` 不作用（K5），`hjkl` 移動（K12）。
- **`Enter`**（Rules K3）：focus 在值上時確定這個值 —— 寫回去、popup 關掉。值不合格就不寫回，錯誤寫在錯誤列，popup 不關。值跟打開時
  一樣，就不寫回、直接關掉 —— 只限打開時就合格的值：打開時是空的、這一欄又不能空，什麼都沒打就按 `Enter` 照樣擋下來，錯誤寫在
  錯誤列（有建議值時 `Enter` 用建議值，見下面的「新建一個值：建議值」）。
- **錯誤點名的是值的名字**：從表單的欄位打開的，就是那一欄的名字；自己打開的 input，標題寫的是這個 popup 在做什麼
  （[`layout/popup`](../layout/popup-zh_TW.md) 的 `RENAME`、`SAVE AS`），值的名字由 app 另外給（`Name`）。例：`SAVE AS` 上寫
  `Name can't have control characters`，不寫 `Save as can't have control characters` —— 標題說的是在做什麼，不是值叫什麼。
- **`Esc`**：關掉，值不變。
- **從表單打開的**：確定之後 focus 留在表單的同一欄（Rules K3）。
- **有按鈕的 input popup**（例：color picker 的 `Choose`）：動作區照 [`dialog/form`](../dialog/form-zh_TW.md) —— `Tab|Shift-Tab`
  在欄位區與動作區之間來回，回來時停在離開前的那一個項目；hint 在欄位上寫 `Tab:actions`、在按鈕上寫 `Tab:fields`（Rules K2）。

## 單行 input popup 的骨架

text、password、number 共用。

```
┏━RENAME━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                          ┃
┃ New name for assets                      ┃   ← 說明列：一句話，Overlay0
┃                                          ┃
┃  assets█                                ┃   ← 打字列：`nf-fa-angle_right` 層色，空一格接值；值 Lavender；游標 Lavender 底、Base 字
┃                                          ┃
┃                                          ┃   ← 錯誤列（layout/popup）
┃                                          ┃
┗━ Enter:rename Esc:cancel ━━━━━━━━━━━━━━━━┛
```

- **說明列**：一句話說要輸入什麼（`New name for assets`），Overlay0。跟值之間空一列。要改的對象是誰，寫進這一句。
- **打字列**：最前面是 `nf-fa-angle_right`（U+F105），離框一格，後面空一格才接值，跟 [`finder`](finder-zh_TW.md) 的打字列一樣。
  顏色照 finder：打字時是層色 —— 單行 input popup 一直在打字，所以一直是層色。一看就知道游標停的這一列是要打字的地方。
- **值**：Lavender —— [`color`](../color-zh_TW.md) 裡 Lavender 是「正在編輯的東西」，input popup 裡正在編輯的就是這個值。游標是一格
  Lavender 底、Base 字；停在控制字元上時，整個控制字元畫成 Red 底、Base 字（見下面的「貼上的控制字元」）。
- **錯誤列**：照 [`layout/popup`](../layout/popup-zh_TW.md)。
- **hint**：`Enter:<動詞> Esc:cancel`，動詞寫按下去做什麼（rename、create、save）。這種 popup 只有打字列，`?` 是字元，所以 hint 要列出
  全部操作（Rules M3）。
- **寬度**：自由打字的值，寬度不確定，用 Rules F7 的上限；有長度上限的值（例：PIN、範圍已知的數字），寬度確定，照
  [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」。
- **跟骨架不同的兩處**：password 的解鎖樣式沒有說明列，要輸入什麼由標題講（[`password`](password-zh_TW.md)）；number 有單位時，
  打字列下面多一列單位列（[`number`](number-zh_TW.md)）。

## 值比框長時

框裡顯示游標附近的那一段，被截掉的那一邊補 `…`。

```
┃  …ideproj/terminu/components/layout█ ┃   ← 打字中：游標在尾端，前面截掉
┃  █/Users/vulcan/Documents/sideproj/… ┃   ← Home 之後：游標在開頭，後面截掉
```

- 游標一定看得到；移動時只捲剛好夠的量，不把游標固定在中間（跟 popup 內容放不下時同一個捲法）。
- 寬度照顯示寬度算（中文一個字 2 格）。一個字不切成兩半，紅色的 `\n`、`\x1b` 也一樣。

## 編輯鍵

打字列上：

| 鍵 | 作用 |
|---|---|
| 字元、`Space` | 插在游標處 |
| `←\|→` | 游標往左、往右移一個字 |
| `Home\|End` | 游標跳到最前面、最後面 |
| `Backspace\|Delete` | 刪游標前面的字、游標上的字 |

- **一個字是看起來的一個字**：中文一個字、emoji 一個、組合字元連同前面的字算一個；貼上進來的控制字元各算一個（`\n`、`\x1b`）。
- **不做 shell 的刪字快捷鍵**：`Ctrl-U`、`Ctrl-W` 不收。其他 `Ctrl-`、`Alt-` 組合在打字列上沒有作用、不打出字。

**為什麼**：編輯鍵只收鍵帽上寫著的那幾個，看得到就知道怎麼用。`Ctrl-U`、`Ctrl-W` 在不同 shell 裡行為不一樣，收進來反而要記
「這裡是哪一種」；改掉長值靠下面的灰字提議（重打一個值不用先刪）。

## 改一個已經有的值：舊值是灰字提議

```
┃  █eport-2025.pdf                    ┃   ← 框是空的；舊值是灰字（Overlay0），游標壓在第一個字（`r`）上
```

- **只用在單行的 input**（text、number；password 的舊值是灰點，見 [`password`](password-zh_TW.md)）；textarea 打開時直接帶入舊值（[`textarea`](textarea-zh_TW.md)）。
- 框打開時是空的，舊值用灰字（Overlay0）顯示，從游標那一格開始：游標壓在第一個字上（跟一般的游標一樣，Lavender 底、Base 的字；
  第一個字是控制字元時照「貼上的控制字元」，Red 底），後面接灰字 —— 像 shell 的自動建議。
- `Tab`：把舊值收進框裡，游標在尾端，接著用 `←|→` 改（Rules K2）。
- 直接打字：重打一個新的值，灰字隱藏；把打的字刪光，灰字再出現。
- 值是空的時候按 `Backspace`：不要這個值，灰字消失；這時按 `Enter` 存成空的（欄位不能空時照錯誤處理）。
- 什麼都沒碰就按 `Enter`：不改，關掉。
- 有灰字時 hint 加 `Tab:edit Backspace:clear`（例：`Enter:rename Tab:edit Backspace:clear Esc:cancel`）。
- 灰字提議有兩種來源：舊值，與沒有舊值時 app 給的建議值（下一節）；兩種不會同時出現。沒有提議時 `Tab` 不作用。

**為什麼**：預填的長值要整個換掉時，得按住 `Backspace` 刪到底；提議讓「重打」不用先刪、「小改」多一下 `Tab`、「不改」直接 `Enter`。
這是單行值（檔名、主機名稱）的情況；多行文字改的多半是補一句、改幾個字，而 textarea 的 `Tab` 是縮排，收不了提議。

## 新建一個值：建議值

```
┃  █ssets.zip                         ┃   ← 沒有舊值；app 建議的值是灰字（Overlay0），游標壓在第一個字（`a`）上
```

- **沒有舊值、app 有合理的預設時**（例：打包成的檔名 `assets.zip`、新建的東西的名字），用灰字提議顯示它，叫建議值。只用在單行的
  input（text、number），跟舊值一樣。
- 長相、`Tab`、直接打字、`Backspace`、hint 都跟舊值的提議一樣。
- **差別只在什麼都沒碰就按 `Enter`**：舊值是「不改」，關掉；建議值是「用這個值」，照確定一個值處理 —— 寫回去、照常檢查。
- 欄位不能空、又有建議值時，什麼都沒打按 `Enter` 就用建議值，不會出現「不能空」的錯誤；按 `Backspace` 讓灰字消失後再按 `Enter`，
  才照錯誤處理。

**為什麼**：新建東西時，多半有一個合理的名字可以直接用；建議值讓「照建議」直接 `Enter`、「小改」多一下 `Tab`、「自己取」直接打。
舊值不碰就按 `Enter` 是什麼都不做，建議值不碰就按 `Enter` 是使用者接受了這個值 —— 不寫回的話，`Enter` 等於沒有作用。

## 不放 placeholder

input popup 裡不放 placeholder：要輸入什麼由說明列講；灰字只留給提議。打字列前面的 `nf-fa-angle_right`（單行 input、finder、
panel filter；[`finder`](finder-zh_TW.md)）是 glyph，不是 placeholder：它不是字，按 `Tab` 不會收進來，打字時也不會消失。

**為什麼**：兩種灰字長得一樣，一種按 `Tab` 會收進來、一種不會，會分不出來。

## 貼上的控制字元

- **範圍**：一行的值。多行的 textarea 見 [`textarea`](textarea-zh_TW.md)：換行（含單獨的 `\r`）是真的換行，其他控制字元跟這裡一樣。
  只收數字的欄位照它原本的過濾。
- **只算貼上的文字**：按下去的 `Tab`、`Enter`、`Ctrl-J` 照它們原本的作用。
- **控制字元一個都不丟，照實畫成紅字**（Red，不切開）：`\r`、`\n`、`\t` 寫名字（2 格），其他 C0、DEL、C1 寫 `\xNN`（4 格，例：
  `\x1b`、`\x7f`、`\x85`）。`\r\n` 也照實畫成 `\r\n` 兩個。整列畫成灰色的列（沒有 focus 的打字列、提議）裡跟著灰。
- **游標停在控制字元上**：整個控制字元（`\x1b` 四格、`\r` 兩格）畫成 Red 底、Base 字；一般的字照舊 Lavender 底。看得出游標在
  這裡，也看得出壓在控制字元上。灰字提議的第一個字是控制字元時一樣。
- **`Backspace` 一次刪一整個**（`\n`、`\x1b`……）。
- **遮罩的值照樣遮罩**（password）。
- **不是使用者打字進來的值走同一個過濾**：原本的名字、檔案或別的程式給的值、清單填回來的值、從啟動目錄來的預設值、提議……
  不一一列舉。
- **值會被拿去用的（送出、存、執行、交給別的程式）**：按 `Enter` 時擋下，錯誤列寫原因並點名值（照「什麼是 input」，例：`Name can't have control
  characters`）。**在去掉前後的空白字元之前檢查**：`Icon\r` 去掉空白字元會變成 `Icon`，先去空白字元就檢查不到。
- **搜尋與篩選的打字列只畫，不擋。**

**為什麼**：換成空白或丟掉，都會悄悄改掉使用者貼進來的東西；照實畫出來，使用者看到的就是真的貼進來的，自己決定要不要刪。
只丟控制字元也清不乾淨：從終端機複製帶顏色的字，丟掉 `\x1b` 會留下 `[31m`。游標停在上面時用紅底：Lavender 底上的紅字對比太弱，
照一般游標畫又看不出是控制字元。

## 值

- **一行的值確定時去掉前後的空白字元**：所有 Unicode 的空白字元（一般空格、全形空格 U+3000、NBSP……），不是只有某一種空白；
  password 不去。控制字元的檢查在去空白字元之前（見上面）。看不見的空白字元最難查：從網頁複製來的主機名稱尾巴夾著一個 NBSP、
  值的後面多打了一個全形空格，畫面上一模一樣，用起來卻不對。

## 在表單與 panel 上怎麼顯示

- **顏色**：Text。
- **空的值**：用灰字（Overlay0）寫出「空著代表什麼」，由 app 寫（`not set`、`ssh decides`、`none`）。一片空白看不出是沒設、設成空字串、
  還是還沒載入。不寫教人按鍵的字（例：`enter to browse ~/.ssh`）：hint 會寫 `Enter:edit`。
- **太長**：從尾端截，加 `…`；路徑從前面截（`…/.ssh/id_ed25519`）。
- **控制字元**：跟打字列一樣，照實寫成紅色的轉義（`\n`、`\x1b`，見上面的「貼上的控制字元」），不丟、不換成空白。
- **各種 input**：

  | input | 顯示 |
  |---|---|
  | text | 值本身 |
  | number | 值本身；有單位時空一格接單位，寫完整的字（`10 seconds`，[`number`](number-zh_TW.md)） |
  | password | 設了：固定 8 個 `•`；沒設：照空值 |
  | textarea | 第一行；後面還有就加 `…` |
  | select | 選中那一項的文字 |
  | checkbox popup（多選） | 選中的項目用 `, ` 接起來，太長加 `…` |
  | reorder | 照目前的順序用 `, ` 接起來，太長加 `…` |
  | radio、checkbox（畫在表單上） | 選項本身（[`radio`](radio-zh_TW.md)、[`checkbox`](checkbox-zh_TW.md)） |
  | slider | 軌道加數字（[`slider`](slider-zh_TW.md)） |
  | datetime picker | 格式化的日期（時間），格式由 app 決定（`2026-10-15`、`2026-10-15 10:05`） |
  | color picker | 3 格的色塊（`███`）、空一格、hex（`███ #2A2A3C`，一律大寫，[`color-picker`](color-picker-zh_TW.md)） |
  | file-picker | 路徑，家目錄寫成 `~` |

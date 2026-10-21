# popup（浮在畫面上的框）

**Language**: [English](popup.md) · 繁體中文

popup 是浮在畫面上的框。這個檔只定框本身，不定框裡放什麼：輸入或選出一個值的是 input（[`input/`](../README-zh_TW.md#input)），
其他的是 dialog（[`dialog/`](../README-zh_TW.md#dialog)）。popup 的分類、尺寸、層疊淡化見 Rules F1–F8。

## 外框

```
┏━TITLE━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                             ┃   ← 留白
┃ content                                     ┃
┃ content                                     ┃
┃                                             ┃   ← 留白
┗━ Enter:run Esc:close ━━━━━━━━━━━━━ 4 of 12 ━┛
```

- **線型**：粗線 `┏━┓`，層色（[`color`](../color-zh_TW.md)）；error popup 例外，框與標題膠囊都是 Red
  （[`dialog/note`](../dialog/note-zh_TW.md)）。popup 一律粗線：最上層的 popup 有 focus，靠亮暗分辨（Rules F8、Principle P6），
  不靠線型 —— 粗線在 popup 上不代表 focus，被蓋在底下、淡化了的 popup 照樣是粗線。
- **標題**：glyph + 文字，做成一個膠囊放在上框 `┏━` 後面：兩端是圓角，左 U+E0B6（`nf-ple-left_half_circle_thick`）、右 U+E0B4
  （`nf-ple-right_half_circle_thick`）；填層色（error popup 填 Red），字 Base 粗體、大寫（[components](../README-zh_TW.md) 的「大寫」）。
  文字寫這個 popup 是做什麼的（`RENAME`、`NEW HOST`、`ADD BOOKMARK`）；裡面的名稱、路徑是內容，大小寫照原樣。要寫對哪一個做時，名稱接在
  後面、用 `: ` 隔開（`EDIT: filu`、`ALTERM: myhost`）；viewer 與 file-picker 照自己的寫法（[`dialog/note`](../dialog/note-zh_TW.md)
  的 `YAML — pod/nginx`、[`input/file-picker`](../input/file-picker-zh_TW.md) 的 `IDENTITY FILE · ~/.ssh`）。太長從尾端截，加 `…`。
  標題後面接 tab 時，tab 照 [`panel`](panel-zh_TW.md) 的膠囊串畫，跟標題之間隔一段線
  （例：`┏━TITLE━CONSOLENETWORK━┓`）。glyph：

  | popup | glyph |
  |---|---|
  | menu | `nf-fa-bars`（U+F0C9） |
  | key reference | `nf-fa-question_circle`（U+F059） |
  | confirm | `nf-md-shield_alert`（U+F0ECC） |
  | toast | 依種類，見 [`dialog/toast`](../dialog/toast-zh_TW.md) |
  | terminal | `nf-md-console`（U+F018D） |
  | input、表單、note | 由 app 選：它編輯或顯示的東西（例：Rename 用一支筆）；避開太細的 outline glyph |

- **hint**：放在下框 `┗━ ` 後面，寫法照 Rules M5。
  - **順序**：`Enter` 第一 → 這個 popup 自己的鍵 → 換塊的 `Tab:…` → `Esc` 最後。terminal 例外：出口鍵第一（[`dialog/terminal`](../dialog/terminal-zh_TW.md)）。
  - **不寫在項目之間移動的鍵**（`j|k`、`↑|↓`），只寫動作與離開：使用者操作一下就知道。切換塊的鍵不算移動，
    照寫（例：finder 的 `Tab:list`、表單的 `Tab:actions`）。
  - **框到了最寬還放不下時，從尾端整組捨棄，但最後的 `Esc` 一定留著**：從 `Esc` 前面的那一組開始，一組一組往前捨，不截在
    項目中間；下框右邊的捲動位置留著。框的寬度本來就算進 hint 與捲動位置（見下面的「寬度」），只有 terminal 太窄時才會捨棄。
    例：`Enter:install Tab:actions Esc:cancel` 放不下時是 `Enter:install Esc:cancel`，再放不下是 `Esc:cancel`。
  - **只有打字列的 popup**（text、password、number）：`?` 在那裡是字元，hint 要列出全部操作，而且 80 欄放得下（Rules M3）。
- **下框右邊**：內容放不下時的捲動位置（見下面的「內容放不下時」）。
- **框上的字與角之間一律隔一段線**：標題 `┏━TITLE`、hint `┗━ Enter:run`、捲動位置 `4 of 12 ━┛`（panel 也一樣，只有
  panel 的膠囊緊接著角，[`panel`](panel-zh_TW.md)）。
- **留白**：內容上下各留一列空白，左右離框一格（有整列 cursor 的，右邊的留白跟箭頭一樣寬，見下一條）。每一種 popup 都有，
  viewer 也一樣；只有 terminal 例外：上下左右都不留白
  （[`dialog/terminal`](../dialog/terminal-zh_TW.md)）。
- **cursor 色塊蓋住留白**：清單的 cursor 從框貼到框，蓋住左右的留白，色塊上的字照樣離框一格（[`dialog/menu`](../dialog/menu-zh_TW.md)、
  [`input/finder`](../input/finder-zh_TW.md)）；表單的 focus 色塊從值開始、一直到框，蓋住右邊的留白（[`dialog/form`](../dialog/form-zh_TW.md)）。
  右邊的留白畫 U+E0B0（`nf-pl-left_hard_divider`），色塊的顏色，像一個箭頭指著這一列（[`panel`](panel-zh_TW.md)
  的一般清單）。有整列 cursor 的 popup，右邊的留白跟箭頭一樣寬（Rules E5 的 powerline 符號寬度：多半是一格；佔兩格的終端機上，
  每一列右邊都留兩格），箭頭剛好放得進去。表單也算：它的 focus 色塊一直到框、尾端是箭頭，右邊的留白一樣跟箭頭同寬。只有整列的
  色塊有箭頭；datetime picker 的日子、時、分這種一格一格的 cursor 沒有。
- **分隔線**：popup 裡的分隔線不接框 —— 橫的左右各留一格空白，直的不畫進上下的留白。顏色 Overlay0。

**為什麼**：標題、hint、留白的位置固定，每一個 popup 一打開，使用者的眼睛就知道去哪裡找「這是什麼」「能按什麼」。
分隔線不接框：接上框的線看起來像把一個框切成兩個框，而它只是把內容分段。cursor 色塊蓋住留白：同一種 cursor 在每一個清單
長得一樣（Principle P4），色塊最寬、最好認（Rules L5）；右邊的留白跟箭頭一樣寬，每一列一樣寬，箭頭不會蓋到字、也不會
把框擠出去。標題後面的 tab 隔一段線：跟框上其他的字一樣，看得出標題與 tab 是兩件事，圓角與斜角兩種膠囊也不會黏在一起。標題是圓角的膠囊、panel 的膠囊是斜角：看兩端就知道是浮在上面的
框，還是畫面上的 panel。

## 寬度

Rules F7 的兩種寬度，打開時定好，開著時不變：

| | 寬度 | 例 |
|---|---|---|
| **內容的寬度打開時就確定** | 最寬的那一列 + 4（左右各一格框、一格留白；右邊的留白跟箭頭一樣寬時照它的寬），至少放得下標題與 hint（hint 的寬 + 6：`┗━ ` 與 ` ━┛`）；要捲的時候也放得下捲動位置（hint 的寬 + 捲動位置最寬時的寬 + 9：`┗━ `、兩者之間至少 ` ━ `、` ━┛`），最寬 `min(terminal 寬 − 2, 120)` | 有長度上限的輸入（PIN 最多 12 碼：內容 12 + 11 個空格 + 4 = 27 格，hint `Enter:save Backspace:clear Esc:cancel` 37 + 6 = 43 格，框取 43 格）、confirm、menu、key reference、toast、error popup、datetime picker、color picker、reorder |
| **內容的寬度不確定** | `min(terminal 寬 − 2, 120)` | 自由打字的 text、網址、串流內容、搜尋結果、表單 |

「確定」指的是打開那一刻就知道最寬會有多寬，不是看現在打了幾個字：PIN 打第一碼時框就是 43 格，不會跟著長。捲動位置也照最寬的時候算
（20 列的 menu 照 `20 of 20`，`N-M of T` 照 `T-T of T`），往下捲時框不會忽寬忽窄；hint 因此永遠完整 —— 最後一組通常是 `Esc`，怎麼關掉
popup 一定要看得到。只有框到了 `terminal 寬 − 2` 還放不下時才捨，捨的時候也留著 `Esc`（見上面的 hint）。

number 有單位時（[`input/number`](../input/number-zh_TW.md)），打字列下面的單位列也算一列內容：最寬的那一列取最多幾位數與單位
裡較寬的那一個。

窄的內容靠左，離框一格（例：confirm、datetime picker、color picker）；toast 的文字與 password 的解鎖遮罩置中。

## 開關動畫

Rules F2：打開與關閉都有動畫，全家族同一種、一樣長。打開分三段：

1. **拉線**（4 格）：在 popup 正中間那一列，一條層色的粗線 `━` 從中間往左右延伸，拉到 popup 的寬度。
2. **停**（1 格）：拉滿的線停一格。
3. **展開**（4 格）：popup 從中間那一列往上下展開；每一格露出的是 popup 正中間的那幾列，最後一格是整個 popup。

- **收起**：同樣的 9 格倒著播 —— 往中間壓成一條線，線再往中間縮掉。
- **長度**：每格 32ms；打開、收起各 9 格，約 288ms。
- **淡化**：打開的第一格起，底下就淡化；開始收起時，底下立刻亮回來（Rules F8：在收的 popup 已經不是最上層）。
- **一邊收、一邊開**（Rules T1 清掉 source 時）：source 收起與 target 打開同時播，不等 source 收完。在收的 source 不算一層：target
  從第一格就用它最後所在那一層的層色（[`color`](../color-zh_TW.md) 的層色）；收到一半的 source 壓在 target 底下，照 F8 淡化。
- **好幾層一起收起**（例：一個動作關掉整疊、Rules T1 清掉兩層以上的 source）：每一層同時收起，各自照自己的大小與層色，一起往
  中間壓成線、再縮掉，總共還是 9 格、約 288ms；不是只有最上面那一層播、底下的直接消失，也不是一層收完再收下一層。
- **按鍵**：打開的動畫播完之前，popup 不收鍵；在收的 popup 也不收鍵（Rules F3）。
- 每一種 popup 都一樣，包括 toast 與 terminal。

**為什麼**：先拉一條線再展開，看得出框從哪裡疊上來、退回哪裡去；線停一格，「有東西要出現」先被看到。288ms 看得清楚這三段，
又不會讓人覺得在等。全家族同一種：換 app 時節奏和樣子都不變。播放中不收鍵：框還沒畫完，使用者看不到自己按到的是什麼。
好幾層一起收、一起播，跟 T1 的「一起播、不等」同一個想法：每一層都看得到自己退下去，又不用三層等上三倍的時間。

## loading

Rules F7：popup 在 loading 時，標題後面一定放一個輪轉的 loading icon；標題後面接著 tab（[`panel`](panel-zh_TW.md) 的膠囊串）時，
放在整串 tab 的後面。表單的按鈕（不關表單的動作與跑得久的送出）在跑時，標題後面也放 loading icon
（[`dialog/form`](../dialog/form-zh_TW.md)）。panel 在 loading 時放在整串膠囊的後面（[`panel`](panel-zh_TW.md)）。前後各空一格。規格：

- 字形：`nf-md-circle_slice_1` 到 `nf-md-circle_slice_8`（U+F0A9E–U+F0AA5）八格，一個圓一片一片填滿，滿了再從頭。
- 速度：一格 90ms，一圈 720ms。
- 哪一格由時鐘決定：`frames[(now / 90ms) % 8]`，不是計數；tick 只在有東西 loading 時續排。
- 寬度：一格；跟它取代的靜止 glyph 同寬，換上換下不位移。braille 點字的形狀與寬度不合，不用。
- 顏色：跟旁邊的字同色；放在 popup 標題後面時用該層的層色（粗體）；放在 panel 上框時用框線色、不加粗（focus 時 Blue、失焦時 Surface2，
  跟著框一起淡化）—— 都是框的顏色。

## 取消與完成

取消回到 source（Rules F4）；完成之後 source 留不留，照 Rules T1。

## 內容放不下時

Rules F7：打開時定高、最高是畫面高度 − 2，超過就在框裡捲動。

- 只有內容區捲動；上下留白、錯誤列、上下框固定不動。
- 跟著 focus 捲，捲最少的量，讓 focus 所在的那一個整個看得到。不把 focus 固定在中間。
- 放不下時，下框右邊寫捲動位置，層色：有 cursor 或游標的寫 `N of M`（focus 所在的那一個是第幾個、總數）；沒有的
  （note、選取模式外的 viewer）寫看得到的行 `N-M of T`。全放得下時不寫。focus 不在捲動的區域裡時（表單的錯誤列、按鈕）不寫。
- 單位：
  - 表單以欄位為單位，上下式的 label 與值兩列、radio 的幾個選項都算同一欄；M 只算欄位，錯誤列與按鈕不算。一列一個值的
    panel 也照這個算（[`panel`](panel-zh_TW.md)）。
  - 在一段文字裡的游標（textarea、選取模式裡的 viewer）以行為單位：游標所在的行、總行數，跟行號同一套數字，不是畫出來的列。
  - 折行的 viewer（選取模式外）一次捲畫出來的一列；`N-M of T` 的 N、M 是最上面、最下面那一列所屬的行（[`dialog/note`](../dialog/note-zh_TW.md)）。

```
┏━TITLE━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                ┃   ← 留白
┃ content                                        ┃   ← 內容區：只有這一段捲動
┃ content                                        ┃
┃ content                                        ┃
┃                                                ┃
┃ error                                          ┃   ← 錯誤列：固定不動
┃                                                ┃
┗━ hint ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4 of 12 ━┛
```

## 錯誤列

- **位置**：內容區下面、固定不捲的一列，跟內容之間空一列。種類可以在它下面再加固定的列（例：表單的分隔線與動作區）。
- **只有值可能不合格的 popup 才預留**（Rules F7）：沒有錯誤時空白，高度不變。
- **只放值的錯**：值不合規則 —— 格式、範圍、必填、名字重複，訊息由 app 寫、很短。
- **值錯太多次而暫停收值時**（例：locku 的 PIN 連錯幾次之後冷卻），倒數也寫在錯誤列：Red，每秒更新（`try again in 27 s`），倒數完
  清掉。暫停期間除了 `Esc` 的鍵都吞掉，不進打字列。
- **樣子**：Red 字，左緣跟內容對齊（內容置中時錯誤列也置中）。框與標題不變色、維持層色：層色說的是「第幾層」，換成 Red
  這個資訊就沒了；而且這個 popup 本身不是錯誤，只是裡面有一個值不合格（表單上還有 Red 的 label）。
- **太長**：只佔一列，從尾端截斷加 `…`。表單上，錯誤列有錯誤時是一個可以 focus 的項目，`Enter` 打開完整的訊息
  （[`dialog/form`](../dialog/form-zh_TW.md)）。input popup 裡錯誤列不拿 focus：那裡是打字的地方（Rules K8）。
- **什麼時候改**：跟著檢查走 —— 只在檢查的時候改：檢查到錯就寫上這次的錯，沒錯就清掉；兩次檢查之間不動，值改了也一樣。
  表單在送出時檢查，input popup 在 `Enter` 時檢查。暫停的倒數例外：它每秒更新。

**動作本身失敗**（寫檔失敗、遠端拒絕、檔案在底下被改了）不寫錯誤列，直接開一個 error popup 蓋在當前的 popup 上
（[`dialog/note`](../dialog/note-zh_TW.md)）；關掉後回到原本的 popup，值都還在（Rules F4、F5）。

**為什麼**：值的錯跟某一欄有關，寫在框裡，使用者修正時一直看得到。動作的失敗跟哪一欄都無關，訊息要完整顯示，使用者看完
才能決定下一步 —— 重試、改值、或放棄。暫停的倒數是值錯太多次造成的，放在錯誤列意思接得上；toast 幾秒就走，倒數卻要一直
看得到，直到又可以打為止。

> **實作參考（不是規定）**：做對 Rules F3、F8 時踩過的坑，給用 Go 與 Bubble Tea 寫的 app 參考。
>
> - 一個 popup 一個檔、一個 animator。
> - `Esc` 只在一個地方處理（`closeTop`）。
> - 離開的 confirm 用自己的 popup，疊在整疊最上面：`Ctrl-C` 可能在另一個 confirm 開著時按下，借用同一個會蓋掉使用者正在回答的問題。
> - 「放在最上層」要同時改三處：按鍵路由、`closeTop`、繪製順序。
> - `?` 的 key reference 疊在其他 popup 上時，按鍵路由與繪製都把它放在最上層；confirm、options 等框排在底下的 menu 之前拿鍵。
> - 判斷一層「還在不在」用開啟中或已開（`owns()`），不用含關閉中的 `isActive()`（Rules F3）。

# form（表單）

**Language**: [English](form.md) · 繁體中文

## 用途

好幾個值填好後一起送出（sshu 的 Host 表單、webu 的 Sign in 與 Add bookmark）。只有一個值時用 input popup（[`input/`](../README-zh_TW.md#input)）；
改了就生效、不用送出的，用 panel 的一列一個值（[`layout/panel`](../layout/panel-zh_TW.md)）。框照 [`layout/popup`](../layout/popup-zh_TW.md)。

表單上不打字。要打字的欄位（text、password…）和選項多到放不下的欄位（select、日期、顏色、選檔），按 `Enter` 打開那一欄的
input popup，在那裡輸入，確定後值寫回表單。選項少的欄位（radio、checkbox），選項直接畫在表單上，在原地選。

**為什麼**：有些 input 放不進表單的一列，一定要另外跳 popup —— color picker、date picker、從清單選。其他欄位如果在表單上
直接打字，同一張表單就有兩種操作方式。全部用 input popup 輸入，每一欄都一樣：`Enter` 進去改、`Enter` 確定。代價是每一欄
多按一次 `Enter`（進去的那一下）。

## 長相

### 標題

寫這張表單要做什麼（`NEW HOST`、`ADD BOOKMARK`），畫成標題膠囊（[`layout/popup`](../layout/popup-zh_TW.md)）。不寫型別（`number`、`path`、`email`）：型別是欄位的性質，欄位多於一個時
也放不進一個標題。

### 欄位的排法

每個欄位從兩種裡挑一種。

| 排法 | 樣子 | 適合 |
|---|---|---|
| **上下式** | label 一列，值在下一列，值佔滿內寬 | 值長的欄位（網址、路徑、指令） |
| **左右式** | 一列：label 在左一欄，值在右 | 值短的欄位；欄位多的表單 |

- 一張表單可以混用兩種，依序排下來。全用上下式、全用左右式也都可以。
- 欄位之間不空行，上下式的 label 與值之間也不空行。分辨靠顏色：label 與值一定不同色（見下面的 label）。
- label、值、錯誤的左緣對齊。
- 左右式的 label 欄寬取**左右式欄位裡**最長的 label（上下式的 label 不算進去），label 欄與值之間兩格。
- 值怎麼顯示，見 [`input/README`](../input/README-zh_TW.md) 的「在表單與 panel 上怎麼顯示」。

```
┏━NEW PROFILE━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                ┃
┃ Name     clock3                                ┃   ← 左右式
┃ Timeout  30                                    ┃   ← 左右式
┃ Command                                        ┃   ← 上下式
┃ tmux new-session -A -s main                    ┃
┃ Layout   row                                   ┃   ← 左右式
┃                                                ┃
┗━ Enter:edit Tab:actions Esc:cancel ━━━━━━━━━━━━┛
```

（這一節與下一節的圖只畫欄位；動作列見「動作列」。）

### 選項畫在表單上

- 選項**五個以內**的 radio、checkbox 畫在表單上；超過五個，改用 select 或 checkbox popup（按 `Enter` 打開）。
- 一律直排，一個選項一列：focus 色塊從那個選項一直到框，橫排時會蓋住後面的選項，看不出它們選了沒。
- glyph 見 [`input/radio`](../input/radio-zh_TW.md) 與 [`input/checkbox`](../input/checkbox-zh_TW.md)。

**為什麼**：超過五個，表單一捲動，其他欄位就看不到了。

### focus 與 label

focus 的項目照 menu 的 cursor 列畫 —— 層色底、Base 粗體（[`dialog/menu`](menu-zh_TW.md)）。範圍從項目的開頭一直到框（蓋住右邊的留白）：
欄位從值開始、選項從那個選項開始、按鈕就是按鈕本身；值空著也是一整塊底色。一直到框的色塊，右邊的留白是箭頭 U+E0B0（層色，
跟 menu 的 cursor 一樣）；按鈕的色塊就是按鈕本身，沒有箭頭。

**label 的顏色**：不因 focus 變色。

| label 的狀態 | 顏色 |
|---|---|
| 一般 | 層色（跟標題膠囊、框線同色） |
| 停用 | Surface2 |
| 它的值出錯 | Red，優先於其他顏色 |

- 停用的欄位留在原位，不拿掉、不改高度（Rules F7）。
- 值在每一個狀態都不能跟它的 label 同色。

```
┏━NEW HOST━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                ┃
┃ Name        web-01                             ┃   label 層色
┃ Host        10.0.0.5▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃   ← focus：從值開始一直到框是層色底、Base 粗體
┃ Port        22                                 ┃
┃ Credential  —                                  ┃   ← 停用：label Surface2
┃                                                ┃
┗━ Enter:edit Tab:actions Esc:cancel ━━━━━━━━━━━━┛
```

**為什麼**：實心色塊不只換顏色、形狀也不同，focus 不只靠顏色（Rules L5）；跟 menu 同一套畫法：在家族的 popup 裡，層色底的那一塊
就是 `Enter` 會作用的地方。Lavender 留給 input popup 裡真正在編輯的值；「掃一眼就知道在哪一欄」由色塊負責，色塊也指得出
停在 radio 的哪一個選項。

### 動作列

```
┏━NEW HOST━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                ┃
┃ Name  web-01                                   ┃   ← 欄位區：放不下時只捲這一段
┃ Host                                           ┃
┃ Port  22                                       ┃
┃                                                ┃
┃ Host is required                               ┃   ← 錯誤列（沒錯時空白）
┃ ────────────────────────────────────────────── ┃   ← 分隔線
┃                                          Save  ┃   ← 動作列：按鈕靠右
┃                                                ┃
┗━ Enter:edit Tab:actions Esc:cancel ━━━━━━━━━━━━┛
```

- **按鈕**：文字左右各留一格空白，一塊底色。沒有 focus 時也有底色（Surface1 底、Text 字），一看就知道它也是一個可以
  focus、可以按的項目，不是一行說明；有 focus 時跟其他項目一樣是層色底、Base 粗體。按鈕上寫這張表單要做的事
  （`Save`、`Connect`、`Sign in`）。
- 不用 `[ Save ]`：家族裡方括號是「鍵」（Rules M5 的 `[A]`、menu 的 `[r]ename`），會被讀成按 `S` 就存。不用膠囊：膠囊在家族裡
  是「名稱」（panel 標題、tab、畫面），按鈕畫成膠囊會被讀成標題（Principle P4）。
- **位置**：欄位區 → 空一列 → 錯誤列 → 分隔線 → 動作列。欄位與錯誤列左緣對齊；按鈕靠右，離框一格。錯誤列就在按鈕上方：
  按了送出被擋下時，眼睛就在附近。
- **分隔線**：在動作列上方，照 [`layout/popup`](../layout/popup-zh_TW.md) 的分隔線（不接框、Overlay0），把動作列跟上面的內容分開。
- **錯誤列、分隔線、動作列固定不捲**：欄位放不下時只捲欄位區，按鈕永遠看得到。
- **捲動位置**：欄位放不下時，下框右邊寫 focus 所在的欄位 `N of M`，M 只算欄位（錯誤列、按鈕不算）。focus 在錯誤列或按鈕上時
  不寫，回到欄位就回來：它們不是欄位，寫不出有意義的號碼。
- **動作列只有一個按鈕（送出）**：需要第二個按鈕時是 tdp 的缺漏，回報後再補，那時再定按鈕之間怎麼移。
- 不放取消的按鈕：取消是 `Esc`（Rules F3），寫在 hint。

## 按鍵

### 移動

表單上 focus 的單位是**項目**：要打字或開 popup 的欄位是一個項目，radio、checkbox 的每一個選項各是一個項目，按鈕是一個
項目；錯誤列有錯誤時也是一個項目（在按鈕前面）。

- **`j|l|↓|→` 下一個項目，`h|k|↑|←` 上一個項目**（表單是一維清單，Rules K12）。走到一欄的最後一個選項
  再往後，就進到下一欄；在第一個選項再往前，就回到上一欄。`gg` 到第一個項目、`G` 到最後一個（按鈕）；`u|d` 以項目為單位
  半頁，到頭尾停住。
- **`Tab|Shift-Tab` 在欄位區與動作列之間來回**（Rules K2）：在欄位區的任何一項按 `Tab` 到按鈕；在按鈕上按 `Tab` 回到離開前的那一個
  項目 —— 跟 [`input/finder`](../input/finder-zh_TW.md) 的打字列與清單一樣。欄位區裡一項一項走用 `j|k`。錯誤列不是 `Tab` 的一站
  （`j|k` 與 `e` 到得了）；它跟按鈕一起固定在底部，算同一塊：在錯誤列上按 `Tab` 也回到欄位區離開前的那一個項目。
- **頭尾繞回**（Rules K12）：按鈕是最後一個項目，`j` 在按鈕上往後回到第一欄；在第一欄往前一步就到按鈕 —— 補上動作列在最底下的距離。
- **停用的欄位與選項跳過**：`j|k` 不停在上面；照樣畫在原位。停用就是「現在不能改」，停在上面按 `Enter` 也沒事可做。
- **打開時**：focus 在第一個能停的項目（跳過停用的），新增與編輯都一樣；app 從某一欄打開表單時（例：panel 上對 Port 那一列
  按編輯），停在那一欄。新增時也不自動打開第一欄的 input popup：只省一次 `Enter`，卻讓新增與編輯打開的樣子不同，而且
  想放棄要按兩次 `Esc`（第一次只關 input popup）。打開的一定是表單本身，一次 `Esc` 就離開。

```
┏━NEW HOST━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                ┃
┃ Name   web-01                                  ┃   ← 1 個項目
┃ Auth   󰐾 password                              ┃   ← 3 個項目
┃        󰐽 privatekey                            ┃
┃        󰐽 credential                            ┃
┃ Agent  󰄲 forward                               ┃   ← 1 個項目
┃                                                ┃
┗━ Enter:edit Tab:actions Esc:cancel ━━━━━━━━━━━━┛
```

`j` 一路往後：Name → password → privatekey → credential → forward。在 privatekey 上按 `Tab` 到按鈕，在按鈕上再按 `Tab` 回到 privatekey。

### `Enter`

- **在要打字或開 popup 的欄位上**：打開那一欄的 input popup，疊在表單上（Rules F8）。
  - 在 input popup 裡按 `Enter` 確定：值寫回表單那一欄，input popup 關掉，**focus 留在同一欄**（Rules K3）。
  - 在 input popup 裡按 `Esc`：關掉 input popup，這一欄的值不變。
  - 從表單打開的 checkbox popup：`Space` 勾、`Enter` 整組寫回、`Esc` 取消（[`input/checkbox`](../input/checkbox-zh_TW.md)）。
- **在 radio 的選項上**：選它；**在 checkbox 的選項上**：在原地翻（`Space` 也能翻，跟 checkbox popup 一樣，Rules K5）。都不開 popup，focus 留在原位，馬上生效；選錯了在原地再按
  一次就好。
- **在按鈕上**：送出。

### 送出

只有一個方法：focus 移到按鈕上，按 `Enter`。明確按下按鈕，才保證是使用者要送出。

- 快的走法：`Tab` 從欄位區到按鈕（在按鈕上再按 `Tab` 回到剛才那一項），或 `G` 直接到按鈕。例：只改 Port 就存 —— 在 Port 上
  `Enter`、打 `2222`、`Enter`、`Tab`、`Enter`。
- 不用字母熱鍵（例 `s`）送出：表單看起來是一排欄位，使用者容易直接開始打字，打 `server` 的第一個字就把表單送出了。
- 不拿 `Esc` 把 focus 移到動作列：Rules F3 規定 `Esc` 立刻關閉 popup，表單若例外，使用者會關不掉。

### 在欄位上打字

表單不是輸入態（Rules K8），使用者卻常以為可以直接打字。focus 在「`Enter` 會打開打字的 input popup」的欄位上（text、password、
number、textarea），按到一個不在表單操作鍵裡的可列印字元時（包括 `q`），跳一個說明的 note：

```
┏━NAME━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                ┃
┃ Press [Enter] to edit Name.    ┃
┃                                ┃
┗━ Enter|Esc:close ━━━━━━━━━━━━━━┛
```

- 標題是欄位名稱；`Enter`、`Esc` 都能關，關掉後回到表單，focus 不動（[`dialog/note`](note-zh_TW.md)）。
- **表單的操作鍵**不跳 note：

  | 鍵 | 在表單上 |
  |---|---|
  | `j` `k` `h` `l`、方向鍵 | 移動（到頭尾繞回，Rules K12） |
  | `Tab\|Shift-Tab` | 在欄位區與動作列之間來回 |
  | `u\|d` | 以項目為單位半頁，到頭尾停住 |
  | `g`（`gg` 的開頭）、`G` | 到第一個、最後一個項目；單按 `g` 不作用 |
  | `e` | 在有問題的欄位上跳到錯誤列、在錯誤列跳回那一欄（見下面的「錯誤」）；其他地方不作用 |
  | `Enter`、`Esc` | 見上面的 `Enter` 與下面的「取消」 |
  | `Space`、`?` | core key：`Space` 在 checkbox 的選項上勾或取消勾、其他地方不作用（Rules K5），`?` 打開 key reference（Rules K6） |

- **其他可列印字元**（數字、`q`、其他字母）：在要打字的欄位上跳 note；在表單的其他項目（選項、按鈕、錯誤列）上不跳，按到
  沒用的鍵就是不作用。`q` 不進離開流程（Rules K9）。

**為什麼**：用 note 不用 toast：note 會把後面打的字全部接住、不作用，表單不會被打亂；toast 讓按鍵穿過去，後面打到的 `e`、`h`、`l`
會在欄位之間亂跳。使用者打完習慣性按 `Enter`，剛好關掉 note。`e`、`u|d`、`g` 都算操作鍵：K12 本來就把這些字母留給不打字
地方的移動，表單就是不打字的地方；同一個鍵的反應也不看狀態（`e` 不會沒錯時跳 note、有錯時跳錯誤列）。以為能直接打字的人，
第一個字剛好是這些鍵時被吃掉，下一個字照樣跳 note，提醒的效果不變。

### hint

```
Enter:edit Tab:actions Esc:cancel
```

- **`Enter` 後面的字跟著 focus 的項目換**，寫按下去會發生什麼：會開 input popup 的欄位 `Enter:edit`、radio 的選項 `Enter:choose`、
  checkbox 的選項 `Enter|Space:toggle`、按鈕寫按鈕的字（小寫：`Save` → `Enter:save`、`Connect` → `Enter:connect`）。
- focus 在有問題的欄位上時加 `e:error`（`Enter:edit e:error Tab:actions Esc:cancel`）；在錯誤列上是 `Enter:show e:edit Tab:fields Esc:cancel`。
- **`Tab` 寫要去的那一塊**：在欄位區 `Tab:actions`，在按鈕與錯誤列上 `Tab:fields`（`Enter:save Tab:fields Esc:cancel`）。不寫 `Tab:save`：
  看起來像按 `Tab` 就存，而送出只有按按鈕一個方法。
- 不寫移動的鍵（`j|k`）：使用者操作一下就知道。
- `Esc:cancel` 不寫 `close`：表單上的 `Esc` 會丟掉內容，跟 confirm 的 `Esc:cancel` 同義。

## 狀態

### 取消

- **沒改過的表單**：`Esc` 直接關（Rules F3）。
- **改過的表單**：`Esc` 先開 confirm 問要不要放棄（例：`Discard changes to New host?`）：`Enter` 放棄並關掉表單；`Esc` 關掉 confirm、
  回到表單，值都還在（Rules F6、K4）。
- **「改過了」的旗標**：有值寫回表單就設起來（input popup 確定了一個跟打開時不同的值、選了 radio 的選項、翻了 checkbox），
  之後不清掉。只比這一個 popup 打開與確定時的值，不比對表單最初的值：改了又改回原值，也算改過。
- **範圍**：一次可能丟掉很多內容的地方才問 —— 表單與 textarea（[`input/textarea`](../input/textarea-zh_TW.md)）。其他 input popup 不問：
  裡面最多一個值，丟了重打就好；用 `Esc` 放棄剛打的字是最常見的操作，每次多一個 confirm 很煩。其他 dialog 沒有可以改的內容；
  terminal 離開本來就先問（Rules K10 的 `Alt-Esc`）。

**為什麼**：沒改過的表單不受影響，改過的多一層保護；程式不用管草稿，只管有沒有改過。連按 `Esc` 會在表單與 confirm 之間來回，
但那不是陷阱：confirm 上寫著 `Enter` 放棄，連按 `Esc` 的人最後停在表單上、內容都在，正是 Rules K4 要的「安全的地方」。

### 錯誤

- **一欄自己的規則**（格式、範圍：Port 要在 1–65535、keyword 只能是英數與連字號）：在 input popup 裡按 `Enter` 時擋，錯誤寫在
  input popup 的錯誤列，值不寫回、popup 不關（見各 input 檔）。不合格的值進不了表單。
- **牽涉整張表單的規則**：按下按鈕送出時才檢查 —— 必填沒填、依另一欄而定的必填（Auth 選 credential 就要選 Credential）、名字重複。
- **檢查沒過**：不存，表單留著、值都在。每一個有問題的欄位 label 都轉 Red（一眼看到全部要補哪些）；錯誤列寫依欄位順序的
  第一個問題，focus 跳到那一欄。
- **`e`**：在有問題的欄位（label Red）上按 `e`（error），focus 跳到錯誤列，錯誤列換成**這一欄**的訊息（一次檢查全部欄位，每一欄的
  訊息本來就都有）；在錯誤列按 `Enter` 打開完整訊息的 error popup（[`dialog/note`](note-zh_TW.md)，標題寫那一欄的名字，`Enter`、`Esc` 都能關）；在錯誤列按 `e`（edit），
  focus 回到這則訊息的那一欄，再按 `Enter` 就開 input popup 改。錯誤列照樣可以用 `j|k` 走到，`e` 是直接跳的捷徑。按錯 `e`
  只是移動 focus，不會改到東西。
- **送出的動作失敗**（檔案在底下被改了、寫檔失敗、遠端拒絕）：不寫錯誤列，直接開 error popup 蓋在表單上（[`layout/popup`](../layout/popup-zh_TW.md)
  的錯誤列）；關掉後回到表單，值都在、focus 還在按鈕上 —— 再按一次 `Enter` 就是重試。
- **錯誤跟著檢查走**：整張表單只在送出時檢查，所以 Red 的 label 與錯誤列一直掛著，值改了也一樣，直到下一次送出：那時有別的錯
  就換成那個，沒錯就存。
- **第一次送出之前**不做整張表單的檢查：打開新表單時不會滿版紅色的「必填」。

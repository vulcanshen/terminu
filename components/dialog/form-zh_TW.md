# form：表單

**Language**: [English](form.md) · 繁體中文

表單是一種 dialog：好幾個值填好後一起送出（sshu 的 Host 表單、webu 的 Sign in 與 Add bookmark）。框本身照
[`layout/popup`](../layout/popup-zh_TW.md)。

表單上不打字。要打字的欄位（text、password…）和選項多到放不下的欄位（select、日期、顏色、選檔），按 `Enter` 打開那一欄的
input popup（[`input/`](../README-zh_TW.md#input)），在那裡輸入，確定後值寫回表單。選項少的欄位（radio、checkbox），選項直接
畫在表單上，在原地選。

**為什麼**（user 2026-10-07）：有些 input 放不進表單的一列，一定要另外跳 popup —— color picker、date picker、從清單選
（sshu 的 Auth 選 credential 就是按 `Enter` 開 menu）。其他欄位如果在表單上直接打字，同一張表單就有兩種操作方式。全部用
input popup 輸入，每一欄都一樣：`Tab` 換欄、`Enter` 進去改、`Enter` 確定。代價是每一欄多按一次 `Enter`（進去的那一下）。

同一天 user 加上 hjkl 之後，選項少的 radio、checkbox 改成直接在表單上選。區分的標準是「要打字或放不下才開 popup」；
`Enter` 一律對 focus 的項目做最直觀的動作（K3）—— 在 Name 上是打開 popup 打字，在一個選項上是選它，在開關上是翻。

## 標題

寫這張表單要做什麼（`New host`、`Add bookmark`）。不寫型別（`number`、`path`、`email`）：型別是欄位的性質，欄位多於一個時
也放不進一個標題；需要讓使用者知道時由欄位自己標，標法見各 input 檔。

## 欄位的排法

每個欄位從兩種裡挑一種。

| 排法 | 樣子 | 適合 |
|---|---|---|
| **上下式** | label 一列，值在下一列，值佔滿內寬 | 值長的欄位（網址、路徑、指令） |
| **左右式** | 一列：label 在左一欄，值在右 | 值短的欄位；欄位多的表單 |

- 一張表單可以混用兩種，依序排下來。全用上下式、全用左右式也都可以。
- 欄位之間不空行，上下式的 label 與值之間也不空行。分辨靠顏色（label 與值一定不同色，見「focus 與換欄」）與值前面
  的 input 指示 icon（見各 input 檔）。
- label、值、錯誤的左緣對齊。
- 左右式的 label 欄寬取**左右式欄位裡**最長的 label（上下式的 label 不算進去），label 欄與值之間留空白。

```
╭─ New profile ──────────────────────────────────╮
│                                                │
│ Name        clock3                             │   ← 左右式
│ Timeout     30                                 │   ← 左右式
│ Command                                        │   ← 上下式
│ tmux new-session -A -s main                    │
│ Layout      row                                │   ← 左右式
│                                                │
╰─ Enter:edit Ctrl-S:save Esc:cancel ────────────╯
```

（這一節與下一節的圖只畫欄位；動作列見「送出」。）

## focus 與換欄

表單上 focus 的單位是**項目**：要打字或開 popup 的欄位是一個項目，radio、checkbox 的每一個選項各是一個項目，按鈕是一個
項目；錯誤列有錯誤時也是一個項目（在按鈕前面，見 [`layout/popup`](../layout/popup-zh_TW.md) 的錯誤列）。

- **`j`/`l`/`↓`/`→` 下一個項目，`h`/`k`/`↑`/`←` 上一個項目**（user 2026-10-07）。不分橫排直排，往後就是往後、往前就是往前，
  hjkl 等於方向鍵（表單是一維清單，見 rules K12）。走到一欄的最後一個選項再往後，就進到下一欄；在第一個選項再往前，就回到上一欄。表單不是輸入態（K8），
  字母是空出來的；使用者以為能直接打字時，打到這幾個字母也只是移動，不會送出。
- **`Tab`/`Shift-Tab` 一次跳一欄**（K2），有錯誤的錯誤列、動作列也各算一站。
- **`Tab`/`Shift-Tab` 跳進 radio、checkbox 那一欄時**（user 2026-10-07）：radio 停在已經選的那個選項，都沒選就停在第一個；
  checkbox 組停在第一個。`Shift-Tab` 從下面進來也一樣：`Tab` 是「跳到那一欄」，落點跟方向無關。radio 停在目前的值上，
  想換就 `j`/`k` 移到旁邊，不換就直接 `Tab` 離開，不會誤選；checkbox 組每個選項各自勾或不勾，沒有「目前那一個」，從頭開始
  最好預期。（`j`/`k` 一格一格走，進到一欄時自然停在最靠近的選項。）
- **頭尾繞回**（user 2026-10-07）：`Tab` 與 `j`/`k` 都一樣。按鈕是最後一個項目，在按鈕上往後回到第一欄；在第一欄往前一步
  就到按鈕 —— 補上動作列在最底下的距離。跟 K2（`Tab` 最後一個之後回到第一個）、[`menu`](menu-zh_TW.md)（`j/k` 頭尾相接）一致。
- **停用的欄位與選項跳過**（user 2026-10-07）：`Tab` 與 `j`/`k` 都不停在上面；照樣畫在原位（見下面 label 的顏色）。停用就是
  「現在不能改」，停在上面按 `Enter` 也沒事可做。
- **打開時**（user 2026-10-07）：focus 在第一個能停的項目（跳過停用的），新增與編輯都一樣；app 從某一欄打開表單時（例：panel
  上對 Port 那一列按編輯），停在那一欄。新增時也不自動打開第一欄的 input popup：只省一次 `Enter`，卻讓新增與編輯打開的樣子
  不同，而且想放棄要按兩次 `Esc`（第一次只關 input popup）。打開的一定是表單本身，一次 `Esc` 就離開。

```
╭─ New host ─────────────────────────────────────╮
│                                                │
│ Name        web-01                             │   ← 1 個項目
│ Auth        (•) password                       │   ← 3 個項目
│             ( ) privatekey                     │
│             ( ) credential                     │
│ Agent       [x] forward                        │   ← 1 個項目
│                                                │
╰─ Enter:edit Ctrl-S:save Esc:cancel ────────────╯
```

`j` 一路往後：Name → password → privatekey → credential → forward。`Tab` 一路往後：Name → Auth → Agent。
（選項的樣子見 `input/radio`、`input/checkbox`，圖裡的 `(•)`、`[x]` 只是示意。）

**focus 的樣子**（user 2026-10-07）：focus 的項目照 menu 的 cursor 列畫 —— 層色底、深色粗體字（見 [`dialog/menu`](menu-zh_TW.md)）。範圍從項目的
開頭到框內右緣：欄位從值開始、選項從那個選項開始、按鈕就是按鈕本身；值空著也是一整塊底色。實心色塊不只換顏色、形狀也
不同，focus 不只靠顏色（L5 的精神）。跟 menu 同一套畫法：在家族的 popup 裡，層色底的那一塊就是 `Enter` 會作用的地方。

**label 的顏色**：不因 focus 變色。

| label 的狀態 | 顏色 |
|---|---|
| 一般 | 層色（跟標題、框線同色） |
| 停用 | Surface2 |
| 它的值出錯 | Red，優先於其他顏色 |

- 原本（popup 第 4 題）值拿到 focus 時 label 變 Lavender 粗體，前提是在表單上打字、有游標。改成在 input popup 輸入後，表單
  上沒有「正在編輯的東西」：Lavender（[`color`](../color-zh_TW.md)）留給 input popup 裡真正在編輯的值；「掃一眼就知道在哪一欄」改由色塊負責，
  色塊也指得出停在 radio 的哪一個選項。
- 停用的欄位留在原位，不拿掉、不改高度（F7）。
- 給 input 檔的條件：值在每一個狀態都不能跟它的 label 同色。

```
╭─ New host ─────────────────────────────────────╮
│                                                │
│ Name          web-01                           │   label 層色
│ Host          10.0.0.5                         │   ← focus：從值開始到右緣是層色底、深色粗體字
│ Port          22                               │
│ Credential    —                                │   ← 停用：label Surface2
│                                                │
╰─ Enter:edit Ctrl-S:save Esc:cancel ────────────╯
```

## 改一個欄位

- focus 在要打字或開 popup 的欄位上按 `Enter`：打開那一欄的 input popup，疊在表單上（F8）。
- input popup 裡按 `Enter` 確定：值寫回表單那一欄，input popup 關掉，focus **自動移到下一欄**（跟 `Tab` 一樣）。從上往下填，
  最後一欄確定完，focus 就停在送出的按鈕上，再按一次 `Enter` 就送出：
  `Enter` 打字 `Enter` → `Enter` 打字 `Enter` → … → `Enter`（按鈕）。
- input popup 裡按 `Esc`：關掉 input popup（K4：關閉最上層），這一欄的值不變。
- radio 的選項上按 `Enter`：選它；checkbox 的選項上按 `Enter`：在原地翻。都不開 popup，focus 留在原位：馬上生效，選錯了
  在原地再按一次就好，focus 跟著往下反而要退回來。

## 送出

- 表單最下面有一列**動作列**，放真的按鈕，按鈕上寫這張表單要做的事（`Save`、`Connect`、`Sign in`）。`Tab` 移到按鈕上、
  按 `Enter` 才送出：明確按下按鈕，才保證是使用者要送出。
- 不放取消的按鈕：取消是 `Esc`（F3），寫在 hint。
- **`Ctrl-S`**：在表單裡按下（focus 在哪都一樣），等於按送出的按鈕。給「只改一欄就存」用：例如改 Port，
  `Enter` `22` `Enter` `Ctrl-S`，不用再 `Tab` 好幾下到按鈕。
- 不用字母熱鍵（例 `s`）：表單看起來是一排欄位，使用者容易直接開始打字，打 `server` 的第一個字就把表單送出了。
  `Ctrl-S` 打不出字，不會撞上。
- 不拿 `Esc` 把 focus 移到動作列（user 提過，自己否決：反人性）：F3 規定 `Esc` 立刻關閉任何 popup，只有表單例外，
  使用者會關不掉。


**按鈕與位置**（user 2026-10-07）：

```
╭─ New host ─────────────────────────────────────╮
│                                                │
│ Name        web-01                             │   ← 欄位區：放不下時只捲這一段
│ Host                                           │
│ Port        22                                 │
│                                                │
│ Host is required                               │   ← 錯誤列（F7 預留，沒錯時空白）
├────────────────────────────────────────────────┤   ← 分隔線
│                                          Save  │   ← 動作列：按鈕靠右
│                                                │
╰─ Enter:edit Ctrl-S:save Esc:cancel ────────────╯
```

- **按鈕**：文字左右各留一格空白，一塊底色。沒有 focus 時也有底色（Surface1 底、Text 字），一看就知道它也是一個可以
  focus、可以按的項目，不是一行說明；有 focus 時跟其他項目一樣是層色底、深色粗體（見「focus 與換欄」）。
- 不用 `[ Save ]`：家族裡方括號是「鍵」（M5 的 `[A]`、menu 的 `[r]ename`），會被讀成按 `S` 就存。不用 powerline 圓角膠囊：
  那是 Nerd Font 的字，字寬在不同終端機上不一定一樣（rules E5）。
- **位置**：欄位區 → 空一列 → 錯誤列 → 分隔線 → 動作列。欄位與錯誤列左緣對齊；**按鈕靠右**，離框一格（user）。錯誤列就在
  按鈕上方：按了送出被擋下時，眼睛就在附近。
- **分隔線**（user 2026-10-07）：在動作列上方，接上左右框（`├─┤`），跟框線同色（層色），把動作列跟上面的內容分開。
- **錯誤列、分隔線、動作列固定不捲**：欄位放不下時只捲欄位區，按鈕永遠看得到。
- **動作列目前只有一個按鈕（送出）**：現有的表單都只要一個動作。需要第二個按鈕時是 tdp 的缺漏，回報後再補，那時再定按鈕之間
  怎麼移。

## hint

user 2026-10-07 定。

```
Enter:edit Ctrl-S:save Esc:cancel
```

- **`Enter` 後面的字跟著 focus 的項目換**，寫按下去會發生什麼：會開 input popup 的欄位 `Enter:edit`、radio 的選項
  `Enter:choose`、checkbox 的選項 `Enter:toggle`、按鈕寫按鈕的字（小寫：`Save` → `Enter:save`、`Connect` → `Enter:connect`）。
  `Ctrl-S` 後面也是按鈕的字。focus 在有問題的欄位上時加 `e:error`（`Enter:edit e:error Ctrl-S:save Esc:cancel`）；在錯誤列上是
  `Enter:show e:edit Ctrl-S:save Esc:cancel`。
- **不寫移動的鍵**（`j/k`、`Tab`）：使用者操作一下就知道（user）。
- `Esc:cancel` 不寫 `close`：表單上的 `Esc` 會丟掉內容，跟 confirm 的 `Esc:cancel` 同義。
- 放不下時照規則從尾端整組捨：先捨 `Esc:cancel`（F3 全家族一樣），再捨 `Ctrl-S`（按鈕就在畫面上），`Enter` 留到最後。

## 取消

- **沒改過的表單**：`Esc` 直接關（F3）。
- **改過的表單**：`Esc` 先開 confirm（user 2026-10-07）。表單只記一個「改過了」的旗標：有值寫回表單（input popup 確定、選了
  radio 的選項、翻了 checkbox）就設起來，之後不清掉；不比對改了什麼，改回原值也算改過。旗標設起來時按 `Esc`，先開 confirm
  問要不要放棄（例：`Discard changes to New host?`）：`Enter` 放棄並關掉表單；`Esc` 關掉 confirm、回到表單，值都還在（F6、K4）。
- **為什麼**（user）：沒改過的表單不受影響，改過的多一層保護；程式不用管草稿，只管有沒有改過。
- 我原本建議不問，理由之一是連按 `Esc` 會在表單與 confirm 之間來回。重看後這不是陷阱：confirm 上寫著 `Enter` 放棄，連按
  `Esc` 的人最後停在表單上、內容都在，正是 K4 要的「安全的地方」。
- **範圍**（user 2026-10-07）：一次可能丟掉很多內容的地方才問 —— 表單與 textarea（見 `input/textarea`）。其他 input popup
  （text、password、number、search，以及選值的）不問：裡面最多一個值，丟了重打就好；用 `Esc` 放棄剛打的字是最常見的操作，
  每次多一個 confirm 很煩；在表單裡 input popup 的 `Esc` 是「這一欄不改了」，再問一次等於放棄一欄要按兩下。其他 dialog
  （menu、confirm、note、toast）沒有可以改的內容；terminal 離開本來就先問（K10 的 `Alt-Esc`）。
- 這是 F3（`Esc` 立即關閉任何 popup）的例外，發 v0.2.0 時寫進 F3。

## 錯誤

user 2026-10-07 定。

- **一欄自己的規則**（格式、範圍：Port 要在 1–65535、keyword 只能是英數與連字號）：在 input popup 裡按 `Enter` 時擋，錯誤寫在
  input popup 的錯誤列，值不寫回、popup 不關（見各 input 檔）。不合格的值進不了表單。
- **牽涉整張表單的規則**：送出時（按鈕或 `Ctrl-S`）才檢查 —— 必填沒填、依另一欄而定的必填（Auth 選 credential 就要選
  Credential）、名字重複。
- **檢查沒過**：不存，表單留著、值都在。每一個有問題的欄位 label 都轉 Red（一眼看到全部要補哪些）；錯誤列寫依欄位順序的
  第一個問題，focus 跳到那一欄。
- **`e`**（user 2026-10-07）：在有問題的欄位（label Red）上按 `e`（error），focus 跳到錯誤列，錯誤列換成**這一欄**的訊息
  （一次檢查全部欄位，每一欄的訊息本來就都有）；在錯誤列按 `Enter` 打開完整訊息的 note；在錯誤列按 `e`（edit），focus 回到
  這則訊息的那一欄，再按 `Enter` 就開 input popup 改。錯誤列照樣可以用 `j`/`k`、`Tab` 走到，`e` 是直接跳的捷徑。按錯 `e`
  只是移動 focus，不會改到東西（跟否決的「`s` 送出」不同）。
- **送出的動作失敗**（submit error：檔案在底下被改了、寫檔失敗、遠端拒絕）：不寫錯誤列，直接開 error popup 蓋在表單上（見
  [`layout/popup`](../layout/popup-zh_TW.md) 的錯誤列）；`Esc` 關掉後回到表單，值都在、focus 不動。
- **錯誤跟著檢查走**（user 2026-10-07 改）：整張表單只在送出時檢查，所以 Red 的 label 與錯誤列一直掛著，值改了也一樣，直到
  下一次送出：那時有別的錯就換成那個，沒錯就存。（原本定的是「送出失敗之後每次寫回就重驗」，user 改成只跟著檢查。）
- **第一次送出之前**不做整張表單的檢查：打開新表單時不會滿版紅色的「必填」。

（錯誤列的位置、跟動作列怎麼排，跟按鈕的樣子一起定。）

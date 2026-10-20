# note（唯讀內容）

**Language**: [English](note.md) · 繁體中文

## 用途

唯讀的內容，可以捲動，可以有自己的熱鍵與模式（Rules F1）：key reference、viewer（YAML 檢視、App Log、檔案內容）、error popup、
表單上的打字說明（[`dialog/form`](form-zh_TW.md)）。viewer 一定有選取模式（見下面的「選取模式」）。有可以用 `Enter` 執行的選項清單時，
它是 menu，不是 note。

## 長相

- 框照 [`layout/popup`](../layout/popup-zh_TW.md)：上下留白一律有，viewer 也一樣。
- **標題**：glyph 加上顯示的東西，畫成標題膠囊：種類大寫；要寫顯示的是哪一個時，接 ` — ` 再接名稱，名稱照原樣（例：
  `YAML — pod/nginx`）。glyph 由 app 選；key reference 與 error popup 的 glyph 見下面。
- **捲動位置**：放不下時，下框右邊寫看得到的行 `N-M of T`；viewer 的選取模式裡寫游標所在的行 `N of M`（見下面的「選取模式」）。
  viewer 折行時，N 是最上面那一列所屬的行，M 是最下面那一列所屬的行，T 是總行數（例：最上面是第 6 行折下來的那一列、最下面是
  第 10 行，寫 `6-10 of 42`）。
- **寬度**：內容打開時就確定的（key reference、error popup、說明）照內容；viewer 的內容寬度不確定，用 Rules F7 的上限。
- **太長時折行**：error popup、表單的打字說明這種一段話的 note，放不下時照 [components 的「折行」](../README-zh_TW.md) 折行，不截斷。
  key reference 的說明例外，見下面。
- **viewer 的折行**：預設折行 —— 一行比框寬時接到下一列畫，照 [components 的「折行」](../README-zh_TW.md)：在空白處斷，一個字本身就比
  一列還長時才照格子切。要對齊的內容（左右並排、表格），app 可以讓它不折行：比框寬的部分截掉，行尾加 `…`。不折行時，選取模式的
  游標走進截掉的部分，畫面跟著左右捲到看得見（捲最少的量，像 vim 的 nowrap），左邊被捲掉的開頭也加 `…`；截掉的內容照樣選得到、
  複製得到。離開選取模式，回到最左邊。
- **viewer 的行號**：viewer 左邊畫不畫行號由 app 決定：檔案內容、YAML 檢視、App Log 這種一行就是一行的內容通常要畫；app 自己排出來的
  表（例：filu 的檔案資訊）行號沒有意義，可以不畫。畫的時候照 [`input/textarea`](../input/textarea-zh_TW.md) 的行號：每一行的
  第一列畫行號，靠右對齊、後面空一格；折下來的列行號欄空白。行號 Overlay0，選取模式裡游標所在那一行的行號 Text。複製不含行號。
  行號欄**至少三位**：打開時就知道行數的（YAML 檢視、檔案內容）取 max(3, 總行數的位數)，打開後不變；串流的 App Log 從三位開始，
  超過 999 行才跳寬。
  **有 tab 的 viewer**（例：DevTools 的 Console、Network）：行號欄照看過的頁裡最寬的那一頁，只變寬、不變窄 —— 打開時照那一頁；
  切到行數更多的頁就變寬；切回行數少的頁，寬度留著不縮回。串流的頁一樣只變寬。
- **viewer 的語法顏色**：內容有固定格式的（YAML、JSON、TOML、HTML、XML、Markdown……）照 [`input/file-picker`](../input/file-picker-zh_TW.md)
  預覽表的文字檔上色（chroma 的 catppuccin-mocha，只上前景色）。語言由 app 給（YAML 檢視是 YAML；DevTools Network 的回應照
  content type）；檔案內容照檔名判斷，跟預覽一樣。沒有固定格式的（例：App Log）、判斷不出來的，上不上色由 app 決定：不上色時是
  純文字 Text；app 知道自己的內容，可以依情境上色（例：log 裡 ERROR、WARN 的行）。lib 不上語法顏色，但保留 app 給的顏色。
  行號照舊 Overlay0；選取模式的範圍照舊 Yellow 底、Base 字，語法顏色在範圍裡不顯示。
- **viewer 裡的 Tab 與控制字元**（跟 [`input/file-picker`](../input/file-picker-zh_TW.md) 的預覽一樣；全家族的規定見 [components](../README-zh_TW.md)
  的「控制字元」）：照終端機會畫的樣子。Tab 畫成 `input_tab_width` 格空白（跟 [`input/textarea`](../input/textarea-zh_TW.md) 同一個設定），
  不對齊 tab 停點；`\n` 是換行，app 一行一行交來的內容，一行裡夾著 `\n` 也拆成兩行；換行前面的 `\r`（CRLF）不畫，算換行的一部分；
  顏色碼（SGR）照著上色；一行裡的 `\r`（進度列）只留最後的狀態；其他控制字元與不是顏色碼的序列畫成名字，Red（`\x07`；清畫面的
  `\x1b[2J` 畫成紅色的 `\x1b` 接著 `[2J`，跟 [`input/README`](../input/README-zh_TW.md) 的「貼上的控制字元」一樣）。複製照原樣，不是畫出來的
  空白或名字。viewer 是用來讀的：程式的輸出本來就是要在終端機裡長那個樣子；CRLF 每一行都掛一個紅色的 `\r` 只是雜訊；控制字元用
  Red，才分得出檔案裡本來就寫著 `\x07` 這四個字。
- **viewer 的搜尋**（有 `/` 時）：命中的字全部加底線，保留原本的顏色；目前那一筆畫成 cursor 色塊（層色底、Base 粗體，
  [`color`](../color-zh_TW.md) 的 cursor），意思是「你在這裡」。不另外加顏色：模式的 Yellow 只留給選取模式的範圍。

```
┃   1 apiVersion: v1                            ┃   ← 行號欄三位（這份 YAML 有 42 行）；行號 Overlay0
┃   2 kind: Pod                                 ┃   ← 內容照 YAML 上語法顏色
┃   3 metadata:                                 ┃
┃   4   name: nginx                             ┃
┃   5   annotations:                            ┃
┃   6     note: restarted by the deploy job     ┃
┃     after the config change                   ┃   ← 同一行折下來：行號欄空白
┃   7 spec:                                     ┃
┃   8   containers:                             ┃
┃   9   - name: nginx                           ┃
┃  10     image: nginx:1.27                     ┃
```

**為什麼**：viewer 打開時就知道有幾行（串流的除外），行號欄的寬度一次定好，畫面不會跳；textarea 的行數是使用者自己打出來的，
跳寬看得出原因，所以它從兩位起跳。三位：999 行以內的內容不會跳。有 tab 時切回去不縮回：看過的寬度留著，來回切 tab 不會一直跳。
語法顏色跟預覽同一套，同一個檔案在預覽與 viewer 裡長得一樣。

## 按鍵

- 捲動：`j|k`、`u|d`、`gg|G`（Rules K12）。viewer 的選取模式見下面。
- **viewer 折行時以畫面上的一列為單位捲**（像 `less`）：`j|k` 一次一列，`u|d` 半頁照列算。比框還高的一行（例：壓縮過的 JSON）
  也看得完；跟 [`input/textarea`](../input/textarea-zh_TW.md) 的 `↑|↓` 照畫出來的列一致。
- **只用 `Esc` 關**。`Enter` 不關；`Space` 也不關（Rules K5）。
- **例外**：error popup（不管是自己跳出來的，還是從表單錯誤列按 `Enter` 打開的）與表單上的打字說明，`Enter` 也能關；key reference
  再按一次 `?` 也能關（Rules K6）。
- **表單上的打字說明只收 `Enter`、`Esc`**：其他可以打的字（包括 `q`、`?`）都不作用 —— 不進離開流程、不開 key reference
  （[`dialog/form`](form-zh_TW.md) 的「在欄位上打字」）。
- **hint**：note 自己的熱鍵寫在前面，`Esc:close` 放最後。例：`y:copy /:search v:visual Esc:close`。

**為什麼**：使用者自己打開的 note，看完按 `Esc` 是最直覺的；`Space` 在 `less`、`man` 這類閱讀器裡是往下翻頁，熟的人在 note 上按
`Space` 想往下翻，note 卻關掉了。自己跳出來的 error popup 與打字說明，出現時使用者的手正在打字或正要送出，`Enter` 是反射動作；
讓 `Enter` 也能關，那一下不會落空，而它們上面也沒有別的東西會被 `Enter` 觸發。從表單錯誤列打開的 error popup 長得一模一樣，
按鍵也一樣：畫面上分不出它是怎麼打開的，而且表單上一路 `Enter` 走得完（錯誤列 `Enter` 看訊息、`Enter` 回來、`e` 跳到那一欄、
`Enter` 改）。

## 選取模式（只有 viewer）

每個 viewer（YAML 檢視、App Log、檔案內容……）都有選取模式，可以把一段文字選起來複製；key reference、error popup、表單的打字說明沒有
這個模式，`j|k` 只捲動。

- **平常沒有游標**：`j|k`、`u|d`、`gg|G` 捲動畫面；有 tab 時 `h|l` 切 tab（Rules K12）。
- **第一次 `v`**：進入選取模式（模式，Rules K11：框與模式名換成模式色 Yellow）。游標出現在畫面第一行的行首，還沒開始選。
  `h|j|k|l`、`w|b|e`、`0|$`、`u|d`、`gg|G` 移動游標，走到畫面邊緣時畫面跟著捲。hint `v:select Esc:cancel`。
- **第二次 `v`**：從游標所在開始選，接著移動游標把範圍拉開。範圍以字為單位（vim 的 `v`）：從起點到游標，含游標那個字；要整行，
  就先把游標移到行首。hint `y:copy Esc:cancel`。開始選之後再按 `v` 不作用。
- **`y`**：複製選起來的文字，離開選取模式，範圍與游標都消失；跳一個 Success toast 說複製好了（[`dialog/toast`](toast-zh_TW.md)）。
- **`Esc`**：在哪一步都是整個離開，不複製，範圍與游標都消失（K11：回到進入前的狀態）。不收 `v` 當離開的別名（K12）。
- **顏色**：游標一格層色底、Base 字（跟 [`input/textarea`](../input/textarea-zh_TW.md)「移」的游標一樣）；範圍 Yellow 底、Base 字，
  游標那格維持層色；範圍裡的空行畫一格。
- **捲動位置**：選取模式裡寫游標所在的行 `N of M`（以行為單位，跟左邊的行號同一套數字）；離開後回到 `N-M of T`。

**為什麼**：先移到起點再開始選 —— 游標一出現的地方不一定是要選的地方，按一次 `v` 就開始選的話，起點永遠被固定在畫面第一行。
平常沒有游標，`j|k` 照樣捲、`h|l` 照樣切 tab，看完就關的 note 不多一個用不到的游標。以字為單位：從 note 裡複製的常常是一個字、
一段指令或一個網址。複製完通常就做完了，不用再多按一次 `Esc`。每個 viewer 都有：使用者不用記哪個 viewer 能選、哪個不能，
家族裡看得到一段文字的地方就複製得到。

## key reference

`?` 打開的「這裡能按什麼鍵」（Rules K6、M4）。

```
┏━ [2] HOSTS KEYS━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                               ┃
┃ 󰋘 ITEM OPERATION                              ┃  ← 區塊標題
┃  Enter     Connect — what it is, then in      ┃
┃  E         Edit — change this host            ┃
┃  X         Delete — remove from hosts.yaml    ┃
┃ 󰋘 PANEL OPERATION                             ┃
┃  A         Add — a new host                   ┃
┃  /         Search — name, user, host, port, … ┃  ← 說明太長（框已經到最寬時）
┃ 󰋘 MOVE                                        ┃
┃  j|k       down, up                           ┃
┃  u|d       half a page up, down               ┃
┃  gg|G      to the top, the bottom             ┃
┃ 󰋘 CORE KEYS                                   ┃
┃  Space     what you can do here               ┃
┃  ?         this list                          ┃
┃  Tab       next panel                         ┃
┃  1–N       jump to panel N                    ┃
┃  q|Ctrl-C  quit                               ┃
┃ 󰋘 APP-WIDE                                    ┃
┃  M         Manage — hosts, credentials, …     ┃
┃                                               ┃
┗━ ?|Esc:close ━━━━━━━━━━━━━━━━━━━━ 1-20 of 23 ━┛
```

- **標題**：`nf-fa-question_circle`（U+F059）加 `<surface> keys`，例：`[2] HOSTS KEYS`、`SPACE MENU KEYS`。
- **每一列一個鍵**：縮兩格，鍵補到跟最寬的鍵一樣寬，空兩格，再接說明。說明太長從尾端截，加 `…`，不折行（「每一列」那一節例外，見下面）。鍵的寫法照 Rules M5
  （不加括號、不加冒號）。
- **從 menu 來的列**：說明寫 `label — 說明`；label 去掉熱鍵標記、大小寫照原樣（menu 上的 `[E]dit` 寫成 `Edit — change this host`）。
- **區塊**：區塊標題跟 menu 一樣（`nf-md-hexagon`、大寫、Overlay0、縮一格、不加粗）。panel 上依序是：
  - `what each row is`（可選，只有一列一個值的 panel）：見下面的「每一列」。
  - `item operation`、`panel operation`：跟 Space menu 一樣。
  - `move`：這裡能用的移動鍵（Rules K12），只列真的能用的（例：有 tab 時才列 `h|l` 切 tab）。一維清單（表單、沒有 tab 的一列一個值
    panel、menu）寫 `h|k` 往前、`j|l` 往後。對象不存在時不列（Rules M6）：清單空了不列移動鍵，內容放得下不列捲動鍵。
  - `core keys`：這個 panel 上有作用的 core key —— `Space`、`?`、`Tab`、`1–N`（好幾個 panel 時，Rules K1）、`q|Ctrl-C`；`Esc` 只在
    這裡有作用時才列（例：有篩選可以清）；`Enter` 已經在 `item operation` 寫了它在這裡做什麼，不重複。
  - `app-wide`：global 熱鍵。離開的 `q` 已經在 `core keys` 列了，這裡不重複（跟 `Enter` 一樣）。
  - 說明**別的 surface** 的段（Rules M6；例：panel 裡的 PTY 進去之後的鍵，標題 `terminal`）：排在最後，`app-wide` 之後。
    每個 panel 前面幾段的順序都一樣，有沒有這一段，`core keys`、`app-wide` 都在原位；先讀「這裡能按什麼」，再讀「進去之後」。
- **每一列**（一列一個值的 panel，可選）：key reference 最前面可以有一節說明 panel 上每一列是什麼意思。左欄是設定的名稱，用一般的字色
  （Text，不是鍵的 Blue：它不是鍵），右欄是說明；按鍵的區塊接在後面。要不要有這一節由 app 決定。說明太長時在右欄折行（照
  [components 的「折行」](../README-zh_TW.md)，名稱欄不動、接下來的列從說明的起點開始），不截斷：這一節是要讀的句子，不是對照表；
  key reference 本來就能捲，長了也看得完。
- **popup 上**只列這個 popup 自己的鍵（Rules K6）：它的熱鍵、`Enter`、`Esc`、移動鍵。
- **顏色**：鍵 Blue、不加粗；說明 Text。現在按不了的鍵，鍵與說明都用 Surface2（Rules M6）。
- **按鍵**：捲動照上面；`?` 或 `Esc` 關，`Enter` 不作用。hint `?|Esc:close`。

**為什麼**：key reference 是唯一列出全部按鍵的地方 —— hint 不列移動、Space menu 只列動作 —— 不列移動鍵，`u|d`、`gg|G` 就沒地方
學（Principle P1）。label 不轉小寫：轉了會弄壞 `SSH config`、`YAML` 這種縮寫，而熱鍵已經寫在左邊的鍵欄。

## error popup

popup 的動作失敗時（[`layout/popup`](../layout/popup-zh_TW.md) 的錯誤列），蓋在那個 popup 上的 note。表單錯誤列 `Enter` 打開的完整訊息
也是它。

```
┏━󰈸 SAVE FAILED━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                 ┃
┃ hosts.yaml changed on disk since it was opened. ┃
┃                                                 ┃
┗━ Enter|Esc:close ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **樣子**：框、文字都是 Red；標題膠囊填 Red、字 Base 粗體（膠囊照 [`layout/popup`](../layout/popup-zh_TW.md)）。標題 glyph 跟
  Error toast 一樣是 `nf-md-fire`（U+F0238）。訊息在框裡折行（照 [components 的「折行」](../README-zh_TW.md)）；太長時 `j|k` 捲動。
- **標題**：寫哪件事失敗了（`RENAME FAILED`、`SAVE FAILED`）。從表單錯誤列打開的，標題寫那一欄的名字（`PORT`）。
- **關掉**：`Enter` 與 `Esc` 都能關，hint `Enter|Esc:close`。
- **關掉之後**：回到底下的 popup，focus 留在原位，值都還在（Rules F4）。連按 `Enter` 時，第一下關掉它，下一下等於在原來的位置再按
  一次 —— 在表單的按鈕上就是重試。失敗的動作沒有改變任何東西，重試最多再看到一次錯誤。

**為什麼**：error popup 整個就是錯誤，框與字都是 Red；它一定在最上層、一個鍵就關掉，少了層色也不會讓人搞不清第幾層。有錯誤列的
popup 本身不是錯誤，只是裡面有一個值不合格，所以那裡的框維持層色。

## App Log

每個 app 都有 App Log（Rules F5）：app 做過的事與出問題的事，最新的在最下面。在 panel 上按 `!` 打開（Rules K1），是一個 viewer
（上面 viewer 的規定與選取模式照樣適用）；開著時新的一筆照樣進來，跟串流的內容一樣。

```
14:02:11 INFO switched to Pods
14:02:40 OK   deployment.apps/nginx scaled
14:03:02 WARN CRD discovery: the server is currently unable to handle the request
14:03:30 ERR  namespace fetch failed: Forbidden
```

- **記什麼**：使用者做的動作與結果；每一個 toast（同一句話）；app 自己在背景做的事（例：Rules E3 的搬家、啟動時建好的預設值、
  讀不到外面的東西的細節）。
- **每一筆**：時間 `HH:MM:SS`（Overlay0）、等級、發生的事。等級跟著 toast 的種類與顏色：`INFO` Text、`OK` Green、`WARN` Peach、
  `ERR` Red，等級欄四格寬、靠左。
- **只放在記憶體**：app 關掉就清空；筆數有上限，滿了丟掉最舊的。
- **沒看過的錯誤與警告**：寫在 footer 的 `!`（[`layout/screen`](../layout/screen-zh_TW.md) 的 footer）；打開 App Log 就算看過。

**為什麼**：toast 幾秒就收掉，沒注意到的人不會知道出過錯；App Log 留著。只記錯誤看不出出錯前做了什麼，前面那幾筆往往就是原因；
app 在背景做的事，使用者也只有這裡看得到。`!` 跟 `?`、`Space` 一樣，在家族哪個 app 都按得到。只放在記憶體：要看的是這次開 app
發生了什麼，不多一種要存、要清的東西。

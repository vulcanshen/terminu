# note（唯讀內容）

**Language**: [English](note.md) · 繁體中文

## 用途

唯讀的內容，可以捲動，可以有自己的熱鍵與模式（Rules F1）：key reference、viewer（YAML 檢視、App Log、檔案內容）、error popup、
表單上的打字說明（[`dialog/form`](form-zh_TW.md)）。有可以用 `Enter` 執行的選項清單時，它是 menu，不是 note。

## 長相

- 框照 [`layout/popup`](../layout/popup-zh_TW.md)：上下留白一律有，viewer 也一樣。
- **標題**：glyph 加上顯示的東西，畫成標題膠囊（例：`YAML — pod/nginx`：`YAML` 大寫，`pod/nginx` 是內容，照原樣）。glyph 由 app 選；key reference 與 error popup 的 glyph 見下面。
- **捲動位置**：放不下時，下框右邊寫看得到的行 `N-M of T`；viewer 的選取模式裡寫游標所在的行 `N of M`（見下面的「選取模式」）。
- **寬度**：內容打開時就確定的（key reference、error popup、說明）照內容；viewer 的內容寬度不確定，用 Rules F7 的上限。

## 按鍵

- 捲動：`j|k`、`u|d`、`gg|G`（Rules K12）。viewer 的選取模式見下面。
- **只用 `Esc` 關**。`Enter` 不關；`Space` 也不關（Rules K5）。
- **例外**：error popup（不管是自己跳出來的，還是從表單錯誤列按 `Enter` 打開的）與表單上的打字說明，`Enter` 也能關。
- **hint**：note 自己的熱鍵寫在前面，`Esc:close` 放最後。例：`y:copy /:search v:visual Esc:close`。

**為什麼**：使用者自己打開的 note，看完按 `Esc` 是最直覺的；`Space` 在 `less`、`man` 這類閱讀器裡是往下翻頁，熟的人在 note 上按
`Space` 想往下翻，note 卻關掉了。自己跳出來的 error popup 與打字說明，出現時使用者的手正在打字或正要送出，`Enter` 是反射動作；
讓 `Enter` 也能關，那一下不會落空，而它們上面也沒有別的東西會被 `Enter` 觸發。從表單錯誤列打開的 error popup 長得一模一樣，
按鍵也一樣：畫面上分不出它是怎麼打開的，而且表單上一路 `Enter` 走得完（錯誤列 `Enter` 看訊息、`Enter` 回來、`e` 跳到那一欄、
`Enter` 改）。

## 選取模式（只有 viewer）

viewer（YAML 檢視、App Log、檔案內容）可以把一段文字選起來複製；key reference、error popup、表單的打字說明沒有這個模式，`j|k` 只捲動。

- **平常沒有游標**：`j|k`、`u|d`、`gg|G` 捲動畫面；有 tab 時 `h|l` 切 tab（Rules K12）。
- **第一次 `v`**：進入選取模式（模式，Rules K11：框與模式名換成模式色 Yellow）。游標出現在畫面第一行的行首，還沒開始選。
  `h|j|k|l`、`w|b|e`、`0|$`、`u|d`、`gg|G` 移動游標，走到畫面邊緣時畫面跟著捲。hint `v:select Esc:cancel`。
- **第二次 `v`**：從游標所在開始選，接著移動游標把範圍拉開。範圍以字為單位（vim 的 `v`）：從起點到游標，含游標那個字；要整行，
  就先把游標移到行首。hint `y:copy Esc:cancel`。開始選之後再按 `v` 不作用。
- **`y`**：複製選起來的文字，離開選取模式，範圍與游標都消失。
- **`Esc`**：在哪一步都是整個離開，不複製，範圍與游標都消失（K11：回到進入前的狀態）。不收 `v` 當離開的別名（K12）。
- **顏色**：游標一格層色底、Base 字（跟 [`input/textarea`](../input/textarea-zh_TW.md)「移」的游標一樣）；範圍 Yellow 底、Base 字，
  游標那格維持層色；範圍裡的空行畫一格。
- **捲動位置**：選取模式裡寫游標所在的行 `N of M`（以行為單位）；離開後回到 `N-M of T`。

**為什麼**：先移到起點再開始選 —— 游標一出現的地方不一定是要選的地方，按一次 `v` 就開始選的話，起點永遠被固定在畫面第一行。
平常沒有游標，`j|k` 照樣捲、`h|l` 照樣切 tab，看完就關的 note 不多一個用不到的游標。以字為單位：從 note 裡複製的常常是一個字、
一段指令或一個網址。複製完通常就做完了，不用再多按一次 `Esc`。

## key reference

`?` 打開的「這裡能按什麼鍵」（Rules K6、M4）。

```
┏━[2] HOSTS KEYS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                               ┃
┃ 󰋘 ITEM OPERATION                              ┃  ← 區塊標題
┃  Enter     Connect — what it is, then in      ┃
┃  E         Edit — change this host            ┃
┃  X         Delete — remove from hosts.yaml    ┃
┃ 󰋘 PANEL OPERATION                             ┃
┃  A         Add — a new host                   ┃
┃  /         Search — name, user, host, port, … ┃
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
- **每一列一個鍵**：縮兩格，鍵補到跟最寬的鍵一樣寬，空兩格，再接說明。說明太長從尾端截，加 `…`，不折行。鍵的寫法照 Rules M5
  （不加括號、不加冒號）。
- **從 menu 來的列**：說明寫 `label — 說明`；label 去掉熱鍵標記、大小寫照原樣（menu 上的 `[E]dit` 寫成 `Edit — change this host`）。
- **區塊**：區塊標題跟 menu 一樣（`nf-md-hexagon`、大寫、Overlay0、縮一格、不加粗）。panel 上依序是：
  - `item operation`、`panel operation`：跟 Space menu 一樣。
  - `move`：這裡能用的移動鍵（Rules K12），只列真的能用的（例：有 tab 時才列 `h|l`）。
  - `core keys`：這個 panel 上有作用的 core key —— `Space`、`?`、`Tab`、`1–N`（好幾個 panel 時，Rules K1）、`q|Ctrl-C`；`Esc` 只在
    這裡有作用時才列（例：有篩選可以清）；`Enter` 已經在 `item operation` 寫了它在這裡做什麼，不重複。
  - `app-wide`：global 熱鍵。
- **popup 上**只列這個 popup 自己的鍵（Rules K6）：它的熱鍵、`Enter`、`Esc`、移動鍵。
- **顏色**：鍵 Blue、不加粗；說明 Text。現在按不了的鍵，鍵與說明都用 Surface2（Rules M6）。
- **按鍵**：捲動照上面；`?` 或 `Esc` 關，`Enter` 不作用。hint `?|Esc:close`。

**為什麼**：key reference 是唯一列出全部按鍵的地方 —— hint 不列移動、Space menu 只列動作 —— 不列移動鍵，`u|d`、`gg|G` 就沒地方
學（Principle P1）。label 不轉小寫：轉了會弄壞 `SSH config`、`YAML` 這種縮寫，而熱鍵已經寫在左邊的鍵欄。

## error popup

popup 的動作失敗時（[`layout/popup`](../layout/popup-zh_TW.md) 的錯誤列），蓋在那個 popup 上的 note。表單錯誤列 `Enter` 打開的完整訊息
也是它。

```
┏━SAVE FAILED━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                 ┃
┃ hosts.yaml changed on disk since it was opened. ┃
┃                                                 ┃
┗━ Enter|Esc:close ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **樣子**：框、文字都是 Red；標題膠囊填 Red、字 Base 粗體（膠囊照 [`layout/popup`](../layout/popup-zh_TW.md)）。標題 glyph 跟
  Error toast 一樣是 `nf-md-fire`（U+F0238）。訊息在框裡折行；太長時 `j|k` 捲動。
- **標題**：寫哪件事失敗了（`RENAME FAILED`、`SAVE FAILED`）。從表單錯誤列打開的，標題寫那一欄的名字（`PORT`）。
- **關掉**：`Enter` 與 `Esc` 都能關，hint `Enter|Esc:close`。
- **關掉之後**：回到底下的 popup，focus 留在原位，值都還在（Rules F4）。連按 `Enter` 時，第一下關掉它，下一下等於在原來的位置再按
  一次 —— 在表單的按鈕上就是重試。失敗的動作沒有改變任何東西，重試最多再看到一次錯誤。

**為什麼**：error popup 整個就是錯誤，框與字都是 Red；它一定在最上層、一個鍵就關掉，少了層色也不會讓人搞不清第幾層。有錯誤列的
popup 本身不是錯誤，只是裡面有一個值不合格，所以那裡的框維持層色。

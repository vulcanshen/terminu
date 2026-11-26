# screen（整個畫面）

**Language**: [English](screen.md) · 繁體中文

整個畫面的骨架。panel 的框見 [`panel`](panel-zh_TW.md)，浮在上面的框見 [`popup`](popup-zh_TW.md)。

## screen.1 由上往下

1. **最上面一列**：多畫面的 app 是畫面 chip 列，下面一條全寬分隔線；單畫面的 app 可以有一列 statusbar（要不要有，app 可以自行決定）。
2. **panel 區**：其餘的高度。每個畫面的 panel 各自從 `[1]` 編號；`1`–`9` 只跳目前畫面裡的 panel（Rules K1）。
3. **最下面一列**：footer。

## screen.2 footer

一列，寫法照 Rules M5 的 hint；鍵 Blue、冒號與說明 Overlay0（[`color`](../color-zh_TW.md)）。寬度不夠時從尾端整組捨棄
（[`popup`](popup-zh_TW.md) 的 hint）。內容依情況：

| 情況 | footer |
|---|---|
| 一般 | `Space:menu ?:help !:log Tab\|1–N:panels q:quit` |
| 只有一個 panel 的畫面 | `Space:menu ?:help !:log q:quit` |
| 在模式裡（Rules K11） | `Space:menu ?:help`、模式自己的鍵、最後 `Esc:<離開的動詞>`；app 自己的模式，中間寫哪些鍵由 app 自行決定，`q:quit` 這種 core key 也可以（Rules K11）；使用者把模式的一個動作放到 `Space` 時，不寫 `Space:menu`，那個動作寫成 `Space:<動作>`，寫在最前面、原本 `Space:menu` 的位置（是用一個動詞講的一對的一半時，照 Rules M5 寫那一對，例：`j|Space:move`；Rules K11）。例：`Space:menu ?:help Enter:drop Esc:cancel` |
| panel filter 打字中（輸入態） | `Enter\|Tab:list Esc:clear` |
| panel filter 打字中，沒有結果 | `Tab:list Esc:clear`（`Enter` 不作用，照 [`input/finder`](../input/finder-zh_TW.md) 的 hint） |
| focus 在 panel 裡的 PTY | 出口鍵，再加 app 保留的鍵（Rules K10）；互動 terminal 再接 `Alt-v:select`、`PgUp:history`（dialog/terminal）。例：`Alt-Esc:leave Alt-z:zoom Alt-v:select PgUp:history` |
| popup 開著時 | 照底下畫面的寫，跟著整個畫面淡化（Rules F8）；popup 自己的鍵在它的下框 hint |

**`!` 的提醒**：App Log（[`dialog/note`](../dialog/note-zh_TW.md)）裡有沒看過的錯誤時，`!:log` 換成 `!:2 errors`（說明 Red）；只有沒看過的
警告時換成 `!:1 warning`（Peach）；打開 App Log 之後回到 `!:log`。

terminal popup 開著時不畫 footer：terminal 蓋住最下面一列，兩端露出來的地方是空白，不露出 footer 的字
（[`dialog/terminal`](../dialog/terminal-zh_TW.md)）。

**為什麼**：footer 是 Rules M1 的入口，寫的必須是現在按得了的鍵。打字時 `Space` `?` `q` 都是字元、
PTY 裡的鍵都送給子程序 —— 照常寫一般的 footer，反而教使用者按錯。popup 開著時 footer 不換字、只跟著淡化：淡化就是「現在不在
這裡」（Principle P6，跟 Rules F8 同一件事）；popup 開開關關，最下面一列只變暗變亮，不會一直換字；`?` 照樣在 footer 上，而
popup 上按 `?` 打開的本來就是這個 popup 的 key reference（Rules M1）。

## screen.3 畫面 chip 列

多畫面的 app 最上面一列：每個畫面一個膠囊，畫法照 [`panel`](panel-zh_TW.md) 的膠囊串，串的顏色是 Blue（選中的畫面填 Blue、
字 Base 粗體；沒選中的底是 Mantle、字 Blue、不加粗）。放不下時照膠囊串的規則縮：先縮成 `[M] [F] [S]`，再收掉沒選中的。

右邊放 statusbar 的內容（見下）。chip 列下面一條全寬的粗線 `━`，Overlay0；長時間的工作（傳檔、下載）進行時，從左邊填 Green
當進度條，旁邊的狀態文字也是 Green。terminal popup 開著時，chip 列與這條分隔線都留著（[`dialog/terminal`](../dialog/terminal-zh_TW.md)）：
在 shell 裡照樣看得到進度。

**單畫面的 app 沒有 chip 列**：長時間工作的進度算 app 的內容，寫在那個工作自己的列裡，進行中用 Green（例：filu 的 `[3] Tasks`
那一列寫 `3/10`，執行中的 glyph 是 Green）。正在 panel 位置列寫的那個地方跑的工作，也可以改寫在那一列（例：位置列那個 repo
的 push；[`panel`](panel-zh_TW.md) 的 panel.10）。terminal popup 開著時那一列被蓋住、看不到進度，這樣就好，不為了它多開一列。

## screen.4 statusbar

要不要有，app 可以自行決定。單畫面的 app 放在最上面一列；多畫面的 app 用 chip 列的右邊，不另開一列。它不是 surface，focus
不會停在上面。

- 寫法照 Rules M5 的 label：有熱鍵就標出來（例：kbu 的 `[C]ontext: prod  [N]amespace: default`）。
- 一組寫成 `label: 值`，冒號後面空一格；組與組之間兩格，不加分隔符號（[components](../README-zh_TW.md) 的「圖與間距」：這裡不套用
  兩格通則）。
- 一般文字 Overlay0；「你現在在哪」的值 Lavender（使用者足跡）；進行中的工作 Green；錯誤、警告的數量 Red、Peach。
- 寬度固定（Rules L2）：最後一個動態欄位不補空白，前面的欄位照樣固定寬；放不下時截斷，不折行（L3）。

## screen.5 窄寬

所有 panel 放不下時，只畫有 focus 的那一個 panel，佔滿寬度；`Tab` 照樣換 panel，一次看一個。門檻 app 可以自行決定，依自己 panel 的
最小寬度定，但不能高於 60（Rules L1：60 欄要能正常用，所有 panel 並排）。窄寬只在 app 的最低尺寸以上才有；比最低尺寸還小時見下面的
「比最低尺寸小時」。

## screen.6 zoom

把一個 panel 放大是 app 的功能，要不要有、用哪個鍵，app 可以自行決定（例：filu 的 `z`）。規範給的是預設：放大時只畫有 focus 的那一個
panel，佔滿 panel 區，跟窄寬一樣；`Tab`、數字鍵照樣換 panel，換到的 panel 也是放大的，再按一次放大的鍵才還原。怎麼放大，app
可以自行決定（例：filu 把同一個 panel 的幾個 tab 並排）；沒有另外定的照預設。

**為什麼**：每個 app 放大想看的東西不一樣，規範只保住一個大家都懂的預設；預設跟窄寬一樣，使用者在窄的畫面上學會的，放大時
照樣能用。

## screen.7 比最低尺寸小時

畫面比 app 的最低尺寸還小時（Rules L1：預設 60×32，app 可以調低，但不能高於 60×32），整個畫面只畫三列，上下左右置中：

```
                kbu
needs a terminal of at least 60×20
   Press [Ctrl-C] twice to quit
```

- **名稱**：app 的指令名稱，Blue 粗體（跟 splash 的名稱一樣，Rules S5）。
- **提示**：名稱下面一列，`needs a terminal of at least <寬>×<高>`，寫 app 的最低尺寸；Overlay0。
- **怎麼離開**：提示下面一列，`Press [Ctrl-C] twice to quit`，Overlay0；照空狀態的提示寫，鍵加方括號（screen.8、Rules M5）。
- **放不下時**：先拿掉提示，再拿掉怎麼離開那一列，名稱一定留著（比畫面還寬時，畫得下多少就畫多少）；提示與怎麼離開那一列
  比畫面寬也算放不下。到 1×1 都不當掉。
- **按鍵都不作用**：不送進 app，也不送進 PTY；`q` 與單按一次 `Ctrl-C` 也不作用。只有連按兩次 `Ctrl-C` 立刻離開（Rules K9 的
  強制離開）。
- **狀態留著**：視窗拉大到最低尺寸以上，就回到原本的畫面，什麼都沒變。

**為什麼**：在比最低尺寸還小的畫面上硬畫，版面一定是壞的，使用者看到的是一堆截掉的框，不知道是 app 壞了還是視窗太小；
直接講名稱與需要多大，拉大視窗就好。這時使用者看不到 app 的狀態，按鍵照常送出去等於矇著眼操作 —— 可能誤刪東西，在 shell 裡
打了什麼也看不到；所以一律不作用，只留連按兩次 `Ctrl-C` 當緊急出口。離開流程可能要開 confirm 問問題，這時畫不出來，所以 `q`
與單按一次 `Ctrl-C` 也不作用。緊急出口寫在畫面上：按什麼都沒反應，不知道規定的人會以為 app 卡住了；視窗拉不大時（例：對半分割
的 tmux 窗格）它是唯一的出口，所以比提示晚拿掉（hostu 2026-10-27 回報）。

## screen.8 空狀態

置中寫一句事實，加上一句點名按鍵的提示，都用 Overlay0；提示裡的鍵加方括號（Rules M5）。例：

```
No hosts yet

Press [A] to add a host, or [Space] to see what you can do here
```

- **太長時**：在空白處折行（[components](../README-zh_TW.md) 的「折行」），每一列置中，左右照樣離框一格；不截斷，也不必為了
  放得下而把句子縮短。
- **清單空了**：空狀態取代整塊，連表頭一起不畫，句子置中在整個 panel（[`panel`](panel-zh_TW.md) 的一般清單）。

panel 的 loading 與錯誤也用這個樣子（[`panel`](panel-zh_TW.md) 的「loading 與錯誤」）。

## screen.9 調整 panel 大小

畫面上不只一個 panel 時，使用者從有 focus 的 panel 移動 panel 之間的線，app 記住線停在哪裡
（user 2026-11-26，來自 gittu 與 ccodu）：

| 鍵 | 做的事 |
|---|---|
| `>` | 有 focus 的 panel 變寬 2 欄 |
| `<` | 變窄 2 欄 |
| `+` | 變高 1 列 |
| `-` | 變矮 1 列 |
| `=` | 目前畫面的每一條線回到預設 |

**線是共用的**：移動的是 panel 邊上的那條線，碰到這條線的 panel 全部跟著動，說明牌也一樣（[`panel`](panel-zh_TW.md) 的 panel.17：
它跟其他 panel 一起縮放），線另一邊的 panel 跟著變大或縮小。panel 沿著一條線接多遠，那條線就有多長：

```
┌───┬───┐      ┌───┬───────┐
│ 1 │ 2 │      │ 1 │   2   │
├───┼───┤      ├───┴───────┤
│ 3 │ 4 │      │     3     │
└───┴───┘      └───────────┘
```

左邊那個，在 [1] 按 `>`，[1] 和 [3] 一起變寬、[2] 和 [4] 一起變窄；在 [1] 按 `+`，[1] 和 [2] 一起變高、[3] 和 [4] 一起變矮。右邊
那個，直的那條線只在上排：在 [1] 按 `>`，只有 [1] 變寬、[2] 變窄，[3] 不動；在 [1] 按 `+`，[1] 和 [2] 一起變高、[3] 變矮。

- **動哪一條**：兩邊都有線的 panel（例：三欄的中間那欄），寬度動右邊那條、高度動下面那條；貼著 panel 區右邊或底部的 panel 改動另
  一邊的線，所以 `>` 一定讓它變寬、`+` 一定讓它變高。
- **最小尺寸**：每個 panel 有最小寬度和高度，由 app 自己定，小到 60×32 時所有 panel 照樣並排（Rules L1）；線一動到任何一個跟著動
  的 panel 到最小，就停，所以快到最小時，這一下只動剩下的（例：1 欄），下一下才跳下面說的 toast。
- **動不了時**：按了一定有反應（Rules M6）：跳一個 Info toast（[`dialog/toast`](../dialog/toast-zh_TW.md)）說為什麼，例：
  `[2] is already full width`、`[2] is already full height`、`[4] is at its minimum width`，點名擋住線的那個 panel，有 focus 的
  優先，用它的 `[N]`；說明牌照它框上的寫法用 label（`INFO is at its minimum height`）。窄寬（screen.5）和 zoom（screen.6）只畫一
  個 panel，那時它就是全寬又全高。每一條線都在預設時按 `=`，說 `The layout is already the default`。
- **那個 toast 放哪裡**：在那個 panel 上、本來會動的那條邊，放在框裡面、不蓋住任何一邊的框：右邊在右上、左邊在左上、下邊在下方中
  間、上邊在上方中間；已經全寬的算右邊，已經全高的算下邊。看的是哪條邊，不是線往哪走：上面的 [1] 按 `>` 和按 `<`，toast 都在 [1]
  的右上。其他照一般 toast：同一句不另開一個（`INFO ×3`），好幾個時往 panel 裡面疊；比 panel 寬的照樣靠那一邊、蓋到旁邊的 panel，
  不跑出畫面。`=` 的 toast 在平常的位置。
- **記住**：使用者移動過線之後，線停在哪裡記在 app 的 state（Rules E3），每個畫面各記各的，寬度依終端機寬度、高度依終端機高度，
  終端機再是那個寬度或高度時就用它；沒記過的尺寸用預設，由 app 自己定。使用者移動線之前什麼都不寫。按 `=` 也把這個畫面在這個寬度
  和這個高度記的值從 state 拿掉。
- **藏起來的位置**（跟著帶頭的 panel 換的 panel，Rules L5）：它的線跟著一起不見，再出現時線回到使用者上次放的地方；其他線留在使
  用者放的地方，因為藏起來而被版面換到別處的線算另一條，有自己的預設與記憶。
- **記著的線放不下時**（app 改了版面或某個 panel 的最小尺寸）：那個寬度或高度用預設，記著的值從 state 拿掉，不跳 toast、不做
  `.bak`、不記 WARN，是 Rules E3「值不合規則」唯一的例外（user 2026-11-26）。
- **不記進 App Log**：調整大小不記，跟 panel filter 一樣；只有動不了時的 toast 會記，跟每一個 toast 一樣
  （[`dialog/note`](../dialog/note-zh_TW.md) 的 note.7；user 2026-11-26）。
- **在選單裡**：`>` `<` `+` `-` 作用在有 focus 的 panel，是每個 panel 的 Space menu 裡的 panel operation；`=` 作用在整個畫面，是
  global operation（Rules M2、M3，Principle P3）：

| 列 | 說明 |
|---|---|
| `[>] Wider` | `2 columns, kept for this width` |
| `[<] Narrower` | `2 columns, kept for this width` |
| `[+] Taller` | `1 row, kept for this height` |
| `[-] Shorter` | `1 row, kept for this height` |
| `[=] Default layout` | `this screen's lines back` |

每一句說明在 60 欄時都放得下（Rules L1），選單裡和 key reference 裡都是。按了只會跳 toast 的列是停用的（M6），`[=]` 在畫面
每一條線都在預設時停用；在 panel 上按它的鍵照樣用 toast 回答，在選單裡按它的熱鍵則跟每一個停用列一樣不作用（變暗的列已經
說了現在不能執行）。只有一個 panel 的畫面沒有線，那四列和 `[=]` 都不列（M6：對象不存在），按鍵照樣用 toast 回答。

- **鍵保留**：在 panel 上，app 不能把這五個鍵拿去做別的事。鍵送到別處時（popup、輸入狀態、PTY、模式），它們在那裡就不是調整大小
  的鍵（Rules K8、K10、K11）。

**為什麼**：線放哪裡合適，要看 panel 裡裝什麼，也看使用者的終端機（很長的 branch 名稱、很寬的 diff），所以讓使用者自己移，app 依
那個尺寸記住：在 200 欄的終端機上調好的位置，到 80 欄就沒有意義。鍵取自 vim 的 `Ctrl-W` `<` `>` `+` `-` `=`。鍵作用在有 focus 的
panel（「這個變寬」），不是照箭頭方向移線，在每個 panel 上按，意思都一樣；線共用，原本對齊的 panel 就一直對齊。2 欄和 1 列看起來
差不多長，因為一格的高大約是寬的兩倍。按了沒反應會被當成鍵壞了；調整大小時眼睛看著那個 panel，所以 toast 出現在正在看的那條邊，
不在畫面下方蓋住正在調的 panel。調整大小不改任何資料，只是換個看法，連按十下記十筆會把真正做過的事擠掉；記著的線只是線放在哪，按
幾下就調回來，為它跳警告、多一份備份，比問題本身還吵。

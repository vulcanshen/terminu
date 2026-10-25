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
| 在模式裡（Rules K11） | `Space:menu ?:help`、模式自己的鍵、最後 `Esc:<離開的動詞>`。例：`Space:menu ?:help Enter:drop Esc:cancel` |
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
那一列寫 `3/10`，執行中的 glyph 是 Green）。terminal popup 開著時那一列被蓋住、看不到進度，這樣就好，不為了它多開一列。

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
最小寬度定，但不能高於 80（Rules L1：80 欄要能正常用）。窄寬只在 app 的最低尺寸以上才有；比最低尺寸還小時見下面的
「比最低尺寸小時」。

## screen.6 zoom

把一個 panel 放大是 app 的功能，要不要有、用哪個鍵，app 可以自行決定（例：filu 的 `z`）。規範給的是預設：放大時只畫有 focus 的那一個
panel，佔滿 panel 區，跟窄寬一樣；`Tab`、數字鍵照樣換 panel，換到的 panel 也是放大的，再按一次放大的鍵才還原。怎麼放大，app
可以自行決定（例：filu 把同一個 panel 的幾個 tab 並排）；沒有另外定的照預設。

**為什麼**：每個 app 放大想看的東西不一樣，規範只保住一個大家都懂的預設；預設跟窄寬一樣，使用者在窄的畫面上學會的，放大時
照樣能用。

## screen.7 比最低尺寸小時

畫面比 app 的最低尺寸還小時（Rules L1：預設 80×40，app 可以調低，但不能高於 80×40），整個畫面只畫兩列，上下左右置中：

```
                kbu
needs a terminal of at least 60×20
```

- **名稱**：app 的指令名稱，Blue 粗體（跟 splash 的名稱一樣，Rules S5）。
- **提示**：名稱下面一列，`needs a terminal of at least <寬>×<高>`，寫 app 的最低尺寸；Overlay0。
- **放不下時**：先拿掉提示，名稱一定留著（比畫面還寬時，畫得下多少就畫多少）；到 1×1 都不當掉。
- **按鍵都不作用**：不送進 app，也不送進 PTY；`q` 與單按一次 `Ctrl-C` 也不作用。只有連按兩次 `Ctrl-C` 立刻離開（Rules K9 的
  強制離開）。
- **狀態留著**：視窗拉大到最低尺寸以上，就回到原本的畫面，什麼都沒變。

**為什麼**：在比最低尺寸還小的畫面上硬畫，版面一定是壞的，使用者看到的是一堆截掉的框，不知道是 app 壞了還是視窗太小；
直接講名稱與需要多大，拉大視窗就好。這時使用者看不到 app 的狀態，按鍵照常送出去等於矇著眼操作 —— 可能誤刪東西，在 shell 裡
打了什麼也看不到；所以一律不作用，只留連按兩次 `Ctrl-C` 當緊急出口。離開流程可能要開 confirm 問問題，這時畫不出來，所以 `q`
與單按一次 `Ctrl-C` 也不作用。

## screen.8 空狀態

置中寫一句事實，加上一句點名按鍵的提示，都用 Overlay0；提示裡的鍵加方括號（Rules M5）。例：

```
No hosts yet

Press [A] to add a host, or [Space] to see what you can do here
```

- **太長時**：在空白處折行（[components](../README-zh_TW.md) 的「折行」），每一列置中，左右照樣離框一格；不截斷，也不必為了
  放得下而把句子縮短。
- **清單空了**：空狀態取代整塊，連表頭一起不畫，句子置中在整個 panel（[`panel`](panel-zh_TW.md) 的一般清單）。

panel 的 loading 與錯誤也用這個樣子（[`panel`](panel-zh_TW.md)）。

# screen（整個畫面）

**Language**: [English](screen.md) · 繁體中文

整個畫面的骨架。panel 的框見 [`panel`](panel-zh_TW.md)，浮在上面的框見 [`popup`](popup-zh_TW.md)。

## 由上往下

1. **最上面一列**：多畫面的 app 是畫面 chip 列，下面一條全寬分隔線；單畫面的 app 可以有一列 statusbar（由 app 決定）。
2. **panel 區**：其餘的高度。
3. **最下面一列**：footer。

## footer

一列，寫法照 Rules M5 的 hint；鍵 Blue、冒號與說明 Overlay0（[`color`](../color-zh_TW.md)）。寬度不夠時從尾端整組捨棄
（[`popup`](popup-zh_TW.md) 的 hint）。內容依情況：

| 情況 | footer |
|---|---|
| 一般 | `Space:menu ?:help Tab/1–N:panels q:quit` |
| 只有一個 panel 的 app | `Space:menu ?:help q:quit` |
| 在模式裡（Rules K11） | `?:help`、模式自己的鍵、最後 `Esc:<離開的動詞>`。例：`?:help Enter:drop Esc:cancel` |
| panel filter 打字中（輸入態） | `Enter/Tab:list Esc:clear` |
| focus 在 panel 裡的 PTY | 出口鍵，再加 app 保留的鍵（Rules K10）。例：`Alt-Esc:leave Alt-z:zoom PgUp:history` |

terminal popup 開著時，它蓋掉 footer（[`dialog/terminal`](../dialog/terminal-zh_TW.md)）。

**為什麼**：footer 是 Rules M1 的入口，寫的必須是現在按得了的鍵。模式裡 `Space` 不作用、打字時 `Space` `?` `q` 都是字元、
PTY 裡的鍵都送給子程序 —— 照常寫一般的 footer，反而教使用者按錯。

## 畫面 chip 列

多畫面的 app 最上面一列：每個畫面一個膠囊，畫法照 [`panel`](panel-zh_TW.md) 的膠囊串，串的顏色是 Blue（選中的畫面填 Blue、
字 Base 粗體；沒選中的不填底色、字 Blue）。放不下時照膠囊串的規則縮：先縮成 `[M] [F] [S]`，再收掉沒選中的。

右邊放 statusbar 的內容（見下）。chip 列下面一條全寬分隔線，Overlay0；長時間的工作（傳檔、下載）進行時，從左邊填 Green
當進度條，旁邊的狀態文字也是 Green。

## statusbar

由 app 決定要不要有。單畫面的 app 放在最上面一列；多畫面的 app 用 chip 列的右邊，不另開一列。它不是 surface，focus
不會停在上面。

- 寫法照 Rules M5 的 label：有熱鍵就標出來（例：kbu 的 `[C]ontext: prod  [N]amespace: default`）。
- 一般文字 Overlay0；「你現在在哪」的值 Lavender（使用者足跡）；進行中的工作 Green；錯誤、警告的數量 Red、Peach。
- 寬度固定（Rules L2），放不下時截斷，不折行（L3）。

## 窄寬

所有 panel 放不下時，只畫有 focus 的那一個 panel，佔滿寬度；`Tab` 照樣換 panel，一次看一個。門檻由 app 依自己 panel 的
最小寬度定，但不能高於 80（Rules L1：80 欄要能正常用）。

## 空狀態

置中寫一句事實，加上一句點名按鍵的提示，都用 Overlay0；提示裡的鍵加方括號（Rules M5）。例：

```
No hosts yet

Press [A] to add a host, or [Space] to see what you can do here
```

panel 的 loading 與錯誤也用這個樣子（[`panel`](panel-zh_TW.md)）。

# checkbox（開關）

**Language**: [English](checkbox.md) · 繁體中文

## 用途

一個開關，或從一組裡勾好幾個。開關與選項少的一組直接在表單或 panel 上翻；選項多的開 popup。

## 長相

選好幾個值的 popup（kbu 的 namespace picker）的列，跟 [`select`](select-zh_TW.md) 用同一套標記：

**每一列最前面放標記**（user 2026-10-07 定，照 kbu 的呈現方式）：

| | 每一列前面 | 選中的那一列 |
|---|---|---|
| **select（單選）** | radio glyph：選中 `󰐾`、沒選 `󰐽` | 字是 Green |
| **checkbox 組（多選）** | checkbox glyph：勾了、沒勾 | 字是 Green |

- 標記在左邊，眼睛往下掃就看得到；所有列的字對齊；選中的那一列有顏色（[`color`](../color-zh_TW.md) 的 Green 是「選中的值」）。
  cursor 停在選中的列上時，底色照 cursor 列、字照樣是 Green。
- 單選用 radio glyph（表單上的 radio 欄位也是這一組），多選用 checkbox glyph：看 glyph 就知道是單選還是多選，畫在表單上
  還是 popup 裡都一樣。
- 現況：kbu 的 namespace picker 就是多選這樣；kbu 的 context picker 用 `* `、webu 的 select 在右邊寫灰字 `current`，要改。

## 按鍵

**選好幾個的 popup**（user 2026-10-07 定，照 kbu 的 namespace picker）：

- **`Enter`**：勾或取消勾 cursor 那一列，**立刻生效**，popup 不關。從表單打開的，立刻寫回表單那一欄（表單記「改過了」）；
  單獨打開的，立刻套用（kbu：panel 2 馬上重抓）。
- **`Esc`**：關掉。勾一下本身就是確定，沒有東西要取消 —— 跟表單上的開關按 `Enter` 立刻翻是同一回事。
- hint：`Enter:toggle Esc:close`。選項多時 `/` 篩選，照 [`select`](select-zh_TW.md)。
- 不加 `Ctrl-S`（user：kbu 的做法比較直觀）。我先提「勾的先記著、`Ctrl-S` 才確定、`Esc` 放棄」，理由是套用表單那一輪的
  「input popup 的 `Esc` 是這一欄不改了」—— 那條是替要打字、`Enter` 才確定的 input popup 定的，不適用勾選。

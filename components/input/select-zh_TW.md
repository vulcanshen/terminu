# select（從清單選）

**Language**: [English](select.md) · 繁體中文

## 用途

從清單選**一個**值。選項少、放得進表單的用 [`radio`](radio-zh_TW.md)；選好幾個的用 [`checkbox`](checkbox-zh_TW.md)。

## 長相

從清單選**一個**值的 input popup（webu 頁面的 `<select>`、kbu 的 context picker；表單裡選項多到放不下的欄位按 `Enter` 打開的
就是它）。選好幾個的歸 [`checkbox`](checkbox-zh_TW.md)。user 2026-10-07 定。

- 長相照 [`dialog/menu`](../dialog/menu-zh_TW.md)：cursor 列的畫法、熱鍵的寫法。打開時 cursor 停在目前的值上。

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

- `j`/`k` 移動（頭尾相接）。**`Enter` 選定**：值寫回去、popup 關掉；從表單打開的，focus 照表單的規則往下一欄。
- **選項多時按 `/` 篩選**：篩選列的規則跟 panel 搜尋列一樣（打字中 `↑`/`↓` 移動、`Enter` focus 到那一項、再 `Enter` 才選定）；
  只有 `Esc` 不同 —— 在 popup 裡 `Esc` 關掉整個 popup（F1：階段不是一層；finder、kbu 現在都是這樣）。
- 選項可以有熱鍵（webu 的數字鍵），寫法照 menu；要不要有由 app 決定。
- 現況：kbu 的 context picker 打字時 `Enter` 直接切換並關閉，要改成先 focus 到那一項。

# slider（範圍內的數值）

**Language**: [English](slider.md) · 繁體中文

## 用途

範圍內的一個數值，位置比數字直觀的時候用（例：比例、亮度）。有 bottom、top、step 三個屬性。

## 長相

user 2026-10-07 定。

```
Red          ━━━━━━●━━━━━ 128
```

- **表單與 panel 上**：一條軌道加數字。軌道用粗線 `━`（user：原本的 `─` 太細），值的位置畫 `●`。軌道的寬度與顏色由 app 決定
  （webu、locku 現在 12 格；locku 把軌道畫成那個色版的顏色）。
- **`Enter` 打開的 popup 就是 [`select`](select-zh_TW.md)**，選項是 bottom 到 top、每 step 一個的數字：每一列前面 radio glyph、
  選中的字 Green（webu、locku 的 `current` 要改）、打開時 cursor 在目前的值、`j`/`k` 移動、`Enter` 選定、**`/` 打數字篩選**
  （打 `20` 只剩 20、120、200–209…，user：「作吧」）。slider 沒有自己的一套按鍵；在一列一個值的 panel 上 `h`/`l` 是移項目，
  不能拿來原地拉。

## 值

- **每個 slider 都要有 bottom、top、step 三個屬性**（user 2026-10-07）：沒有它們，數字清單就不知道有幾項。step 沒設時是
  `(top − bottom) / 10`。step 可以是小數（webu 現在只列整數，記為未做）。
- webu 現在「超過 10000 列就把步進乘 10」的做法由 step 取代；列很多時靠 `/` 篩選。

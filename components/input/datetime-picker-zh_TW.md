# datetime-picker（日期與時間）

**Language**: [English](datetime-picker.md) · 繁體中文

## 用途

選一個日期（date picker），或日期加時間（datetime picker）。月曆參考 [pickdate](https://github.com/maraloon/pickdate)，做成家族自己的。

## 長相

**日期**：

```
╭─ Due date ───────────────────────────────────╮
│                                              │
│     October   2026                           │   ← 月、年：各是一個可以 focus 的項目
│     Mo  Tu  We  Th  Fr  Sa  Su               │   ← 星期：Overlay0
│                  1   2   3   4               │
│      5   6   7   8   9  10  11               │   ← 7 號是今天：底線
│     12  13  14  15  16  17  18               │   ← 15 號是目前的值：Green；打開時 cursor 也在這裡
│     19  20  21  22  23  24  25               │
│     26  27  28  29  30  31                   │
│                                              │   ← 第 6 列：這個月用不到，照樣留著
│                                              │
╰─ Enter:choose t:today Tab:month Esc:cancel ──╯
```

- 月、年各是一個可以 focus 的項目；拿到 focus 時，那個字照 cursor 畫（層色底、Base 粗體）。
- 日曆**固定畫 6 列**：一個月會佔 4 到 6 週，固定 6 列，框的高度就不會因為換月而變（Rules F7）。
- 日曆上 cursor 停的那一天照 menu 的 cursor 畫。**cursor 停在哪一天，就是要寫回去的那一天**，沒有「選了還沒確定」的另一個狀態。
- 欄位原本的值字用 Green（跟 select 的目前的值一樣）；打開時 cursor 停在這一天，沒有值就停在今天。
- 今天加底線，不另外上色；週末也不另外上色（Principle P4：不多加顏色的意思）。
- 一週從週一或週日開始，由 app 決定。
- 範圍外的日子用 Surface2（停用），cursor 不停在上面。

**日期加時間**：右邊用一條直的分隔線切出另一塊放時間；只選日期的沒有這一塊。

```
╭─ Meeting ───────────────────────────────────╮
│                                             │
│     October   2026              │  06   50  │
│     Mo  Tu  We  Th  Fr  Sa  Su  │  07   55  │
│                  1   2   3   4  │  08   00  │
│      5   6   7   8   9  10  11  │  09   05  │
│     12  13  14  15  16  17  18  │  10   10  │   ← 時 10 與分 05 是目前的值：Green
│     19  20  21  22  23  24  25  │  11   15  │
│     26  27  28  29  30  31      │  12   20  │
│                                 │  13   25  │
│                                             │
╰─ Enter:time t:today Tab:time Esc:cancel ────╯
```

- 分隔線照 [`layout/popup`](../layout/popup-zh_TW.md)：不接上下框，只畫在內容那幾列。
- **時間分成「時」與「分」兩欄**：時 00–23，分每 5 分鐘一格（00–55）。兩欄都短，不需要搜尋，所以這一塊不是 finder。目前的值是 Green；
  跟日曆一樣高，超出就捲。目前的值不在格子上（10:07）時，打開時 cursor 停在它之前最近的那一格（10:05）。
- 有 focus 的那一塊 cursor 是層色底；沒有 focus 的那一塊，cursor 是層色 cursor 再淡化一次（Principle P6）。
- **寬度**：版面固定，照 [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」。

**為什麼**：選日期時間是「挑」，用移動就夠了；拆成時、分兩欄，一眼就知道是幾點幾分。

## 按鍵

可以拿 focus 的是：**月、年、日曆、時間**（只選日期的沒有時間）。整個 picker 只用 `Tab`、hjkl、`Enter`、`Esc`，加上 `t`。

- **`Tab`** 照畫面順序換 focus：月 → 年 → 日曆 → 時間 → 回到月。打開時 focus 在日曆。
- **月、年上**：`h`/`l`（`←`/`→`）換上一個、下一個月或年；日曆跟著翻，cursor 停在同一天（那個月沒有這一天就停在最後一天）。
- **日曆上**：`h`/`l` 前後一天，`j`/`k` 前後一週，走過月底自然換月（方向鍵在格子裡就是上下左右，Rules K12）。範圍外的日子跳過，
  停在那個方向下一個範圍內的日子；那個方向已經沒有了，就不動。
- **時間上**：`j`/`k` 在一欄裡移，`h`/`l` 在「時」與「分」兩欄之間換。
- **`Enter`**：
  - 月、年上：focus 移到日曆，不選。
  - 日曆上：只選日期的 → **確定**（寫回去、關掉）；datetime → focus 移到時間。
  - 時間上：確定，寫回「日曆 cursor 的那一天」加「時間 cursor 的那一格」，關掉。
- **`t`**：日期跳到今天，每一塊都能用；在時間上按，時間的 cursor 也跳到現在（分往前取最近的 5 分鐘）。
- **`Esc`**：關掉，不改。
- **hint**（順序照 [`layout/popup`](../layout/popup-zh_TW.md)：`Enter` 第一，`Esc` 最後；`Tab` 寫出下一塊是什麼）：

| focus 在 | hint |
|---|---|
| 日曆（datetime） | `Enter:time t:today Tab:time Esc:cancel` |
| 日曆（只選日期） | `Enter:choose t:today Tab:month Esc:cancel` |
| 月 | `Enter:days h/l:month t:today Tab:year Esc:cancel` |
| 年 | `Enter:days h/l:year t:today Tab:days Esc:cancel` |
| 時間 | `Enter:choose t:today Tab:month Esc:cancel` |

**為什麼**：換月換年不用 pickdate 的 `p`/`n`/`P`/`N`：那些是移動，hint 上看不到，使用者很難發現；`t` 會被用到，所以寫在 hint 上。

## 值

- **範圍**：可以設最早與最晚。
- **表單與 panel 上**：格式化的日期（時間），格式由 app 決定（`2026-10-15`、`2026-10-15 10:05`）；空的照 [`input/README`](README-zh_TW.md) 的空值規則。

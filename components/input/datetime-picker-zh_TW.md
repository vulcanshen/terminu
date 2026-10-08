# datetime-picker（日期與時間）

**Language**: [English](datetime-picker.md) · 繁體中文

選日期（date picker）或日期加時間（datetime picker）的 input popup。參考 [pickdate](https://github.com/maraloon/pickdate)
的月曆，做成家族自己的。user 2026-10-07 定。

## 用途

選一個日期，或日期加時間。

## 長相

**日期**：

```
╭─ Due date ─────────────────────────────────╮
│                                            │
│         October    2026                    │   ← 月、年：各是一個可以 focus 的項目，層色粗體
│    Mo  Tu  We  Th  Fr  Sa  Su              │   ← 星期：Overlay0
│                 1   2   3   4              │
│     5   6   7   8   9  10  11              │   ← 7 號是今天：底線
│    12  13  14  15  16  17  18              │   ← 15 號是目前的值（Green），打開時 cursor 也在這裡
│    19  20  21  22  23  24  25              │
│    26  27  28  29  30  31                  │
│                                            │
╰─ Enter:choose t:today Tab:month Esc:cancel ╯
```

- 日曆上 cursor 停的那一天照 menu 的 cursor（層色底、深色粗體）。欄位目前的值字用 Green（跟 select 的「選中的值」一樣）；
  打開時 cursor 停在這一天，沒有值就停在今天。
- 今天加底線，不另外上色；週末也不另外上色（P4：不多加顏色的意思；pickdate 兩者都上色）。
- 一週從週一或週日開始，由 app 決定（台灣的月曆多從週日開始，ISO 從週一）。
- 月、年拿到 focus 時，那個字照 cursor 畫（層色底、深色粗體）。

**日期加時間**：右邊用一條直的分隔線切出另一塊放時間（user）；只選日期的沒有這一塊。

```
╭─ Meeting ──────────────────────────────────┬────────────╮
│                                            │            │
│         October    2026                    │ 󰐽 09:50    │
│    Mo  Tu  We  Th  Fr  Sa  Su              │ 󰐽 09:55    │
│                 1   2   3   4              │ 󰐽 10:00    │
│     5   6   7   8   9  10  11              │ 󰐾 10:05    │   ← 10:05 是目前的值：Green
│    12  13  14  15  16  17  18              │ 󰐽 10:10    │
│    19  20  21  22  23  24  25              │ 󰐽 10:15    │
│    26  27  28  29  30  31                  │ 󰐽 10:20    │
│                                            │            │
╰─ Enter:time t:today Tab:time Esc:cancel ───┴────────────╯
```

- 分隔線跟框線同色，上下接到框（`┬`、`┴`），跟表單動作列上方的分隔線同一個做法。
- 時間從 00:00 開始，**每 5 分鐘一格**（user：15 分鐘太粗）。清單照 [`select`](select-zh_TW.md)：每一列前面 radio glyph、目前的值
  Green；跟日曆一樣高，超出就捲；`/` 打字篩選（打 `10:3` 只剩 10:30、10:35）。目前的值不在格子上（10:07）時，cursor 停在
  它之前最近的那一格（10:05）。
- 拿鍵的那一塊 cursor 是層色底，其他塊的 cursor 變淡的反白（Subtext1 底），照 finder 的規則。

## 按鍵

可以拿 focus 的有四塊：**月、年、日曆、時間**（只選日期的沒有時間）。整個 picker 只用 `Tab`、hjkl、`Enter`、`Esc`，加上 `t`
（user 2026-10-07 定；原本照 pickdate 的 `p`/`n`/`P`/`N` 換月換年不要 —— 那些是移動，hint 上看不到，使用者很難發現）。

- **`Tab`** 照畫面順序換 focus：月 → 年 → 日曆 → 時間 → 回到月。打開時 focus 在日曆。
- **月、年上**：`h`/`l`（`←`/`→`）換上一個、下一個月或年；日曆跟著翻，cursor 停在同一天（那個月沒有這一天就停在最後一天）。
- **日曆上**：`h`/`l` 前後一天，`j`/`k` 前後一週，走過月底自然換月 —— 方向鍵在格子裡就是上下左右（一維清單裡是前後；rules K12）。
- **`Enter`**：
  - 月、年上：focus 移到日曆，不選（「`Enter` 先 focus 到那一項」）。
  - 日曆上：只選日期的 → **確定**（寫回去、關掉）；datetime → 選好日期，focus 移到時間。
  - 時間上：日期與時間一起確定、關掉。
- **`t`**：日期跳到今天，每一塊都能用；在時間上按，時間的 cursor 也跳到現在（往前取最近的 5 分鐘，這點我補的）。
- **`Esc`**：關掉，不改。
- **hint**（user：`t` 放 hint 上）：

| focus 在 | hint |
|---|---|
| 日曆（datetime） | `Enter:time t:today Tab:time Esc:cancel` |
| 日曆（只選日期） | `Enter:choose t:today Tab:month Esc:cancel` |
| 月 | `h/l:month Enter:days t:today Tab:year Esc:cancel` |
| 年 | `h/l:year Enter:days t:today Tab:days Esc:cancel` |
| 時間 | `Enter:choose t:today Tab:month Esc:cancel` |

  順序是改值（`h/l`）→ `Enter` → `t` → `Tab` → `Esc`；`Tab` 寫出下一塊是什麼（切換階段的鍵照寫）。最長 48 字，80 欄的 terminal
  放得下（popup 寬度照 F7）；窄到放不下時照規則從尾端整組捨：先捨 `Esc:cancel`，再捨 `Tab:…`。

## 值

- **範圍**：跟 slider 一樣可以設最早與最晚；範圍外的日子用 Surface2 畫，cursor 不停在上面。
- **表單與 panel 上**：格式化的日期（時間），格式由 app 決定（`2026-10-15`、`2026-10-15 10:05`）；空的照 text 的空值規則。
- 現況：webu 讓使用者打格式字串，要改成這個 picker。

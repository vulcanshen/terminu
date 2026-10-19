# number（數字）

**Language**: [English](number.md) · 繁體中文

## 用途

輸入一個數字：port、秒數、次數、欄數。範圍小、用點選比打字快的值，用 [`slider`](slider-zh_TW.md)。

## 長相

- 骨架照 [`input/README`](README-zh_TW.md) 的單行 input popup。
- **說明列寫出範圍**（`Port, 1-65535`），不要等打錯才知道。
- **單位**（app 給了單位才有，例：秒數）：打字列下面多一列單位列，寫完整的字（`seconds`，不寫 `s`），灰字（Overlay0），跟值的
  第一格對齊，不跟著打的字移動。表單與 panel 上照 [`input/README`](README-zh_TW.md) 的顯示寫成 `10 seconds`。沒有單位的數字沒有這一列。

```
┏━REFRESH━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                  ┃
┃ Seconds between runs while nothing happens, 1-60 ┃
┃                                                  ┃
┃  10█                                            ┃
┃   seconds                                        ┃   ← 單位列：Overlay0，跟值的第一格對齊
┃                                                  ┃
┃                                                  ┃   ← 錯誤列
┃                                                  ┃
┗━ Enter:save Esc:cancel ━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **寬度**：範圍已知時，最多幾位數就確定，照 [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」；有單位列時，
  單位列也算進最寬的那一列。

**為什麼**：輸入的時候就看得到單位，知道自己在輸入什麼 —— `10` 是十秒還是十分鐘；單位寫完整的字，不用猜縮寫。

## 按鍵

- 編輯鍵、灰字提議、貼上照 [`input/README`](README-zh_TW.md)。
- **打字當下只收這個欄位可能用到的字**：數字；欄位允許負數才收 `-`，允許小數才收 `.`。其他鍵按了沒反應。貼上時只留下會收的字。
- 不做 `↑|↓` 加減：要點選的值用 slider。

**為什麼**：不可能對的字沒必要讓它進來再擋。

## 值

- **範圍在 `Enter` 時檢查**，錯了寫錯誤列，點名值（照 [`README`](README-zh_TW.md) 的「什麼是 input」：`Port must be 1-65535`）。
- **欄位可以空時**：空的值不做範圍檢查，存成空的；空著代表什麼，表單與 panel 上由 app 用灰字寫（照 [`README`](README-zh_TW.md) 的
  「在表單與 panel 上怎麼顯示」，例：`30 (default)`、`ssh decides`）。欄位不能空時，空的值照錯誤處理。

**為什麼**：範圍要等整個數打完才知道，打到一半不能擋 —— 要打 `22`，打第一個 `2` 時還不到最小值。

# confirm（確認）

**Language**: [English](confirm.md) · 繁體中文

## 用途

問一句，`Enter` 接受、`Esc` 取消，並說出後果（Rules F6）：刪除前、離開前、「連線到 X？」。哪些動作要問由 app 決定（F6）。

## 長相

```
╭─ Quit ────────────────────────────────╮
│                                       │
│ 2 live sessions will be closed.       │  ← 要先看的內容：Overlay0；警告的那一句 Peach
│                                       │
│ Quit sshu?                            │  ← 問句：Text，放最後
│                                       │
╰─ Enter:quit Esc:cancel ───────────────╯
```

- **標題**：`nf-md-shield_alert`（U+F0ECC）加動作名（`Delete`、`Quit`、`Connect`）。
- **問句放最後**，下面接著就是 hint。回答前要看的內容放在問句上面，跟問句之間空一列（Rules F1）；沒有內容時就只有問句。
- **顏色**：問句用 Text，不加粗；內容用 Overlay0；內容裡警告的那一句（例：「無法復原」「2 個 session 會被關掉」）用 Peach，
  哪一句算警告由 app 決定。
- **太長**：問句與內容都折行，不截斷。內容長時只有內容那一段用 `j/k` 捲，問句固定在最後。
- **寬度**：內容打開時就確定，照 [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」；長的折行到上限為止。

**為什麼**：讀的順序是先看內容、再看問句、最後是按鍵；問句緊貼著 hint，讀到問題時，答案就在下一列。標題用盾牌：confirm 存在
就是擋這一下、讓使用者再想一次；警告的 ⚠ 若掛在每個 confirm 上，警告的意思就用掉了（Principle P4）。警告用 Peach 不用 Red：
Red 是已經發生的錯誤，這時候還沒有出錯。

## 按鍵

- `Enter` 接受，`Esc` 取消（Rules F6）。confirm 自己的熱鍵（例：`y` / `n`）可以有，要列在 `?` 裡。`Space` 不作用（Rules K5）。
- **hint**：`Enter:<動詞> Esc:cancel`，動詞寫接受會做的事（例：`Enter:delete Esc:cancel`）。

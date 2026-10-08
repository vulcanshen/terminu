# terminal（框裡跑子程序）

**Language**: [English](terminal.md) · 繁體中文

## 用途

框裡跑的子程序（shell、編輯器、遠端 session）：按鍵都給它，只有出口鍵與 app 保留的組合鍵屬於 app（Rules F1、K10）。PTY 放在
panel 裡時（例：sshu 的格子）不是 popup：框照 [`layout/panel`](../layout/panel-zh_TW.md)，PTY 的鍵寫在 footer（[`layout/screen`](../layout/screen-zh_TW.md)）。

## 長相

```
 [M]anage  [F]ile transfer  [S]SH       2 live sessions    ← statusbar／畫面 chip 列：留著
╭─ Alterm: myhost ───────────────────────────────────────╮
│ $ kubectl get pods                                     │
│ NAME          READY   STATUS    RESTARTS   AGE         │
│ nginx-7d4f    1/1     Running   0          3d          │
│ $ █                                                    │
╰─ Alt-Esc:exit Alt-t:hide PgUp:history ─────────────────╯   ← 一直到畫面最後一列，蓋掉 footer
```

- **大小**（Rules F7 的 terminal 例外）：寬度 `terminal 寬 − 2`，不受 120 欄上限。上面留著 statusbar 或畫面 chip 列；下面一直到畫面
  最後一列，蓋掉 footer。沒有 statusbar 的 app，從第一列開始。
- **不留白**：子程序需要每一列，內容從框裡第一列畫到最後一列。
- **標題**：`nf-md-console`（U+F018D）加上跑的是什麼（`Shell`、`Alterm: myhost`、`Edit: pod/x`）。

**為什麼**：statusbar 上有正在進行的狀態（kbu 的 context、sshu 的傳檔進度），在 shell 裡工作時照樣會想瞄一眼。footer 不需要：
focus 在 PTY 裡時，footer 上的 `Space`、`?`、`q` 都送給子程序，照常顯示反而誤導；PTY 的鍵只出現在一個地方，就是這個框的下框，
不會有兩列 hint。

## 按鍵

- 按鍵都送給子程序（Rules K10）。
- **hint**：出口鍵永遠是第一個，放不下時最後才捨。動詞寫按下去真正會發生的事：
  - `Alt-Esc:exit`：結束子程序。
  - `Alt-Esc:leave`：離開，子程序還留著。
  - 不寫 `close`。
- 出口鍵後面跟 app 保留的組合鍵（例：`Alt-t:hide`、`PgUp:history`）。
- `Alt-Esc` 一律先 confirm（Rules K10）。

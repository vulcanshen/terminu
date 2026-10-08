# textarea（多行文字）

**Language**: [English](textarea.md) · 繁體中文

## 用途

輸入多行文字：網頁表單的留言、說明。程式碼、設定檔這種「一行就是一行」的內容，交給使用者的 `$EDITOR`。

## 長相

**一行太長時自動折行，左邊有行號**（user 2026-10-07 定）：

```
│  1 Thanks for the quick reply. The new   │
│    build fixes the crash on start.       │   ← 同一行折下來：行號欄空白
│  2                                       │
│  3 One more thing: the export button█    │   ← 游標所在的行
```

- 超過框寬就接到下一列畫，不左右捲。折行只在畫面上，值裡不多出換行。寬度照顯示寬度算，一個字不折成兩半。
- **行號**：每一行的第一列畫行號，靠右對齊、寬度取最大行號的位數，後面空一格；折下來的列行號欄空白 —— 看得出哪幾列是
  同一行（user）。行號 Overlay0，游標所在那一行的行號 Text（我補的）。
- 要編輯「一行就是一行」的內容（程式碼、設定檔），交給使用者的 `$EDITOR`（sshu 的 File transfer 就是這樣），components 不另做
  左右捲的 textarea。
- 現況：webu 只左右捲游標那一行、其他行超寬直接切掉、照字數算寬度，要改。

## 按鍵

**兩種狀態與送出**（user 2026-10-07 定）：

| 狀態 | 做什麼 | hint |
|---|---|---|
| **寫** | 打字。`Enter` 換行、`Tab` 縮排（K8）。打開時在這裡 | `Esc:move` |
| **移** | 在「寫」裡按 `Esc` 進來。`h`/`j`/`k`/`l` 移游標，`i`、`a`、`o` 回到「寫」；**`Enter` 存** | `Enter:save i:write Esc:cancel` |

- **送出就是「移」狀態的 `Enter`，沒有 `Ctrl-S`**（user 2026-10-07 改：textarea 本來就有兩種狀態，`Ctrl-S` 是多的；先定的是
  兩態都可以 `Ctrl-S` 送出）。`Ctrl-S` 只留在表單：表單的 `Enter` 用來開欄位，才需要另一個送出鍵。
- `Esc`：在「寫」裡進到「移」（hint 會換成 `Enter:save`，照著就知道怎麼存）；在「移」裡關掉（內容改過先 confirm，見下一點）。
- 兩種狀態是 webu 現在的做法，rules K3、K8 也這樣寫；保留它是因為 user 要 hjkl（表單也是）。

**「寫」的編輯鍵**（從已定的規則推）：text 的那一組，加上多行才要的 —— `↑`/`↓` 換到上一列、下一列（照畫出來的列，折行也算一列）；
`←`/`→` 到行頭、行尾時跨到上一行、下一行；行首的 `Backspace` 跟上一行合併。貼上的換行就是真的換行（貼上規則本來就排除 textarea；
webu 現在把貼上的換行塞在同一行，要改）。

- 內容改過時，`Esc` 先開 confirm 問要不要放棄，跟表單一樣（見 [`dialog/form`](../dialog/form-zh_TW.md) 的「取消」；user 2026-10-07）。

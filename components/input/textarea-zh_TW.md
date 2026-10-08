# textarea（多行文字）

**Language**: [English](textarea.md) · 繁體中文

## 用途

輸入多行文字：網頁表單的留言、說明。程式碼、設定檔這種「一行就是一行」的內容，交給使用者的 `$EDITOR`（例：sshu 的 File transfer），
不用 textarea。

## 長相

**一行太長時自動折行，左邊有行號**：

```
│  1 Thanks for the quick reply. The new   │
│    build fixes the crash on start.       │   ← 同一行折下來：行號欄空白
│  2                                       │
│  3 One more thing: the export button█    │   ← 游標所在的行
```

- 超過框寬就接到下一列畫，不左右捲。折行只在畫面上，值裡不多出換行。寬度照顯示寬度算，一個字不折成兩半。
- **行號**：每一行的第一列畫行號，靠右對齊、寬度取最大行號的位數，後面空一格；折下來的列行號欄空白 —— 看得出哪幾列是同一行。
  行號 Overlay0，游標所在那一行的行號 Text。
- **寬度**：內容不確定，用 Rules F7 的上限。

## 按鍵

**兩種狀態**：

| 狀態 | 做什麼 | hint |
|---|---|---|
| **寫** | 打字（輸入態）。`Enter` 換行、`Tab` 縮排（Rules K8）。打開時在這裡 | `Esc:move` |
| **移** | 在「寫」裡按 `Esc` 進來。移動游標；`i`、`a`、`o` 回到「寫」；**`Enter` 確定** | `Enter:save i:write Esc:cancel` |

- **確定就是「移」裡的 `Enter`**。
- `Esc`：在「寫」裡進到「移」（hint 會換成 `Enter:save`，照著就知道怎麼存）；在「移」裡關掉。內容改過時，先開 confirm 問要不要放棄
  （[`dialog/form`](../dialog/form-zh_TW.md) 的「取消」）。
- **「寫」的編輯鍵**：[`input/README`](README-zh_TW.md) 的那一組，加上多行才要的 —— `↑`/`↓` 換到上一列、下一列（照畫出來的列，折行也算
  一列）；`←`/`→` 到行頭、行尾時跨到上一行、下一行；行首的 `Backspace` 跟上一行合併。貼上的換行就是真的換行。
- **「移」的鍵**：移動照 Rules K12 —— `h/j/k/l`、`w/b/e`、`0/$`、`u/d`、`gg/G`。`i` 在游標前開始寫、`a` 在游標後開始寫、`o` 在下面開新的
  一行再寫（照 vim）。
- 「移」不是模式，也不是輸入態：core key 照 Rules K1（`?` 打開 key reference）。

**為什麼**：多行的 `Enter` 要拿來換行，確定只能換一個鍵或換一個狀態；有兩種狀態，「移」裡的 `hjkl` 可以移動、`Enter` 可以確定，
不用另外的送出鍵。

## 值

在表單與 panel 上：第一行；後面還有就加 `…`（[`input/README`](README-zh_TW.md)）。

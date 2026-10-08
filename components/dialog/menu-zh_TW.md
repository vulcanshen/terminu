# menu（從清單選一列執行）

**Language**: [English](menu.md) · 繁體中文

長相與按鍵 2026-10-07 從 defaults D4 搬來（從 defaults 升成規定）。

## 用途

從清單選一列執行（F1）：Space menu、global operation popup、選項清單、工作清單（`Enter` 打開那一列的全文）。

## 長相

- menu 列：` [k]label` 左對齊，說明靠右、暗色。
- 熱鍵字母是 label 的第一個字母就原地加括號（`[r]ename`），在字中間就原地包（`UR[L]`），否則放前面（`[n] New`）。
  core key 直接寫進 label：`[Enter] Edit`。
- label 本身已經寫出鍵的列（`[/] Search`）不要再括一次。
- cursor 列：popup 層色底、深色粗體字（defaults D3 的 finder 一段寫明「跟 menu 的 cursor 列一樣」）。
- menu 標題是 focus panel 的 `[N] label`。
- popup 寬度統一照 Rules F7；說明太長時在框裡換行或截尾，不為了它加寬框。

## 按鍵

- `j/k` 移動（頭尾相接），`Enter` 執行，熱鍵直接執行；下框 hint `Enter:run Esc:close`（不寫移動鍵，見 [`layout/popup`](../layout/popup-zh_TW.md) 的 hint；D4 原本是 `j/k:move Enter:run Esc:close`）。

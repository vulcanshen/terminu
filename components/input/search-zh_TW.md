# search（搜尋與篩選）

**Language**: [English](search.md) · 繁體中文

## 用途

兩種樣子：**finder**（一個 popup：打字列 + 結果清單 + 預覽；filu 的 Search、Find、Goto，webu 的 `/`）與 **panel 裡直接打字的搜尋列**
（見 [`layout/panel`](../layout/panel-zh_TW.md)）。[`file-picker`](file-picker-zh_TW.md) 是 finder 的一種。

## 長相

**finder 的骨架**（user 2026-10-07 定；file-picker 共用）：

- **兩個區塊**：上面是打字列（右邊寫結果數），一條分隔線，下面是結果清單。`Tab` 在兩區之間切換。
- **預覽是規定**（user）：選中的那一筆在旁邊預覽。寬度 ≥ 96 時清單與預覽左右並排，不夠就上下疊；預覽框的標題是選中那一筆
  的名字（或它在哪裡），預覽不拿 focus。預覽的內容由 app 決定（檔案內容、目錄樹、網頁的那一段）。現況：filu、webu 的 finder
  都已經是這樣。
- **邊找邊列**：結果陸續到時照樣列出，標題後面放 loading icon；一筆都還沒到時寫 `(indexing…)`（filu）。
- 高度打開時定好（F7）。

## 狀態

- **finder 的 focus**（Rules F1；2026-10-07 從 defaults D3 搬來）：打字時篩選列亮、清單的 cursor 列是淡的反白；`Tab` 到清單後，
  篩選列整列用灰色（Overlay0，[`color`](../color-zh_TW.md) 的暗字）畫，不用 F8 的淡化、也不畫反白與游標，清單的 cursor 列換成 popup 層色底加深色粗體字
  （跟 menu 的 cursor 列一樣）。只有拿鍵的那一邊是亮的，跟 F8「只有最上層亮」同一套語言（kbu `40a0573`）。

## 按鍵

**finder**（user 2026-10-07 定）：

- **打字時按 `Enter`**：focus 移到清單上反白的那一筆，不執行；沒有結果時不作用。
- **在清單上按 `Enter`**：去那裡（file-picker 是選中檔案，見它的檔）。
- `Tab` 在兩區之間切換；`Esc` 關掉整個 finder（F1：階段不是一層）。
- 理由：跟 panel 搜尋列同一個原則（user：「`Enter` 先 focus 到那一項，要執行再按一次」）—— finder 的打字列與 panel 的搜尋列
  是同一種 input，同一個鍵在兩處次數不同，使用者記不住。代價是多按一下 `Enter`；fzf、VS Code 快速開檔那種「打字時 `Enter`
  直接去」不採用。
- 現況：webu 是這樣；filu 打字時 `Enter` 直接去，要改。filu 那樣是 2026-09-28 user 的裁定（當時從「`Enter` 交給清單」改成「直接選」，
  rules F1 也寫「`Enter` 送出選中的那一筆」）；我提出這個衝突後，user 確認改回「`Enter` 進清單」—— filu 現在的做法不好。F1 已改。
- panel 裡直接打字的搜尋列見 [`layout/panel`](../layout/panel-zh_TW.md)。

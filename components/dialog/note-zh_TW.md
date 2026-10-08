# note（唯讀內容）

**Language**: [English](note.md) · 繁體中文

## 用途

唯讀的內容，可以捲動（`j`/`k`、`u`/`d`、`gg`/`G`，K12），可以有自己的熱鍵與模式（F1）：key reference、YAML 檢視、App log、error popup。

## error popup

popup 的動作失敗時（submit error，見 [`layout/popup`](../layout/popup-zh_TW.md) 的錯誤列），蓋在那個 popup 上的 note。表單錯誤列
`Enter` 打開的完整訊息也是它。user 2026-10-07 定。

- **樣子**：框、標題、文字都是 Red。訊息在框裡換行；太長時 `j`/`k` 捲動，跟其他 note 一樣。
- **標題**：寫哪件事失敗了（`Rename failed`、`Save failed`），照「標題寫這個 popup 是做什麼的」。從表單錯誤列打開的，標題寫
  那一欄的名字（`Port`）。
- **關掉**：`Enter` 與 `Esc` 都能關，hint `Enter/Esc:close`。上面沒有東西可以執行，看完按 `Enter` 是反射動作（K3）；連按
  `Enter` 也不出事 —— 第一下關掉它，下一下只是在按鈕上再送出一次。
- **關掉之後**：回到底下的 popup，focus 留在原位，值都還在（F4）。

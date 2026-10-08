# select（從清單選一個值）

**Language**: [English](select.md) · 繁體中文

## 用途

從清單選**一個**值：webu 頁面的 `<select>`、kbu 的 context picker、表單裡選項多到放不下的欄位；slider 的數字清單、color picker 的
00–FF 也是它。選項五個以內、畫在表單上的用 [`radio`](radio-zh_TW.md)；選好幾個的用 [`checkbox`](checkbox-zh_TW.md) 的 popup。

select 是 finder 的一種（[`input/finder`](finder-zh_TW.md)）：這裡只寫跟 finder 不同的地方。

## 長相

- finder 的骨架，**沒有預覽**；打字列一直顯示，短清單也是。
- 每一列前面放 radio glyph，目前的值是 Green（finder 的「清單的標記」）。
- 選項可以有熱鍵（例：webu 的數字鍵），寫法照 Rules M5；要不要有由 app 決定。
- **寬度**：選項打開時就確定，照 [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」。

## 按鍵

- **打開時 focus 在清單上，cursor 停在目前的值**。
- 清單上 `Enter`：選定 —— 值寫回去、popup 關掉；從表單打開的，focus 留在那一欄。
- 打字列與清單的其他鍵照 finder。
- **hint**：清單 `Enter:choose Tab:filter Esc:cancel`；打字列 `Enter/Tab:list Esc:cancel`。

**為什麼**：選值多半是從目前的值移一兩格：開在清單上，`Enter`（打開）`j` `Enter` 就好；開在打字列上要多按一下。打字列一直顯示，
要篩選時框的高度不用變（Rules F7）。

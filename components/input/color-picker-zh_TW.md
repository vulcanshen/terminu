# color-picker（顏色）

**Language**: [English](color-picker.md) · 繁體中文

## 用途

選一個顏色：webu 網頁上的顏色欄位、locku 的配色設定。

## 長相

```
┏━BACKGROUND━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                      ┃
┃ ████████  ████████                   ┃
┃ ████████  ████████  ███  ███  ███    ┃   ← R、G、B：小色塊，畫那個色版自己的顏色
┃ old       new       R▓▓  G    B      ┃   ← focus 在 R：下面的名稱與 hex 兩列照 cursor 畫，寬度跟色塊一樣
┃ #1E1E2E   #2A2A3C   2A▓  2A   3C     ┃   ← 一律寫 hex
┃                                      ┃
┃ ──────────────────────────────────── ┃
┃                              Choose  ┃   ← 動作區：按鈕 `Choose`；`Tab` 在色版與按鈕之間來回
┃                                      ┃
┗━ Enter:edit Tab:actions Esc:cancel ━━┛
```

- **一整列由左到右**：old、new、R、G、B，五個項目之間兩格。版面小，不佔一大塊。
- **old、new 兩個色塊畫大一點**（8 格寬、2 列高）：old 是打開時的顏色，一直不變；new 是調整中的顏色，跟著 R、G、B 即時變。下面寫 `old`、`new` 與各自的
  hex。並排比較，看得出改了多少。
- **R、G、B 是小色塊**（3 格寬、1 列高），不是 slider：色塊畫那個色版自己的顏色（R 是 `#RR0000`）；下面寫它的值，**一律用 hex**。
- **動作區**：內容下面一條分隔線，右邊一個按鈕 `Choose`，畫法照 [`dialog/form`](../dialog/form-zh_TW.md) 的按鈕（沒 focus 時 Surface1 底、
  Text 字；有 focus 時層色底、Base 粗體；靠右，離框一格）。color picker 不會不合格，沒有錯誤列。
- **寬度**：版面固定，照 [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」。

**為什麼**：三條 slider 太佔版面；一列小色塊加 hex，一眼看完。顏色在家族裡都寫成 hex（`#2A2A3C`），各色版也用 hex，對得起來。

## 按鍵

- **可以 focus 的是 R、G、B 與 `Choose` 四個**，依序 R → G → B → `Choose`，`h|l` 左右移動（一維：`j|k` 也是前後；到頭尾繞回，
  Rules K12）。**old、new 不拿 focus**：old 不改就 `Esc`；new 是 R、G、B 改出來的結果，不用另外 focus。打開時 focus 在 R。
  focus 在色版上時，下面的名稱與 hex 兩列都照 cursor 畫（層色底、Base 粗體），寬度跟上面的色塊一樣（3 格 × 2 列）。
- **`Tab|Shift-Tab` 在色版（R、G、B）與 `Choose` 之間來回**，回來時停在離開前的那個色版 —— 照表單的欄位區與動作區
  （Rules K2、[`input/README`](README-zh_TW.md)）。
- **`Enter`** 對 focus 的項目做最直觀的動作（Rules K3）：
  - R、G、B：打開數字的 [`select`](select-zh_TW.md)（00–FF、step 1、cursor 在目前的值），每一列寫 hex、括號裡附十進位：`2A (42)`；
    打字篩選，打 hex 或十進位都篩得到。選完回來，new 跟著變，focus 留在那個色版。
  - `Choose`：確定，寫回去，關掉。
- **`Esc`**：關掉，不改。
- **hint**：R、G、B 上 `Enter:edit Tab:actions Esc:cancel`；`Choose` 上 `Enter:choose Tab:fields Esc:cancel`。

**為什麼**：R、G、B 改的就是 new，new 自己沒有東西可以 focus；確定照表單用按鈕，一樣是按 `Enter`，按鈕看得到 ——「欄位改值，按鈕送出」
跟表單同一套，`Tab` 也跟表單一樣在色版與按鈕之間來回。
focus 的色塊蓋住名稱與 hex 兩列、跟色塊一樣寬：一格的色塊很容易漏看，正在改的 hex 值也一起亮。

## 值

表單與 panel 上：一小格色塊加 hex（`███ #2A2A3C`）；空的照 [`input/README`](README-zh_TW.md) 的空值規則。cursor 在這一欄時，
色塊保留自己的顏色，hex 照樣換成 Base（[`color`](../color-zh_TW.md) 的 cursor 色塊）。

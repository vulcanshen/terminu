# color：配色

**Language**: [English](color.md) · 繁體中文

一整套配色的**呈現規則 + 計算方式 + 色碼**，全家族照用。2026-10-07 從 defaults D2 搬來，從 defaults 升成規定（user 定；原本是
「不想處理配色的 app 整套照用，要自訂的 app 自己決定用哪些」）。意義要不要同時用顏色以外的方式（框線、符號）表達，由 app
決定 —— rules 另有規定的除外（例：focus 不能只靠顏色，L5）。

**呈現規則**

1. **最少錨點，其餘推導**：先選三個錨點 —— 底色、使用者足跡、popup 最上層 —— 其餘層次
   從錨點推導，不為每個元素各挑顏色。
2. **明度是 z 軸，不反轉**：從底色到最上層的 popup，明度單向遞進，越上層越亮。TUI 沒有
   陰影與高度，明度是唯一能表達「哪個在上面」的工具。
3. **明度帶專職**：每個意義佔一條明度帶，其他意義不用同一條（Principle P4）。例：
   「使用者足跡」用了 lavender，popup 邊框就不用 lavender。
4. **警示色不參與 z 軸**：錯誤、警告色在任何一層都是同一個顏色，不跟著層級變亮變暗。
5. **同鍵兩處指示**（Rules M9）：會觸發的那個亮、不會的那個暗。
6. **失焦的 panel**：邊框換色與框線；內容照 F8 的 dim 變暗，串流內容除外（Rules T2，2026-10-07 起；原本是「內容不變暗」）。

**計算方式：dim（Rules F8）**

改寫已經畫好的畫面裡每一個顏色碼（SGR），不動文字與版面：

```
dim(c) = c × 0.45 + base × 0.55        base = #1e1e2e
```

- 前景與背景都照這個算；16 色、256 色先換成 RGB 再算。
- **淡化絕不讓顏色變亮**：每個通道取原值與淡化值較小的那個 —— 比 base 還暗的顏色（例：`#000000`）淡化後會變亮，那就維持原色。
- 輸出一律是 24-bit（`38;2;…` / `48;2;…`）：家族要求 truecolor terminal（rules E4），dim 不必照色彩深度降階。
- 沒有指定前景的文字，給淡化後的預設字色（`dim(Text #cdd6f4)`）。
- bold、reverse、游標移動、文字本身不動。
- filu 的 `internal/ui/dim.go` 是參考實作。

**計算方式：popup 邊框依層數插值**

```
layer K 的邊框色 = lerp(使用者足跡, popup 最上層, K / N)    N = 4
K ≥ N 時固定為 popup 最上層
```

以 catppuccin-mocha 代入（Lavender → Sapphire）：

| layer | 1 | 2 | 3 | 4+ |
|---|---|---|---|---|
| 邊框色 | `#A4C0FA` | `#94C3F5` | `#84C5F0` | `#74c7ec` |

**色碼（catppuccin-mocha）**

| 用途 | 色 |
|---|---|
| 底色 | Base `#1e1e2e` |
| focus 邊框 | Blue `#89b4fa`，雙線 `╔═╗` |
| 非 focus 邊框 | Surface2 `#585b70`，圓角 `╭─╮`（跟雙線同寬，切換零位移） |
| popup 邊框 | 見上表 |
| 正在編輯的東西、使用者足跡 | Lavender `#b4befe` |
| 錯誤 | Red `#f38ba8` |
| 值得注意、但沒壞 | Peach `#fab387` |
| 選中的值（select、checkbox 組裡選中、勾了的那一列；2026-10-07 加） | Green `#a6e3a1` |
| 選取；模式（外框與右上角的模式名，Rules K11） | Yellow `#f9e2af` |
| 暗字；hint 與 footer 的冒號與說明 | Overlay0 `#6c7086` |
| hint、footer、key reference 裡的鍵 | Blue `#89b4fa` |
| key reference 的說明 | Text `#cdd6f4` |
| 失焦 panel 邊框上的 hint：鍵 / 冒號與說明 | Overlay0 `#6c7086` / Surface2 `#585b70`（Blue 是 focus 的顏色，只給拿鍵的地方） |

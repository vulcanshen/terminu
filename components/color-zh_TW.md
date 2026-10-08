# color（配色）

**Language**: [English](color.md) · 繁體中文

一整套配色的**呈現規則 + 色碼 + 計算方式**，全家族照用。意義要不要同時用顏色以外的方式（框線、符號）表達，由 app
決定 —— rules 另有規定的除外（例：focus 不能只靠顏色，L5）。內容本身的顏色（檔案類型、pod 狀態、log 等級、語法上色）
由 app 決定；這裡管的是 tdp 定的介面元素（Principle P4）。

## 呈現規則

1. **最少錨點，其餘推導**：先選三個錨點 —— 底色、使用者足跡、popup 的終點色 —— 其餘層次從錨點推導，不為每個元素各挑顏色。
2. **層色是 z 軸**：popup 的框與標題用層色。起點是使用者足跡（Lavender），終點是 Sapphire，中間分 N = 4 段；第 K 層取第 K 段，
   第 N 層以上固定是終點色。最底下的 popup 是第 1 層；toast 不算一層，一律用第 1 層的顏色（Rules F1）。
3. **顏色專職**：每個意義佔一個顏色，其他意義不用同一個（Principle P4）。例：「使用者足跡」用了 Lavender，popup 的框就不用
   Lavender —— 層色的起點是它，但第 1 層已經往終點走了一段。
4. **警示色不跟層數換色**：錯誤、警告在哪一層都是同一個 Red、Peach；被蓋在底下時照 F8 一起淡化。
5. **亮的就是有 focus 的**（Principle P6）：最上層以外淡化（F8）、失焦的 panel 淡化（T2，串流內容除外）、同鍵兩處指示時
   會觸發的那個亮（M9）、沒有 focus 的那一塊上的 cursor 淡化。
6. **粗體只用在**：cursor 上的字、popup 的標題、膠囊的字、模式名、標題後面的 loading icon。

## 色碼（catppuccin-mocha）

| 意義 | 用在 | 色 |
|---|---|---|
| 底色 | 畫面的底；淡化的目標 | Base `#1e1e2e` |
| focus | focus 的框（雙線 `╔═╗`）；hint、footer、key reference 裡現在按得了的鍵；有 focus 的 panel 的 label 與表頭；畫面 chip 列 | Blue `#89b4fa` |
| 用不到 | 失焦的框（圓角 `╭─╮`，跟雙線同寬，切換零位移）；停用的列、label、選項；範圍外的日子 | Surface2 `#585b70` |
| 層色 | popup 的框與標題；popup 裡的 cursor 色塊 | 見下面的「popup 的層色」 |
| 正在編輯、使用者足跡 | input popup 裡的值與游標；使用者留下的位置（麵包屑的「你在這裡」、statusbar 上「你現在在哪」的值） | Lavender `#b4befe` |
| 生效中 | 目前生效的值（select 選的、勾著的、開著的）；活著的 session；進行中的工作與進度條；成功完成的 | Green `#a6e3a1` |
| 模式 | 模式的外框與模式名、模式裡選起來的範圍（Rules K11） | Yellow `#f9e2af` |
| 警告：值得注意、但沒壞 | confirm 裡警告的那一句；Warning toast 的字 | Peach `#fab387` |
| 錯誤 | 錯誤列、出錯的 label、error popup、Error toast 的字、貼上的 `\n` `\t` | Red `#f38ba8` |
| 暗字 | menu 的說明與區塊標題；hint、footer 的冒號與說明；說明列；灰字提議；空值的說明；沒有 focus 的打字列；空狀態；分隔線（popup 裡的、畫面 chip 列下面的） | Overlay0 `#6c7086` |
| 一般文字 | 表單與 panel 上的值；menu 的 label；key reference 的說明 | Text `#cdd6f4` |
| panel 的 cursor | panel 上 cursor 所在那一列的底，字是 Base 粗體 | Subtext1 `#bac2de` |
| 按鈕 | 沒有 focus 的按鈕的底，字是 Text | Surface1 `#45475a` |

- **cursor 色塊**：popup 裡是層色底、panel 上是 Subtext1 底，字都是 Base 粗體；沒有 focus 的那一塊上的 cursor，是有 focus 時的
  cursor 再淡化一次（P6）。
- 字要放在 cursor 色塊上時，一律換成 Base；原本的顏色不保留。

## popup 的層色

```
第 K 層的層色 = lerp(使用者足跡, 終點色, K / N)    N = 4
K ≥ N 時固定為終點色
```

以 catppuccin-mocha 代入（Lavender → Sapphire）：

| 層 | 1 | 2 | 3 | 4+ |
|---|---|---|---|---|
| 層色 | `#A4C0FA` | `#94C3F5` | `#84C5F0` | `#74c7ec` |

## 淡化（Rules F8、T2）

改寫已經畫好的畫面裡每一個顏色碼（SGR），不動文字與版面：

```
dim(c) = c × 0.45 + base × 0.55        base = #1e1e2e
```

- 前景與背景都照這個算；16 色、256 色先換成 RGB 再算。
- **淡化絕不讓顏色變亮**：每個通道取原值與淡化值較小的那個 —— 比 base 還暗的顏色（例：`#000000`）淡化後會變亮，那就維持原色。
- 輸出一律是 24-bit（`38;2;…` / `48;2;…`）：家族要求 truecolor terminal（Rules E4），淡化不必照色彩深度降階。
- 沒有指定前景的文字，給淡化後的預設字色（`dim(Text #cdd6f4)`）。
- bold、reverse、游標移動、文字本身不動。
- **對畫好的畫面淡化一次**：已經淡過的（失焦的 panel）在 popup 底下會再暗一點，看得出 popup 打開前 focus 在哪（F8）。

> **實作參考（不是規定）**：filu 的 `internal/ui/dim.go`。

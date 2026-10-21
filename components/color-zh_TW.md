# color（配色）

**Language**: [English](color.md) · 繁體中文

一整套配色的**呈現規則 + 色碼 + 計算方式**，全家族照用。意義要不要同時用顏色以外的方式（框線、符號）表達，由 app
決定 —— rules 另有規定的除外（例：focus 不能只靠顏色，L5）。內容本身的顏色（檔案類型、pod 狀態、log 等級、語法上色）
由 app 決定；這裡管的是 tdp 定的介面元素（Principle P4）。

## 呈現規則

1. **最少錨點，其餘推導**：先選三個錨點 —— 底色、使用者足跡、popup 的終點色 —— 其餘層次從錨點推導，不為每個元素各挑顏色。
2. **層色是 z 軸**：popup 的框與標題用層色（error popup 用 Red，見 [`dialog/note`](dialog/note-zh_TW.md)）。起點是使用者足跡
   （Lavender），終點是 Sapphire，中間分 N = 4 段；第 K 層取第 K 段，第 N 層以上固定是終點色。最底下的 popup 是第 1 層；toast 不算
   一層，一律用第 1 層的顏色（Rules F1）。
3. **顏色專職**：每個意義佔一個顏色，其他意義不用同一個（Principle P4）。例：「使用者足跡」用了 Lavender，popup 的框就不用
   Lavender —— 層色的起點是它，但第 1 層已經往終點走了一段。
4. **警示色不跟層數換色**：錯誤、警告在哪一層都是同一個 Red、Peach；被蓋在底下時照 F8 一起淡化。
5. **亮的就是有 focus 的**（Principle P6）：最上層以外淡化（F8）、失焦的 panel 淡化（T2，串流內容除外）、同鍵兩處指示時
   會觸發的那個亮（M9）、沒有 focus 的那一塊上的 cursor 淡化。
6. **粗體只用在**：cursor 上的字、popup 的標題、選中的膠囊的字、模式名、popup 標題後面的 loading icon、splash 的名稱（Rules S5）、
   畫面比 app 的最低尺寸小時正中央的 app 名稱（Rules L1，[`layout/screen`](layout/screen-zh_TW.md)）。

## 色碼（catppuccin-mocha）

| 意義 | 用在 | 色 |
|---|---|---|
| 底色 | 不塗在畫面上；用在要明確寫出底色的地方：色塊上的字（cursor、膠囊） | Base `#1e1e2e` |
| 沒選中的膠囊 | 膠囊串裡沒選中的段與中間接縫的底（[`layout/panel`](layout/panel-zh_TW.md) 的膠囊串）；被蓋住淡化時剛好變成 Crust `#11111b` | Mantle `#181825` |
| focus | focus 的框（粗線 `┏━┓`）；hint、footer、key reference 裡現在按得了的鍵；有 focus 的 panel 的 label 與清單的表頭；畫面 chip 列 | Blue `#89b4fa` |
| 用不到 | 失焦的框（細線 `┌─┐`，跟粗線同寬，切換零位移）；停用的列、label、選項；checkbox 不可用的選項（只畫狀態，照樣能勾）；範圍外的日子 | Surface2 `#585b70` |
| 層色 | popup 的框（粗線 `┏━┓`）與標題膠囊的底；popup 裡的 cursor 色塊 | 見下面的「popup 的層色」 |
| 正在編輯、使用者足跡 | input popup 裡的值與游標；使用者留下的位置（panel 的位置列 —— 麵包屑，目前的路徑或 drill 到的層，見 [`layout/panel`](layout/panel-zh_TW.md)；statusbar 上「你現在在哪」的值） | Lavender `#b4befe` |
| 生效中 | 目前生效的值（select 選的、勾著的、開著的；popup 裡跟著畫面上的勾，讀成「按 `Enter` 就是這個值」）；活著的 session；進行中的工作與進度條（單畫面的 app 寫在工作的列裡，見 [`layout/screen`](layout/screen-zh_TW.md)）；成功完成的（Success toast 的字） | Green `#a6e3a1` |
| 模式 | 模式的外框與模式名、模式裡選起來的範圍、Drag 拿著的那一列（Rules K11） | Yellow `#f9e2af` |
| 警告：值得注意、但沒壞 | confirm 裡警告的那一句；Warning toast 的字 | Peach `#fab387` |
| 錯誤 | 錯誤列、出錯的 label、error popup、Error toast 的字、畫成名字的控制字元（`\n`、`\x1b`……，[components](README-zh_TW.md) 的「控制字元」；游標停在上面時是它的底，字 Base） | Red `#f38ba8` |
| 暗字 | menu 的說明與區塊標題；一列一個值的 panel 的表頭；hint、footer 的冒號與說明，以及隔開幾個鍵的 `\|`（`j\|k`）；說明列；灰字提議；空值的說明；沒有 focus 的打字列；空狀態；畫面比最低尺寸小時名稱下面的提示；分隔線（popup 裡的、畫面 chip 列下面的） | Overlay0 `#6c7086` |
| 一般文字 | 表單與 panel 上的值；menu 的 label；key reference 的說明 | Text `#cdd6f4` |
| panel 的 cursor | panel 上 cursor 所在那一列的底，字是 Base 粗體 | Subtext1 `#bac2de` |
| 按鈕 | 沒有 focus 的按鈕的底，字是 Text | Surface1 `#45475a` |

- **cursor 色塊**：popup 裡是層色底、panel 上是 Subtext1 底，字都是 Base 粗體；沒有 focus 的那一塊上的 cursor，是有 focus 時的
  cursor 再淡化一次（P6）。
- **文字裡的搜尋**（例：viewer 的 `/`）不加新顏色：每一個命中的字加底線、保留原本的顏色；目前那一筆畫成 cursor 色塊，意思是
  「你在這裡」。模式的 Yellow 只留給選取的範圍，搜尋不用它。
- 字要放在 cursor 色塊上時，一律換成 Base；原本的顏色不保留。**例外是色塊**：內容本身就是顏色的格子（表單、panel 上顏色值的
  `███`，kamonu 畫 mark 的格子）保留自己的顏色，同一塊上的其他字照樣換成 Base。顏色就是那一格的值，正要改它的時候最需要
  看到它。
- **畫面不塗底色**：沒有指定背景的格子留給終端機自己的底色。終端機的底不是 Base 時，淡化照樣往固定的 `#0c0c13` 靠，
  不是往終端機的底；家族配色照深色底設計，深色終端機上差很小。

**為什麼**：不蓋掉使用者的終端機主題、透明背景與背景圖；家族的 app 本來就都不塗底色，改用共用的 lib 時畫面不會變。

## popup 的層色

```
第 K 層的層色 = lerp(使用者足跡, 終點色, K / N)    N = 4
K ≥ N 時固定為終點色
```

每個通道四捨五入（.5 進位），跟淡化一樣。

以 catppuccin-mocha 代入（Lavender → Sapphire）：

| 層 | 1 | 2 | 3 | 4+ |
|---|---|---|---|---|
| 層色 | `#A4C0FA` | `#94C3F5` | `#84C5F1` | `#74c7ec` |

- **在收的 popup 不算進 K**：開始收起時它已經不是最上層（[`layout/popup`](layout/popup-zh_TW.md) 的開關動畫）。target 打開、source
  同時收起時（Rules T1），target 從第一格就用它最後所在那一層的層色，source 收完時不跳色。

## 淡化（Rules F8、T2）

改寫已經畫好的畫面裡每一個顏色碼（SGR），不動文字與版面：

```
dim(c) = c × 0.45 + t × 0.55        t = #0c0c13
```

- **t 是 Crust 的下一格**：catppuccin-mocha 的 Base、Mantle、Crust 是同一個色相，亮度每格少 3%（15%、12%、9%），t 是往下
  推一格的 6%。catppuccin 沒有這一色；它不畫在畫面上，只用在這個公式。
- 前景與背景都照這個算；16 色、256 色先換成 RGB 再算：256 色的 16–255 照標準值；0–15（16 色）用終端機的調色盤 —— 啟動時用
  OSC 4 問（跟 Rules E5 的 icon 寬度探測同一個時間點），問不到就用 xterm 的預設值。
- **每個通道四捨五入**（.5 進位），再跟原值比。
- **淡化絕不讓顏色變亮**：每個通道取原值與淡化值較小的那個 —— 比 t 還暗的顏色（例：`#000000`）淡化後會變亮，那就維持原色。
- 輸出一律是 24-bit（`38;2;…` / `48;2;…`）：家族要求 truecolor terminal（Rules E4），淡化不必照色彩深度降階。
- 沒有指定前景的文字，給淡化後的預設字色（`dim(Text #cdd6f4)`）。
- bold、reverse、游標移動、文字本身不動。
- **對畫好的畫面淡化一次**：已經淡過的（失焦的 panel）在 popup 底下會再暗一點，看得出 popup 打開前 focus 在哪（F8）。

**為什麼**：16 色的實際顏色由使用者的調色盤決定；照 xterm 的值淡化，調色盤不是 xterm 時色相會跳 —— 例：調色盤把 16 色的藍設成
`#89b4fa` 時，照 xterm 的 `(0,0,238)` 淡化是飽和的深藍 `(0,0,118)`，照實際的顏色是灰藍 `(68,88,123)`，違背「同一個顏色只是
變淡」。問不到時用 xterm，跟家族的 app 現在的做法一樣。目標是 t 而不是 Base：比 Base 暗的顏色淡化後也會變暗 —— 膠囊串沒選中的段
是 Mantle，淡化剛好變成 Crust，被蓋住的那一層整串退到後面；往 Base 靠時，它們淡化後一點都不變。

> **實作參考（不是規定）**：filu 的 `internal/ui/dim.go`（xterm 的 16 色在這裡）。問調色盤：16 個 `ESC ] 4 ; n ; ? ESC \`（n = 0–15）
> 一起送，後面接一個 DA1（`ESC [ c`）；終端機照順序回答 `ESC ] 4 ; n ; rgb:RRRR/GGGG/BBBB`（每個通道取高 8 位），收到 DA1 的
> 回答時還沒回的顏色就是問不到 —— 不支援 OSC 4 的終端機照樣回 DA1，不用等逾時。DA1 也沒回時，整體逾時（例：200ms）後全部
> 用 xterm 的值。

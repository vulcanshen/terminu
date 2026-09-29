# tdp Family defaults

**Language**: [English](defaults.md) · 繁體中文

terminu family 的 app 實際收斂出來的具體值與慣例。**照用最省事**：新 app 直接套用，
就跟家族其他成員長得一樣、用起來一樣。**偏離不算違規**，也不需要寫理由 —— 只要
仍然符合 [Rules](rules-zh_TW.md)。

引用方式：`tdp D3` 等。

---

## D1 版面與 chrome

- **footer 一列**，內容固定為：

  ```
  Space:menu ?:help Tab/1–N:panels q:quit
  ```

  寫法照 Rules M5 的 hint；寬度不夠時從尾端整組捨棄；鍵 Blue、冒號與說明 Overlay0（D2）。
- **panel 膠囊**：每個 panel 的上框有 `[N] label` 膠囊（powerline 圓角），`N` 同時是
  直接跳到該 panel 的數字鍵。
- **多畫面的 app**：上方一列畫面 chip（`[W]eb ╱ [B]ookmarks …`），下方一條全寬分隔線，
  長時間工作時兼當進度條。
- **窄寬門檻**：寬度 < 72 欄（側欄較窄的 app 用 60 欄）時只畫 focus 那一側。
- **空狀態**：置中寫一句事實，加上一句點名按鍵的提示（例如「沒有 host —— 按 `[A]` 或 `[Space]`」）。

## D2 色彩系統

一整套配色的**呈現規則 + 計算方式 + 色碼**。不想處理配色的 app 整套照用；要自訂的 app
自己決定用哪些、不用哪些。意義要不要同時用顏色以外的方式（框線、符號）表達，也由 app 決定。

**呈現規則**

1. **最少錨點，其餘推導**：先選三個錨點 —— 底色、使用者足跡、popup 最上層 —— 其餘層次
   從錨點推導，不為每個元素各挑顏色。
2. **明度是 z 軸，不反轉**：從底色到最上層的 popup，明度單向遞進，越上層越亮。TUI 沒有
   陰影與高度，明度是唯一能表達「哪個在上面」的工具。
3. **明度帶專職**：每個意義佔一條明度帶，其他意義不用同一條（Principle P4）。例：
   「使用者足跡」用了 lavender，popup 邊框就不用 lavender。
4. **警示色不參與 z 軸**：錯誤、警告色在任何一層都是同一個顏色，不跟著層級變亮變暗。
5. **同鍵兩處指示**（Rules M9）：會觸發的那個亮、不會的那個暗。
6. **失焦只換邊框**：非 focus 的 panel 只換邊框色與框線，內容不變暗。

**計算方式：dim（Rules F8）**

改寫已經畫好的畫面裡每一個顏色碼（SGR），不動文字與版面：

```
dim(c) = c × 0.45 + base × 0.55        base = #1e1e2e
```

- 前景與背景都照這個算；16 色、256 色先換成 RGB 再算。
- **淡化絕不讓顏色變亮**：每個通道取原值與淡化值較小的那個 —— 比 base 還暗的顏色（例：`#000000`）淡化後會變亮，那就維持原色。
- 輸出一律是 24-bit（`38;2;…` / `48;2;…`）：家族要求 truecolor terminal（D6），dim 不必照色彩深度降階。
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
| 選取；模式（外框與右上角的模式名，Rules K11） | Yellow `#f9e2af` |
| 暗字；hint 與 footer 的冒號與說明 | Overlay0 `#6c7086` |
| hint、footer、key reference 裡的鍵 | Blue `#89b4fa` |
| key reference 的說明 | Text `#cdd6f4` |
| 失焦 panel 邊框上的 hint：鍵 / 冒號與說明 | Overlay0 `#6c7086` / Surface2 `#585b70`（Blue 是 focus 的顏色，只給拿鍵的地方） |

## D3 Popup

- 一個 popup 一個檔、一個 animator。
- 標題放在上框：glyph + 文字；hint 嵌在下框；內容上下各留一列空白。
- 動畫（Rules F2）：8 格 × 16ms ≈ 128ms，開啟與關閉對稱。
- **loading icon**（Rules F7；出自 webu 載入網址時的 icon）：
  - 字形：Nerd Font `nf-md-circle_slice_1` 到 `_8`（U+F0A9E–U+F0AA5）八格，一個圓一片一片填滿，滿了再從頭。
  - 速度：一格 90ms，一圈 720ms。
  - 哪一格由時鐘決定：`frames[(now / 90ms) % 8]`，不是計數；tick 只在有東西 loading 時續排。
  - 寬度：一格；跟它取代的靜止 glyph 同寬，換上換下不位移（braille 點字的形狀與寬度不合，不用）。
  - 顏色：跟旁邊的字同色；放在 popup 標題後面時用該層的層色（bold）。
- toast：顯示 2200ms，固定在畫面底部。
- `Esc` 只在一個地方處理（`closeTop`）。
- 離開的 confirm 用自己的 popup，疊在整疊最上面：`Ctrl-C` 可能在另一個 confirm 開著時按下，借用同一個會蓋掉使用者正在回答的問題。
- 「放在最上層」要同時改三處：按鍵路由、`closeTop`、繪製順序。
- `?` 的 key reference 疊在其他 popup 上時，按鍵路由與繪製都把它放在最上層；confirm、options 等框排在底下的 menu 之前拿鍵。
- 判斷一層「還在不在」用開啟中或已開（`owns()`），不用含關閉中的 `isActive()`（Rules F3）。
- confirm 的下框 hint：`Enter:<動詞> Esc:cancel`（例：`Enter:delete Esc:cancel`）。
- 下框 hint 放不下時，從尾端整組捨棄（跟 D1 的 footer 一樣），不截在項目中間。
- **finder 的 focus**（Rules F1）：打字時篩選列亮、清單的 cursor 列是淡的反白；`Tab` 到清單後，篩選列整列用灰色
  （Overlay0，D2 的暗字）畫，不用 F8 的淡化、也不畫反白與游標，清單的 cursor 列換成 popup 層色底加深色粗體字
  （跟 menu 的 cursor 列一樣）。只有拿鍵的那一邊是亮的，跟 F8「只有最上層亮」同一套語言（kbu `40a0573`）。
- **模式名的標籤**（Rules K11）：接頭跟框同色、線型跟著框 —— 雙線框用 `╡` `╞`，單線框用 `┤` `├`；模式名用模式色加粗；
  盡量一個詞（`Drag`、`Visual`、`Select`：窄的 panel 放不下兩個詞，右上角的字會整個被丟掉）；放不下時先截標題，模式名
  留著。panel 的 `[N] label` 膠囊跟著外框換成模式色（kbu `248f883`）。
- 取消回到 source；完成動作清掉整個 stack（T1 的常見答案）。

## D4 Menu

- menu 列：` [k]label` 左對齊，說明靠右、暗色。
- 熱鍵字母是 label 的第一個字母就原地加括號（`[r]ename`），在字中間就原地包（`UR[L]`），
  否則放前面（`[n] New`）。core key 直接寫進 label：`[Enter] Edit`。
- menu 內：`j/k` 移動（頭尾相接），`Enter` 執行，熱鍵直接執行；下框 hint
  `j/k:move Enter:run Esc:close`。
- menu 標題是 focus panel 的 `[N] label`。
- popup 寬度統一照 Rules F7；說明太長時在框裡換行或截尾，不為了它加寬框。
- label 本身已經寫出鍵的列（`[/] Search`）不要再括一次。

## D5 熱鍵參考

**tdp 不規定熱鍵**（[Principle P5](README-zh_TW.md#p5-固定區與概念區)），這裡只記錄家族目前的做法，
新 app 想省事可以照用：

| 鍵 | 慣例 |
|---|---|
| `j` `k` / `↑` `↓` | 上下移動；有 cursor 的清單頭尾相接 |
| `u` `d` / `Ctrl-U` `Ctrl-D` | 半頁 |
| `gg` `G` | 到頂、到底 |
| `h` `l` | 切換 panel 內的 tab |
| `/` | 搜尋 |
| `1`–`9` | 直接跳到 `[N]` panel |
| `z` / `Z` | zoom |
| `Alt-Esc` | PTY 的出口鍵（Rules K10）；按了之後做什麼由 app 決定 |
| 選取文字的模式裡：`h/j/k/l`、`w/b/e`、`0/$`、`gg/G`、`u/d` | 照 vim 移動：一格、一個字（`w` 下一個字頭、`b` 上一個字頭、`e` 字尾）、行首行尾、頭尾、半頁 |

- **離開流程**（tdp K9）：有東西會遺失（進行中的傳輸、未存的草稿）時先 confirm。
- **導覽字母不綁動作**：`j k u d g G h l` 保留給移動，任何動作不佔用。
- **大小寫分層**：小寫作用在 item，大寫作用在 panel 或全域。
- **刪除用 `x`**（`d` 是半頁）。
- **`Alt-Esc` 一律先 confirm**：按了會讓 focus 離開 PTY 或結束子程序時，不論子程序留不留著，都先跳 confirm（`Enter` 離開、
  `Esc` 回到 PTY）；在 PTY 裡面的動作（例：退一階 zoom）不用問。理由：終端機把 Alt 組合送成「`Esc` 加那個鍵」，`Alt-Esc`
  跟兩次 `Esc` 的 byte 一模一樣。app 忙的時候，讀鍵的一端卡住，兩次 `Esc` 就會疊在一起被讀成 `Alt-Esc`（2026-09-29 用
  bubbletea v1.3.10 實測：前面有鍵在排隊時，間隔 150ms 的兩次 `Esc` 也會黏在一起）。vim 裡連按 `Esc` 很常見，confirm 讓
  誤觸的人按 `Esc` 回到 PTY。
- **其他 Alt 組合的出口鍵**（例：kbu 的 `Alt-t` 隱藏 Alterm、sshu 鎖住的格子的 `Alt-Enter`）同樣會被「`Esc` 再按那個鍵」
  拼出來；要不要 confirm 由 app 決定。

## D6 發布與環境

- 單一靜態 binary，goreleaser 建置；`install.sh` / `uninstall.sh`（`curl | sh`、免 sudo），
  另發到 Homebrew tap `vulcanshen/homebrew-tap`。
- 設定在 `$XDG_CONFIG_HOME/<app>`（fallback `~/.config/<app>`）；資料在 `~/.<app>/`。
- **環境變數的命名**：`<大寫 app 名>__<變數名>` —— app 名後面兩個底線，變數名全大寫、單字之間一個底線（例：`FILU__ICON_WIDTH`、
  `KBU__ALTERM_LOGIN_SHELL`）。app 自己讀的變數（含測試用、傳給自己子程序的）都照這個寫。共用的名字：

  | 變數 | 意思 |
  |---|---|
  | `<APP>__CONFIG` | 設定**目錄**（設定檔在裡面） |
  | `<APP>__STATE` | 狀態目錄（app 有另外存狀態時） |
  | `<APP>__DATA` | 資料目錄 |
  | `<APP>__CACHE` | 快取目錄 |
  | `<APP>__ICON_WIDTH` | icon 佔幾格的手動覆寫（見下方 icon 的實際寬度） |
  | `TERMINU__ICON_WIDTH` | 家族共用：有 PTY 的 app 設給子程序，告訴它 icon 佔幾格（見下方） |

  例外：給別的程式讀的變數照對方的要求（例：sshu 經 ssh 帶到遠端的 `LC_SSHU_COLORTERM` —— OpenSSH 預設只轉送 `LANG` 與
  `LC_*`）。改名時不留舊名。
- 需要 Nerd Font；PUA glyph 在程式碼裡寫成 code point。
- 需要 truecolor terminal（24-bit 色）：catppuccin 的淡色與 D2 的層色漸變在 256 色下分不出來，dim 也一律輸出 24-bit（D2）。README 的需求段跟 Nerd Font 並列寫明。
- 跨尺寸的畫面測試：多種終端機尺寸下，每一列都剛好等於終端機寬度（Rules L4）。
- **icon 的實際寬度**：有些字型讓 icon 佔兩格（游標前進兩格），lipgloss 卻量成一格，框線就歪。要量的是**游標實際前進幾格**：
  icon 看起來比一格寬、但游標只前進一格的字型（glyph 溢出到隔壁），照一格算。app 啟動時探測（CPR：印一個 icon、問游標位置），
  所有量寬度的地方（補空白、截斷、置中、並排、框線、疊 popup）都走同一個顯示寬度函式；L4 的畫面測試也跑一次「icon 佔兩格」，
  每一種 popup 各開一次，量單獨的框與疊上去的整個畫面。
  - 參考實作：filu `internal/ui/width.go` —— `isWideIcon()`、`dispWidth()`、`dispClip()`、`padDisp()`、`dispCutLeft()`、
    `compositeDisp()`（取代 overlay 的 `Composite`，介面相同）、`centerDisp()`（取代 `lipgloss.Place`）、`joinH()` / `joinV()`
    （取代 `lipgloss.JoinHorizontal` / `JoinVertical`）；探測在 `iconwidth_unix.go` 的 `DetectIconWidth()`，在 `tea.NewProgram`
    之前呼叫；測試照 `d6_test.go`。
  - 手動覆寫：環境變數 `<APP>__ICON_WIDTH`（filu 是 `FILU__ICON_WIDTH`）。探測只在 unix 做；Windows 預設一格，靠環境變數覆寫。
  - **在別的 app 的 PTY 裡**：探測由外層 app 的終端模擬器回答，它把 icon 當一格，量不到真的寬度。所以有 PTY 的 app 開子程序時，
    在子程序的環境設 `TERMINU__ICON_WIDTH=<自己用的格數>`；每個 app 取 icon 寬度的順序是 `<APP>__ICON_WIDTH` → `TERMINU__ICON_WIDTH`
    → 探測。這樣家族裡任何一個 app 跑在另一個的 PTY 裡都對（filu 在 kbu 的 Alterm 裡、kbu 在 filu 的 shell 裡）。環境變數過不了
    ssh，遠端巢狀要靠 app 自己的通道（sshu 的巢狀指令通道）。
  - 疊 popup 時 popup 可能比畫面寬或高（調整終端機大小的那一格還是舊尺寸）：起點取 0、超出畫面的部分切掉，**不可以 panic**；
    寬、高兩邊都比畫面大時也一樣切，不可以把整個框原樣交出去。測試的邊界要含這三種情況（filu 的 `TestD6CompositeDispOversized`）。
  - 做完的驗收：`internal/ui` 裡除了寬度函式本身，找不到 `lipgloss.Width`、`lipgloss.Size`、`lipgloss.Place`、
    `ansi.StringWidth`、`ansi.Truncate` 的呼叫。
- `docs/icon.svg` 是家族 mark；splash（Rules S 章）由它逐格畫出，用測試守住兩者一致。
- `V` 保留給 splash（Rules S1）。
- demo gif 用 VHS 錄，腳本放在 `.local/demos/`；README 只放一張代表性的 gif。

## D7 文件

**README**：`README.md`（英文）與 `README-zh_TW.md`（繁中）內容對齊，只寫使用者需要知道的：

1. 標題、badge、語言切換（`English · 繁體中文`）
2. 一句話定位 + 一段「它能做什麼」
3. **一張**代表性的 demo gif
4. 特色：使用者拿到什麼，不寫怎麼做到的
5. 安裝：前置需求、安裝方式、第一次啟動會發生什麼、移除
6. 快速開始
7. 使用方式與按鍵
8. 設定與資料存放位置
9. 限制（用使用者的語言寫）
10. 相關連結：CHANGELOG、`docs/dev-remarks.md`
11. terminu family：遵循 terminu design、列出家族其他成員
12. License

不寫死版本號的「現況」段 —— 版本交給 badge 與 CHANGELOG。

**`docs/dev-remarks.md`**（繁中）：開發者開發過程中要提醒自己、或 AI 協作時記下的決策。

```
# <app> 開發者備忘
前言（一句話 + 遵循 terminu design principle）
## 運作方式
## 設計決定（決定 + 理由）
## 已否決，不要重提
## 已知的牆與未做
## 偏離 tdp（哪一條、在哪裡、為什麼）
## 設計文件導讀
## 建置與開發
## 發布（含踩過的坑）
```

**`docs/<app>-terminu-fix.md`**：尚未符合 tdp 的地方，逐條待修（違反了哪一條、在哪裡、現況、該怎麼改）。

**其他設計文件**（`ui.md`、`ux.md`、`function.md`……）由各 app 自己決定要不要有、怎麼切，
tdp 不規定；dev-remarks 的「設計文件導讀」一節負責指路。不另外維護「逐條對照 tdp」的文件
—— 符合的不必記，偏離的寫在 dev-remarks，違反的寫在 fix.md。

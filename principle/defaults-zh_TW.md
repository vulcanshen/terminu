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
  space menu   ? help   tab/1-N panels   q quit
  ```

  寬度不夠時從尾端整組捨棄；key 用亮色、說明用暗色。
- **panel 膠囊**：每個 panel 的上框有 `[N] label` 膠囊（powerline 圓角），`N` 同時是
  直接跳到該 panel 的數字鍵。
- **多畫面的 app**：上方一列畫面 chip（`[W]eb ╱ [B]ookmarks …`），下方一條全寬分隔線，
  長時間工作時兼當進度條。
- **窄寬門檻**：寬度 < 72 欄（側欄較窄的 app 用 60 欄）時只畫 focus 那一側。
- **空狀態**：置中寫一句事實，加上一句點名按鍵的提示（例如「沒有 host —— 按 `[A]` 或 `Space`」）。

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
| 選取 | Yellow `#f9e2af` |
| 暗字、hint | Overlay0 `#6c7086` |

## D3 Popup

- 一個 popup 一個檔、一個 animator。
- 標題放在上框：glyph + 文字；hint 嵌在下框；內容上下各留一列空白。
- 動畫（Rules F2）：8 格 × 16ms ≈ 128ms，開啟與關閉對稱。
- toast：顯示 2200ms，固定在畫面底部。
- `Esc` 只在一個地方處理（`closeTop`）。
- confirm 的下框 hint：`Enter <動詞> · Esc cancel`。
- 取消回到 source；完成動作清掉整個 stack（T1 的常見答案）。

## D4 Menu

- menu 列：` [k]label` 左對齊，說明靠右、暗色。
- 熱鍵字母是 label 的第一個字母就原地加括號（`[r]ename`），在字中間就原地包（`UR[L]`），
  否則放前面（`[n] New`）。core key 直接寫進 label：`[Enter] Edit`。
- menu 內：`j/k` 移動（頭尾相接），`Enter` 執行，熱鍵直接執行；下框 hint
  `j/k move · Enter run · Esc close`。
- menu 標題是 focus panel 的 `[N] label`。

## D5 熱鍵參考

**tdp 不規定熱鍵**（[Principle P5](README-zh_TW.md#p5-固定區與概念區)），這裡只記錄家族目前的做法，
新 app 想省事可以照用：

| 鍵 | 慣例 |
|---|---|
| `j` `k` / `↑` `↓` | 上下移動；有 cursor 的清單頭尾相接 |
| `u` `d` / `Ctrl-u` `Ctrl-d` | 半頁 |
| `gg` `G` | 到頂、到底 |
| `h` `l` | 切換 panel 內的 tab |
| `/` | 搜尋 |
| `1`–`9` | 直接跳到 `[N]` panel |
| `V` | splash 彩蛋，啟動時不播，不列進 menu |
| `z` / `Z` | zoom |

- **離開流程**（tdp K9）：有東西會遺失（進行中的傳輸、未存的草稿）時先 confirm。
- **導覽字母不綁動作**：`j k u d g G h l` 保留給移動，任何動作不佔用。
- **大小寫分層**：小寫作用在 item，大寫作用在 panel 或全域。
- **刪除用 `x`**（`d` 是半頁）。

## D6 發布與環境

- 單一靜態 binary，goreleaser 建置；`install.sh` / `uninstall.sh`（`curl | sh`、免 sudo），
  另發到 Homebrew tap `vulcanshen/homebrew-tap`。
- 設定在 `$XDG_CONFIG_HOME/<app>`（fallback `~/.config/<app>`），可用 `<APP>_CONFIG` 覆寫；
  資料在 `~/.<app>/`。
- 需要 Nerd Font；PUA glyph 在程式碼裡寫成 code point。
- 跨尺寸的畫面測試：多種終端機尺寸下，每一列都剛好等於終端機寬度（Rules L4）。
- `docs/icon.svg` 是家族 mark；splash 由 icon 逐格畫出，有測試守住一致。
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

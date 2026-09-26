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

## D2 色彩（catppuccin-mocha）

| 用途 | 色 |
|---|---|
| 底色 | Base `#1e1e2e` |
| focus 邊框 | Blue `#89b4fa`，雙線 `╔═╗` |
| 非 focus 邊框 | Surface2 `#585b70`，圓角 `╭─╮`（跟雙線同寬，切換零位移） |
| popup 邊框 layer 1 → 4+ | `#A4C0FA` → `#94C3F5` → `#84C5F0` → Sapphire `#74c7ec` |
| 正在編輯的東西、使用者足跡 | Lavender `#b4befe`（**popup 邊框不用 lavender**） |
| 錯誤 | Red `#f38ba8` |
| 值得注意、但沒壞 | Peach `#fab387` |
| 選取 | Yellow `#f9e2af` |
| 暗字、hint | Overlay0 `#6c7086` |

- 非 focus 的 panel **只換邊框**，內容不變暗。

## D3 Popup

- 一個 popup 一個檔、一個 animator。
- 標題放在上框：glyph + 文字；hint 嵌在下框；內容上下各留一列空白。
- 動畫：8 格 × 16ms ≈ 128ms。
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

## D5 按鍵慣例

**這些是熱鍵，tdp 不規定**（[Principle P5](README-zh_TW.md#p5-固定區與概念區)），列在這裡是因為家族多數成員這樣做：

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
- `docs/icon.svg` 是家族 mark；splash 由 icon 逐格畫出，有測試守住一致。
- demo gif 用 VHS 錄，腳本放在 `.local/demos/`；README 只放一張代表性的 gif。

## D7 文件

- `README.md`（英文）與 `README-zh_TW.md`（繁中）內容對齊，只寫使用者需要知道的。
- `docs/dev-remarks.md`（繁中）：開發過程的決策、理由、已否決的做法、偏離 tdp 的地方、
  建置與發布。
- `docs/<app>-terminu-fix.md`：尚未符合 tdp 的地方，逐條待修。

# panel：panel 上的 input

**Language**: [English](panel.md) · 繁體中文

## 外框

panel 的框（2026-10-07 從 defaults D1、D3 搬來，從 defaults 升成規定）。邊框的顏色與線型照 [`color`](../color-zh_TW.md)
（focus 雙線、失焦圓角，Rules L5）；失焦時內容變暗，串流內容除外（Rules T2）。

- **`[N] label` 膠囊**：每個 panel 的上框有 `[N] label` 膠囊（powerline 圓角），`N` 同時是直接跳到該 panel 的數字鍵。
- **模式名的標籤**（Rules K11）：接頭跟框同色、線型跟著框 —— 雙線框用 `╡` `╞`，單線框用 `┤` `├`；模式名用模式色加粗；
  盡量一個詞（`Drag`、`Visual`、`Select`：窄的 panel 放不下兩個詞，右上角的字會整個被丟掉）；放不下時先截標題，模式名
  留著。panel 的 `[N] label` 膠囊跟著外框換成模式色（kbu `248f883`）。

## 一列一個值

設定畫面這種一列一個值的 panel（locku 的 preference、webu 的 Settings、webu 頁面上的欄位）。user 2026-10-07 定。

```
╔[2] preference═════════════════════════════════╗
║ Property                   Value              ║
║ PIN                        not set            ║
║ profile                    clock              ║
║ show_status                on                 ║
║ pin_prompt_timeout         30                 ║
╚═══════════════════════════════════════════════╝
```

- **照 [`dialog/form`](../dialog/form-zh_TW.md) 的規則**：focus 一個項目一個項目移動（`j`/`l`/`↓`/`→` 往後、`h`/`k`/`↑`/`←` 往前）；
  `Enter` 打開那個值的 input popup，radio、checkbox 在原地選；focus 用色塊；label 的顏色；一欄自己的錯在 input popup 裡擋。
- **不一樣的地方：沒有送出。** 每個值在 input popup 按 `Enter` 確定的那一刻就生效、就存；開關與 radio 在原地選的那一刻也是。
  所以沒有動作列、沒有 `Ctrl-S`，也沒有「改過了要先問」。locku 與 webu 現在就是這樣。
- **focus 色塊**（user 2026-10-07）：Subtext1 底、Base 粗體字；範圍跟表單一樣，從項目開頭到 panel 內的右緣（欄位從值開始、
  選項從那個選項開始）。這是家族在 panel 上已經在用的 cursor 顏色（locku 的設定畫面、webu 的頁面欄位與清單）；popup 裡用
  層色、panel 上用 Subtext1，同一個「cursor 在這裡」的畫法，底色跟著所在的地方換。
- **label 的顏色**（user 2026-10-07）：

  | label 的狀態 | 顏色 |
  |---|---|
  | 一般 | Blue（跟 focus 的雙線框同色） |
  | 停用 | Surface2 |
  | 它的值出錯 | Red，優先於其他顏色 |

  跟表單同一個道理：表單的 label 用層色，就是 popup 框的顏色。panel 失焦時整個內容照 Rules T2 變暗，Blue 也跟著暗下去，
  所以 Blue 只有在拿鍵的 panel 裡是亮的（[`color`](../color-zh_TW.md)「Blue 只給拿鍵的地方」）。經過：user 問「label 直接用 Blue 有什麼不適」；
  我原本提 Text（值也大多是 Text，會違反「label 與值一定不同色」），再提「focus Blue、失焦 Overlay0」，又發現那會違反
  defaults D2 第 6 條「失焦內容不變暗」（現在在 `color`）；user 指出失焦的 panel 本來就該變暗、只有 log 這類除外 —— 查了規則，原本是「app 決定、
  家族預設不變暗」，user 定為全家族一定要做（T2 與那一條已改），label 就一律 Blue。
- **`h`/`l`**：在一列一個值的 panel 裡照表單的 hjkl 移項目。照 rules K12：panel 沒有 tab 時是前後；放在有 tab 的 panel 裡，`h`/`l` 切 tab、`j`/`k` 移項目。

## 在 panel 裡直接打字的搜尋列

按 `/` 之後在 panel 最上面出現一列，打字的同時清單即時篩選，不開 popup（kbu 的 panel 搜尋、sshu 的 Hosts、webu 的清單篩選）。
user 2026-10-07 定。

```
╔[2] Hosts═════════════════════════════════════╗
║  prod                                  2 of 5║   ← 搜尋列
║ prod-web-01        deploy   10.0.3.14        ║
║ prod-db            postgres 10.0.3.20        ║
╚══════════════════════════════════════════════╝
```

搜尋列有兩種狀態：

- **打字中**：輸入態（K8），字母都是字元，清單即時篩選。
  - `↑`/`↓` 在符合的項目之間移 cursor（方向鍵打不出字，不衝突）。
  - `Enter`：結束打字、篩選留著，**focus 到 cursor 那一項，不執行它**；要執行，再按一次 `Enter`（user 2026-10-07 改：原本
    定的是 `Enter` 順便做那一項的動作，那樣從打字回到清單的唯一出路會順手打開東西）。沒有符合的項目時 `Enter` 等於 `Esc`。
  - `Esc`：清掉篩選、結束打字。
  - `Tab`：結束打字、篩選留著，focus 照 K2 移到下一個 panel（打字時 `Tab` 也是換 panel，不會被困在搜尋列）。
- **篩選留著**：panel 照常操作，清單是篩選過的；`j`/`k`、熱鍵、`Enter` 恢復原本的作用。搜尋列留在畫面上，用灰色畫
  （Overlay0，跟 finder 沒拿鍵的那一側一樣）。`Esc` 清掉篩選；`/` 再進入打字。

focus 離開與回來（user 2026-10-07 定）：

- **focus 離開 panel 時篩選留著**，往哪個方向離開都一樣：篩選是這個 panel 目前的樣子，到別的 panel 看一眼回來不該不見。
- **focus 回到有搜尋列的 panel 時，直接是打字中**，不用再按 `/`（user；sshu 的做法）。要操作篩選過的清單，按 `Enter`
  focus 到那一項。
- **篩選留著時按 `/`**：接著舊的字打，游標在尾端；要從頭開始，先 `Esc` 清掉再按 `/`。

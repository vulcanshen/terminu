# VTP — terminu design principle 的前身

這個目錄是**歷史紀錄**、不是現行規範。現行規範是 [terminu design principle（tdp）](../principle/)。

tdp 不是憑空寫出來的：它先在 kbu 裡長成一份 design guide、抽出來成為跨 app
的 interface、改名兩次、被五個 app 實作過、最後才落地成一組可以驗證的 rules。
這裡保存那段過程，讓每一條 rule 的來歷都查得到。

| 檔案 | 內容 |
|---|---|
| [`vtp-final.md`](vtp-final.md) | VTP 最後一版原文（thoughts repo `e3c57d7`、2026-09-21）、原樣保存、未去個人化 |
| [`vtp-score-readme.md`](vtp-score-readme.md) | VTP score 時期的總覽（thoughts repo `3eb1b7f`、2026-09-01）、score 模型後來被整個拿掉 |

---

## 時間線

### 2026-06 — kbu 裡的 design guide（ZLC）

kbu（當時叫 km8）開發到 v1.7.x、popup 慣例改到第二版、開始把教訓寫成 design
guide。目標叫 **ZLC — Zero Learning Curve**：使用者不看文件就能用。

- 2026-06-27 popup convention v2：一個 popup 一個 animator、title = glyph + 文字、
  上下留白、hint 嵌下框
- 2026-06-29 把 v1.7.6 的教訓寫成 §2.6（panel-aware 視覺消歧）、§4.4（熱鍵標記）、
  §6.6.1（主要意圖提前）
- 2026-06-30 guide 拆成兩半：**通用 interface** 與 **km8 implementation**。
  「原則」與「某個 app 怎麼做」從這天開始分家

### 2026-07-27 — 抽出到 thoughts repo

filu 要開工、原則不該只屬於 kbu。`tui-design-principle.md` 搬到獨立的
thoughts repo、拿掉 ZLC 品牌、kbu 與 filu 對稱地引用它。

### 2026-09-01 — 改名 VTP、加上 score

ZLC 改名 **VTP**（當時全名帶作者名字）。文件加上一個量化模型：

```
VTP score = X × min(1, 5/Y) × 100%
X = 可從 core-key 入口直接執行的操作數 ÷ app 全部操作數
Y = core-key role 數量（≤ 5 不扣分）
```

並附上 kbu / nano / vim / vim + which-key 的比較表。vim + which-key 的案例留了
下來：揭露 layer 可以疊在 app core 上、跟 app core 分離。

### 2026-09-10 — 拿掉 score、規定 core-key 語意

三個實作（kbu、filu、sshu）之後、score 被整個拿掉：數字本身沒有指導設計、
它真正主張的事改寫成定性規則 ——「揭露是唯一機制、揭露的必須是可執行的動作
清單、不是文件」。

- core-key 從「不超過 5 個」改成「`Tab` / `Enter` / `Esc` / `Space` / `?` 的
  語意固定」
- Space menu 被規格化：toggle、item / panel 兩區、`[]` 熱鍵標記、名稱 + 說明
- 文件改名「My TUI Design Principle」、三個 app 改稱「this TUI Design Principle」
- 同日新增 §4.5「輸入態屏蔽熱鍵」（`Space` 與 `?` 是可列印字元）、§3 符號語彙
  改為「明確劃出去、不含規範」

### 2026-09-21 — Enter 放寬

`Enter` 從「確認 / 進入」放寬為「對 focus 項目最直觀的操作、由 app context 定義」
—— 開檔、連線、送出表單都是 `Enter`、沒有一個字面上是「確認」。

### 2026-09-26 — 落地成 terminu design principle

五個 app（kbu、filu、sshu、webu、locku）都照 VTP 做過一遍之後、做了這次整理：

- **名稱**：去個人化、改名 **terminu design**（總覽）與 **terminu design principle、
  tdp**（細節）。兩者分開、類似 Material Design 與它的 guidelines。thoughts repo 與
  這些專案的關係退場、VTP 只以本目錄的形式保留
- **家族**：「u-family」改稱 **terminu family**
- **結構**：VTP 一份文件同時寫精神與規則；tdp 拆成三層 ——
  **Principle**（精神、為什麼）、**Rules**（必須遵守、每條附理由、可在寫明原因下偏離）、
  **Family defaults**（家族共用的具體值、照用即可、偏離不算違規）
- **從「介面式描述」落地成 rule**：VTP 多數條文只說「要滿足什麼」、把怎麼滿足交給各
  app。五個實作收斂出來的做法、能驗證的升成 rule（例：`Esc` 永不離開 app、
  menu 區塊名稱固定、每一列等於終端機寬度）、屬於具體數值的放進 defaults
- **新增 global operation**：VTP 的 §A.2 定義了 non-contextual track、但五個 app 沒有
  一個把全域動作做成可執行清單 —— `?` 都只是說明頁、全域動作混在 panel operation
  裡。tdp 把操作範圍定成三種（item / panel / global）、`?` 必須有可執行的 global
  operation 區、Space menu 也加上第三區 global operation
- **明確不定義 letter hotkey**：哪個字母做什麼（刪除用 `D` 還是 `x`、大小寫怎麼
  分層）交給各 app。VTP §A.0.B 已經說 hotkey ergonomics 不在範圍、tdp 把這條
  貫徹到底、並寫明原因
- **VTP score、`Y ≤ 5`、「My」字樣** 不再出現

---

## VTP 條目 → tdp 對照

各 app 的設計文件與程式碼註解原本引用 VTP 的 § 編號，改引用 tdp 時照這張表換：

| VTP | tdp | VTP | tdp |
|---|---|---|---|
| §0 Meta | P0 | §2.4 Override 色 | D2 |
| 術語定義 | Principle 術語 | §2.5 layer 插值 | D2 |
| §A VTP 核心 | P1、P3 | §2.6 panel-aware 消歧 | M9 |
| §A.0 揭露 | P2 | §3 符號語彙 | P5 |
| §A.0.L 可疊加 layer | （移除） | §4.1 core key | K1 |
| §A.0.B 範圍邊界 | P5 | §4.2 letter hotkey ⊆ 入口 | M3 |
| §A.0.K core-key 語意 | K1、K7 | §4.3 `Esc` 通殺 | K4、F3 |
| §A.1 Space 入口 | K5、M1、M2 | §4.4 熱鍵標記 | M5 |
| §A.1.1 menu 分區 | M2 | §4.5 輸入態屏蔽 | K8 |
| §A.1.2 `[]` 標記 | M5 | §5.1 / §5.2 Mouse | X1 / X2 |
| §A.1.3 名稱 + 說明、完整性 | M5、M3 | §6.1 浮層分類 | F1 |
| §A.2 `?` 入口 | K6、M1、M4 | §6.2 動畫 | F2 |
| 入口不能沒回應 | M7 | §6.3 border 色 | D2 |
| §B 元素專職化 | P4 | §6.4 保留 source | F4 |
| §1.1 窄寬可用 | L1 | §6.5 auto-dismiss 也算 | F3 |
| §1.2 Width stability | L2 | §6.6 menu cursor-first | M2、M8 |
| §1.3 footer 行數固定 | L3 | §6.7 錯誤呈現 | F5 |
| §2.1 最少錨點 | D2 | §7.1 source 是否仍有意義 | T1 |
| §2.2 明度 z 軸 | D2 | §7.2 streaming 不退階 | T2 |
| §2.3 顏色帶專職 | D2 | 結語 | （移除） |

tdp 相對 VTP 的主要變動：

- **新增**：`global operation`（P3、M2 第三區、M4 可執行區）、K2 `Tab` 在同層物件間切換、
  K3 `Enter` 在 input popup 裡 submit 並驗證、K9 `q` 成為 core key 並與 `Ctrl-C` 同義、
  K10 PTY、M6 暫不可執行的列變暗、L1 最低 80×40、L4 每列等於終端機寬度、L5 focus 不位移、
  F6 confirm
- **收窄**：K5 `Space` 只在 panel 上開關 Space menu、在其他 popup 上不作用；K6 `?` 在 popup 上
  只顯示該 popup 的 help；F2 動畫必須有、長度不規定
- **移到 defaults**：整個色彩章（D2）
- **移除**：VTP 與外部工具（vim、which-key、nano）的比較、可疊加 layer 論證、結語
- **新結構**：每條 rule 分 `固定` 與 `概念`；defaults 是通用預設建議，不照用不算違規

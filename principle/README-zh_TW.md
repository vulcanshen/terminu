# terminu design principle（tdp）

**Language**: [English](README.md) · 繁體中文

tdp 是 [terminu design](../README-zh_TW.md) 的細節規範，分三層：

| 層 | 文件 | 性質 |
|---|---|---|
| **Principle** | 本文件 | 精神：要達成什麼、為什麼 |
| **Rules** | [rules-zh_TW.md](rules-zh_TW.md) | 必須遵守，每條附理由；分固定區與概念區（P5） |
| **Family defaults** | [defaults-zh_TW.md](defaults-zh_TW.md) | 通用預設建議：terminu family 共用的具體值、配色系統與慣例。照用最省事，不照用不算違規 |

tdp 回答一個問題：**在 terminal UI 上，什麼樣的設計能讓使用者不看文件就能用？**

---

## P0 規則服務 UX，不是反過來

tdp 是過去 UX 決策的結晶，不是未來 UX 的枷鎖。**規則跟它原本要服務的 UX
衝突時，UX 贏，規則該擴充，而不是把 UX 壓掉。**

判斷一條規則該堅持還是該擴充：

1. **回想規則的 origin UX**：它當初要解決什麼使用者面對的問題？
2. **檢查眼前的衝突**：那個問題在這裡還存在嗎？還是兩個不同目標剛好落在同一個畫面上？
3. **不適用就擴充**：寫下例外與理由，而不是削掉 UX。

反向也要警覺：新情境剛好符合既有規則時，問一句「**這次合規是真的 UX 對齊，還是
僥倖？**」規則是縮短推導距離的捷徑，不是推導的替代品。

## P1 不看文件就能用

使用者**不需要讀文件、不需要事先記熱鍵**，靠一組**跨畫面、跨 app 意義不變的
core key**，就能用完整個 app。學一次，走遍整個 app，換到家族裡另一個 app 也不必重學。

## P2 揭露是唯一的機制

做到 P1 的方法只有一個：**把使用者能做的事揭露出來，讓他不用事先學就找得到。**
兩件事同時成立才算做到：

| | 問題 | 沒做到的後果 |
|---|---|---|
| **入口被揭露** | 使用者知不知道有這個鍵可以按？ | 入口等於不存在 |
| **動作被列全** | 按下去之後，能做的事是不是全在裡面？ | 沒列的動作只能靠事先學 |

**看得到不等於揭露。** 揭露的必須是**可直接執行的動作清單**，不是文件：

| 形式 | 從看到到執行 | 算揭露 |
|---|---|---|
| 互動 menu（`j/k` 選、`Enter` 執行） | 1 步 | ✓ |
| 常駐提示（footer 上看到鍵、立刻按） | 1 步 | ✓ |
| 說明文字（讀 → 找 → 記 → 打） | 多步、要記憶 | ✗ |

把說明文件搬進 app 裡，不會讓它變成揭露 —— 使用者仍然在讀文件。

唯一刻意不揭露的是家族彩蛋 splash（Rules S 章）。

## P3 操作分三種範圍

使用者在 app 裡遇到的每個動作，都依**作用對象**歸入一種範圍：

| 範圍 | 作用對象 | 例 |
|---|---|---|
| **item operation** | cursor 指的那**一個**項目 | 開啟、重新命名、刪除這一列 |
| **panel operation** | 當前 focus 的 panel（或它的 tab）**整體** | 搜尋、排序、新增、重新整理、對整批標記動手 |
| **global operation** | 不屬於任何 panel，屬於整個 app | 切換畫面、開設定、切換 context、離開 |

判準永遠是**作用對象在哪裡**，不是「這個動作重不重要」。一個便利小功能只要作用在
cursor 上，就是 item operation；一個關鍵的全域開關不屬於任何 panel，就是 global operation。

邊界情況：

- **對整批標記的項目做事**是 panel operation —— 作用對象是「這個 panel 裡標記的那一批」，
  不是 cursor 上的那一個。例：filu 把 marks 複製到當前目錄、sshu 的 transfer all。
- **只跟另一個 panel 有關的動作**，只出現在**它所屬 panel** 的 menu 裡，不塞進當前 focus，
  也不升格成 global。使用者 `Tab` 過去就找得到。例：filu focus 在 `[1]` 時，「清空 marks」
  只屬於 `[3]`；但「把 marks 貼到這裡」作用在 `[1]` 的目錄，所以是 `[1]` 的 panel operation。
- **切換畫面**是 global operation。例：sshu 的 `[M]anage` / `[F]ile transfer` / `[S]SH`、
  webu 的 `[W]eb` / `[B]ookmarks` / `[H]istory`。

三種範圍各有明確的位置（Rules M 章）：`Space` 開出「當前 focus 能做的事」，依
item → panel → global 排列；`?` 開出「整個 app 能做的事」，global operation 可以直接執行。

## P4 一個元素、一個意義

任何視覺或互動元素 —— 顏色、明度帶、符號、按鍵、框線樣式、固定版位 —— 一旦被
指派一個意義，就**專職化**，其他意義不能借用它。

- 某個顏色代表「使用者足跡」，浮層邊框就不能用同一個明度，即使好看
- `Esc` 代表「取消」，就不能在某個畫面拿來「確認」
- 標籤上的某個版位代表「這是哪一類畫面」，就不能兼當裝飾

兼職的代價是使用者要學兩套規則，直接違反 P1。這條也是檢驗新規則是否站得住的試紙。

## P5 固定區與概念區

每一條 rule 屬於兩區之一：

| 區 | tdp 規定什麼 | app 能做什麼 |
|---|---|---|
| **固定區** | 行為本身 | 照做。性質真的不合時可以偏離，但要寫明原因 |
| **概念區** | 語意 —— 這件事要達成什麼 | 自己決定具體怎麼做。沒有「偏離」這回事：違反了語意，就是違反固定的部分 |

以 core key 為例：

- `Space` 在**固定區**：按 `Space` 一定開 / 關當前 focus 的 Space menu；輸入態時它是空白字元，
  這個例外也由 tdp 寫死。
- `Enter` 在**概念區**：tdp 規定它是「對 focus 項目最直觀的那個動作」，不規定那個動作
  是什麼 —— filu 是進目錄，sshu 是連線，locku 是翻轉設定值。

**tdp 不規定的：**

- **letter hotkey**。哪個字母做什麼、大小寫要不要分層、要不要 chord 或 `Alt`、要不要
  `Shift-Tab` 反向切換，由各 app 決定。熱鍵依賴領域（kbu 的 `S` 是 shell、filu 的 `S` 是排序），
  而且不在「不需事先學習」的路徑上 —— 使用者要找的都在 `Space` 與 `?` 裡。tdp 只管熱鍵的
  兩件事：**必須出現在 menu 裡、用 `[]` 標出**，以及**不能佔用 core key**。
- **配色**。tdp 在 [Family defaults D2](defaults-zh_TW.md#d2-色彩系統) 提供一整套呈現規則、計算方式與
  色碼，不想處理配色的 app 直接套用；要不要遵循、意義要不要只靠顏色表達，由各 app 決定。
- **符號語彙**。用哪套 icon font、哪個 glyph、在各種終端機與 CJK 字型下畫幾格，綁在具體
  環境上，由各 app 決定。其他規則仍然約束符號的使用方式（P4 專職化、寬度穩定、熱鍵要顯式標記）。

---

## 術語

### Surface

能取得 focus、跟使用者直接互動的 UI 容器，分成 **panel** 與 **popup** 兩種。常駐顯示區
（footer、statusbar、tab 列）不是 surface —— focus 不會停在上面。

### Screen（畫面）

一組同時顯示的 panel。有些 app 只有一個畫面，有些有多個，用 global operation 切換。

- 單畫面：kbu、filu、locku
- 多畫面：sshu 的 `[M]anage` / `[F]ile transfer` / `[S]SH`；webu 的 `[W]eb` / `[B]ookmarks` /
  `[H]istory` / `[D]ownloads` / `[S]ettings`

### Panel

畫面上常駐的一塊區域，有自己的 cursor 與內容，用 `[N]` 編號。

- kbu：`[1]` 資源種類側欄、`[2]` 資源清單、`[3]` 詳細資料
- filu：`[1]` 檔案清單、`[2]` 預覽、`[3]` Marks / Tasks / Favorites
- locku：`[1]` 側欄（Profiles、Savers、Integration、Settings）、`[2]` cursor 所在項目的屬性表

### Panel tab

同一個 panel 內可切換的幾頁內容。切換 panel tab 不換 panel、不換畫面。

- kbu `[3]` 的 Logs / Events / Conditions / Relatives / History
- filu `[1]` 最多 5 個目錄 tab；`[3]` 的 Marks / Tasks / Favorites

### Popup

疊在 panel 之上的暫時性 surface，關掉之後回到底下的東西。例：

- menu：Space menu、kbu 的排序選擇器
- confirm：filu 刪除前的確認
- input：filu 的重新命名、locku 的 PIN 輸入
- viewport：kbu 的 YAML 檢視、兩個資源的 Compare
- toast：操作完成或失敗的短訊息
- PTY：kbu 的 Alterm、filu 的 shell —— 一個跑在 popup 裡的子程序

### Focus

使用者當下按鍵會送到的位置，分兩層：

1. **surface 層**：哪個 panel 或 popup。例：kbu 的 `[2]`，或疊在上面的 Space menu
2. **位置層**：該 surface 裡 cursor 指的那一列、選中的那個 panel tab。例：kbu `[2]` 裡
   cursor 所在的那個 pod

「作用對象在 focus 範圍內」指作用對象是當前 surface 本身，或它位置層上的那一項。

### 輸入態

使用者正在打字的狀態：focus 在一個會把按鍵當字元收下的欄位上。例：filu 的重新命名框、
sshu 的 host 表單、webu 的網址列（`L`）、locku 的 PIN 輸入、任何 `/` 搜尋列。

### 模式

panel 或 popup 裡的一個暫時狀態：進入之後，一部分鍵換成這個模式自己的意思，`Esc` 離開。
例：webu 的 visual mode（選字）、kbu 的拖曳模式（排 pin 的順序）、sshu 的 `Alt+v` 選取模式、
filu yank viewport 裡的選取。模式不是輸入態 —— 按鍵不會變成字元。規則見 Rules K11。

### Core key

tdp 規定意義、在所有 surface 意義不變的鍵：`Tab`、`Enter`、`Esc`、`Space`、`?`（Rules K 章）。

### Letter hotkey

app 自己指定、用來直接執行 menu 裡某一列的鍵。例：filu 的 `[r]ename`、kbu 的 `[C]ompare`、
sshu 的 `[t]ransfer` 與 `[T]ransfer all`。它是捷徑，不是額外的功能（Rules M3）。

### Source 與 target

從 popup A 開出 popup B 時，A 是 source、B 是 target。例：kbu 在 Compare viewport 上按
`Space` 開出版面切換 menu —— Compare 是 source，menu 是 target。

### 串流內容

持續有新資訊流入的內容。例：kbu `[3]` 的 Logs、sshu 的 SSH session、filu 的搜尋結果逐筆出現。

### 偏離與違反

- **偏離**：app 有意不照某條 rule 的固定部分做，並在自己的 `docs/dev-remarks.md`「偏離 tdp」
  一節寫明哪一條、在哪裡、為什麼。例：locku 的鎖定畫面不顯示 footer（M1），因為唯一的
  動作是按任意鍵叫出 PIN。
- **違反**：沒寫原因就不照固定的部分做。列進該 app 的 `docs/<app>-terminu-fix.md` 待修。

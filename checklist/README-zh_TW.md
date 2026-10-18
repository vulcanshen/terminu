# terminu checklist

**Language**: [English](README.md) · 繁體中文

terminu checklist 是 [tdp](../principle/README-zh_TW.md) 的條目清單：把 principle、components、project 的規定拆成一條一條可以檢查的
項目，用來數一個家族 app 有多少 terminu 的 gene。版號、CHANGELOG 跟 tdp 一起走，每一版 tdp 有自己那一版的清單。條目在
[`items-zh_TW.md`](items-zh_TW.md)。

## 規範才是依據

- 清單從規範拆出來；兩者對不上時，以規範的文字為準，對不上的地方回報成 tdp 的缺漏。
- **只看 tdp，不看用什麼實作**：用不用 terminu-go、用什麼語言寫，都照同一份清單判。用 terminu-go 的 app 也不會自動全部符合 ——
  app 自己交的東西（例：`docs/icon.svg`、README、dev-remarks）lib 管不到。
- 規範裡寫明「由 app 決定」的部分、例子、「為什麼」、「實作參考（不是規定）」不拆成條目。

## 每一條

| 欄 | 寫什麼 |
|---|---|
| 編號 | `出處-序號`（例：`K4-1`、`form-3`），見下面的「編號」 |
| 出處 | rules 寫規則編號（`K4`）；components 與 project 寫 `<檔名> §<節>`（例：`popup §外框`）；principle 寫 `P3` 或 `術語`。從圖拆出來的，後面標 `（圖）` |
| 檢查什麼 | 一件可以回答「是／不是」的事 |
| 適用 | app 有哪個功能時才算這一條，見下面的「適用」 |
| 怎麼驗 | 按哪個鍵、看畫面的哪裡；畫面上看不到的寫「讀程式」或「讀檔案」 |

## 編號

- **固定不變**：規定刪掉時編號作廢、不再用；新的規定接在同一個出處的最後。不同版本的成績單用編號對得起來。
- **前綴**：rules 用規則編號（`K4-1`）；components 與 project 用檔名（`popup-3`、`checkbox-4`），`components/README` 用 `components-`、
  `input/README` 用 `input-`、`project/README` 用 `project-`。沒有規則編號的段落：rules 開頭的「偏離」「引用」用 `departure-`、
  `references-`，principle 的術語用 `terms-`，S 章開頭（splash 佔滿整個畫面）用 `S0-`。編號只用英文字母、數字與 `-`，中英文兩份一樣，
  工具也讀得了。

## 適用

- **`都要`**：每個家族 app 都要符合。
- **功能的名字**：app 有這個功能時，這一條才算數。用「、」隔開的，有其中一個就算；用「＋」連起來的，要同時有。
- **功能裡的情況**：條目寫的是某種情況（例：「confirm 有警告句時……」），app 有這個功能、卻沒有那種情況時，這一條判不適用。

| 功能 | 什麼樣的 app 算有 |
|---|---|
| 多畫面 | 有兩個以上的畫面（畫面 chip 列） |
| 多 panel | 有一個畫面有兩個以上的 panel |
| panel tab | 有 panel 有 tab |
| 一列一個值的 panel | 有一列一個值的 panel |
| 分組清單 | panel 上有分組的清單 |
| 明細 panel | 有跟著另一個 panel 的 cursor 換內容的明細 |
| 表頭 | 有清單有表頭（多欄的一般清單一定有） |
| 排序 | 有可以排序的清單 |
| 標記 | 有可以標記、整批操作的清單 |
| Drag | 有 Drag mode |
| panel filter | 有 panel filter |
| statusbar | 有 statusbar |
| 串流內容 | 有一直進來的內容（例：log） |
| loading | 有 panel 或 popup 要等內容載入 |
| 模式 | 有模式（Rules K11） |
| 停用 | 有暫時不能執行的動作、停用的項目或欄位 |
| 長時間工作 | 有長時間的工作（畫面 chip 列下的進度） |
| PTY | 有 PTY（在 panel 裡或 terminal popup） |
| terminal popup | 有 terminal popup |
| popup tab | 有帶 tab 的 popup |
| 表單 | 有表單 |
| viewer | 有 viewer |
| toast | 有 toast |
| error popup | 有 error popup |
| confirm | 有 confirm |
| input | 有任何一種 input（input popup，或表單、panel 上的欄位） |
| text、password、number、select、radio、checkbox、slider、textarea、color picker、datetime picker、file-picker、reorder | 有這一種 input |
| finder | 有 finder，或任何一種 finder（select、checkbox popup、file-picker 都是 finder 的一種，input/finder） |
| 存設定或資料 | 有設定、資料、狀態或快取寫到磁碟 |
| 出 Windows 版 | 發布 Windows 版 |
| mouse | 有做 mouse |

## 判法

每一條判成下面其中一種：

| 判定 | 意思 |
|---|---|
| 符合 | 做到這一條 |
| 偏離 | 沒做到，但 dev-remarks 的「偏離 tdp」寫了這一條與原因（Rules 開頭的「偏離」） |
| 違反 | 沒做到，也沒寫成偏離 |
| 不適用 | app 沒有這一條的「適用」寫的功能，或沒有條目寫的那種情況 |

判的時候標明照哪一版 tdp 判。偏離、違反、不適用列出來，告訴 app 缺了哪些、為什麼缺。

## gene

- **每一條就是一個 gene**：app 判成符合的一條，就是 app 有的一個 terminu gene。偏離、違反、不適用都不算。
- **只數有幾個，不算比例**：寫成 `tdp-<版本> <數> gene`（例：`tdp-0.7.2 860 gene`）。
- **跟那一版 tdp 綁在一起**：那一版 tdp 的 gene 總數就是它的條目數；tdp 改版時總數會變，已經判過的結果照舊是當時那一版的數字。
  不同版本的數字不直接比較。
- app 做了 tdp 沒規範的東西，不算 gene，也不扣：判的時候另外列出來，回報成 tdp 的缺漏。

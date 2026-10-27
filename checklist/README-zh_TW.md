# terminu checklist

**Language**: [English](README.md) · 繁體中文

terminu checklist 是 [tdp](../principle/README-zh_TW.md) 的條目清單：把 principle、components、project 的規定拆成一條一條可以檢查的
項目，寫出一個 app 照 tdp 要做到什麼、什麼情況下要做、從哪裡看得到。版號、CHANGELOG 跟 tdp 一起走，每一版 tdp 有自己那一版的
清單。條目在 [`items-zh_TW.md`](items-zh_TW.md)。

清單只寫要查什麼。怎麼判 —— 判定有哪幾種、怎麼數、怎樣算通過 —— 由 terminu harness 決定，不在 tdp 裡（見下面的「怎麼判」）。

## 規範才是依據

- 清單從規範拆出來；兩者對不上時，以規範的文字為準，對不上的地方回報成 tdp 的缺漏。
- **只看 tdp，不看用什麼實作**：用不用 terminu-go、用什麼語言寫，都照同一份清單查。用 terminu-go 的 app 也不會自動全部符合 ——
  app 自己交的東西（例：`docs/icon.svg`、README）lib 管不到。
- 規範裡的例子、「為什麼」、「實作參考（不是規定）」不拆成條目；寫「app 可以自行決定」的放行本身也不拆，範圍內還要守的規定照樣拆。

## 每一條

| 欄 | 寫什麼 |
|---|---|
| 編號 | `出處-序號`（例：`K4-1`、`form-3`），見下面的「編號」 |
| 出處 | rules 寫規則編號（`K4`）；components 與 project 寫節編號（例：`popup.1`，Rules 開頭的「引用」）；principle 寫 `P3` 或術語的編號（`terms.1`）。從圖拆出來的，後面標 `（圖）` |
| 檢查什麼 | 一件可以回答「是／不是」的事 |
| 適用 | app 有哪個功能時才算這一條，見下面的「適用」 |
| 怎麼驗 | 按哪個鍵、看畫面的哪裡；畫面上看不到的寫「讀程式」或「讀檔案」 |

## 編號

- **固定不變**：規定刪掉時編號作廢、不再用；新的規定接在同一個出處的最後。不同版本的結果用編號對得起來。
- **前綴**：rules 用規則編號（`K4-1`）；components 與 project 用檔名（`popup-3`、`checkbox-4`），`components/README` 用 `components-`、
  `input/README` 用 `input-`、`project/README` 用 `project-`。沒有規則編號的段落：rules 開頭的「引用」用 `references-`（`departure-` 已作廢），
  principle 的術語用 `terms-`，S 章開頭（splash 佔滿整個畫面）用 `S0-`。編號只用英文字母、數字與 `-`，中英文兩份一樣，
  工具也讀得了。

## 適用

- **`都要`**：每個 app 都要符合。
- **功能的名字**：app 有這個功能時，這一條才算數。用「、」隔開的，有其中一個就算；用「＋」連起來的，要同時有。
- **功能裡的情況**：條目寫的是某種情況（例：「confirm 有警告句時……」），app 有這個功能、卻沒有那種情況時，這一條不適用。
- **不在 TUI 裡的畫面**（例：locku 鎖定時的螢幕保護與 PIN 框）不是 surface：「每一個 surface」的條目不管它（Rules K1）。

| 功能 | 什麼樣的 app 算有 |
|---|---|
| 多畫面 | 有兩個以上的畫面（畫面 chip 列） |
| 多 panel | 有一個畫面有兩個以上的 panel |
| panel tab | 有 panel 有 tab |
| 一列一個值的 panel | 有一列一個值的 panel |
| 分組清單 | panel 上有分組的清單 |
| 明細 panel | 有跟著另一個 panel 的 cursor 換內容的明細 |
| 表頭 | 有清單有表頭（多欄的一般清單一定有） |
| 位置列 | 有 panel 的位置列（layout/panel） |
| 排序 | 有可以排序的清單 |
| 標記 | 有可以標記、整批操作的清單 |
| 旗標 | 有在標記欄畫領域旗標的清單（不能標記的清單，panel.7） |
| Drag | 有 Drag mode |
| panel filter | 有 panel filter |
| statusbar | 有 statusbar |
| zoom | 有放大 panel 的功能（layout/screen） |
| 串流內容 | 有一直進來的內容（例：log） |
| 沒有 cursor 的 panel | 有沒有 cursor 的 panel（預覽、log） |
| loading | 有 panel 或 popup 要等內容載入 |
| 模式 | 有模式（Rules K11） |
| 模式（在 panel 上） | 有開在 panel 上的模式（例：panel 的 Drag） |
| 模式（在 popup 裡） | 有開在 popup 裡的模式（例：viewer 的選取模式、reorder 的 Drag） |
| 停用 | 有暫時不能執行的動作、停用的項目或欄位 |
| 長時間工作 | 有長時間的工作（畫面 chip 列下的進度，或單畫面 app 工作那一列的進度） |
| 工作清單 | 有工作清單：列出 app 正在跑或跑過的工作的 menu（例：sshu 的 Jobs） |
| PTY | 有 PTY（在 panel 裡或 terminal popup） |
| 互動 terminal | 有讓使用者在裡面打自己指令的 PTY（shell、ssh 連線、`kubectl exec`）；app 開一個程式做一件事的（編輯器、讓 doas 問密碼）不算 |
| terminal popup | 有 terminal popup |
| 提權 | 要用系統的提權工具（例：sudo）寫 app 以外的檔 |
| popup tab | 有帶 tab 的 popup |
| 表單 | 有表單 |
| viewer | 有 viewer |
| toast | 有 toast |
| error popup | 有 error popup |
| confirm | 有 confirm |
| input | 有任何一種 input（input popup，或表單、panel 上的欄位） |
| text、password、number、select、radio、checkbox、slider、textarea、color picker、datetime picker、file-picker、reorder | 有這一種 input |
| finder | 有 finder，或任何一種 finder（select、checkbox popup、file-picker 都是 finder 的一種，input/finder） |
| 有預覽的 finder | 有帶預覽的 finder：一般的 finder、file-picker（select、checkbox popup 沒有預覽） |
| 有檔案預覽 | 有預覽檔案、目錄的 popup：file-picker，或預覽檔案的 finder |
| 存設定或資料 | 有設定、資料、狀態或快取寫到磁碟 |
| 比較模式 | 有 panel 的比較模式（先挑 anchor、再挑另一列來比） |
| 被指到的 panel | 清單的一列代表畫面上另一個 panel，cursor 會指出那個 panel（例：sshu 的 sessions 清單與網格） |
| app 自己的 popup | 有七類裝不下、內容由 app 自己畫的 popup（例：kamonu 畫格子的 popup） |
| panel 內容的框 | panel 的內容自己會畫出框（例：webu 顯示的網頁跳出的彈窗） |
| 不再用的檔 | 改版後有不再用的設定、狀態或資料檔（例：sshu 的 errors.yaml、kbu 的 theme.yaml） |
| 出 Windows 版 | 發布 Windows 版 |
| 發過版 | 發布過（有 tag 與 GitHub release）；還沒發過版的 app，只有發版之後才有的東西（release、tap 上的 formula……）不適用，看得到的照現在的 repo 查 |
| mouse | 有做 mouse |

有 color picker 就算有 select（R、G、B 按 `Enter` 開 00–FF 的 select），也就算有 finder。

### 家族成員與照 tdp 做的 app

條目寫了兩種寫法的（Homebrew tap、splash 的作者信箱、README 的 terminu family 段；Rules 的 E 章開頭），照 app 是家族成員
還是照 tdp 做的 app，查那一種。project 的條目（`project-`）只查家族成員（project.1）；其他條目兩種 app 都一樣。

### 比最低尺寸小的畫面

「怎麼驗」要縮小終端機的（例：窄寬、放不下時），縮到 app 的最低尺寸為止（Rules L1）。比最低尺寸小的畫面只畫名稱與提示：那裡只有
L1-3～L1-6 與 E5-13 的極小尺寸適用，畫面上的其他條目都不適用。

## 怎麼判

清單只寫查什麼、什麼時候算數、去哪裡看。判定有哪幾種、怎麼數、怎樣算通過、從畫面量時間時容許多少誤差、一個東西整個沒做時它的
細節條目怎麼判，都由 terminu harness 決定。

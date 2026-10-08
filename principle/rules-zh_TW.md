# tdp Rules

**Language**: [English](rules.md) · 繁體中文

這裡的每一條都是 **必須遵守**。每條附上「為什麼」，那是它的 origin UX（[Principle P0](README-zh_TW.md#p0-規則服務-ux不是反過來)）。

**什麼是規定**：rules 與 [components](../components/README-zh_TW.md) 裡的敘述都是規定。不是規定的只有四種：寫明「由 app 決定」的部分、
標成「例」的例子、「為什麼」、標成「實作參考（不是規定）」的段落。

**分區**：每條標題後標 `固定` 或 `概念`（[Principle P5](README-zh_TW.md#p5-固定區與概念區)）。`概念` 條目裡，語意部分仍是固定的，只有實作方式交給 app。
固定條裡可以用「（概念）」標出交給 app 的部分，概念條裡可以用「（固定）」標出寫死的部分。

**偏離**：固定的部分原則上照做。app 的性質讓某條不適用時，要在該 app 的
`docs/dev-remarks.md`「偏離 tdp」一節寫明**哪一條、在哪裡、為什麼**；寫明原因的是**偏離**，
沒寫原因的是**違反**，列進 `docs/<app>-terminu-fix.md`。components 全部算固定區：偏離 components 除了寫明原因，還要回報成 tdp 的
缺漏 —— components 的方案不合用，就是 tdp 少了一個方案。

**引用**：用 `tdp` 加編號，例如 `tdp K4`、`tdp M2`。編號一旦發布就不重排；
廢除的條目保留編號、標記廢除。

| 章 | 範圍 |
|---|---|
| [K](#k-core-key) | Core key |
| [M](#m-menu-與揭露) | Menu 與揭露 |
| [L](#l-版面) | 版面 |
| [F](#f-popup) | Popup |
| [X](#x-mouse) | Mouse |
| [T](#t-時間軸) | 時間軸 |
| [S](#s-splash) | Splash（家族彩蛋） |
| [E](#e-app-與環境) | App 與環境：命令列、環境變數、需求、發布、文件 |

---

## K Core key

### K1 Core key 的意義全 app 不變 `固定`

| 鍵 | 意義 | 條目 |
|---|---|---|
| `Tab` | focus 移到同層的下一個物件 | K2 |
| `Enter` | 對 focus 的東西做最直觀的那個動作；focus 在值上時是確定這個值 | K3 |
| `Esc` | 取消 / 關閉最上層 | K4 |
| `Space` | 在 panel 上開 / 關 Space menu（這裡能做什麼） | K5、M2 |
| `?` | 開 / 關 key reference：最前端那個 surface 能按什麼鍵（唯讀） | K6、M4 |
| `q` | 離開 app | K9 |

表上的鍵在**每一個 surface** 都是這個意義，例外只有輸入態（K8）、PTY（K10）、模式（K11）與表單上的 `q`（K9）。app 可以
不用到全部（單一 panel 的 app 不需要 `Tab`），也可以另外指定自己的 core key；自訂的
core key 一旦指定，同樣在所有 surface 意義不變。**letter hotkey 不能佔用表上的鍵。**

**為什麼**：使用者學的單位是**角色**（「取消」「換 focus」「現在能做什麼」），不是
按鍵。角色固定，學一次就在所有 surface、所有家族 app 有效。只要有一個 surface
讓 `Space` 做別的事，使用者就得多學一條「哪裡例外」。

### K2 `Tab` 在同層物件之間切換 focus `固定`

`Tab` 把 focus 移到**當前 surface 裡同一層的下一個物件**，最後一個之後回到第一個：

| focus 所在 | `Tab` 在什麼之間切換 |
|---|---|
| 畫面 | panel |
| 表單（[components/dialog/form](../components/dialog/form-zh_TW.md)） | 欄位；錯誤列有錯誤時與動作列也各是一站（欄位裡的選項用 hjkl，K12） |
| 有好幾塊的 popup（finder、datetime picker） | 塊 |

- `Tab` 不跨畫面、不離開當前 popup。
- focus 在 PTY 裡時，`Tab` 屬於子程序（K10）。
- **打字列上**（finder 與 select 的打字列、panel filter）：`Tab` 到它的清單（[components/input/finder](../components/input/finder-zh_TW.md)）。
- **只有一塊的 input popup**：有灰字提議（舊值）時，`Tab` 接受提議；沒有提議時不作用。
- 多行文字的寫入狀態下，`Tab` 是縮排字元，不是換欄位（K8）。
- 反向切換（例如 `Shift-Tab`）是熱鍵，由 app 決定要不要做；表單裡一定有 `Shift-Tab`。

**為什麼**：使用者按 `Tab` 期待的是「換下一塊」—— 在畫面上是下一個 panel，在表單裡是
下一個欄位。這是同一個角色在不同層級的樣子。跨畫面切換屬於 global operation（P3）。

### K3 `Enter` 對 focus 的東西做最直觀的動作 `概念`

`Enter` 對 focus 項目做**最直觀的那個動作** —— 進目錄、連線、開啟、翻轉設定值。
具體是什麼由 app 決定，但同一種項目在同一個 app 裡永遠是同一個動作。
panel 本身是一個內容區、沒有「項目」可選時（例：預覽、log），`Enter` 對整個 panel 做最直觀的動作，由 app 決定
（例：開一個可捲動的檢視）。

**`Enter` 不移動 focus**（固定）：按完 `Enter`，focus 留在原處 —— 表單上確定了一欄的 input popup，回到同一欄；原地選 radio、
翻 checkbox 也不動。換位置只有 `Tab` 與移動鍵（K2、K12）。

**在 input popup 裡**（固定），`Enter` 對 focus 的那一塊做事：

- **focus 在值上**：確定這個值 —— 寫回去、popup 關掉。值不合格就**不寫回**，錯誤寫在預留的錯誤列（F7），popup 不關。
  值跟打開時一樣，就不寫回、直接關掉。
- **多行文字**：寫入狀態下 `Enter` 是換行；離開寫入狀態之後的 `Enter` 才確定。
- **打字列**（finder 與 select 的打字列、panel filter）：`Enter` 把 focus 移到清單上 cursor 那一項，不執行它；在清單上
  再按 `Enter` 才執行或選定。沒有結果時不作用。
- **其他部分**（例：datetime picker 的月份、color picker 的 R）：做最直觀的那件事（例：移到日曆、打開選值的清單）。

**表單**（[components/dialog/form](../components/dialog/form-zh_TW.md)）不是 input popup：表單裡的 `Enter` 對 focus 的項目做事 ——
打開那一欄的 input popup、選 radio、翻 checkbox、按按鈕。送出只有按鈕：那時檢查**所有**欄位，有不合格的就不送出，
focus 跳到第一個有問題的欄位。

在其他 popup（menu、confirm）裡，`Enter` 是執行 cursor 所在列 / 接受。

**為什麼**：「確認 / 進入」這種字面定義撐不過真實 app，使用者對 `Enter` 的期待是
「對這個東西做那件理所當然的事」。在 input popup 裡，那件事就是確定這個值 —— 確定一個不合格的值、或確定不了卻不說
為什麼，都讓使用者卡住。`Enter` 不移動 focus：一直按 `Enter` 只會在同一個地方開開關關，使用者不用猜按完會停在哪。

### K4 `Esc` 一次關一層，永不離開 app `固定`

`Esc` 取消當前操作或關閉最上層：有 popup 關 popup（包括 toast，F3），沒有 popup 就退出
當前模式（選取、拖曳）或往上一層（例：清掉 panel filter）—— 「上一層」是什麼由 app 定義。**一次一層**，
而且 **`Esc` 永遠不會離開 app**，到了最上層就什麼都不做。

popup 開出 popup 時（例：Space menu → global operation popup → confirm），`Esc` **只關最上層那一個**，
底下的 popup 階層原樣留著、照原樣呈現；再按一次才關下一層（F4）。

**為什麼**：使用者迷路時會連按 `Esc` 想回到安全的地方。如果連按的終點是 app 被關掉，
`Esc` 就變成危險鍵，使用者不敢按，也就失去了「取消」這個安全出口。離開 app 有自己的
鍵（K9）。

### K5 `Space` 在 panel 上開關 Space menu `固定`

- focus 在 panel 上時，`Space` 打開 Space menu（M2）；Space menu 開著時，再按 `Space` 關掉它。
  `Esc` 也能關。
- **`Space` 只關它自己開的 Space menu。** 其他 popup（由 `Enter` 或熱鍵打開的 confirm、input、
  note……）上按 `Space` **不作用**，它們由 `Esc` 或自己的流程關閉。唯一的例外：checkbox popup 的清單上，`Space` 是勾或取消勾
  （[components/input/checkbox](../components/input/checkbox-zh_TW.md)）。
- popup 自己的操作用熱鍵執行，揭露在 popup 下框的 hint 與
  該 popup 的 `?` help（K6），不在 popup 上再疊一個 Space menu。

**為什麼**：只能開、不能用同一個鍵關的入口是陷阱 —— 使用者伸手按同一個鍵想退出，
結果沒反應。但 `Space` 若也能關 confirm，它就兼了 `Esc` 的「取消」（P4）；若能在 popup
上再疊 menu，框上疊框的層數就沒有盡頭。家族的流程一律是：panel 上 `Space` 開 menu，
選一列 `Enter`，才打開下一個 popup。checkbox popup 是例外：在清單上勾選，`Space` 是大家熟的鍵，而那裡的 `Enter`
要留給確定整組（P0）。

### K6 `?` 隨時開關 key reference `固定`

`?` 在任何 surface 都有回應，再按一次 `?` 關掉，`Esc` 也能關。它打開的是**最前端那個 surface 的
key reference**：唯讀、可以捲動，沒有游標、不能執行（M4；樣子見 [components/dialog/note](../components/dialog/note-zh_TW.md)）。

| focus 在 | key reference 列出 |
|---|---|
| panel | 這個 panel 能按的鍵，以及 core key 與 global 熱鍵 |
| popup（包括 Space menu、global operation popup） | **只有這個 popup** 能按的鍵 |

輸入態、PTY、模式依 K8、K10、K11。

**為什麼**：按 `?` 的人是想**讀**「這裡能按什麼」。讀與做放在同一個框裡，使用者站在一個有游標、
每一列都按得下去的清單上，反而不敢動（F1：一個 popup 只屬於一類）。能做的事在 `Space`，能讀的鍵在 `?`。

### K7 別名要完整 `固定`

一個角色綁多個鍵時，別名必須**在所有 surface 同樣有效**。做不到就不要做別名。

**為什麼**：半套別名（某個鍵只在主畫面能取消、popup 裡不行）比沒有別名更糟 —— 它
偽裝成便利，實際上多了一條「哪裡可以、哪裡不行」的規則要學。

### K8 輸入態：熱鍵全部失效 `固定`

**輸入態**是以打字輸入的文字當內容的狀況：focus 在一個打字列上 —— input popup 的值、textarea 的寫入狀態、finder 與
select 的打字列、panel filter。select 與 picker 的清單、textarea 的移動狀態、表單本身都不是輸入態。

在輸入態裡，**所有會產生字元的鍵都是字元**，不觸發任何動作：

| 鍵 | 輸入態下 |
|---|---|
| letter hotkey、`Space`、`?`、`q` | 當成字元輸入 |
| `Esc` | 取消輸入（K4） |
| `Enter` | 見 K3 |
| `Tab` | 接受灰字提議；打字列上到清單（K2）；多行文字的寫入狀態下是字元（縮排） |
| `Ctrl-C` | 離開流程（K9） |

離開輸入面立刻恢復。

**多行文字的寫入狀態**：`Tab` 是字元（縮排），就像 `Enter` 是換行（K3）；要確定，先離開寫入狀態（`Esc`），
再按 `Enter`。縮排插入 `\t` 還是空白，由 app 決定。

**為什麼**：`Space`、`?`、`q` 都是可列印字元。不屏蔽的話，使用者打不出含空白的檔名、
含問號的密碼。`Esc` 與 `Enter` 保留，因為它們不跟字元競爭，而且少了它們輸入框就是
出不去的陷阱。

### K9 `q` 與 `Ctrl-C` 離開 app `固定`

- `q` 與 `Ctrl-C` 做**同一件事**：進入 app 的離開流程。`q` 在輸入態是字元（K8），在表單上不作用
  （[components/dialog/form](../components/dialog/form-zh_TW.md)）；`Ctrl-C` 在輸入態與表單上仍然有效。focus 在 PTY 裡時兩個都屬於
  子程序（K10）。
- **離開流程由 app 決定**（概念）：直接離開、先確認，或讓使用者選擇離開的方式。
  例：sshu 有 session 開著時先問要不要關掉；filu 讓使用者選要不要把 shell 切到最後的目錄。
- **離開流程進行中再按一次 `Ctrl-C`，立刻離開**，不再詢問。
- 離開列在 global operation popup 裡（M4）。

**為什麼**：`Ctrl-C` 是所有終端機使用者的肌肉記憶，`q` 是 TUI 的慣例；兩者行為不同，
使用者就得記哪個會問、哪個不會。連按兩次 `Ctrl-C` 強制離開，讓使用者不會被自己的確認框困住。表單上的 `q` 是例外：
表單看起來像可以打字的地方，使用者以為在打字、打到 `q` 卻離開了 app，這個代價太高。

### K10 PTY：按鍵屬於子程序，至少留一個出口鍵 `固定`

focus 在 PTY（跑在 app 裡的 shell、編輯器、遠端 session）時，**按鍵都送給子程序**：core key 與 app 的
熱鍵都失效 —— vim 需要 `Esc`、shell 需要 `Tab` 與 `Ctrl-C`、遠端程式可能要任何一個組合鍵。

- app **至少**指定一個出口鍵，讓 focus 離開 PTY（選一個子程序幾乎不會用到的組合；家族用 `Alt-Esc`），
  並在 focus 位於 PTY 時常駐揭露它（樣子見 [components/dialog/terminal](../components/dialog/terminal-zh_TW.md) 與
  [components/layout/screen](../components/layout/screen-zh_TW.md) 的 footer）。
- **`Alt-Esc` 一律先 confirm**：按了會讓 focus 離開 PTY 或結束子程序時，不論子程序留不留著，都先跳 confirm（`Enter` 離開、
  `Esc` 回到 PTY）；在 PTY 裡面的動作（例：退一階 zoom）不用問。理由：終端機把 Alt 組合送成「`Esc` 加那個鍵」，`Alt-Esc`
  跟兩次 `Esc` 的 byte 一模一樣；app 忙的時候，讀鍵的一端卡住，兩次 `Esc` 就會疊在一起被讀成 `Alt-Esc`。vim 裡連按 `Esc`
  很常見，confirm 讓誤觸的人按 `Esc` 回到 PTY。
- **其他 Alt 組合的出口鍵**（例：kbu 的 `Alt-t` 隱藏 Alterm、sshu 鎖住的格子的 `Alt-Enter`）同樣會被「`Esc` 再按那個鍵」
  拼出來；要不要 confirm 由 app 決定。
- 出口鍵以外，PTY 裡要不要再保留其他 app 的組合鍵（例：sshu 在格子裡的放大、換格、捲歷史），由 app 決定。
  保留的鍵跟出口鍵一樣常駐揭露（M1）。
- 按了出口鍵之後 focus 落在哪裡，由 app 決定。
- 子程序還沒準備好收鍵時（例：遠端還在連線），app 可以不轉送一般的按鍵（免得晚幾分鐘才落到遠端）；但 **`Ctrl-C` 照樣
  轉送給子程序**，出口鍵照樣有效、照樣揭露。focus 在 PTY 裡時，使用者認為每個鍵都是在 PTY 裡按的；例外只有明示揭露的
  出口鍵與 app 保留的組合鍵。

> **實作參考（不是規定）**：用 bubbletea v1.3.10 實測，前面有鍵在排隊時，間隔 150ms 的兩次 `Esc` 也會黏在一起。

**為什麼**：focus 在 PTY 裡時，使用者做的事幾乎都是 PTY 裡的事，app 攔下的鍵越多，越可能弄壞子程序，
也讓「這個鍵現在屬於誰」變成要記的東西。但沒有出口的 PTY 是陷阱，所以至少要有一個出口鍵，而且看得到；
其餘要不要攔，看 app 的 PTY 是怎麼用的 —— 一格 shell 跟一整片同時活著的遠端 session，答案不一樣。

### K11 模式裡的 core key `固定`

focus 在一個模式裡時（術語「模式」），core key 這樣作用：

| 鍵 | 模式裡 |
|---|---|
| `Space` | **不開任何 menu**，不作用 |
| `?` | 這個模式的 key reference（唯讀，K6）：模式裡能按什麼鍵、做什麼 |
| `Esc` | 離開模式（K4），回到進入前的狀態 |
| `q`、`Ctrl-C` | 照 K9 進入離開流程 |
| `Tab` | 模式可以暫停 `Tab`，但按了要有回應，說明先 `Esc` 離開模式（例：toast）；toast 還在時，第一個 `Esc` 先收掉它（K4） |

- 模式裡沒有 Space menu，也沒有任何可以執行的按鍵清單。模式自己的鍵（移動、選取、拖曳）直接按；它們揭露在
  `?` 的 key reference 與 footer / 下框 hint（footer 在模式裡的樣子見 [components/layout/screen](../components/layout/screen-zh_TW.md)）。
- **模式要標示自己**：模式名顯示在模式所在的框（panel 或 popup）的上框右側，外框換成模式色；離開模式就恢復。模式名是字，
  不只靠顏色：模式裡 focus 的 panel 照樣看得出是 focus（L5）。樣子見 [components/layout/panel](../components/layout/panel-zh_TW.md)。

**為什麼**：模式一定是特殊情況，裡面的鍵是移動、選取這類要直接、連續按的鍵，不是對某個 item 的動作，也沒有
item / panel / global 可分。把它們做成一個能選、能執行的清單（連 `h j k l` 都要從清單執行）只是多繞一層；使用者
要的只是「這裡能按什麼」，那正是 `?` 的工作。

### K12 導覽字母保留給移動，hjkl 是方向鍵 `固定`

不在打字的地方，`j k u d g G h l` 保留給移動，任何動作都不佔用。`h`/`j`/`k`/`l` 就是 `←`/`↓`/`↑`/`→`，意思看畫面的排法：

- **有左右結構時**（同一個 surface 裡的 tab、左右兩側、格子）：上下左右。`j`/`k` 在清單裡上下，`h`/`l` 往左右 —— 切 tab、
  跨到另一側、日曆的前後一天。
- **只有一維清單、沒有左右結構時**（表單、沒有 tab 的「一列一個值」panel、menu）：`h`/`k`（`←`/`↑`）往前，`j`/`l`（`↓`/`→`）
  往後，不分選項橫排還是直排。
- 一維清單放在有 tab 的 panel 裡：`h`/`l` 給 tab，`j`/`k` 照樣在清單裡移。
- **`u`/`d` 半頁，`gg`/`G` 到頭、到尾**。`g` 只當兩鍵組合的開頭：`gg` 是到頭，其他 `g` 開頭的組合可以當熱鍵（例：filu、
  webu 的 `[go]to`）；單按 `g` 不做任何事。不收 `Ctrl-U`/`Ctrl-D` 當別名。
- **在一段文字裡移動**（note 的選取、textarea 的移動狀態）：再加上 `w`/`b`/`e`（下一個字頭、上一個字頭、字尾）與
  `0`/`$`（行首、行尾），照 vim。

**為什麼**：hjkl 在家族裡是方向鍵，表單、panel、清單都靠它移動；一個 app 把其中一個綁成動作，使用者以為在移動，卻觸發
了動作。有左右結構時左右就是左右（filu、kbu、webu 的 `h`/`l` 切 tab，sshu 的 `h`/`l` 跨到另一側）；沒有左右結構時左右鍵閒著，
給它「往前往後」，使用者不用想選項是橫排還是直排。不收 `Ctrl-U`/`Ctrl-D`：一個動作一組鍵，少一組要記；而 `Ctrl-U` 在 shell
與很多輸入框裡是「清掉這一行」，同一個組合在家族裡一處翻頁、一處刪字，按錯的代價太高。

---

## M Menu 與揭露

### M1 入口要被看得到 `固定`

非輸入態的每一個畫面都必須**常駐顯示** `?`，以及 `Space`（模式裡 `Space` 不作用，不必顯示，K11），讓第一次打開
app、沒讀過任何文件的使用者看得到。樣子見 [components/layout/screen](../components/layout/screen-zh_TW.md) 的 footer。

**為什麼**：使用者不可能按一個不知道存在的鍵。入口沒被揭露，後面揭露得再完整也
等於不存在（Principle P2）。

### M2 Space menu：item → panel → global 三區 `固定`

Space menu 列出**當前 panel 能做的所有事**，依作用對象（Principle P3）分區，順序固定：

| 順序 | 區塊標題 | 內容 |
|---|---|---|
| 1 | `item operation` | cursor 指的那一個項目能做的事 |
| 2 | `panel operation` | 當前 panel（或它的 tab）整體能做的事 |
| 3 | （不加標題） | **固定一列** `Global operation`（沒有熱鍵）：`Enter` 打開 global operation popup（M4）。全域動作只有一個時也一樣 |

- **區塊標題字串固定**，全 app、全家族都用上表的英文原字。
- **global 那一列不加區塊標題**：列名 `Global operation` 已經說明它是什麼，再掛一個 `global operation` 標題只是重複；它跟上面的區塊之間照樣用分隔線隔開。
- **沒有對象就沒有那一區**：空清單沒有 item，item operation 連標題一起不出現。
- **panel 上的 Space menu，item 與 panel 兩區一律加區塊標題**（即使只剩其中一區）：global 那一列永遠在，menu 永遠不只一種東西。不加標題只適用於 global 那一列，與不分區的其他 menu（M8）。
- 區塊之間用分隔線隔開。樣子見 [components/dialog/menu](../components/dialog/menu-zh_TW.md)。

**為什麼**：使用者從上往下讀，先看到「對我選的這個東西能做什麼」，再看到「對這一整塊」，
最後才是全域。固定的標題字串讓使用者一眼認出「這是同一種 menu」—— 措辭不同的 menu
會被讀成另一**種**選單。global 區放在最後、只佔一列，讓使用者只要記得 `Space` 一個鍵就找得到所有事，又不會讓全域動作
比當前 panel 自己的動作還長；家族每個 app 的 Space menu 都長成同一個樣子。

### M3 每個動作都要能從 menu 找到 `固定`

- 每個 panel 的每個 item operation 與 panel operation，都在該 panel 的 Space menu 裡。
- 每個 global operation 都在 global operation popup 裡（從 Space menu 的 global 列打開）。
- popup 自己的操作，都在該 popup 的下框 hint 與 `?` key reference 裡（K5、K6）。
- **只有打字列的 popup**（text、password、number）：`?` 在那裡是字元（K8），所以它的 hint 要列出全部操作，而且 80 欄放得下
  （[components/layout/popup](../components/layout/popup-zh_TW.md) 的 hint）。
- **letter hotkey 是某個清單裡某一列的捷徑，不是額外的功能**。只能靠熱鍵觸發、哪裡都
  找不到的動作是違反。

判斷一個動作該進哪一區，只看**作用對象**，不看它重不重要（Principle P3）。

**為什麼**：沒看過熱鍵的新使用者只靠 `Space` 與 `?`，就要能在每個地方做完所有事。
只要有一個動作要靠事先學，「不看文件就能用」就破了一個洞。

### M4 global operation popup 與 key reference `固定`

**global operation popup**（能做）

- 從 Space menu 的 global 列（M2）按 `Enter` 打開，疊在 Space menu 上；是一種 menu（F1），
  列出 app **全部**全域動作，`j/k` 選、`Enter` 或熱鍵執行。離開 app 必須在這裡（K9）。
- `Esc` 回到 Space menu（F4）；執行了會關掉整疊的動作，照 T1。
- 目前所在畫面的切換列照 M6 停用（例：在 `[M]anage` 上的 `[M]anage`）。
- **global 熱鍵**：沒有 popup 開著時，global operation popup 裡的熱鍵在 panel 上也能直接按。跟 panel 自己的熱鍵撞鍵時，
  panel 的優先，那個 panel 的 key reference 不列被蓋掉的 global 鍵。`q` 照 K9。

**key reference**（能讀）

- `?` 打開（K6）。唯讀、可以捲動，沒有游標、不能執行，不是 menu。
- 列什麼見 K6；樣子見 [components/dialog/note](../components/dialog/note-zh_TW.md)。

**為什麼**：只能讀的說明頁不能取代可執行的清單（Principle P2）—— 能做的事都在 `Space` 與
global operation popup，一步就能執行；`?` 是在旁邊對照的常駐 cheatsheet。讀與做分成兩個框，
各自只屬於一類（F1）。全域動作集中在一個 popup，就不用在每個 Space menu 各列一次；熟了的人在 panel 上直接按 global 熱鍵，
不用每次開兩層 menu。

### M5 每一列 = 名稱 + 說明，熱鍵用 `[]` 標出 `固定`

menu 的每一列左邊是**動作名稱**，右邊是**一句單行說明**：

```
 item operation
 [o]pen                        open it with the OS default app
 [r]ename                                    this item, in place
  ───────────────────────────────────────────────────────────
 panel operation
 [/] Search                                everything under here
  ───────────────────────────────────────────────────────────
 Global operation                      actions for the whole app
```

熱鍵的寫法全 app 一套（menu、footer、panel hint、popup hint、key reference，以及 README）。label 裡的標記：

| 情境 | 寫法 |
|---|---|
| 單一字母，是 label 的第一個字母 | 原地加括號：`[r]ename`、`[D]elete` |
| 單一字母，在 label 中間 | 原地包：`UR[L]` |
| 字母不在 label 裡 | 放前面：`[n] New` |
| 含 modifier | `[Alt-t]erm` |
| 多字元 | `[go]to` |
| 數字 | 一律放前面：`[3] Favorites`，不嵌進字裡 |
| core key | 放前面：`[Enter] Edit` —— 標的是在 panel 上按這個鍵就是這個動作；在 menu 裡 `Enter` 照樣執行 cursor 那一列 |
| 沒有熱鍵 | 不加括號 |

- **括號裡印的就是要按的鍵，大小寫算數**：`[A]dd` 是 `Shift-A`。
- label 本身已經寫出鍵的列（`[/] Search`）不再括一次。
- 不能只用顏色或 glyph 暗示「這是熱鍵」，要顯式標出來。
- 說明寫什麼由 app 決定，但必須是單行。

**鍵名**（畫面上所有地方與 README 都一樣）：

- 用鍵帽上的名字，大駝峰、不自創縮寫：`Esc`、`Tab`、`Enter`、`Space`、`Backspace`、`Delete`、`Home`、`End`、`PgUp`、
  `PgDn`；方向鍵 `↑` `↓` `←` `→`。
- 字母照實際要按的大小寫：`q`、`A`（就是 `Shift-A`）、`Alt-z`。`Ctrl` 後面的字母一律大寫（`Ctrl-C`、`Ctrl-U`）：終端機
  分不出 `Ctrl` 組合的大小寫。
- modifier 用 `-` 連接：`Alt-t`、`Ctrl-C`、`Shift-Tab`、`Alt-Esc`。
- 幾個鍵做同一件事用 `/`：`j/k`、`h/l`；範圍用 `–`：`1–9`。

**依位置的寫法**：

| 位置 | 寫法 | 例子 |
|---|---|---|
| label（menu 的列、statusbar chip、panel 標題） | 上表的括號標記 | `[r]ename`、`[Alt-t]erm` |
| 句子（空狀態、toast、錯誤訊息，以及 menu 與 key reference 說明欄裡提到的鍵） | 鍵一律加方括號 | `Press [A] or [Space]`、`see App Log [!]`、`next tab [h]/[l]` |
| hint、footer | `鍵:說明`，冒號前後不空格，項目之間一個空格 | `Enter:delete Esc:cancel` |
| key reference | 兩欄：鍵、說明；鍵不加括號、不加冒號 | 鍵欄 `Esc`、說明欄 `close this popup` |

- hint 與 footer 的鍵和說明用不同顏色分開：鍵一個色，冒號與說明另一個色（見 [components/color](../components/color-zh_TW.md)）。說明可以是幾個詞，項目靠鍵的
  顏色分得出來。
- **README**：內文提到的鍵用 Markdown 的 code 標（`` `Enter` ``、`` `Ctrl-C` ``），不加方括號；鍵名與寫法照上面。引用畫面上的
  label 照畫面寫（`[A]dd`）。
- **別的工具自己的按鍵**（例：tmux 的 `prefix l`、`C-a x`）照那個工具的寫法：使用者要把它打進那個工具的設定、或對照它的文件。

**為什麼**：名稱回答「這是什麼動作」，說明回答「它會對什麼做什麼」—— 同一個動詞在
不同 panel 可能意義不同（刪檔案還是取消收藏？）。說明寫不進一行，通常是動作的
命名有問題。數字不嵌進字裡，因為 `432hz` 會被畫成 `4[3]2hz`。

### M6 暫時不能執行的動作：停用 `固定`

- **對象不存在**：那一列（或那一區）不出現（M2）。
- **對象存在、但現在不能執行**：列照樣出現、用停用色（[components/color](../components/color-zh_TW.md)），說明欄維持原本那句，
  不另外寫原因；cursor 跳過它，按熱鍵也不作用。
- **`?` 的 key reference 照同一套**：對象存在、現在不能按的鍵照樣列出、用停用色；對象不存在就不列。下框 hint 與 footer
  空間有限、常駐畫面，只列現在按得了的鍵也可以，由 app 決定。
- key reference 裡另外加標題、說明**別的 surface** 的一段（例：sshu 清單上 `?` 裡的 `ssh grid`，格子裡看不到 key
  reference），不算這個 surface 的鍵，照常顯示。

**為什麼**：藏起來的動作，使用者會以為 app 不支援；停用讓使用者知道「有這件事，只是
現在不行」。不另寫原因，是因為原因千變萬化，塞進單行說明會讓每一列的字數失控（M5）。cursor 跳過它，是因為停上去
也只是按了沒反應。

### M7 panel 上的入口永遠有回應 `固定`

focus 在 panel 上時，`Space` 與 `?` 按下去都要有反應：`Space` 打開 Space menu（global 那一列永遠在，menu 不會是空的，
M2），`?` 打開 key reference。在 popup 上，永遠有回應的是 `?`（K6）。

**為什麼**：按下去沒反應，使用者會以為鍵壞了，而不是「這裡沒事可做」。

### M8 其他分組 menu：cursor 相關的放最前 `概念`

Space menu 以外的 menu（例：排序選擇器、open-with 清單）若要分組，第一組是跟當前
cursor 相關的動作，其後每組加上說明類型的標題。不需要分組時直接列出。

**為什麼**：使用者打開 menu 時，最常找的是「對著我選的這個東西」能做什麼 —— 跟 Space menu 把 item 區放最前面是同一個
理由（M2）。分組的 menu 都照這個順序，使用者不用每個 menu 重新找。

### M9 同一個鍵有兩處指示時，標出哪個會觸發 `固定`

同一個熱鍵在不同 panel 做不同事、而兩處指示**同時看得到**時，要讓使用者一眼看出**在當前
focus 按下去會觸發哪一個**：會觸發的那個亮、不會的那個暗（[components/color](../components/color-zh_TW.md)）。

**為什麼**：兩個一樣的鍵同時出現在畫面上，使用者無從判斷按下去會做哪一件。亮的就是有 focus 的（Principle P6）。

---

## L 版面

### L1 最低支援 80 欄 × 40 列 `固定`

在 **80 欄 × 40 列**下，app 必須能完成所有核心任務。這大約是 16:9 螢幕切一半（8:9）
開一個終端機視窗的大小。panel 怎麼拆由 app 決定；放不下所有 panel 時怎麼畫，見
[components/layout/screen](../components/layout/screen-zh_TW.md) 的窄寬。

**為什麼**：終端機常常只佔半個螢幕 —— 另一半是編輯器、瀏覽器或另一個終端機。只有全螢幕
才好用的 TUI，在日常的分割視窗裡就不能用。

### L2 寬度不隨內容浮動 `固定`

標題、statusbar、chip 等動態文字必須用固定寬度的欄位或 padding，寬度不能跟著內容
長度變。

**為什麼**：寬度一浮動，主畫面跟著左右晃，popup 開關時整個畫面在抖。

### L3 固定列數的 chrome `固定`

footer、statusbar、tab 列等常駐列的**列數由 app 決定，一旦決定就鎖死**，不能因為
內容多寡改變。內容放不下就截斷或從尾端捨棄，不折行。

**為什麼**：chrome 多一列，主畫面就少一列，整個 layout 連鎖位移。穩定永遠優先於省空間。

### L4 每一列剛好等於終端機寬度 `固定`

畫面上的每一列都剛好等於終端機寬度，不多不少。

**為什麼**：多一格，終端機就折行，整個畫面錯位；少一格，殘影留在畫面上。CJK 字元與
icon 的寬度估錯是最常見的來源。

### L5 Focus 看得出來，而且不位移 `固定`

focus 所在的 surface 必須一眼可辨，而切換 focus **不能讓任何內容位移**。

- **focus 不能只靠顏色分辨**：要有顏色以外的差別（例：線型）。模式會把外框換成模式色（K11），只靠顏色的話，一進模式
  就看不出 focus 在哪。樣子見 [components/layout/panel](../components/layout/panel-zh_TW.md)。

**為什麼**：使用者要知道按鍵會送到哪裡；而 focus 一換畫面就跳，眼睛就得重新定位。

---

## F Popup

### F1 popup 分七類，一個時間只屬於一類 `固定`

家族的 popup 只有這七類，每一類的按鍵意義固定：

| 類別 | 使用者能做什麼 | 例 |
|---|---|---|
| **menu** | 沒有搜尋的清單：`j/k` 移動 cursor，`Enter` 或熱鍵執行那一列 | Space menu、global operation popup、排序選擇器、工作清單（`Enter` 打開那一列的全文） |
| **confirm** | 讀一段提醒或警告，`Enter` 接受、`Esc` 取消（F6）；要先看的內容在上、問句最後 | 刪除前的確認、離開的確認、帶著明細的「連線到 X？」 |
| **input** | 輸入或選出一個值，確定後寫回去；一個 popup 一個值。打字列上是輸入態（K8），其他部分照 K1 | 重新命名、網址列、select、datetime picker |
| **form** | 一列一個值；`Tab` 一次跳一欄、hjkl 一個一個項目移（K12），`Enter` 對 focus 的項目做事（打開那一欄的 input popup、選 radio、翻 checkbox、按按鈕），按鈕送出（[components/dialog/form](../components/dialog/form-zh_TW.md)） | sshu 的 Host 表單、webu 的 Sign in 與 Add bookmark |
| **note** | 唯讀，可以捲動（K12）；沒有可用 `Enter` 執行的選項清單 | key reference、YAML 檢視、App Log、error popup |
| **toast** | 從下方彈出的短訊息，`Esc` 或時間到就收掉；除了 `Esc`，按鍵都穿過它 | 「已複製」、操作失敗 |
| **terminal** | 跑在框裡的子程序，按鍵都給它，只有出口鍵與 app 保留的組合鍵屬於 app（K10） | kbu 的 Alterm、filu 的 shell |

- **note 可以有自己的熱鍵與模式**：例如 YAML 檢視的 `/` 搜尋、`y` 複製、`v` 選取（模式，K11）。熱鍵揭露在下框 hint 與
  `?`；但一旦有可用 `Enter` 執行的選項清單，它就是 menu，不是 note。
- **menu 的 `Enter` 可以打開那一列的全文**：有 cursor、本身沒有別的動作的清單（例：工作清單），`Enter` 開一個 note 顯示
  那一列的完整內容，它仍是 menu。
- **confirm 可以帶一段回答前要看的內容**：問句是 confirm 存在的理由，上面可以放回答前要看的資訊（例：「連線到 X？」上面是
  X 的明細），內容長時用 `j/k` 捲動；它仍然只是 confirm，不是 note 加 confirm，不必拆成兩個 popup。
- **一個 popup 可以依階段換類別，但同一時間只屬於一類**。例：finder 打字時是 input，結果清單取得 focus 時是 menu；
  `Tab` 在打字與清單之間切換 focus，`Esc` 關掉整個 finder（K4：階段不是一層）。旁邊的預覽不取得 focus，不算另一個 surface。
  **focus 在哪一邊要看得出來**：只有有 focus 的那一邊是亮的（Principle P6；樣子見 [components/input/finder](../components/input/finder-zh_TW.md)）。
- **清單加搜尋就是 finder**：一般的 finder、select、checkbox popup、file-picker 都是 finder 的一種 —— 打字列是輸入態，清單是選；
  打字列的按鍵見 [components/input/finder](../components/input/finder-zh_TW.md)。它們仍是 input，不是同時兩類。沒有搜尋的清單是 menu。
- **toast 不是一層**：不觸發淡化（F8）、不算層色的層數；但 `Esc` 先收掉它（K4）。
- **多步驟的流程，每一步是自己的 popup**：例如排序先選欄位、再選方向，是兩個疊起來的 popup（F4 保留 source），不在同一個框裡
  換內容 —— 每一步有自己的 UX，也有自己打開時定好的大小（F7）。
- 不屬於這七類的：splash（S 章）、app 自己畫成框的 panel 內容（例：webu 頁面自己的彈窗，webu 的偏離）。

**為什麼**：類別就是使用者對「這個框裡按鍵會怎樣」的預期。家族只有七類、每類意義固定，換一個 app
也不用重學；同一時間混兩類的 popup，會讓同一組鍵在框裡有兩種可能。

### F2 開關都有動畫 `固定`

popup 打開與關閉**都要有動畫**。長度全家族一樣（見 [components/layout/popup](../components/layout/popup-zh_TW.md)）；
動畫的形式由 app 決定。

**為什麼**：沒有動畫，popup 是「突然出現、突然消失」，使用者感受不到它疊上來、退下去
的層次變化。長度一樣：同一個動作在家族每個 app 花一樣久，換 app 時節奏不變。

### F3 `Esc` 立刻關閉任何 popup `固定`

任何看得到的 popup —— 包括會自動消失的 toast —— 按 `Esc` 都**立即**開始關閉，不必等 toast
倒數結束。關閉照常有動畫（F2）；已經在跑關閉動畫的 popup 不再理會 `Esc`，也不再接收其他按鍵。

**例外**：

- focus 在 PTY 裡時，`Esc` 屬於子程序（K10）；terminal 用出口鍵離開。這時 toast 只能等時間到收掉。
- textarea 在寫入狀態時，`Esc` 是離開寫入狀態、進入移動狀態（K8）。
- 內容改過的表單與 textarea，`Esc` 先開 confirm 問要不要放棄（[components/dialog/form](../components/dialog/form-zh_TW.md)）。

**為什麼**：使用者沒有等倒數的義務。已經在關的 popup 再收一次 `Esc`，或還吃其他鍵，使用者的
下一個按鍵就會送錯地方。PTY 與 textarea 的 `Esc` 本來就是子程序與寫字要用的；改過的內容一次丟掉代價高，所以多問一次。

### F4 預設保留 source `固定`

從 popup A 開出 popup B 時，A 預設留在底下；取消 B 回到 A。多層時也一樣：`Esc` 只關最上層，
底下的階層原樣呈現（K4）。

**為什麼**：使用者沒有撤掉 A，只是在 B 上做了一次互動。取消 B 卻連 A 一起不見，
使用者要重新走一遍。（完成 B 之後 A 還要不要留，見 T1。）

### F5 錯誤立刻看得到，但不擋住 app `概念`

錯誤必須立刻出現（toast 或 popup），`Esc` 可關，且**不能阻塞 app**。有沒有錯誤歷史
可查由 app 決定。

**為什麼**：看不到的錯誤等於沒發生；擋住 app 的錯誤讓使用者無法處理錯誤本身。

### F6 Confirm：`Enter` 接受、`Esc` 取消，說出後果 `固定`

- **哪些動作要 confirm 由 app 決定**，跟動作可不可逆無關。一個動作一旦決定要 confirm，
  每次都 confirm。例外：經由 picker 明確選定的那一次，可以算已確認（例：從「開啟方式」清單選了預設 app），由 app 決定。
- `Enter` 接受，`Esc` 取消（K3、K4）。confirm 自己的熱鍵（例：`y` / `n`）可以有，要列在
  confirm 的 `?` help 裡（K6）。
- 提示寫出**接受會做的事**（動詞與對象），而不是抽象的 OK。
- confirm 不能被誤觸完成（例：滑鼠點一下不能等於接受）。
- 樣子見 [components/dialog/confirm](../components/dialog/confirm-zh_TW.md)。

**為什麼**：使用者按 `Enter` 前要知道後果。要不要停下來確認，取決於這個動作對使用者
的份量 —— 開一個外部程式、切斷一條 session、刪一個檔案，份量由 app 最清楚，不是一條
「可逆就不用問」的規則能判斷的。

### F7 popup 的尺寸與位置 `固定`

- **寬度**，打開時定好，開著時不變：
  - **內容的寬度打開時就確定**（例：有長度上限的輸入、confirm、menu、key reference、toast、error popup、datetime picker、
    color picker）：最寬的那一列 + 4（左右各一格框、一格留白），至少放得下標題與 hint，最寬不超過 `min(terminal 寬 − 2, 120)`。
  - **內容的寬度不確定**（例：自由打字的 text、網址、串流內容、搜尋結果、表單）：`min(terminal 寬 − 2, 120)`。
  - 水平置中。
- **高度**：依內容，**打開時定好**，之後不跟著內容伸縮；最高是畫面高度 − 2（最上面一列與 footer 永遠看得到），
  超過就在框裡捲動。只有兩種情況允許開著時改變高度：
  - **loading**：打開時內容還不確定（串流、載入中）的 popup，在 loading 期間高度可以變。loading 結束，高度就定下來。
  - **使用者操作造成的改變**：使用者在這個 popup 裡的動作讓列數改變（刪了一列、選了一項後多出一列、打字篩選候選），
    高度**可以**跟著變 —— 這是使用者預期的改變；app 也可以維持原高。原則是揭露的資訊要正確。
- **loading 一定要揭露**：popup 在 loading 時，標題後面**一定**放一個輪轉的 loading icon（規格見 [components/layout/popup](../components/layout/popup-zh_TW.md)），跟高度會不會變無關；
  loading 結束 icon 就消失。這裡的 loading 指的是**整個 popup** 的內容還沒到（例：清單的項目還沒載完）。若只是**某一個
  項目**本身是持續進來的資料流（例：一筆一直有資料的連線），loading 的是那個項目，不是 popup —— 那個項目怎麼揭露由 app 決定。
- **位置**：垂直置中。toast 例外：在畫面下方置中，下框貼在 panel 下框的上面（[components/dialog/toast](../components/dialog/toast-zh_TW.md)）。
- **值可能不合格的 popup 預留一列錯誤列**（input popup、表單）：打開時高度就含一列錯誤列，沒有錯誤時空白；值不合格時錯誤
  寫在這一列（K3），框的高度不變。不會不合格的（例：多行編輯器）不必預留。動作本身失敗（寫檔失敗、遠端拒絕）不寫錯誤列，
  開 error popup（[components/layout/popup](../components/layout/popup-zh_TW.md)）。
- **terminal 類例外**：寬度 `terminal 寬 − 2`，不受 120 欄上限；上面留著 statusbar 或畫面 chip 列，下面一直到畫面最後一列、
  蓋掉 footer —— 子程序需要空間，而在 PTY 裡不需要外面的 footer（[components/dialog/terminal](../components/dialog/terminal-zh_TW.md)）。

**為什麼**：每個 popup 依內容隨時伸縮，打開前無法預期它長什麼樣，內容一變框就跳（L2）。寬度只有兩種算法、打開時定好，
框的樣子永遠可以預期；內容確定的不必撐到全寬，寬螢幕上不空、窄螢幕上不擠；120 欄的上限讓寬螢幕上的 menu 名稱與說明
不至於相隔太遠。錯誤列預留在框裡，而不是另開一個 popup：使用者修正時錯誤一直看得到，也不必先多按一次鍵關掉它。

### F8 層疊時，最上層以外全部淡化 `固定`

有 popup 開著時，**最上層那個 popup 以外的一切** —— 底下的 popup 與整個 base 畫面 —— 都淡化。
連續開 popup、popup 裡再開 popup 時也一樣：永遠只有最上層是亮的（Principle P6）。

- 底下的串流內容（log、遠端 session）與警示色也一起淡化：T2 管的是失焦，不是被蓋住。
- **淡化的做法：把每一個顏色 —— 前景與背景 —— 都往底色淡化，形狀與版面原封不動。** 不可以剝掉顏色重畫、不可以丟掉
  背景、不可以把所有前景換成同一個淡色：那會拆掉靠背景畫出來的元素（powerline 膠囊的本體、cursor bar、選取反白）。
  層色、警示色、串流內容照同一個淡化，自然成為各自顏色的淡化版本。計算方式見 [components/color](../components/color-zh_TW.md)。
- **對畫好的畫面淡化一次**：失焦的 panel 已經淡過（T2），在 popup 底下會再暗一點 —— 看得出 popup 打開前 focus 在哪。
- **toast 不觸發淡化**：除了 `Esc` 它不收鍵（F1），不是一層。
- **邊框也一起淡化，但保留層色**：底下那幾層 popup 的邊框畫成它自己層色（components/color）的淡化版本，不是統一的淡色 ——
  暗了，但仍看得出它是第幾層。

**為什麼**：popup 寬度不一定一樣，上層仍可能蓋住下層的邊界，看框不一定分得出層次；亮暗是分層次的主要線索，
也正是 P6 的意思：只有正在操作的那一層是亮的。

---

## X Mouse

### X1 Mouse 可有可無 `固定`

沒有 mouse 也必須能完整操作 app。

**為什麼**：mouse 不是終端機的一等輸入，很多環境（tmux、SSH、螢幕閱讀）根本沒有。

### X2 Mouse 只是鍵盤的對應 `固定`

有做 mouse 時，每個 mouse 動作都對應到一個鍵盤動作，**不能有只有 mouse 能做的事**。

**為什麼**：mouse 應該是「鍵盤的另一種按法」，不是「另一套要學的東西」。

---

## T 時間軸

這一章的規則在截圖上看不出來，只存在於使用流程裡 —— 要 app 長到一定完整度才會浮現，會隨實作持續增加。

### T1 完成 target 之後，source 還有意義嗎？ `概念`

預設保留 source（F4）。只有在功能上明確判斷「使用者完成 target 之後，source 已經
失去意義」，target 才在進場前清掉 source：

| target | 清掉 source？ | 判斷 |
|---|---|---|
| 短的 confirm / 訊息 | 保留 | 使用者可能想回原 menu 繼續或取消 |
| 選一個值（input popup、select）寫回表單或 picker | 保留 | 值寫回去之後，使用者還在 source 上繼續 |
| 長時間的 session（shell、編輯器） | 清掉 | 從 session 出來時注意力已轉移，舊 menu 浮著讓人恍神 |
| 大幅切換 context（drill-down、換頁） | 清掉 | 底下的畫面已經換了，舊 menu 的對象不在了 |

**為什麼**：保留是安全的預設，清掉要有理由 —— 否則使用者完成一件事就找不到回去的路。而「該不該清」寫不成通則：
code 裡兩者長得一樣，截圖上也看不出來，只能從「使用者用完 target 之後，心裡還想不想看 source」推演。

### T2 失焦的 panel 變暗，串流內容除外 `固定`

失焦的 panel **用 F8 同一套淡化把內容變暗**（邊框照 components/color 的失焦邊框）；**串流內容（log、即時輸出、遠端 session）
失焦時不變暗**。popup 蓋在上面時例外：那時注意力在 popup 上，底下一切照 F8 淡化。

**為什麼**：變暗的意思是「焦點不在這，晚點再看也行」—— 亮的就是有 focus 的（Principle P6）。串流內容沒有晚點 —— 資訊正在
流過，變暗等於切斷使用者用餘光掃過的路徑。這也是「規則服務 UX」（Principle P0）的典型
例子：「失焦變暗」的 origin UX 是「不搶焦點」，串流的 UX 是「用餘光看更新」—— 兩個目標
剛好落在同一個 panel 上，規則該擴充，而不是犧牲串流。

---

## S Splash

splash 是 terminu family 共同的彩蛋，也是 tdp 裡**唯一刻意不揭露**的東西。揭露規則
（M1、M3、M4）與 core key 規則（K1）對它不適用；它也不是 popup，F 章不適用。
splash 只記載在 tdp，不寫進任何 app 的 README 或 app 內的 menu、help。

### S1 每個 app 都有 splash，用 `V` 打開 `固定`

每個 terminu app 都有 splash，在 panel 上按 **`V`** 打開。`V` 保留給 splash：

- 某個 panel 的 panel operation 真的需要 `V` 時，**該 panel** 可以把 `V` 給 app 自己用，
  那個 panel 上就叫不出 splash。
- 但 app 裡**至少要有一個 panel** 的 `V` 仍然是 splash。

**為什麼**：彩蛋要在家族每個成員都按得出來，才是「家族的」彩蛋；而某些 app 的領域動作
確實需要 `V`（例：選取模式），讓一個 panel 讓出去，比讓整個 app 失去彩蛋好。

### S2 不揭露 `固定`

splash 不出現在 Space menu、global operation popup、key reference、footer、panel hint，也不寫進 README。

**為什麼**：彩蛋被列出來就不是彩蛋了。它是 tdp「揭露是唯一機制」（Principle P2）的唯一
例外，而且只有這一個 —— 所以寫在這裡，不寫在任何 app 裡。

### S3 任意鍵只關掉 splash `固定`

splash 開著時，**任何鍵都只會關掉它**，包括 `q`、`Ctrl-C`、`Esc`、`Space`、`?`；那個鍵
不會再做別的事。第一次按 `Ctrl-C` 只關 splash，不離開 app。

**為什麼**：使用者看到一個沒見過的畫面，第一反應是隨便按個鍵讓它消失。那一鍵若同時
觸發了別的動作（離開、開 menu），彩蛋就變成陷阱。

### S4 只在 panel 上、只在按了之後 `固定`

- 啟動時不播。
- 只能在 panel 上用 `V` 叫出來；popup 開著、輸入態、PTY 裡按 `V` 都不叫出 splash
  （輸入態的 `V` 是字元，K8；PTY 的 `V` 屬於子程序，K10）。

**為什麼**：啟動就播的 splash 是每次都要等的開場，不是彩蛋；而在 popup、輸入框、PTY 裡
冒出來，會打斷使用者正在做的事。

### S5 內容是家族 icon `固定`

splash 畫的是該 app 的 `docs/icon.svg` —— terminu family 的 mark —— 一格對一格，帶揭露
動畫。動畫怎麼跑由 app 決定。

**為什麼**：splash 是家族的簽名。每個成員畫的都是自己那一版的家族 mark，按下 `V` 就認得出
這是同一家的東西。

---

## E App 與環境

app 在畫面以外的事：命令列、環境變數、需求、icon 的寬度、發布、文件。這一章不是畫面上的 UX；它的理由是家族一致 ——
五個 app 用同一套做法，使用者裝過一個就會裝其他的，也知道去哪找設定與資料。

### E1 命令列：`version` 與 `help` `固定`

每個 app 都要有：

- **`<app> version`**：印出版號。`--version`、`-v` 可以當別名。
- **`<app> help`**：印出命令列的用法（跟 app 裡 `?` 的 key reference 無關）。`-h`、`--help` 可以當別名。

其他指令（例：`filu iconwidth`、`locku lock`、`webu <網址>`）由 app 決定。

**為什麼**：使用者遇到一個命令列工具，第一個會試的就是 `help` 與 `version`。五個 app 都用同一組，問一個 app 問得到，
問每一個都問得到。

### E2 環境變數的命名 `固定`

`<大寫 app 名>__<變數名>` —— app 名後面兩個底線，變數名全大寫、單字之間一個底線（例：`FILU__ICON_WIDTH`、
`KBU__ALTERM_LOGIN_SHELL`）。app 自己讀的變數（含測試用、傳給自己子程序的）都照這個寫。共用的名字：

| 變數 | 意思 |
|---|---|
| `<APP>__CONFIG` | 設定**目錄**（設定檔在裡面） |
| `<APP>__STATE` | 狀態目錄（app 有另外存狀態時） |
| `<APP>__DATA` | 資料目錄 |
| `<APP>__CACHE` | 快取目錄 |
| `<APP>__ICON_WIDTH` | icon 佔幾格的手動覆寫（E5） |
| `TERMINU__ICON_WIDTH` | 家族共用：有 PTY 的 app 設給子程序，告訴它 icon 佔幾格（E5） |

例外：給別的程式讀的變數照對方的要求（例：sshu 經 ssh 帶到遠端的 `LC_SSHU_COLORTERM` —— OpenSSH 預設只轉送 `LANG` 與
`LC_*`）。改名時不留舊名。

**為什麼**：一眼看出變數屬於哪個 app，`TERMINU__` 一看就是全家族共用的。用兩個底線分開 app 名與變數名，因為變數名
本身也有單底線（`ICON_WIDTH`），兩個底線不會跟它混在一起。

### E3 設定與資料的位置 `固定`

| 什麼 | 預設位置 | 覆寫（E2） |
|---|---|---|
| 設定 | `$XDG_CONFIG_HOME/<app>`（fallback `~/.config/<app>`） | `<APP>__CONFIG` |
| 狀態（app 有另外存時） | 設定目錄裡 | `<APP>__STATE` |
| 資料 | `~/.<app>/` 底下 | `<APP>__DATA` |
| 快取 | 系統的快取目錄（macOS `~/Library/Caches/<app>`；Linux `$XDG_CACHE_HOME/<app>`，fallback `~/.cache/<app>`） | `<APP>__CACHE` |

**為什麼**：五個 app 放在同一套位置，使用者知道去哪裡找、要備份哪些。快取放在系統的快取目錄，清快取的工具才找得到它，
也不會被當成要備份的資料。

### E4 需求：Nerd Font 與 truecolor `固定`

- 需要 Nerd Font；PUA glyph 在程式碼裡寫成 code point。
- 需要 truecolor terminal（24-bit 色）：catppuccin 的淡色與 components/color 的層色漸變在 256 色下分不出來，淡化也一律輸出 24-bit（components/color）。README 的需求段跟 Nerd Font 並列寫明。

**為什麼**：家族的 icon、loading icon、radio 與 checkbox 的 glyph 都是 Nerd Font 的字；truecolor 的理由寫在上面。

### E5 icon 的實際寬度 `固定`

有些字型讓 icon 佔兩格（游標前進兩格），量寬度的函式卻量成一格，框線就歪。要量的是**游標實際前進幾格**：
icon 看起來比一格寬、但游標只前進一格的字型（glyph 溢出到隔壁），照一格算。

- **執行時量**：app 啟動時探測（CPR：印一個 icon、問游標位置）。所有量寬度的地方（補空白、截斷、置中、並排、框線、
  疊 popup）都走同一個顯示寬度函式。
- **覆寫與順序**：取 icon 寬度的順序是 `<APP>__ICON_WIDTH` → `TERMINU__ICON_WIDTH` → 探測。探測只在 unix 做；Windows
  預設一格，靠環境變數覆寫。
- **在別的 app 的 PTY 裡**：探測由外層 app 的終端模擬器回答，它把 icon 當一格，量不到真的寬度。所以有 PTY 的 app 開子程序時，
  在子程序的環境設 `TERMINU__ICON_WIDTH=<自己用的格數>`。這樣家族裡任何一個 app 跑在另一個的 PTY 裡都對（filu 在 kbu 的
  Alterm 裡、kbu 在 filu 的 shell 裡）。環境變數過不了 ssh，遠端巢狀要靠 app 自己的通道（sshu 的巢狀指令通道）。
- **疊 popup 不能當掉**：popup 可能比畫面寬或高（調整終端機大小的那一格還是舊尺寸）：起點取 0、超出畫面的部分切掉，
  **不可以 panic**；寬、高兩邊都比畫面大時也一樣切，不可以把整個框原樣交出去。
- **測試**：L4 的畫面測試也跑一次「icon 佔兩格」，每一種 popup 各開一次，量單獨的框與疊上去的整個畫面；邊界要含 popup
  比畫面寬、比畫面高、兩邊都大三種情況。

> **實作參考（不是規定）**：filu `internal/ui/width.go` —— `isWideIcon()`、`dispWidth()`、`dispClip()`、`padDisp()`、
> `dispCutLeft()`、`compositeDisp()`（取代 overlay 的 `Composite`，介面相同）、`centerDisp()`（取代 `lipgloss.Place`）、
> `joinH()` / `joinV()`（取代 `lipgloss.JoinHorizontal` / `JoinVertical`）；探測在 `iconwidth_unix.go` 的 `DetectIconWidth()`，
> 在 `tea.NewProgram` 之前呼叫；測試照 `d6_test.go` 與 `TestD6CompositeDispOversized`。做完可以這樣驗：`internal/ui` 裡除了
> 寬度函式本身，找不到 `lipgloss.Width`、`lipgloss.Size`、`lipgloss.Place`、`ansi.StringWidth`、`ansi.Truncate` 的呼叫。

**為什麼**：框線歪掉，整個畫面就讀不下去；而同一個字型在不同終端機上，游標前進的格數可能不同，只能在執行時量。

### E6 發布、測試與家族資產 `固定`

- 單一靜態 binary，goreleaser 建置；`install.sh` / `uninstall.sh`（`curl | sh`、免 sudo），
  另發到 Homebrew tap `vulcanshen/homebrew-tap`。
- 跨尺寸的畫面測試：多種終端機尺寸下，每一列都剛好等於終端機寬度（L4）。
- `docs/icon.svg` 是家族 mark；splash（S 章）由它逐格畫出，用測試守住兩者一致。
- demo gif 用 VHS 錄，腳本放在 `.local/demos/`（README 放幾張見 E7）。

**為什麼**：五個 app 同一種安裝、移除與發布方式，使用者裝過一個就會裝其他的。畫面測試守住 L4；icon 與 splash 的測試
讓換 icon 時不會忘了 splash。

### E7 文件 `固定`

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

README 講 icon 寬度的地方（通常在前置需求的 Nerd Font 那一段），寫出 `<APP>__ICON_WIDTH` 與 `TERMINU__ICON_WIDTH` 兩個變數，並說明
後者是全家族共用的：設一次，家族每個 app 都讀到；在家族 app 的 PTY 裡跑時，外層 app 會替它設好（E5）。寫法不限（表格或一句話）。
不舉「一定佔兩格」的字型當例子 —— 同一個字型在不同終端機上游標前進的格數可能不同。

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

**為什麼**：README 是工具的介紹，使用者要的是「這是什麼、怎麼裝、怎麼用」；開發者的備忘另外放，兩邊都好找。

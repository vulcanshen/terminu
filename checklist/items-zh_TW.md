# terminu checklist：條目

**Language**: [English](items.md) · 繁體中文

tdp v1.0.1 的條目。每一欄的意思與適用見 [README-zh_TW.md](README-zh_TW.md)。

## principle — P0–P6

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| P3-1 | P3 | 對整批標記的項目做事的動作放在 panel operation | 標記 | 標記幾列後按 `Space`，那個動作在 panel operation 區 |
| P3-2 | P3 | 只跟另一個 panel 有關的動作，只出現在它所屬 panel 的 Space menu：不放進當前 focus 的 panel，也不升格成 global | 多 panel | 看每個 panel 的 Space menu 與 global operation popup，沒有只作用在別的 panel 的動作 |
| P3-3 | P3 | 切換畫面是 global operation，列在 global operation popup | 多畫面 | `Space` → `Global operation`，裡面有切到各畫面的列 |

## principle — 術語

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| terms-1 | terms.1 | focus 不會停在常駐顯示區（footer、statusbar、畫面 chip 列）上 | 都要 | 連按 `Tab`、數字鍵，focus 只在 panel 之間 |
| terms-2 | terms.8 | 版面的切換（例：zoom）由它自己的鍵還原 | 都要 | 切換之後按它自己的鍵，版面回到原樣 |

## rules — 引用

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| references-1 | 引用 | app 的檔案（README、CLAUDE.md、程式註解）引用 tdp 的條目時，一律寫成 `tdp` 加編號（例 `tdp K4`、`tdp panel.1`）；`Rules K4` 與沒加前綴的 `K4` 都不算 | 都要 | 讀檔案：README、CLAUDE.md 與程式註解裡提到 tdp 條目的地方 |

## rules — K Core key

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| K1-1 | K1 | `Tab` `Enter` `Esc` `Space` `?` `!` `q` `1`–`9` 在每一個 surface 都是 K1 表上的意義，例外只有輸入態、PTY、模式、表單上的 `q` 與表單的打字說明 note | 都要 | 在每種 panel 與 popup 上按這幾個鍵，沒有哪裡拿去做別的事 |
| K1-2 | K1 | app 自訂的 core key 在所有 surface 意義不變 | 都要 | 在每種 panel 與 popup 上按那個鍵，做的是同一件事 |
| K1-3 | K1 | letter hotkey 不佔用 K1 表上的鍵 | 都要 | 讀程式或看所有 menu、key reference：沒有熱鍵用 `Tab` `Enter` `Esc` `Space` `?` `q`（`[Enter] Edit` 這種標 core key 本身動作的不算；數字見 K1-7） |
| K1-4 | K1 | panel 上（沒有 popup 開著時）按 `1`–`9`，focus 跳到目前畫面框上標 `[N]` 的那個 panel | 多 panel | 在 panel 上按 `1`、`2`…；多畫面的換到別的畫面再按，跳的是那個畫面的 panel |
| K1-5 | K1 | 每個畫面的 panel 各自從 `[1]` 編號 | 都要 | 看每個畫面 panel 框上的號碼，從 `[1]` 起 |
| K1-6 | K1 | 畫面上沒有那個號碼的 panel 時，按那個數字不作用 | 都要 | 在 panel 上按比 panel 數大的數字，什麼都沒發生 |
| K1-7 | K1 | app 不在 panel 上把數字登記成熱鍵 | 都要 | 讀程式或看 panel 的 Space menu、key reference：沒有數字熱鍵 |
| K1-8 | K1 | 用數字的 global 熱鍵只能在 global operation popup 裡按；在 panel 上按那個數字是跳 panel | 都要 | 在 panel 上按那個數字只跳 panel；在 global operation popup 裡按才執行 |
| K1-9 | K1 | panel 上按 `!` 打開 App Log | 都要 | 在 panel 上按 `!` |
| K2-1 | K2 | 畫面上 `Tab` 把 focus 移到同一個畫面的下一個 panel，最後一個之後回到第一個，不跨畫面 | 多 panel | 在 panel 上連按 `Tab`，走完一輪回到第一個，畫面不換 |
| K2-2 | K2 | 有動作區的 popup（表單、有按鈕的 input popup）裡，`Tab` 在欄位區與動作區之間切換 | 表單、color picker | 打開表單按 `Tab`，focus 在欄位區與動作區之間來回 |
| K2-3 | K2 | `Tab` 回到一區時，停在離開前的那一個項目 | 表單、color picker | 在欄位區移到第三欄，`Tab` 到動作區再 `Tab` 回來，focus 在第三欄 |
| K2-4 | K2 | 欄位區、動作區裡的項目之間用 hjkl 移動 | 表單、color picker | 在兩區裡各按 hjkl，focus 在同一區的項目之間移動 |
| K2-5 | K2 | `Tab` 不離開當前 popup | 都要 | 在每種 popup 上按 `Tab`，focus 不會跑到底下的 panel |
| K2-6 | K2 | 打字列上（finder 與 select 的打字列、panel filter），`Tab` 到它的清單 | panel filter、select、finder | 在打字列打幾個字後按 `Tab`，focus 到清單 |
| K2-7 | K2 | 只有一塊的 input popup 沒有灰字提議時（含有舊密碼的 password：灰點不是提議，`Tab` 不收進舊密碼），`Tab` 不作用 | input | 打開空的 input popup 按 `Tab`，什麼都沒變 |
| K2-8 | K2 | 有動作區的 popup 裡一定有 `Shift-Tab`（反向切換） | 表單、color picker | 在表單上按 `Shift-Tab`，focus 往反方向切換 |
| K3-1 | K3 | `Enter` 對 focus 項目做最直觀的那個動作 | 都要 | 在每種 panel 的項目上按 `Enter`，判斷是不是那種項目最直觀的動作 |
| K3-2 | K3 | 同一種項目在同一個 app 裡，`Enter` 永遠是同一個動作 | 都要 | 在不同 panel、不同畫面的同一種項目上按 `Enter`，做的事一樣 |
| K3-3 | K3 | panel 本身是內容區、沒有項目可選時（例：預覽、log），`Enter` 對整個 panel 做最直觀的動作 | 都要 | 在這種 panel 上按 `Enter`，判斷是不是最直觀的動作 |
| K3-4 | K3 | 按完 `Enter`，focus 原則上留在原處（表單上、一列一個值的 panel 上確定了一欄的 input popup，回到同一欄／同一列；選 radio、翻 checkbox 不動）；會換位置的，是元件寫死的三處（進明細、打字列上的 `Enter` 到清單、表單送出被擋時跳到第一個有問題的欄位），或使用者按下去時就預期會換的 app 動作 | 都要 | 在 panel、表單、radio、checkbox 上按 `Enter`，看 focus 停在哪；換了位置的，判斷使用者按下去時是不是就預期會換 |
| K3-5 | K3 | `Enter` 換了 panel 或畫面時，落點是使用者按下去時就預期的（例：明細的 `Enter` 到顯示那一項明細的 panel） | 都要 | 在清單上按 `Enter` 換了 panel 或畫面時，判斷落點是不是使用者按下去時就預期的 |
| K3-6 | K3 | input popup 裡 focus 在值上時，`Enter` 確定這個值：寫回去、popup 關掉 | input | 改值後按 `Enter`，popup 關掉、值寫回 |
| K3-7 | K3 | 值不合格（一欄自己的規則：格式、範圍、不能空）時 `Enter` 不寫回，錯誤寫在預留的錯誤列，popup 不關；從表單打開的也在 input popup 這一層擋，不等表單送出。打開時是空的、又不能空的欄位，什麼都沒打就按 `Enter` 也算不合格（有建議值時用建議值） | input | 打一個不合格的值按 `Enter`；打開一個空的、不能空的欄位，什麼都不打按 `Enter` |
| K3-8 | K3 | 值跟打開時一樣、而且打開時就合格（例：有舊值、沒改）時，`Enter` 不寫回、直接關掉（從表單打開的，表單不記成改過） | input | 不改值按 `Enter`，popup 關掉；讀程式：沒有寫回 |
| K3-9 | K3 | 多行文字：寫入狀態下 `Enter` 換行；離開寫入狀態（`Esc`）之後的 `Enter` 才確定 | textarea | 寫入狀態按 `Enter` 換行；按 `Esc` 再按 `Enter`，值確定 |
| K3-10 | K3 | 打字列（finder 與 select 的打字列、panel filter）上 `Enter` 把 focus 移到清單上 cursor 那一項、不執行；在清單上再按 `Enter` 才執行或選定 | panel filter、select、finder | 在打字列按 `Enter`，focus 到清單、沒有執行；再按一次才執行 |
| K3-11 | K3 | 打字列沒有結果時（包括邊找邊列、一筆都還沒到時）`Enter` 不作用 | panel filter、select、finder | 打一串沒有結果的字按 `Enter` |
| K3-12 | K3 | input popup 的其他部分（例：datetime picker 的月份、color picker 的 R），`Enter` 做最直觀的那件事 | input | 在那些部分按 `Enter`，判斷是不是最直觀的事 |
| K3-13 | K3 | 按送出按鈕時檢查所有欄位；有不合格的就不送出，focus 跳到第一個有問題的欄位 | 表單 | 留兩欄不合格按送出 |
| K3-14 | K3 | 背景發生的事（載入完成、工作結束、遠端送來的變化）不移動 focus、不換畫面 | 都要 | 讓背景的事發生（重新載入、工作結束、遠端的變化），focus 與畫面都不動 |
| K3-15 | K3 | 新增一項之後（New、Copy、Import 確定之後），cursor 移到新的那一項，捲到看得到 | 都要 | 新增一項，看 cursor 停在新的那一項上 |
| K4-1 | K4 | 沒有 popup 時，`Esc` 退出當前模式或往上一層（例：panel filter 不論 focus 在打字列或清單，`Esc` 都清掉篩選） | 都要 | 進模式、或打 panel filter 後按 `Esc` |
| K4-2 | K4 | `Esc` 一次只退一層：疊了幾層 popup，按一次只關最上面那一個 | 都要 | 疊三層（Space menu → global operation popup → confirm）按一次 `Esc`，只關掉 confirm |
| K4-3 | K4 | 關掉最上層之後，底下的 popup 階層原樣留著、照原樣呈現 | 都要 | 同上，底下兩層還在，cursor 與內容跟打開 confirm 前一樣 |
| K4-4 | K4 | `Esc` 永遠不離開 app，到了最上層什麼都不做 | 都要 | 在 panel 上沒有 popup、沒有模式時連按 `Esc`，app 不關 |
| K5-1 | K5 | focus 在任何 panel 上（包括沒有項目的 panel，以及 cursor 停在 checkbox 那一列時），`Space` 打開 Space menu，不翻 checkbox | 都要 | 在每個 panel 上按 `Space` |
| K5-2 | K5 | Space menu 開著時，再按 `Space` 關掉它 | 都要 | 開 Space menu 後再按 `Space` |
| K5-3 | K5 | Space menu 以外的 popup 上，`Space` 不作用（popup 裡的模式除外） | 都要 | 在 global operation popup、key reference、confirm 上按 `Space`，什麼都沒發生 |
| K5-4 | K5 | checkbox 的選項上（checkbox popup 的清單、表單上直接畫出來的 checkbox），`Space` 勾或取消勾 | checkbox | 在 checkbox 選項上按 `Space` |
| K5-5 | K5 | popup 自己的操作用熱鍵執行，popup 上不再疊 Space menu（popup 裡的模式除外） | 都要 | 在各種 popup 上找不到開 menu 的方式，操作都靠熱鍵 |
| K5-6 | K5 | app 自己的 popup 裡，focus 的那一格有好幾個值可以輪流換時，`Space` 換到下一個值 | app 自己的 popup | 在那種格子上連按 `Space`，值照順序換 |
| K6-1 | K6 | `?` 在任何 surface 都有回應（輸入態、PTY 照 K8、K10；textarea 的「移」不是輸入態，照樣打開 key reference） | 都要 | 在每種 panel、popup、模式裡按 `?` |
| K6-2 | K6 | key reference 開著時再按 `?` 關掉 | 都要 | 開 key reference 後再按 `?` |
| K6-3 | K6 | `?` 打開的是最前端那個 surface 的 key reference | 都要 | 在 popup 上按 `?`，列的是那個 popup 的鍵，不是底下 panel 的 |
| K6-4 | K6 | key reference 唯讀：沒有游標、不能執行 | 都要 | 開 key reference，沒有 cursor 列，按 `Enter` 什麼都不執行 |
| K6-5 | K6 | panel 的 key reference 列出這個 panel 能按的鍵，含移動鍵 | 都要 | 在 panel 上按 `?` |
| K6-6 | K6 | popup（含 Space menu、global operation popup）的 key reference 只列這個 popup 能按的鍵：自己的熱鍵、`Enter`、`Esc`、移動鍵 | 都要 | 在 Space menu 上按 `?`，沒有 panel 或 global 的鍵 |
| K6-7 | K6 | key reference 的移動鍵照 K12 列出按得到的全部：一維清單（表單、沒有 tab 的一列一個值 panel、menu）寫 `h\|k` 往前、`j\|l` 往後 | 都要 | 在表單、menu、沒有 tab 的一列一個值 panel 上按 `?`，看 `move` |
| K6-8 | K6、M6 | 清單空了（沒有東西可以移）、內容整個放得下（沒有東西可以捲）時，key reference 不列移動鍵、捲動鍵 | 都要 | 讓清單空掉、讓內容放得下，各按 `?` |
| K6-9 | K6 | 一列一個值的 panel 的 key reference 有「每一列」一節時，放在最前面：每一列的名稱（一般的字色，不是鍵的顏色）與它是什麼意思，按鍵的節排在後面 | 一列一個值的 panel | 在有這一節的 panel 上按 `?`，看節的順序與名稱的顏色 |
| K7-1 | K7 | 一個角色綁多個鍵時，別名在所有 surface 同樣有效 | 都要 | 在每種 panel 與 popup 上按別名鍵，跟主鍵做一樣的事 |
| K8-1 | K8 | 輸入態裡所有會產生字元的鍵（含 letter hotkey、splash 的 `V`、`Space`、`?`、`q`）都當成字元輸入，不觸發任何動作 | input、panel filter | 在打字列打 `q`、`?`、空白與熱鍵字母，都變成字 |
| K8-2 | K8 | 輸入態裡 `Esc` 取消輸入 | input、panel filter | 在打字列按 `Esc` |
| K8-3 | K8 | 輸入態裡 `Ctrl-C` 進入離開流程 | input、panel filter | 在打字列按 `Ctrl-C` |
| K8-4 | K8 | 離開輸入面，熱鍵立刻恢復作用 | input、panel filter | 離開打字列後馬上按熱鍵 |
| K8-5 | K8 | 多行文字寫入狀態下 `Tab` 插入 `input_tab_width` 個空白（預設 4），不插 `\t` | textarea | 寫入狀態按 `Tab`，數插入的空白；讀程式：不是 `\t` |
| K9-1 | K9 | `q` 與 `Ctrl-C` 做同一件事：進入 app 的離開流程 | 都要 | 在 panel 上分別按 `q`、`Ctrl-C`，出現的流程一樣 |
| K9-2 | K9 | `q` 在表單與表單的打字說明 note 上不進入離開流程（在要打字的欄位上跳說明 note，其他地方不作用） | 表單 | 在表單上（不在打字列）按 `q`；在要打字的欄位上打一個字跳出說明 note 後再按 `q` |
| K9-3 | K9 | `Ctrl-C` 在表單與表單的打字說明 note 上仍然進入離開流程 | 表單 | 在表單上與打字說明 note 上各按 `Ctrl-C` |
| K9-4 | K9 | 離開流程進行中（例：離開前的 confirm 開著時）再按一次 `Ctrl-C`，立刻離開、不再詢問（直接離開的 app 只有 popup 開著時才有這種情況，K9-6） | 都要 | 按 `Ctrl-C` 出現確認後再按一次 `Ctrl-C` |
| K9-5 | K9 | 離開列在 global operation popup 裡 | 都要 | `Space` → `Global operation`，裡面有離開 |
| K9-6 | K9 | 有 popup 開著時，第一下 `q` 或 `Ctrl-C` 一定不會直接離開：當下會直接離開的流程改開離開的 confirm（`Quit <app>?`），第一步本來就會問的照舊；按 `Esc` 回到 popup；在 panel 上照 app 的流程 | 都要 | 開 Space menu 按 `q`，再按 `Esc`；關掉 menu 後在 panel 上按 `q` |
| K9-7 | K9 | 照表單的 app 自己的 popup（有要送出的值）上，`q` 不進入離開流程，`Ctrl-C` 照樣進入 | app 自己的 popup | 在那種 popup 上按 `q`，再按 `Ctrl-C` |
| K10-1 | K10 | focus 在 PTY 時（panel 裡或 terminal popup）按鍵都送給子程序，core key 與 app 的熱鍵（含 splash 的 `V`）都失效，只有出口鍵與 app 保留的組合鍵（互動 terminal 還有 `Alt-v`、`PgUp`）屬於 app；`Esc` 也給子程序，toast 開著時只能等時間到收掉 | PTY | 在 PTY 裡按 `Space` `?` `q` `Tab` `Esc` `1` 與 app 的熱鍵，都進子程序 |
| K10-2 | K10 | 至少有一個出口鍵讓 focus 離開 PTY | PTY | 在 PTY 裡按出口鍵能回到 app |
| K10-3 | K10 | 出口鍵用 `Alt-Esc` | PTY | 在 PTY 裡按 `Alt-Esc` |
| K10-4 | K10 | 按 `Alt-Esc` 會讓 focus 離開 PTY 或結束子程序時，一律先跳 confirm：`Enter` 離開、`Esc` 回到 PTY | PTY | 在 PTY 裡按 `Alt-Esc` 出現 confirm；按 `Esc` 回到 PTY，再按一次 `Alt-Esc` 後按 `Enter` 離開 |
| K10-5 | K10 | 子程序還沒準備好收鍵時，`Ctrl-C` 照樣轉送給子程序 | PTY | 子程序啟動或連線中按 `Ctrl-C`；讀程式：有轉送 |
| K10-6 | K10 | 子程序還沒準備好收鍵時，出口鍵照樣有效、照樣揭露 | PTY | 子程序啟動或連線中看 footer、按出口鍵 |
| K11-1 | K11 | 模式裡 `Space` 打開模式的 Space menu，只列模式裡能做的事 | 模式 | 進模式按 `Space` |
| K11-2 | K11 | 模式裡 `?` 打開這個模式的 key reference：模式裡能按什麼鍵、做什麼 | 模式 | 進模式按 `?` |
| K11-3 | K11 | 模式裡 `Esc` 離開模式，回到進入前的狀態；模式有好幾層時一次退一層（`Visual>select` 退回 `Visual`） | 模式 | 進模式做點事後按 `Esc`，狀態回到進入前 |
| K11-4 | K11 | panel 與 popup 裡的模式，`q`、`Ctrl-C` 照 K9 進入離開流程 | 模式 | 進模式按 `q`、`Ctrl-C` |
| K11-5 | K11 | 模式在 panel 上暫停 `Tab` 或數字鍵時，按了要有回應，說明先 `Esc` 離開模式 | 模式（在 panel 上） | 進模式按 `Tab`、`2`，出現說明（例：toast） |
| K11-6 | K11 | 模式裡只有模式自己的鍵與 K11 表上的 core key 作用：panel 的熱鍵與 global 熱鍵都不作用 | 模式 | 進模式按 panel 的熱鍵與 global 熱鍵，都沒作用 |
| K11-7 | K11 | 模式裡按了不作用的熱鍵不出聲 | 模式 | 同上，沒有 toast 或任何提示 |
| K11-8 | K11 | 模式裡沒有任何可以執行的按鍵清單 | 模式 | 進模式後找不到能選、能執行的鍵清單 |
| K11-9 | K11 | 模式自己的鍵揭露在 footer 或下框 hint | 模式 | 進模式看 footer（panel 上的模式）或下框 hint（popup 裡的模式） |
| K11-10 | K11 | 離開模式，模式名與外框顏色恢復 | 模式 | 按 `Esc` 離開後看那個框 |
| K11-11 | K11 | 模式在 popup 裡時，`Tab` 與數字鍵照那個 popup 本來的作用（不換 panel），不另外回應；footer 照 popup 開著時的樣子，不換成模式的字 | 模式（在 popup 裡） | 在 popup 裡進模式，按 `Tab`、`2`，看 footer |
| K11-12 | K11 | 模式在 PTY 上時（terminal 的歷史模式、選取模式），模式自己的鍵、`?`、`Esc` 以外的鍵先離開模式，再送給子程序；`q`、`Ctrl-C` 也一樣，不進離開流程 | PTY | 在 PTY 上進歷史模式，打一個字、按 `q`、`Ctrl-C`，看模式先離開、鍵落在子程序裡 |
| K11-13 | K11 | 模式裡 `!` 不作用 | 模式 | 進模式按 `!` |
| K12-1 | K12 | 不在打字的地方，`j` `k` `u` `d` `g` `G` `h` `l` 不被任何動作佔用（`g` 開頭的兩鍵組合除外） | 都要 | 讀程式或看所有 menu、key reference：這幾個字母沒有登記成動作 |
| K12-2 | K12 | `h\|j\|k\|l` 就是 `←\|↓\|↑\|→`：方向鍵做一樣的事 | 都要 | 在清單、menu、表單上分別按 hjkl 與方向鍵，效果一樣 |
| K12-3 | K12 | 有左右結構時（同一個 surface 裡的 tab、左右兩側、格子），`j\|k` 上下、`h\|l` 左右（切 tab、跨到另一側） | 都要 | 在有 tab 的 panel 按 `h\|l` 切 tab |
| K12-4 | K12 | 只有一維清單、沒有左右結構時（表單、沒有 tab 的一列一個值 panel、menu），`h\|k` 往前、`j\|l` 往後 | 都要 | 在 Space menu 上按 `l` 往下、`h` 往上 |
| K12-5 | K12 | 一維清單放在有 tab 的 panel 裡：`h\|l` 切 tab，`j\|k` 在清單裡移 | panel tab | 在有 tab 的清單 panel 上按 `h\|l`、`j\|k` |
| K12-6 | K12 | `u\|d` 移動半頁 | 都要 | 在超過一頁的清單上按 `u`、`d` |
| K12-7 | K12 | `gg\|G` 到頭、到尾 | 都要 | 在清單上按 `gg`、`G` |
| K12-8 | K12 | 單按 `g` 不做任何事 | 都要 | 按 `g` 後等著，畫面不變 |
| K12-9 | K12 | `g` 後面接的鍵沒有登記成組合時，當作 `g` 沒按過，那個鍵照常作用 | 都要 | 按 `g` 再按 `j`，往下一列 |
| K12-10 | K12 | 不收 `Ctrl-U\|Ctrl-D` 當別名 | 都要 | 在清單上按 `Ctrl-U`、`Ctrl-D`，不翻頁 |
| K12-11 | K12 | `Home`、`End` 在打字列把游標移到最前面、最後面 | input、panel filter | 在打字列打幾個字後按 `Home`、`End` |
| K12-12 | K12 | `Home`、`End` 在清單、menu、viewer、textarea 的移動狀態上不作用 | 都要 | 在清單與 menu 上按 `Home`、`End`，cursor 不動 |
| K12-13 | K12 | 一步一步的移動（`j\|k`、`h\|l`、方向鍵、`Tab`）在一串項目上到頭尾繞回：最後一個往後一步回到第一個，第一個往前一步到最後一個（panel 清單、menu、表單、panel tab、finder 的清單與打字列上的 `↑\|↓`、reorder、color picker 的 R → G → B、datetime picker 的時欄（23 之後 00）與分欄（55 之後 00）都是） | 都要 | 在 panel 清單、menu、表單、panel tab 等各走到頭尾再多走一步 |
| K12-14 | K12 | Drag mode 拿著時 `j\|k` 搬動那一項，到頭尾也繞回：拿著最後一項往後一步，它到第一個、其他各往後一格；拿著第一項往前一步，它到最後一個 | Drag | 拿著最後一項按 `j` |
| K12-15 | K12 | `u\|d` 到頭尾停在第一個、最後一個，不繞 | 都要 | 在倒數幾列按 `d`，停在最後一列 |
| K12-16 | K12 | 照空間走、不是一串項目的不繞：日曆的日子、月與年、左右兩側、在一段文字裡移動（含輸入框打字列的游標） | 都要 | 在日曆最後一天往後、在右側再往右、在打字列的最後一個字往右，不繞回 |
| K12-17 | K12 | 二維內容（一列有好幾個項目，例：網頁同一列的連結、表格的格）放在有 tab 的 panel 裡：`h\|l` 換 tab，`j\|k` 照閱讀順序一個項目一個項目走（同一列從左到右，再到下一列），到頭尾繞回 | panel tab | 在有 tab、內容是二維的 panel 上按 `h\|l`、`j\|k` |

## rules — M Menu 與揭露

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| M1-1 | M1 | 非輸入態的每一個畫面都常駐顯示 `?`、`Space` 與 `!`（模式裡 `!` 不作用，可以不顯示） | 都要 | 在每個畫面、每個模式看 footer |
| M1-2 | M1 | focus 在 PTY 裡時不顯示 `?`、`Space` 與 `!`，常駐顯示的是出口鍵與 app 保留的鍵（互動 terminal 還有 `Alt-v`、`PgUp`） | PTY | 進 PTY 看 footer 或 terminal 的下框 |
| M2-1 | M2 | Space menu 依作用對象分區，順序固定：`item operation` → `panel operation` → global 那一列 | 都要 | 在每個 panel 上按 `Space` |
| M2-2 | M2 | 動作放對地方：作用在 cursor 那一項的在 item operation，作用在當前 panel（或它的 tab）整體的在 panel operation，不屬於任何 panel 的在 global operation popup | 都要 | 看每個 panel 的 Space menu 與 global operation popup，逐列判斷作用對象 |
| M2-3 | M2 | 最後固定一列 `Global operation`，沒有熱鍵 | 都要 | 看 Space menu 最後一列 |
| M2-4 | M2 | 在 `Global operation` 那一列按 `Enter` 打開 global operation popup | 都要 | cursor 移到那一列按 `Enter` |
| M2-5 | M2 | 全域動作只有一個時，照樣是一列 `Global operation` 打開 global operation popup | 都要 | 看 Space menu 最後一列，不是直接放那個動作 |
| M2-6 | M2 | 區塊標題字串固定用英文原字 `item operation`、`panel operation`，不換措辭 | 都要 | 看 Space menu 的區塊標題 |
| M2-7 | M2 | global 那一列不加區塊標題 | 都要 | 看 Space menu 最後一列上面沒有標題 |
| M2-8 | M2 | 區塊之間用分隔線隔開，global 那一列跟上面的區塊之間也是 | 都要 | 看 Space menu 的區塊之間 |
| M2-9 | M2 | 沒有對象就沒有那一區：空清單上 item operation 連標題一起不出現 | 都要 | 清單空的時候按 `Space` |
| M2-10 | M2 | panel 上的 Space menu，item 與 panel 兩區一律加區塊標題，只剩其中一區也加 | 都要 | 在只剩一區的情況（例：空清單）按 `Space`，剩下那區有標題 |
| M3-1 | M3 | 每個 panel 的每個 item operation 與 panel operation 都在該 panel 的 Space menu 裡 | 都要 | 讀程式列出每個 panel 的動作，逐一在 Space menu 裡找 |
| M3-2 | M3 | 每個 global operation 都在 global operation popup 裡 | 都要 | 讀程式列出全域動作，逐一在 global operation popup 裡找 |
| M3-3 | M3 | popup 自己的操作都在該 popup 的 `?` key reference 裡 | 都要 | 在每種 popup 上按 `?`，對照讀程式的操作清單 |
| M3-4 | M3 | 只有打字列的 popup（text、password、number）的 hint 列出全部操作 | text、password、number | 看那個 popup 的下框 hint，對照讀程式 |
| M3-5 | M3 | 只有打字列的 popup 的 hint 在 60 欄放得下 | text、password、number | 終端機調成 60 欄打開那個 popup，hint 沒被截 |
| M3-6 | M3 | 沒有只能靠熱鍵觸發、哪裡都找不到的動作：每個 letter hotkey 都是某個清單裡某一列的捷徑 | 都要 | 讀程式：每個登記的熱鍵都對應到 Space menu、global operation popup 或其他 menu 的某一列（popup 自己的鍵見 M3-3） |
| M4-1 | M4 | 目前所在畫面的切換列照 M6 停用 | 多畫面 | 在某個畫面打開 global operation popup，切到這個畫面的那一列是停用色、cursor 跳過 |
| M4-2 | M4 | 沒有 popup 開著時，global operation popup 裡的熱鍵在 panel 上也能直接按 | 都要 | 在 panel 上直接按 global 熱鍵 |
| M4-3 | M4 | global 熱鍵跟 panel 自己的熱鍵撞鍵時，panel 的優先 | 都要 | 在那個 panel 上按撞的鍵，執行的是 panel 的動作 |
| M4-4 | M4 | 撞鍵的那個 panel 的 key reference 不列被蓋掉的 global 鍵 | 都要 | 在那個 panel 上按 `?` |
| M5-1 | M5 | 熱鍵字母出現在 label 裡（不分大小寫）時，原地包第一次出現的那個字母（`[r]ename`、`[n]ew`、`D[e]lete`、`UR[L]`、`Ex[P]ort`） | 都要 | 看 menu 的列、statusbar chip、panel 標題 |
| M5-3 | M5 | 熱鍵字母不在 label 裡時，放前面（`[x] Reset`） | 都要 | 同上 |
| M5-4 | M5 | 含 modifier 的熱鍵整個放進括號（`[Alt-t]erm`） | 都要 | 同上 |
| M5-5 | M5 | 多字元的熱鍵整個放進括號（`[go]to`） | 都要 | 同上 |
| M5-6 | M5 | 數字熱鍵一律放前面（`[3] Favorites`），不嵌進字裡 | 都要 | 同上 |
| M5-7 | M5 | core key 標在 label 上時放前面（`[Enter] Edit`） | 都要 | 同上 |
| M5-8 | M5 | 沒有熱鍵的 label 不加括號 | 都要 | 看 `Global operation` 那一列與其他沒熱鍵的列 |
| M5-9 | M5 | 括號裡與鍵名裡的字母照實際要按的大小寫（`[A]dd` 是 `Shift-A`；label 裡的字母跟鍵的大小寫不同時，括號裡照鍵寫，例：熱鍵是 `Shift-P` 的 `Export` 寫成 `Ex[P]ort`）；轉成大寫的 chip、標題裡也照原樣（`[m]ANAGE`），hint、footer、key reference 的鍵名不轉大寫 | 都要 | 對照讀程式：標 `[A]` 的要按 `Shift-A`，標 `[a]` 的按 `a` |
| M5-10 | M5 | label 本身已經寫出鍵的列（`[/] Search`）不再括一次 | 都要 | 看那幾列，鍵只標一次 |
| M5-11 | M5 | 熱鍵顯式標出來，不只用顏色或 glyph 暗示 | 都要 | 看 menu、statusbar、panel 標題：有熱鍵的地方都有括號標記 |
| M5-12 | M5 | 畫面上（footer、hint、key reference）的鍵名用鍵帽上的名字，大駝峰、不自創縮寫（`Esc` `Tab` `Enter` `Space` `Backspace` `Delete` `Home` `End` `PgUp` `PgDn`） | 都要 | 看 footer、hint、key reference |
| M5-13 | M5 | 畫面上的方向鍵寫成 `↑` `↓` `←` `→` | 都要 | 看 footer、hint、key reference |
| M5-14 | M5 | 畫面上 `Ctrl` 後面的字母一律大寫（`Ctrl-C`、`Ctrl-U`） | 都要 | 看 footer、hint、key reference |
| M5-15 | M5 | 畫面上 modifier 用 `-` 連接（`Alt-t`、`Shift-Tab`、`Alt-Esc`） | 都要 | 看 footer、hint、key reference |
| M5-16 | M5 | 畫面上用 `\|` 接起幾個做同一件事的鍵（`h\|k`、`Enter\|Esc:close`），與一對方向相反、用一個動詞講的鍵（`j\|k:move`、`u\|d`、`gg\|G`），不用 `/` | 都要 | 看 footer、hint、key reference |
| M5-17 | M5 | 範圍用 `–`（`1–9`） | 都要 | 看 footer、key reference |
| M5-18 | M5 | statusbar chip、panel 標題上的熱鍵也用 label 的括號標記 | 都要 | 看 statusbar、panel 標題 |
| M5-19 | M5 | 句子（空狀態、toast、錯誤訊息，以及 menu 與 key reference 說明欄）裡提到的鍵一律加方括號（`Press [A] or [Space]`） | 都要 | 看空狀態、toast、錯誤訊息、說明欄 |
| M5-20 | M5 | hint、footer 寫成 `鍵:說明`，冒號前後不空格，項目之間一個空格 | 都要 | 看 footer 與各 popup 的下框 hint |
| M5-21 | M5 | key reference 分兩欄：鍵、說明；鍵不加括號、不加冒號 | 都要 | 按 `?` 看 |
| M5-22 | M5 | README 內文提到的鍵用 Markdown 的 code 標，不加方括號 | 都要 | 讀檔案：README |
| M5-23 | M5 | README 引用畫面上的 label 照畫面寫（`[A]dd`） | 都要 | 讀檔案：README |
| M5-24 | M5 | 別的工具自己的按鍵照那個工具的寫法（例：tmux 的 `prefix l`） | 都要 | 讀檔案：README 與畫面上提到其他工具按鍵的地方 |
| M5-25 | M5 | label 照它本來的大小寫寫，不為了熱鍵改字（`Export`，不寫成 `ExPort`） | 都要 | 看 menu 的列、statusbar chip、panel 標題 |
| M5-26 | M5 | README 的鍵名用鍵帽上的名字，大駝峰、不自創縮寫（`Esc` `Tab` `Enter` `Space` `Backspace` `Delete` `Home` `End` `PgUp` `PgDn`） | 都要 | 讀檔案：README |
| M5-27 | M5 | README 的方向鍵寫成 `↑` `↓` `←` `→` | 都要 | 讀檔案：README |
| M5-28 | M5 | README 裡 `Ctrl` 後面的字母一律大寫（`Ctrl-C`、`Ctrl-U`） | 都要 | 讀檔案：README |
| M5-29 | M5 | README 的 modifier 用 `-` 連接（`Alt-t`、`Shift-Tab`、`Alt-Esc`） | 都要 | 讀檔案：README |
| M5-30 | M5 | README 裡用 `\|` 接起幾個做同一件事的鍵、一對方向相反的鍵（`gg\|G`），不用 `/` | 都要 | 讀檔案：README |
| M6-1 | M6 | 對象不存在的動作，那一列不出現 | 都要 | 讓對象消失（例：清空清單）後看 menu |
| M6-2 | M6 | 對象存在、但現在不能執行的動作：列照樣出現，用停用色 | 停用 | 讓動作暫時不能執行後看 menu |
| M6-3 | M6 | 停用的列說明欄維持原本那句，不另外寫原因 | 停用 | 同上，比對停用前後的說明 |
| M6-4 | M6 | cursor 跳過停用的列 | 停用 | 在 menu 上用 `j\|k` 經過停用列 |
| M6-5 | M6 | 按停用列的熱鍵不作用 | 停用 | 按那一列的熱鍵 |
| M6-6 | M6 | key reference 裡，對象不存在的鍵不列 | 都要 | 按 `?` |
| M6-7 | M6 | key reference 裡另外加標題、說明別的 surface 的一段照常顯示，不用停用色 | 都要 | 按 `?` 看那一段的顏色 |
| M6-8 | M6 | 說明別的 surface 的那一段排在最後，在 `app-wide` 之後 | 都要 | 按 `?` 看段落順序 |
| M7-1 | M7 | focus 在 panel 上時，`Space` 一定打開 Space menu：global 那一列永遠在，menu 不會是空的 | 都要 | 在每個 panel（含空的、唯讀的）上按 `Space` |
| M8-1 | M8 | Space menu 以外的 menu 要分組時，第一組是跟當前 cursor 相關的動作 | 都要 | 打開那個 menu 看第一組 |
| M8-2 | M8、M2 | 分組 menu 的每一組（含第一組）都有說明類型的標題 | 都要 | 打開那個 menu 看每一組，第一組也有標題 |
| M9-1 | M9 | 同一個熱鍵在不同 panel 做不同事、兩處指示同時看得到時，在當前 focus 按下去會觸發的那個亮、不會的那個暗 | 都要 | 兩個 panel 的下框 hint 都有同一個鍵時看顏色，換 focus 再看 |

## rules — L 版面

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| L1-1 | L1 | 在 60 欄 × 32 列下能完成所有核心任務，所有 panel 並排 | 都要 | 終端機開成 60 × 32，把 app 的每一個核心任務走一遍 |
| L1-2 | L1 | app 的最低尺寸不高於 60×32（預設 60×32，app 可以調低） | 都要 | 讀程式：最低尺寸的設定；把終端機調到 60×32，看 app 照常畫 |
| L1-3 | L1 | 比最低尺寸小時（寬或高任一邊不夠），不畫 app 的畫面，只在正中央畫三列：app 的名稱（Blue 粗體）、提示 `needs a terminal of at least <W>×<H>`（Overlay0，寫 app 的最低尺寸）、`Press [Ctrl-C] twice to quit`（Overlay0） | 都要 | 把終端機縮到比最低尺寸小（只縮寬、只縮高各一次） |
| L1-4 | L1 | 放不下時先拿掉提示，再拿掉 `Press [Ctrl-C] twice to quit`，名稱一定留著；一列比畫面寬也算放不下；一直縮到 1×1 都不當掉 | 都要 | 縮到只剩兩列高、縮到比提示窄（例：30 欄）各看一次，再一直縮到 1×1 |
| L1-5 | L1 | 比最低尺寸小時按鍵都不作用（不送進 app，也不送進 PTY）；`q` 與單按一次 `Ctrl-C` 不作用，只有連按兩次 `Ctrl-C` 立刻離開 | 都要 | 縮小後按幾個平常會改東西的鍵、`q`、一次 `Ctrl-C`，拉大看什麼都沒變；再縮小連按兩次 `Ctrl-C` |
| L1-6 | L1 | 視窗拉大到最低尺寸以上，回到原本的畫面，狀態沒變（cursor、開著的 popup 都在） | 都要 | 移動 cursor、打開一個 popup 後縮小，再拉大 |
| L2-1 | L2 | 標題、statusbar、chip 等動態文字用固定寬度的欄位或 padding，寬度不跟著內容長度變（一列裡最後一個動態欄位可以不補空白） | 都要 | 讓動態文字變長變短（換 tab、進度、計數），看欄位寬度與旁邊的內容不左右移 |
| L3-1 | L3 | 常駐列的列數固定、不因內容多寡改變：最上面一列（多畫面的 app 是畫面 chip 列加它下面的分隔線；單畫面的 app 有 statusbar 時是一列 statusbar）與 footer 一列 | 都要 | 讓 statusbar、chip 列、footer 的內容變多變少，縮放終端機，最上面一列（含分隔線）與 footer 的列數不變 |
| L3-2 | L3 | panel 的 tab 畫在 panel 的上框，不另佔一列 | panel tab | 看有 tab 的 panel：tab 在上框的膠囊串裡，框外沒有另一列 tab |
| L4-1 | L4 | 畫面上的每一列都剛好等於終端機寬度，不多不少 | 都要 | 多種尺寸、icon 一格與兩格下看每一列：右框不折行、不留殘影；或讀程式：畫面測試在 icon、powerline 符號一格與兩格下跑（E5-11） |
| L5-1 | L5 | focus 所在的 surface 一眼可辨（進模式時也一樣） | 都要 | 在每個畫面看一眼就說得出 focus 在哪個 panel 或 popup |
| L5-2 | L5 | 切換 focus 不讓任何內容位移 | 多 panel | 按 `Tab` 換 panel，前後比對畫面，字與框的位置不動 |
| L5-3 | L5 | focus 不只靠顏色分辨，有顏色以外的差別（例：線型） | 多 panel | 比較 focus 與失焦 panel 的外框，除了顏色還有別的差別；進模式後照樣分得出 focus 在哪 |

## rules — F Popup

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| F1-1 | F1 | app 的每一個 popup 都屬於八類之一：menu、confirm、input、form、note、toast、terminal、app 自己的 popup（splash 不是 popup；panel 內容自己畫的框是內容，不是 popup） | 都要 | 打開每一個 popup，逐一歸類 |
| F1-2 | F1 | menu 用 `j\|k` 移動 cursor | 都要 | 打開 Space menu 按 `j`、`k`，cursor 上下移 |
| F1-3 | F1 | menu（含 Space menu、global operation popup）用 `Enter` 或熱鍵執行那一列 | 都要 | 在 Space menu 對一列按 `Enter`、對另一列按它的熱鍵，都執行那一列 |
| F1-4 | F1 | input popup 一個 popup 只處理一個值 | input | 打開每個 input popup，裡面只輸入或選出一個值 |
| F1-5 | F1 | 表單一列一個值 | 表單 | 打開每個表單，每一列只有一個欄位 |
| F1-6 | F1 | note 是唯讀的 | 都要 | 打開 `?` 的 key reference 等 note，按鍵改不到內容 |
| F1-7 | F1 | toast 開著時，除了 `Esc`，按鍵都穿過它 | toast | toast 還在時按 `j`、`Space`，底下照常反應，toast 不吃鍵 |
| F1-8 | F1 | 有可用 `Enter` 執行的選項清單的 popup 照 menu 做，不是 note | 都要 | 看每個有選項清單的唯讀 popup，都是 menu 的樣子與按鍵 |
| F1-9 | F1 | menu 的 `Enter` 打開那一列的全文時（例：工作清單上沒有動作可做的列），開一個 note 顯示那一列的完整內容 | 都要 | 在那種 menu 的一列按 `Enter`，疊出一個 note 寫著完整內容 |
| F1-10 | F1 | 帶內容的 confirm 是一個 confirm，不拆成 note 加 confirm 兩個 popup | confirm | 觸發帶明細的 confirm，只疊出一層 popup |
| F1-11 | F1 | 依階段換類別的 popup，同一時間只屬於一類，鍵照當時那一類 | 都要 | 在 finder 的打字列與清單各按 `j`、`Enter`，鍵的意思照當時那一類 |
| F1-12 | F1 | 依階段換類別的 popup，`Esc` 關掉整個 popup，不是退回上一個階段（focus 在打字列或清單都一樣） | 都要 | focus 在 finder 的清單時按 `Esc`，整個 finder 關掉 |
| F1-13 | F1 | 清單加搜尋的 popup（select、checkbox popup、file-picker 等）照 finder 做：打字列是輸入態，清單是選 | finder | 打開每個可搜尋的清單 popup，打字列打的字是內容、清單用來選 |
| F1-14 | F1 | 沒有搜尋的清單 popup 照 menu 做；只有 reorder 例外，是 input | 都要 | 看每個沒有搜尋的清單 popup，除了 reorder 都是 menu 的樣子與按鍵 |
| F1-15 | F1 | toast 不算層色的層數 | toast | popup 上冒出 toast 時再開一層 popup，新 popup 的層色跟沒有 toast 時一樣 |
| F1-16 | F1 | toast 與 popup 同時開著時，`Esc` 先收掉 toast | toast | popup 上冒出 toast 時按一次 `Esc`，只有 toast 收掉 |
| F1-17 | F1 | 多步驟的流程每一步是自己的 popup，疊起來，不在同一個框裡換內容 | 都要 | 走一遍多步驟流程（例：先選欄位再選方向），每一步都疊出新的一層 |
| F1-18 | F1 | app 自己的 popup 只裝七類裝不下的內容；七類裝得下的（清單、確認、一個值、一列一個值的表單、唯讀內容、短訊息、子程序）照那一類做 | app 自己的 popup | 打開每個 app 自己的 popup，裡面的內容七類都裝不下 |
| F1-19 | F1 | app 自己的 popup 有要送出的值時照表單：動作區在內容下面，`Tab` 在內容與動作區之間切換，按鈕送出 | app 自己的 popup | 在那種 popup 上按 `Tab`，再按按鈕 |
| F1-20 | F1 | panel 內容自己畫的框不是一層：在它上面按 `Space`、`?` 打開的是它所在 panel 的 Space menu、key reference，`Esc` 照 K4 在 panel 上的行為 | panel 內容的框 | 內容畫出框時按 `Space`、`?`、`Esc` |
| F2-1 | F2 | 動畫每格 32ms，打開、收起各 9 格（約 288ms） | 都要 | 讀程式或錄影逐格數：每格 32ms、各 9 格 |
| F2-2 | F2 | 打開的動畫播完之前，popup 不收鍵 | 都要 | 打開 popup 後立刻按 `j`，動畫播完前 cursor 不動 |
| F2-3 | F2 | 好幾層一起收起時（一個動作關掉整疊、T1 清掉兩層以上的 source），每一層同時收起，各自照自己的大小與層色，總共還是約 288ms；不是只有最上面那一層播 | 都要 | 讀程式；或從兩層的 popup 執行會清掉 source 的動作，逐格看兩層一起收 |
| F3-1 | F3 | 任何看得到的 popup（含 toast：不等倒數結束）按 `Esc` 都立即開始關閉（例外只有 F3 列的：PTY、textarea 的寫入狀態、popup 裡的模式、改過的表單／textarea／reorder／照表單的 app 自己的 popup） | 都要 | 在每一類 popup 上按 `Esc`，關閉動畫馬上開始 |
| F3-2 | F3 | 已經在跑關閉動畫的 popup 不再理會 `Esc`，也不接收其他按鍵 | 都要 | 按 `Esc` 後趁關閉動畫還在播時按 `j`、`Enter`，正在關的那層沒有反應；關閉動畫中再按一次 `Esc`，關的是下一層 |
| F3-3 | F3 | textarea 在寫入狀態時，`Esc` 是離開寫入狀態、進入移動狀態 | textarea | 在 textarea 寫字時按 `Esc`，回到移動狀態，popup 還在 |
| F3-4 | F3、K4 | popup 裡正在模式中時（例：viewer 的選取模式、reorder 的 Drag mode），`Esc` 先離開模式、popup 不關；再按一次才關 popup | 模式 | 在 viewer 按 `v` 進選取模式（或在 reorder 按 `D`）後按 `Esc`，模式離開、popup 還在；再按一次 `Esc` popup 才關 |
| F3-5 | F3 | 內容改過的表單按 `Esc`，先開 confirm 問要不要放棄 | 表單 | 改一欄後按 `Esc`，疊出放棄的 confirm |
| F3-6 | F3 | 內容改過的 textarea 按 `Esc` 關閉時，先開 confirm 問要不要放棄 | textarea | 改過內容、回到移動狀態後按 `Esc`，疊出放棄的 confirm |
| F3-7 | F3 | 搬過順序的 reorder 按 `Esc`，先開 confirm 問要不要放棄 | reorder | 搬一個項目後按 `Esc`，疊出放棄的 confirm |
| F3-8 | F3 | 內容改過的 app 自己的 popup（有要送出的值）按 `Esc`，先開 confirm 問要不要放棄 | app 自己的 popup | 改過內容後按 `Esc`，疊出放棄的 confirm |
| F4-1 | F4 | 從 popup A 開出 popup B 時，A 留在底下 | 都要 | 從 Space menu 開 global operation popup，再從 Space menu 執行 app 自己會開出另一個 popup 的動作，底下照樣看得到（淡化的）Space menu |
| F4-2 | F4 | 取消 B 回到 A | 都要 | 在 global operation popup 與 app 自己的動作開出的 popup 上各按 `Esc`，都回到 Space menu |
| F5-1 | F5 | 錯誤立刻出現（toast 或 popup） | 都要 | 觸發一個錯誤（例：斷網、沒有權限），馬上看到 toast 或 popup |
| F5-2 | F5 | 錯誤不阻塞 app | 都要 | 錯誤出現後 app 照常運作，使用者能接著處理錯誤本身 |
| F5-3 | F5 | 錯誤也記進 App Log，toast 收掉之後照樣查得到 | 都要 | 觸發一個錯誤，等 toast 收掉後按 `!` |
| F6-1 | F6 | 決定要 confirm 的動作每次都 confirm（經由 picker 明確選定的那一次可以算已確認） | confirm | 同一個動作做兩三次，每次都出 confirm |
| F6-2 | F6 | confirm 上 `Enter` 接受、`Esc` 取消 | confirm | 在 confirm 上分別按 `Enter`、`Esc` |
| F6-3 | F6 | confirm 的回答只有 `Enter`、`Esc` 兩個鍵，沒有 `y`、`n` | confirm | 在 confirm 上按 `y`、`n`，不作用 |
| F6-4 | F6 | confirm 的提示寫出接受會做的事（動詞與對象），不是抽象的 OK | confirm | 讀每個 confirm 的問句與 `Enter` 的 hint |
| F6-5 | F6 | confirm 不能被誤觸完成（例：滑鼠點一下不能等於接受） | confirm | 在 confirm 上點滑鼠、按回答以外的鍵，都不會接受 |
| F7-1 | F7 | popup 的寬度打開時定好，開著時不變 | 都要 | 在開著的 popup 裡讓內容變長變短（打字、篩選），框的寬度不變 |
| F7-2 | F7 | 內容寬度確定的 popup，寬度不超過 `min(terminal 寬 − 2, 120)` | 都要 | 在 200 欄與很窄的終端機各開一次（例：menu、confirm、select、checkbox popup），寬度不超過上限 |
| F7-3 | F7 | 內容寬度不確定的 popup，寬度是 `min(terminal 寬 − 2, 120)` | 都要 | 在 80 欄與 200 欄各開一次（例：網址、邊找邊列的搜尋結果、表單），寬度是 78 與 120 |
| F7-4 | F7 | popup 水平置中 | 都要 | 量每個 popup 左右到畫面邊緣的距離 |
| F7-5 | F7 | popup 的高度依內容、打開時定好，之後不跟著內容伸縮（loading 期間與使用者操作造成的改變除外） | 都要 | popup 開著時讓背景的資料更新，框的高度不變 |
| F7-6 | F7 | popup 最高是畫面高度 − 2：畫面 chip 列或 statusbar 與 footer 永遠看得到（chip 列下面的分隔線可以被蓋住） | 都要 | 打開內容很長的 popup，畫面 chip 列（或 statusbar）與 footer 沒被蓋到 |
| F7-7 | F7 | 內容超過最高時在框裡捲動 | 都要 | 在矮的終端機打開長清單，在框裡捲動看得到全部 |
| F7-8 | F7 | 使用者操作讓 popup 的列數改變時（刪一列、多出一列、打字篩選），不論高度跟不跟著變，揭露的資訊都正確 | 都要 | 在 popup 裡刪一列或打字篩選，框裡沒有殘留、缺漏或錯位的列 |
| F7-9 | F7 | 整個 popup 的內容還在 loading 時，標題後面一定有輪轉的 loading icon | loading | 在載入慢的情況打開那個 popup，標題後面的 icon 在轉 |
| F7-10 | F7 | loading 結束，loading icon 就消失 | loading | 等載入完，標題後面的 icon 不見 |
| F7-11 | F7 | popup 垂直置中（toast 除外） | 都要 | 量每個 popup 上下到畫面邊緣的距離 |
| F7-12 | F7 | 值可能不合格的 popup（input popup、表單）打開時高度就含一列錯誤列，沒有錯誤時空白 | input | 打開它們，框裡留著一列空白的錯誤列 |
| F7-13 | F7 | 值不合格時錯誤寫在錯誤列，框的高度不變 | input | 輸入不合格的值按 `Enter`，錯誤出現在那一列，框不變高 |
| F7-14 | F7 | terminal popup 寬度是 `terminal 寬 − 2`，不受 120 欄上限 | terminal popup | 在 200 欄的終端機打開，寬度是 198 |
| F7-15 | F7 | terminal popup 下面一直到畫面最後一列，蓋掉 footer | terminal popup | 打開 terminal popup，下框在最後一列，footer 不見 |
| F7-16 | F7 | terminal popup 框裡上下左右都不留白 | terminal popup | 看子程序的內容緊貼四邊的框線 |
| F8-1 | F8 | 有 popup 開著時，最上層 popup 以外的一切（底下的 popup 與整個 base 畫面）都淡化，只有最上層是亮的 | 都要 | Space menu 開 global operation popup，底下的 Space menu 與 base 畫面都暗 |
| F8-2 | F8 | 底下的串流內容（log、遠端 session）與警示色也一起淡化 | 串流內容 | 在串流內容或警示色上面開 popup，它們也變暗 |
| F8-3 | F8 | 淡化把前景與背景都往底色淡化，不丟掉背景 | 都要 | 開 popup 後看底下的 powerline 膠囊本體、cursor bar、選取反白仍在，只是變暗 |
| F8-4 | F8 | 每個顏色各自淡化，不剝掉顏色重畫、不把所有前景換成同一個淡色（底下各層 popup 的邊框是各自層色的淡化版，看得出第幾層） | 都要 | 開 popup 後看底下的層色、警示色、串流內容各是自己顏色的淡化版 |
| F8-5 | F8 | 對畫好的畫面淡化一次：失焦的 panel 在 popup 底下會再暗一點 | 多 panel | 開 popup 後，底下失焦的 panel 比打開前 focus 的那個更暗 |
| F8-6 | F8 | toast 不觸發淡化 | toast | 冒出 toast 時，底下畫面不變暗 |

## rules — X Mouse

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| X1-1 | X1 | 沒有 mouse 也能完整操作 app | 都要 | 不用 mouse，只用鍵盤把所有功能走一遍 |
| X2-1 | X2 | 每個 mouse 動作都對應到一個鍵盤動作，沒有只有 mouse 能做的事 | mouse | 列出 app 的每個 mouse 動作，各找到對應的鍵 |

## rules — T 時間軸

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| T1-1 | T1 | 從 popup 開出另一個 popup 的動作，確定之後 source 留不留照 T1 的表（看確定之後的動作）；表上沒有的動作，被清掉的 source 都是使用者用完 target 之後已經不想看的 | 都要 | 走過 app 每個從 menu 執行、會再開 popup 的動作，對照 T1 的表 |
| T1-2 | T1 | 動作前面的 confirm 只是門：在 confirm 上取消，一律回到 source（menu） | confirm | 從 menu 執行一個要先確認的動作，在 confirm 上按 `Esc`，回到原 menu |
| T1-3 | T1 | 確定之後是選一個值寫回去（input popup、select 寫回表單或 picker）時，source 保留 | 表單、input | 在表單選完一欄的值，回到表單 |
| T1-4 | T1 | 確定之後是開 shell 時，清掉 source | PTY | 從 menu 開 shell，離開後原 menu 不在 |
| T1-5 | T1 | 確定之後是換畫面（切到 chip 列的另一個畫面）或 drill-down（例：進目錄、Deployment → Pods）時，清掉 source | 都要 | 從 menu 換畫面或 drill-down，原 menu 不在 |
| T1-6 | T1 | 清掉 source 時，target 打開的同時 source 收起，兩段動畫一起播，不等 source 收完；source 有好幾層時每一層一起收（F2） | 都要 | 錄影看 target 的打開動畫與 source 的收起動畫同時開始 |
| T1-7 | T1 | 確定之後是打開東西來看（YAML 檢視、明細、全文）時，source 保留 | 都要 | 從 menu 打開一個來看的東西，關掉後回到原 menu |
| T1-8 | T1 | 確定之後是用編輯器改那一項（例：`kubectl edit`、`$EDITOR`）時，source 保留 | 都要 | 從 menu 用編輯器改一項，離開編輯器後回到原 menu 或 viewer |
| T1-9 | T1 | 確定之後是讓那一項不在了（刪除、搬走）時，清掉 source | 都要 | 從 menu 刪除一項，確定後原 menu 不在 |
| T2-1 | T2 | 失焦的 panel 用 F8 同一套淡化把內容（含表頭、分組標題、label、cursor）變暗，cursor 不另外換顏色 | 多 panel | `Tab` 換 panel，失焦的 panel 內容變暗、各顏色是自己的淡化版 |
| T2-2 | T2 | 串流內容（log、即時輸出、遠端 session）失焦時不變暗 | 串流內容 | focus 移到別的 panel，串流內容那個 panel 不變暗 |
| T2-3 | T2 | 串流 panel 失焦時內容不變暗，但下框的 hint 照樣變暗 | 串流內容 | focus 移到別的 panel，看串流 panel 的 hint 變暗 |

## rules — S Splash

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| S0-1 | S 章開頭 | splash 佔滿整個畫面，開著時原本的畫面（chip 列、panel、footer）都不畫 | 都要 | 按 `V`，畫面上只有 splash |
| S0-2 | S 章開頭 | 關掉 splash 回到原本的畫面 | 都要 | 關掉 splash，畫面跟按 `V` 之前一樣 |
| S1-1 | S1 | 在 panel 上按 `V` 打開 splash（把 `V` 給 panel operation 用的 panel 除外） | 都要 | 在每個 panel 上按 `V` |
| S1-2 | S1 | 有 panel 把 `V` 拿去用時，app 裡至少有一個 panel 的 `V` 仍是 splash | 都要 | 在每個 panel 按 `V`，至少一個打開 splash |
| S2-1 | S2 | splash 不出現在 Space menu、global operation popup、key reference、footer、panel hint | 都要 | 打開這些地方，找不到 `V` 或 splash |
| S2-2 | S2 | README、CHANGELOG 與 release notes 不寫 splash，已經發出去的舊段落與 release notes 也一樣 | 都要 | 讀檔案：兩份 README、CHANGELOG（含舊版本的段落）都沒提到 splash 或 `V` 的彩蛋；發過版的看 GitHub 上每一個 release 的內文也沒有 |
| S3-1 | S3 | splash 開著時任何鍵都只關掉它，那個鍵不再做別的事（包括 `q`、`Ctrl-C`、`Esc`、`Space`、`?`） | 都要 | 打開 splash 後分別按這些鍵，每次都只關 splash；按 `Ctrl-C` 不離開 app |
| S4-1 | S4 | 啟動時不播 splash | 都要 | 啟動 app，直接進主畫面 |
| S4-2 | S4 | popup 開著時按 `V` 不叫出 splash | 都要 | 開著 Space menu 按 `V` |
| S5-1 | S5 | splash 畫的是該 app 的 `docs/icon.svg`，一格對一格 | 都要 | 按 `V`，跟 `docs/icon.svg` 逐格比對 |
| S5-2 | S5 | `docs/icon.svg` 的 viewBox 是 250 × 250；每一格是一個 10 × 10 的 rect；底色是 `#000000` | 都要 | 讀檔案：`docs/icon.svg` |
| S5-3 | S5 | mark 佔 25 × 19 格（x 0–240、y 30–210），最左、最右一欄是底 | 都要 | 讀檔案：rect 的座標範圍 |
| S5-4 | S5 | U 框是 `#205090`，跟全家族一樣、不改 | 都要 | 讀檔案：`<!-- U -->` 底下的 rect 跟 tdp 的 `principle/icon.svg` 的 U 框相同 |
| S5-5 | S5 | 框裡的字是 `#f2b753`，寫的是 app 自己的名字 | 都要 | 讀檔案並看 splash：金色的字拼出 app 的名字 |
| S5-6 | S5 | 用 XML 註解分字：一個註解開始一個字、註解只寫那個字，後面的 rect 屬於它直到下一個註解；第一個註解是 `<!-- U -->` | 都要 | 讀檔案：註解的位置與內容 |
| S5-7 | S5 | 一格畫一個 `nf-fa-square`（U+F0C8）、佔兩欄；icon 佔一格時後面補一個空白 | 都要 | 在 icon 一格與兩格（`<APP>__ICON_WIDTH`）下各按一次 `V`，每格都是兩欄寬 |
| S5-8 | S5 | 底的格子畫成 Surface0 `#313244` 的方塊 | 都要 | 看 splash 的底 |
| S5-9 | S5 | mark 上下各多畫一列底，共 21 列，四邊的底一樣寬 | 都要 | 數 splash 上 mark 的列數與四邊底的寬度 |
| S5-10 | S5 | mark 下面空一列，接著六列字（介紹與 `developed by` 之間、信箱與提示之間各空一列） | 都要 | 數 mark 下面的列 |
| S5-11 | S5 | 下面的字每一列在 mark 的寬度裡置中 | 都要 | 看每一列左右的空白 |
| S5-12 | S5 | 下面的字每一列都不超過 mark 的寬（50 欄） | 都要 | 量每一列的寬度 |
| S5-13 | S5 | 第一列是名稱：app 的指令名稱，Blue 粗體 | 都要 | 看 splash 的第一列 |
| S5-14 | S5 | 第二列是版本：跟 `<app> version` 印的版號一樣，Blue | 都要 | 比對 splash 的版本與 `<app> version` |
| S5-15 | S5 | 第三列是一句介紹，Text | 都要 | 看 splash 的第三列 |
| S5-16 | S5 | 接著是 `developed by`，Overlay0 | 都要 | 看 splash |
| S5-17 | S5 | 接著是作者的信箱，mark 的金色 `#f2b753`：家族成員寫 `vulcan.shen.2304@gmail.com`，照 tdp 做的 app 寫自己的（E 章開頭） | 都要 | 看 splash |
| S5-18 | S5 | 最後一列是 `Press any key to close`，Overlay0 | 都要 | 看 splash |
| S5-19 | S5 | 整塊（mark、空一列、下面的字，共 30 列 × 50 欄）在畫面上上下左右都置中 | 都要 | 在大的終端機按 `V`，量四邊的空白 |
| S5-20 | S5 | 終端機不到 50 欄或 30 列時不畫 mark，只畫下面的字，上下左右置中 | 都要 | 縮到 49 欄或 29 列以下按 `V` |
| S5-21 | S5 | 放不下 mark 時下面的字照樣分兩批出現：打開 400ms 後名稱、版本、介紹，再 500ms 後作者與提示 | 都要 | 讀程式：放不下 mark 時兩批字的時間 |
| S5-22 | S5 | 太窄時折行，折下來的每一列照樣置中（斷在哪裡照 components 的折行） | 都要 | 縮到比介紹還窄後按 `V` |
| S5-23 | S5 | 一個字本身比終端機寬、照格子切成好幾段時，每段置中，內容不丟 | 都要 | 縮到比信箱（26 欄）還窄後按 `V` |
| S5-24 | S5 | 還是太矮時從下面往上截：最先拿掉提示，接著作者兩列、介紹 | 都要 | 一列一列縮矮後按 `V`，看拿掉的順序 |
| S5-25 | S5 | 名稱與版本一定出現；只有 1 列時只畫名稱 | 都要 | 縮到最矮按 `V`，名稱與版本還在；縮到 1 列，只剩名稱 |
| S5-26 | S5 | 拿掉一組時它上面的空白列跟著拿掉，最底下不留空白列 | 都要 | 縮矮後按 `V`，最後一列有字 |
| S5-27 | S5 | 揭露動畫照順序分段畫（底、金色的字、U 框、下面的字），一個 tick 10ms；第 1–3 段（底、金色的字、U 框）段與段之間停 250ms | 都要 | 讀程式：段的順序、一個 tick 10ms、段與段之間的 250ms |
| S5-28 | S5 | 底：一個 tick 一整列，由上往下鋪滿 | 都要 | 讀程式：底一個 tick 一整列、由上往下 |
| S5-29 | S5 | 金色的字：照 svg 裡註解的順序一個字一段，一個 tick 出現 2 格，同一個字的格子打散出現 | 都要 | 讀程式：照註解的順序、一個 tick 2 格、同一個字的格子打散 |
| S5-30 | S5 | U 框：由下往上一列一列長；同一列從中間往兩端，一個 tick 一對左右對稱的兩格，中線上的第 13 格自己一個 tick | 都要 | 讀程式：由下往上、同一列從中間往兩端、一個 tick 一對、中線上的第 13 格自己一個 tick |
| S5-31 | S5 | 下面的字：從 U 框最後一格出現起算 400ms 後（不再加 250ms）名稱、版本、介紹一起出現，再 500ms 後 `developed by`、信箱、提示一起出現 | 都要 | 讀程式：從 U 框最後一格起算 400ms、再 500ms |

## rules — E App 與環境

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| E1-1 | E1 | `<app> version` 印出版號 | 都要 | 執行 `<app> version` |
| E1-2 | E1 | `<app> help` 印出命令列的用法（不是 key reference） | 都要 | 執行 `<app> help` |
| E2-1 | E2 | app 自己讀的環境變數（含測試用、傳給自己子程序的）都叫 `<大寫 app 名>__<變數名>`：兩個底線，變數名全大寫、單字之間一個底線 | 都要 | 讀程式：找出所有讀寫的環境變數名，除了給別的程式讀的都照這個寫 |
| E2-2 | E2 | `<APP>__CONFIG` 指的是設定目錄（設定檔在裡面），不是設定檔 | 存設定或資料 | 設 `<APP>__CONFIG` 為一個目錄啟動，app 讀那個目錄裡的設定檔 |
| E2-3 | E2 | 環境變數改名時不留舊名 | 都要 | 讀程式：舊名不再被讀 |
| E2-4 | E2 | 要經 ssh 帶到遠端的變數用 `LC_` 開頭（OpenSSH 預設只轉送 `LANG` 與 `LC_*`） | 都要 | 讀程式：帶到遠端的環境變數都是 `LC_` 開頭（沒有 ssh 的 app 沒有這種情況） |
| E3-1 | E3 | 設定預設在 `$XDG_CONFIG_HOME/<app>`（fallback `~/.config/<app>`） | 存設定或資料 | 讀程式或不設環境變數啟動，看設定讀寫的位置 |
| E3-2 | E3 | 設定的位置可以用 `<APP>__CONFIG` 覆寫 | 存設定或資料 | 設 `<APP>__CONFIG` 啟動，設定改到那裡 |
| E3-3 | E3 | app 另外存的狀態預設在設定目錄裡 | 存設定或資料 | 讀程式或啟動後看狀態檔的位置 |
| E3-4 | E3 | 狀態的位置可以用 `<APP>__STATE` 覆寫 | 存設定或資料 | 設 `<APP>__STATE` 啟動，狀態改存到那裡 |
| E3-5 | E3 | 資料預設在 `~/.<app>/` 底下 | 存設定或資料 | 讀程式或啟動後看資料的位置 |
| E3-6 | E3 | 資料的位置可以用 `<APP>__DATA` 覆寫 | 存設定或資料 | 設 `<APP>__DATA` 啟動，資料改存到那裡 |
| E3-7 | E3 | 快取在系統的快取目錄（macOS `~/Library/Caches/<app>`；Linux `$XDG_CACHE_HOME/<app>`，fallback `~/.cache/<app>`；Windows `%LOCALAPPDATA%\<app>\cache`） | 存設定或資料 | 讀程式或啟動後看快取的位置 |
| E3-8 | E3 | 快取的位置可以用 `<APP>__CACHE` 覆寫 | 存設定或資料 | 設 `<APP>__CACHE` 啟動，快取改存到那裡 |
| E3-9 | E3 | Windows 上 `~` 是 `%USERPROFILE%`：設定 `%USERPROFILE%\.config\<app>`、資料 `%USERPROFILE%\.<app>\`，不用 `%APPDATA%` | 出 Windows 版 | 讀程式：Windows 的路徑算法 |
| E3-10 | E3 | popup 預覽裡藏起私鑰與只有擁有者能讀的檔，用設定 key `hide_secrets_in_preview`（放在 app 的設定檔），預設 `false`：全部照常顯示 | 有檔案預覽 | 讀程式與設定檔：key 的名字與預設值 |
| E3-11 | E3 | （只有 App Log 的 app 不算）寫入狀態按 `Tab` 插入幾個空白、拿來讀的內容（viewer、檔案預覽、panel 上的 log）裡的 Tab 畫幾格，用設定 key `input_tab_width`，預設 `4` | textarea、viewer、串流內容、有檔案預覽 | 讀程式與設定檔：key 的名字與預設值 |
| E3-12 | E3 | 設定檔是設定目錄裡的 `config.yaml` | 存設定或資料 | 讀程式或啟動後看設定檔的名字與格式 |
| E3-13 | E3 | 東西照「刪掉會怎樣」放：app 自己一個一個的選項是設定；刪了只是回到預設的是狀態；刪了找不回來、會想備份的（書籤、紀錄、log、使用者寫給 app 用的清單——就算內容是 app 怎麼運作的選項——、app 替使用者記下的原值）是資料；刪了會自己重建或重抓的是快取 | 存設定或資料 | 讀程式：每一種寫到磁碟的東西，放在哪一類的位置 |
| E3-14 | E3 | 改版換了位置時，第一次啟動逐項搬：新位置沒有的那一項搬過去，跳一個 toast 說從哪裡搬到哪裡；搬完把空了的舊目錄拿掉 | 存設定或資料 | 讀程式；或在舊位置放東西後啟動新版（app 換過位置時） |
| E3-15 | E3 | 搬不動時照舊用舊位置，開 error popup 寫出兩個路徑 | 存設定或資料 | 讀程式；或讓新位置寫不進去後啟動 |
| E3-16 | E3 | 搬家時新位置已經有的那一項：快取刪掉舊的；設定、狀態、資料不刪、留在舊位置，開 error popup 寫出兩個路徑 | 存設定或資料 | 讀程式；或在新、舊位置都放同一項後啟動新版 |
| E3-17 | E3 | app 自己的設定、狀態、資料讀不了時，啟動時開 confirm 寫出路徑與原因，hint 是 `Enter:move Esc:quit` | 存設定或資料 | 把設定檔改成壞掉的格式後啟動 |
| E3-18 | E3 | 讀不了的 confirm 按 `Enter`：檔案改名成 `.bak`，像第一次打開一樣照常開始 | 存設定或資料 | 同上按 `Enter`：有 `.bak`，app 跟第一次打開時一樣（第一次打開會建的檔又建了） |
| E3-19 | E3 | `.bak` 已經在時用 `.bak.1`、`.bak.2`……，不蓋掉；問句寫實際會用的名字 | 存設定或資料 | 先放一個 `.bak` 再讓檔案壞掉、啟動 |
| E3-20 | E3 | 讀不了的 confirm 按 `Esc`：離開 app，路徑與原因寫到 stderr | 存設定或資料 | 同上按 `Esc`，看 app 結束、終端機上的訊息 |
| E3-21 | E3 | 快取讀不了時不問，丟掉重建 | 存設定或資料 | 把快取的檔弄壞後啟動，沒有 confirm |
| E3-22 | E3 | 資料是一筆一個檔時，讀不了的那一筆按 `Enter` 只改名成 `.bak`、不另外建，其他照常讀；問句寫 `go on without it` | 存設定或資料 | 把其中一筆的檔弄壞後啟動，按 `Enter` |
| E3-23 | E3 | app 不再用的設定、狀態、資料檔不刪、不跳 toast；檔案還在時每次啟動在 App Log 記一筆 INFO，寫出路徑 | 不再用的檔 | 放一個 app 不再用的舊檔後啟動，看 App Log 與磁碟；重開再看一次 App Log |
| E4-1 | E4 | 程式碼裡的 PUA glyph 寫成 code point | 都要 | 讀程式：掃原始碼找不到 PUA 字元 |
| E4-2 | E4 | README 的需求段寫明需要 Nerd Font | 都要 | 讀兩份 README 的前置需求 |
| E4-3 | E4 | README 的需求段跟 Nerd Font 並列寫明需要 truecolor terminal（24-bit 色） | 都要 | 讀兩份 README 的前置需求 |
| E5-1 | E5 | 量的是游標實際前進幾格（glyph 溢出到隔壁、游標只前進一格的照一格算） | 都要 | 在 icon 佔兩格的終端機開 app，框線對齊 |
| E5-2 | E5 | icon（PUA，powerline 符號除外）與 powerline 符號（U+E0A0–U+E0D7）分開量、各自記 | 都要 | 讀程式：兩種各有自己的寬度；在「icon 兩格、powerline 一格」下框線都對齊 |
| E5-3 | E5 | app 啟動時用 CPR 探測：印一個 icon 問游標位置，再印一個 powerline 符號再問一次 | 都要 | 讀程式：啟動時的探測 |
| E5-4 | E5 | 所有量寬度的地方（補空白、截斷、置中、並排、框線、疊 popup）都走同一個顯示寬度函式 | 都要 | 讀程式：找不到繞過顯示寬度函式量寬度的呼叫 |
| E5-5 | E5 | icon 的寬度照 `<APP>__ICON_WIDTH` → `TERMINU__ICON_WIDTH` → `LC_TERMINU_ICON_WIDTH` → 探測的順序取 | 都要 | 幾個變數都設、只設一部分、都不設各啟動一次，看用的是哪個值 |
| E5-6 | E5 | powerline 符號的寬度照 `<APP>__POWERLINE_WIDTH` → `TERMINU__POWERLINE_WIDTH` → `LC_TERMINU_POWERLINE_WIDTH` → 探測的順序取 | 都要 | 幾個變數都設、只設一部分、都不設各啟動一次，看用的是哪個值 |
| E5-7 | E5 | 探測只在 unix 做；Windows 預設一格，靠環境變數覆寫 | 出 Windows 版 | 讀程式：Windows 不探測、預設一格 |
| E5-8 | E5 | 開子程序時在子程序的環境設 `TERMINU__ICON_WIDTH` 與 `TERMINU__POWERLINE_WIDTH`（自己用的格數） | PTY | 在 PTY 裡 `echo $TERMINU__ICON_WIDTH $TERMINU__POWERLINE_WIDTH` |
| E5-9 | E5 | 有 ssh 的 app 連線時，把自己用的格數放進 `LC_TERMINU_ICON_WIDTH` 與 `LC_TERMINU_POWERLINE_WIDTH` 帶到遠端 | PTY | 讀程式：連線時送出這兩個變數；在遠端跑家族 app，框線對齊 |
| E5-10 | E5 | 疊 popup 時 popup 比畫面寬或高（含兩邊都大），起點取 0、超出畫面的部分切掉，不 panic | 都要 | 把終端機縮得比 popup 小再開 popup、邊開邊調整大小，app 不當掉 |
| E5-11 | E5 | app 的 L4 畫面測試（自己的版面加上自己會開的 popup）另外跑兩次：「icon 佔兩格、powerline 符號一格」與「兩種都佔兩格」 | 都要 | 讀程式：測試 |
| E5-12 | E5 | 上面的測試量疊上去的整個畫面；不用 lib 的 app 也單獨量每一種 popup 的框（用 lib 時單獨量框歸 lib，E8） | 都要 | 讀程式：測試 |
| E5-13 | E5 | 上面的測試邊界含 popup 比畫面寬、比畫面高、兩邊都大三種情況，以及比 L1 的最低尺寸小、一直到 1×1 的尺寸（例：80×5、1×1）：不當掉，畫出名稱與提示 | 都要 | 讀程式：測試 |
| E6-1 | E6 | 單一靜態 binary，goreleaser 建置 | 都要 | 讀檔案：`.goreleaser.yaml`（`CGO_ENABLED=0`），發布的是單一執行檔 |
| E6-2 | E6 | 有 `install.sh`、`uninstall.sh`，用 `curl \| sh` 安裝與移除，免 sudo | 都要 | 照 README 的指令安裝再移除，不需要 sudo |
| E6-3 | E6 | 另發到 Homebrew tap：家族成員發到 `vulcanshen/homebrew-tap`，照 tdp 做的 app 發到自己的 tap | 發過版 | 看 tap 有這個 app 最新版的 formula |
| E6-4 | E6 | 有跨尺寸的畫面測試：自己的版面加上自己會開的 popup，多種終端機尺寸下每一列都剛好等於終端機寬度 | 都要 | 讀程式：測試 |
| E6-5 | E6 | 有測試守住程式裡給 splash 用的那一份（`internal/` 裡的副本檔或寫死的格子）跟 `docs/icon.svg` 一模一樣 | 都要 | 讀程式：測試比對兩份 |
| E6-6 | E6 | demo gif 用 VHS 錄，腳本放在 `.local/demos/` | 都要 | 讀檔案：`.local/demos/` 有 tape |
| E7-1 | E7 | 有 `README.md`（英文）與 `README-zh_TW.md`（繁中） | 都要 | 讀檔案 |
| E7-2 | E7 | 兩份 README 內容對齊 | 都要 | 讀檔案：兩份逐段對照 |
| E7-3 | E7 | README 只寫使用者需要知道的 | 都要 | 讀兩份 README：每一段都是使用者用這個工具需要知道的 |
| E7-4 | E7 | README 第 1 段：標題、badge、語言切換（`English · 繁體中文`） | 都要 | 讀兩份 README 的開頭 |
| E7-5 | E7 | README 第 2 段：一句話定位 + 一段「它能做什麼」 | 都要 | 讀兩份 README |
| E7-6 | E7 | README 第 3 段只有一張代表性的 demo gif | 都要 | 讀兩份 README 的第 3 段，數 gif |
| E7-7 | E7 | README 第 4 段：特色，寫使用者拿到什麼，不寫怎麼做到的 | 都要 | 讀兩份 README 的特色段 |
| E7-8 | E7 | README 第 5 段：安裝，寫了前置需求、安裝方式、第一次啟動會發生什麼、移除 | 都要 | 讀兩份 README 的安裝段，四項都在 |
| E7-9 | E7 | README 第 6 段：快速開始 | 都要 | 讀兩份 README |
| E7-10 | E7 | README 第 7 段：使用方式與按鍵 | 都要 | 讀兩份 README |
| E7-11 | E7 | README 第 8 段：設定與資料存放位置 | 都要 | 讀兩份 README |
| E7-12 | E7 | README 第 9 段：限制，用使用者的語言寫 | 都要 | 讀兩份 README 的限制段 |
| E7-13 | E7 | README 第 10 段：相關連結，有 CHANGELOG | 都要 | 讀兩份 README 的相關連結 |
| E7-14 | E7 | README 第 11 段：terminu family —— 家族成員寫遵循 terminu design，附上 tdp、terminu-go、terminu-harness 的連結，不列家族成員；照 tdp 做的 app 寫照 terminu design 做、附上 tdp 的連結 | 都要 | 讀兩份 README：三個連結都在，沒有列其他 app |
| E7-15 | E7 | README 第 12 段：License | 都要 | 讀兩份 README |
| E7-16 | E7 | README 的 12 段都在，照 1–12 的順序 | 都要 | 讀兩份 README 的段落順序 |
| E7-17 | E7 | README 沒有寫死版本號的「現況」段 | 都要 | 讀兩份 README |
| E7-18 | E7 | README 的設定段寫出這個 app 用到的 E3 共用設定 key 與預設值 | 存設定或資料 | 讀兩份 README 的設定段 |
| E7-19 | E7 | README 講 icon 寬度的地方寫出 `<APP>__ICON_WIDTH`、`TERMINU__ICON_WIDTH`、`<APP>__POWERLINE_WIDTH`、`TERMINU__POWERLINE_WIDTH` | 都要 | 讀兩份 README 講 Nerd Font 或 icon 寬度的地方 |
| E7-20 | E7 | README 說明 `TERMINU__` 的是全家族共用：設一次家族每個 app 都讀到，在家族 app 的 PTY 裡跑時外層 app 會替它設好 | 都要 | 讀兩份 README 同一處 |
| E7-21 | E7 | README 不舉「一定佔兩格」的字型當例子 | 都要 | 讀兩份 README 講 icon 寬度的地方 |
| E7-38 | E7 | 屬於 12 段裡某一段的內容放進那一段當小節（例：更新放進「安裝」，跟移除放在一起） | 都要 | 讀兩份 README 的段落與小節 |
| E7-39 | E7 | app 自己加的段只在第 4 段（特色）到第 9 段（限制）之間，接在最有關的那一段後面；第 1–3 段、第 10–12 段之間沒有別的段 | 都要 | 讀兩份 README 的段落順序 |
| E7-40 | E7 | 有疑難排解的段時，放在「使用方式與按鍵」之後 | 都要 | 讀兩份 README（沒有疑難排解的 app 沒有這種情況） |

## components（README）

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| components-1 | components.2 | label 與值之間兩格（statusbar 的 `label: 值` 例外，見 components-25） | 都要 | 看表單、一列一個值的 panel 上 label 與值之間的空格數 |
| components-2 | components.2 | 表格的欄與欄之間兩格 | 表頭 | 看清單的表頭與各列，欄與欄之間的空格數 |
| components-3 | components.2 | 並排的項目之間兩格 | 都要 | 看並排的項目（statusbar 的組、chip、並排的按鈕……）之間的空格數 |
| components-4 | components.2 | glyph 與它後面的字之間一格 | 都要 | 看 popup 標題、menu 區塊標題、標記的列這些 glyph 後面的空格數 |
| components-5 | components.3 | 要折行的文字（textarea、viewer、confirm、note、toast、error popup、空狀態的句子、太窄時的 splash）在空白處斷：一列放不下下一個字時，整個字接到下一列；放不下就折行、不截斷 | 都要 | 在 textarea、viewer、confirm、toast、error popup 裡放一段比框寬的英文，縮窄終端機後按 `V`，看英文單字沒有被切開 |
| components-6 | components.3 | 寬字（佔兩格的字，例：中文、日文）每個字之間、跟它前後的字之間都可以斷，一列填滿再換列 | 都要 | 放一段比框寬的中文或中英混排，看每一列都填滿才換列 |
| components-7 | components.3 | 一個字本身就比一列還長時（例：很長的網址），才照格子切；這一列前面已經有字時，先換到新的一列再切 | 都要 | 放一個前面有字、比框寬的網址，看它從新的一列開頭照格子切成好幾段 |
| components-8 | components.3 | 照格子切時寬字不切成兩半：一列只剩一格時，那個寬字整個接到下一列 | 都要 | 放含中文的長字串，看列尾沒有半個寬字、框線不歪 |
| components-9 | components.4 | panel 的 `[N] label` 膠囊大寫 | 都要 | 看每個 panel 左上角的膠囊 |
| components-10 | components.4 | panel 的 tab 大寫 | panel tab | 看有 tab 的 panel 上框的每一個 tab |
| components-11 | components.4 | 畫面 chip 大寫 | 多畫面 | 看最上面一列的每一個 chip |
| components-12 | components.4 | popup 的標題大寫 | 都要 | 打開幾種 popup，看標題膠囊的字 |
| components-13 | components.4 | 表頭大寫 | 表頭、一列一個值的 panel | 看清單與一列一個值的 panel 的表頭 |
| components-14 | components.4 | 清單的分組標題大寫 | 分組清單 | 看分組清單的每一個分組標題 |
| components-15 | components.4 | 一列一個值的 panel 的 label 大寫 | 一列一個值的 panel | 看設定這類 panel 的 label 欄 |
| components-16 | components.4 | 值不改大小寫（color picker 的 hex 一律大寫是顏色的寫法，不算改值） | 都要 | 看表單、一列一個值的 panel 上的值跟原本的大小寫一樣 |
| components-17 | components.4 | menu 的 label 與說明不改大小寫 | 都要 | 按 `Space` 看各列的 label 與說明沒被轉成大寫 |
| components-18 | components.4 | hint 與 footer 的說明不改大小寫 | 都要 | 看 footer 與下框 hint 冒號後面的字 |
| components-19 | components.4 | 模式名不改大小寫 | 模式 | 進入模式，看上框右邊的模式名（`Drag` 不寫成 `DRAG`） |
| components-20 | components.4 | app 自己的內容（statusbar、清單裡的資料）不改大小寫 | 都要 | 看 statusbar 與清單裡的資料照原樣 |
| components-21 | components.4 | 標題裡的名稱、路徑照原樣（`EDIT: filu`、`IDENTITY FILE · ~/.ssh`） | 都要 | 打開對某一個東西做的 popup，看名稱部分沒被轉成大寫 |
| components-22 | components.6 | 元件的樣子只從 components 列出的方案裡挑，不在 app 裡自己發明 | 都要 | 對照各元件列出的方案，看 app 用的都是其中一種 |
| components-23 | components.3 | 一個字剛好填滿一列、後面接著空白時，那個空白畫在下一列的第一格 | textarea、viewer | 在 textarea 打字，讓一個字剛好填滿一列再打空白，看空白在下一列開頭、游標停得上去 |
| components-24 | components.3 | 只是顯示的文字（confirm、note、toast、error popup、空狀態、splash）斷在空白處時，那個空白不畫：下一列開頭不會多一格空白 | 都要 | 讓 toast、confirm 或太窄時的 splash 的文字剛好在一個字後面折行，看下一列開頭沒有空白、置中沒有偏 |
| components-25 | components.2 | statusbar 的一組寫成 `label: 值`，冒號後面空一格；組與組之間兩格，不另外加分隔符號 | statusbar | 看 statusbar 的每一組與組之間 |
| components-26 | components.4 | panel 標題裡的名稱照原樣（`[2] PODS: nginx-7d4f`），整個 label 就是名稱時照原樣（`[1] prod-web-01`） | 都要 | 看 label 裡有名稱的 panel 的膠囊 |
| components-27 | components.5 | 名字與短字（表單與 panel 上的值、清單的格子、menu、popup 標題、toast、confirm、error popup、選項、說明列、空狀態、statusbar、tab 名稱、finder 的項目）裡的控制字元，連 Tab、`\n`、顏色碼的 ESC，都畫成紅色的名字；不丟、不換成空白、不原樣送給終端機 | 都要 | 讓一個會出現在這些地方的名字（例：檔名、網頁標題）含 Tab 或 `\x1b[31m`，看清單、menu、confirm；或讀程式 |
| components-28 | components.5 | panel 上的 log 照終端機的樣子畫：`\n` 是換行，Tab 是空白，顏色碼照著上色，一行裡的 `\r` 只留最後的狀態，其他控制字元與不是顏色碼的序列畫成紅色的名字 | 串流內容 | 讓 log 收到一行彩色的字、一行 `10%\r100%`、一行含 `\x1b[2J`，看 log panel |
| components-29 | components.5 | app 標成「一行文字」的清單欄（原始碼、log 的一行）裡，Tab 畫成 `input_tab_width` 格空白，其他控制字元照舊畫成紅色的名字 | 都要 | 讓那一欄有一行含 Tab 的文字，看縮排；讀程式：哪些欄標了 |
| components-30 | components.5 | app 自己寫的名字與短字裡沒有換行字元：用一般資料（沒有刁鑽值）走過時，畫面上沒有紅色的 `\n` | 都要 | 用一般資料走過每個會跳訊息的地方（error popup、toast、confirm）；或讀程式：app 的字串裡沒有 `\n` |
| components-31 | components.5 | error popup 的訊息、toast、confirm 的內容有好幾列時，每一列另起一列、太長折行，列跟列之間不空列 | 都要 | 讓一個訊息有兩列，看畫面 |
| components-32 | components.5 | 外面來的好幾行字不整段放進短字：放說原因的那一行，全文寫進 App Log | 都要 | 讓外面的程式失敗、吐出好幾行錯誤，看 toast 或 error popup 與 App Log |

## color

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| color-1 | color.1 | 介面元素的顏色只用 color 的色碼（catppuccin-mocha）與從錨點推導出的層色，不為個別元素另挑顏色 | 都要 | 讀程式：介面元素的顏色都引用色碼表與層色；畫面上的介面顏色都對得上表裡的色碼 |
| color-2 | color.1 | 一個顏色只代表一個意義，其他意義不用同一個顏色 | 都要 | 對照色碼表看各介面元素（例：popup 的框不是 Lavender） |
| color-3 | color.1、color.3 | 第 K 層 popup 的框與標題用第 K 層的層色：最底下的 popup 是第 1 層，第 1、2、3 層依序是 `#A4C0FA` `#94C3F5` `#84C5F1`，第 4 層以上固定 `#74c7ec`；error popup 例外，用 Red | 都要 | 一層一層疊開 popup（到第 5 層），量每一層框與標題膠囊的顏色 |
| color-4 | color.1 | 錯誤 Red、警告 Peach 在哪一層都是同一個顏色，不跟層數換色 | 都要 | 在第 1 層與第 2 層的 popup 裡各出一次錯誤或警告，比顏色 |
| color-5 | color.1 | 粗體只用在 cursor 上的字、popup 的標題、選中的膠囊的字、模式名、popup 標題後面的 loading icon、splash 的名稱、畫面比最低尺寸小時正中央的 app 名稱 | 都要 | 看各畫面：表頭、分組標題、label、hint、footer、沒選中的膠囊、panel 上框的 loading icon 都不加粗 |
| color-6 | color.2 | popup 下框 hint 的鍵 Blue（`#89b4fa`），冒號與說明 Overlay0（`#6c7086`） | 都要 | 打開任何 popup 看下框的 hint |
| color-7 | color.2 | 停用的列、label、選項用 Surface2（`#585b70`） | 停用 | 讓一個動作或選項暫時不能用，看它的顏色 |
| color-8 | color.2 | popup 裡的 cursor 色塊是層色底、字 Base（`#1e1e2e`）粗體，字原本的顏色不保留 | 都要 | 按 `Space` 看 menu 的 cursor 那一列 |
| color-9 | color.2 | panel 的位置列（麵包屑）用 Lavender | 位置列 | 看位置列 |
| color-10 | color.2 | 活著的 session 用 Green | PTY | 看活著的 session 的標示 |
| color-11 | color.2 | 進行中的工作與進度條用 Green（單畫面的 app 寫在工作自己的列裡） | 長時間工作 | 開始一個長時間的工作，看進度條與工作的標示 |
| color-12 | color.2 | 成功完成的用 Green：Success toast 的字 | toast | 完成一個動作，看 Success toast 的字 |
| color-13 | color.2 | 模式的外框用 Yellow（`#f9e2af`） | 模式 | 進入模式，看外框的顏色 |
| color-14 | color.2 | 隔開幾個鍵的 `\|`（`j\|k`）用 Overlay0，不用鍵的顏色 | 都要 | 看 footer、hint 裡含 `\|` 的那一組 |
| color-15 | color.2 | 沒有 focus 的按鈕（表單的動作區、color picker 的 `Choose`）也有底色：Surface1 底、字 Text | 表單、color picker | 看表單動作區裡沒有 focus 的按鈕 |
| color-16 | color.2 | 內容本身是顏色的格子（顏色值的 `███`）放在 cursor 色塊上時保留自己的顏色，同一塊上的其他字照樣換成 Base | color picker | 把 cursor 移到顏色值那一列，看 `███` 的顏色不變、其他字是 Base |
| color-17 | color.2 | 畫面不塗底色：沒有指定背景的格子留給終端機自己的底色 | 都要 | 把終端機底色換成不是 Base 的顏色，看畫面沒有被塗成 Base |
| color-18 | color.3 | 在收的 popup 不算進 K：target 打開、source 同時收起時，target 從第一格就用它最後所在那一層的層色，source 收完時不跳色 | 都要 | 從會被清掉的 source 打開 target，逐格看 target 框的顏色 |
| color-19 | color.4 | 淡化公式是 `dim(c) = c × 0.45 + t × 0.55`（t `#0c0c13`，Crust 的下一格），每個通道四捨五入（.5 進位） | 都要 | 開 popup，量底下的顏色（例：Blue `#89b4fa` 淡化成 `(68,88,123)`） |
| color-20 | color.4 | 256 色的 16–255 照標準值換成 RGB 再淡化 | 都要 | 讀程式：256 色轉 RGB 用標準值 |
| color-21 | color.4 | 16 色（0–15）用終端機的調色盤換成 RGB：啟動時（跟 Rules E5 的 icon 寬度探測同一個時間點）用 OSC 4 問 | 都要 | 讀程式：啟動時送 OSC 4 的查詢；在改過調色盤的終端機裡看 16 色內容淡化後色相不跳 |
| color-22 | color.4 | 問不到調色盤時用 xterm 的預設值 | 都要 | 讀程式：沒回答時的 16 色值是 xterm 的預設 |
| color-23 | color.4 | 淡化絕不讓顏色變亮：每個通道取原值與淡化值較小的那個 | 都要 | 讓底下有 `#000000` 的字，開 popup 後它維持原色 |
| color-24 | color.4 | 淡化後的輸出一律是 24-bit（`38;2;…` / `48;2;…`） | 都要 | 擷取 popup 打開時的輸出，看淡化後的顏色碼 |
| color-25 | color.4 | 沒有指定前景的文字，淡化後給 `dim(Text #cdd6f4)` | 都要 | 擷取輸出，看原本沒有前景色的字淡化後的顏色碼 |
| color-26 | color.4 | 淡化不動 bold、reverse、游標移動、文字與版面 | 都要 | 開 popup 前後比對底下畫面的字、位置與粗體 |

## layout/screen

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| screen-1 | screen.1 | 多畫面的 app 最上面一列是畫面 chip 列 | 多畫面 | 看畫面最上面一列 |
| screen-2 | screen.1 | 最上面一列（多畫面的 app 是 chip 列加它下面的分隔線，共兩列）與 footer 之間其餘的高度都是 panel 區 | 都要 | 看 panel 從最上面一列（多畫面的 app 從 chip 列下的分隔線，沒有最上面一列的單畫面 app 從第一列）下面一直排到 footer 上面 |
| screen-3 | screen.1 | 最下面一列是 footer，只佔一列 | 都要 | 看畫面最下面一列 |
| screen-4 | screen.2 | footer 的鍵 Blue、冒號與說明 Overlay0 | 都要 | 看 footer 的顏色 |
| screen-5 | screen.2 | footer 寬度不夠時從尾端整組捨棄 | 都要 | 把終端機縮窄，看 footer 從尾端少掉整組 `鍵:說明` |
| screen-6 | screen.2 | 畫面有好幾個 panel 時，footer 是 `Space:menu ?:help !:log Tab\|1–N:panels q:quit` | 多 panel | 在有好幾個 panel 的畫面看 footer |
| screen-7 | screen.2 | 只有一個 panel 的畫面，footer 是 `Space:menu ?:help !:log q:quit` | 都要 | 在只有一個 panel 的畫面看 footer（多畫面的 app 每個畫面各看一次） |
| screen-8 | screen.2 | 模式在 panel 上時，footer 是 `Space:menu ?:help`、模式自己的鍵、最後 `Esc:<離開的動詞>` | 模式（在 panel 上） | 進入模式，看 footer |
| screen-9 | screen.2 | panel filter 打字中，footer 是 `Enter\|Tab:list Esc:clear` | panel filter | 按 `/` 打字時看 footer |
| screen-10 | screen.2 | focus 在 panel 裡的 PTY 時，footer 寫出口鍵，再加 app 保留的鍵（互動 terminal 還有 `Alt-v`、`PgUp`）；不寫 `?` 與 `Space` | PTY | 進 PTY，看 footer 第一組是出口鍵 |
| screen-11 | screen.2 | popup 開著時 footer 照底下畫面的寫，不換字（terminal popup 例外：footer 不畫，terminal-13） | 都要 | 開 popup 前後比對 footer 的字 |
| screen-12 | screen.3 | 每個畫面一個膠囊，照膠囊串畫 | 多畫面 | 看最上面一列 |
| screen-13 | screen.3 | 選中的畫面填 Blue、字 Base 粗體 | 多畫面 | 看目前畫面的 chip |
| screen-14 | screen.3 | 沒選中的畫面底是 Mantle、字 Blue、不加粗 | 多畫面 | 看其他畫面的 chip |
| screen-15 | screen.3、screen.4 | 多畫面的 app 把 statusbar 的內容放在 chip 列的右邊，不另開一列 | 多畫面＋statusbar | 看 chip 列右邊 |
| screen-16 | screen.3 | chip 列下面一條全寬的粗線 `━`，Overlay0 | 多畫面 | 看第二列 |
| screen-17 | screen.3 | 長時間的工作進行時，分隔線從左邊填 Green 當進度條 | 多畫面＋長時間工作 | 開始一個長時間的工作，看 chip 列下面的線 |
| screen-18 | screen.4 | 單畫面的 app 的 statusbar 放在最上面一列 | statusbar | 看最上面一列 |
| screen-19 | screen.4 | statusbar 的一般文字 Overlay0 | statusbar | 看 statusbar 的顏色 |
| screen-20 | screen.4 | statusbar 上「你現在在哪」的值 Lavender | statusbar | 看 statusbar 上表示目前位置的值 |
| screen-21 | screen.4 | statusbar 上錯誤的數量 Red | statusbar | 製造錯誤，看 statusbar 的錯誤數 |
| screen-22 | screen.4 | statusbar 上警告的數量 Peach | statusbar | 製造警告，看 statusbar 的警告數 |
| screen-23 | screen.4 | statusbar 放不下時截斷，不折行 | statusbar | 把終端機縮窄，看 statusbar 還是一列 |
| screen-24 | screen.5 | 所有 panel 放不下時，只畫有 focus 的那一個 panel，佔滿寬度 | 多 panel | 把終端機縮窄到窄寬的門檻以下（最低尺寸以上） |
| screen-25 | screen.5 | 窄寬時 `Tab` 照樣換 panel，一次看一個 | 多 panel | 窄寬時按 `Tab` |
| screen-26 | screen.5 | 窄寬的門檻不高於 60 欄 | 多 panel | 把終端機調到 60 欄，看 panel 照常並排 |
| screen-27 | screen.8 | 空狀態寫一句事實，加上一句點名按鍵的提示 | 都要 | 讓一個 panel 沒有資料，看中間 |
| screen-28 | screen.8 | 空狀態置中 | 都要 | 同上，看兩句的位置 |
| screen-29 | screen.8 | 空狀態的兩句都用 Overlay0 | 都要 | 同上，看顏色 |
| screen-30 | screen.8（圖） | 事實與提示之間空一列 | 都要 | 讓一個 panel 沒有資料，看事實與提示兩句之間 |
| screen-31 | screen.2 | panel filter 打字中、沒有結果時，footer 是 `Tab:list Esc:clear`（沒有 `Enter`） | panel filter | 按 `/` 打一串比對不到的字，看 footer |
| screen-32 | screen.3 | 單畫面的 app，長時間工作的進度寫在那個工作自己的列裡 | 長時間工作 | 在單畫面的 app 開始一個長時間的工作，看工作那一列 |
| screen-33 | screen.6 | 放大一個 panel，沒有另外定怎麼放大時照預設做（只畫有 focus 的那一個 panel、佔滿 panel 區；`Tab`、數字鍵換到的 panel 也放大；再按一次放大的鍵才還原） | zoom | 放大後按 `Tab`、數字鍵，再按放大的鍵 |
| screen-34 | screen.8 | 空狀態的句子太長時在空白處折行，每一列置中，左右照樣離框一格；不截斷 | 都要 | 把一個沒有資料的 panel 縮窄，看兩句 |
| screen-35 | screen.2 | App Log 有沒看過的錯誤時 footer 的 `!:log` 換成 `!:N errors`（Red），只有警告時 `!:N warning`（Peach）；打開 App Log 後回到 `!:log` | 都要 | 觸發一個錯誤，看 footer；按 `!` 看過後再看 |

## layout/panel

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| panel-1 | panel.1 | 有 focus 的 panel 框是 Blue 粗線 `┏━┓` | 都要 | 看有 focus 的 panel 的框線 |
| panel-2 | panel.1 | 失焦的 panel 框是 Surface2 細線 `┌─┐`（直角） | 多 panel | 按 `Tab` 換 panel，看離開的那一個的框 |
| panel-3 | panel.1 | 每個 panel 上框左邊有 `[N] label` 膠囊，緊接著左上角 | 都要 | 看每個 panel 的左上角，膠囊與角之間沒有線 |
| panel-4 | panel.1 | panel 在 loading 時，loading icon 放在整串膠囊（含 tab）的後面，前後各空一格 | loading | 讓 panel 重新載入，看上框膠囊串後面 |
| panel-5 | panel.3 | 模式名放在模式所在的框（panel 或 popup）的上框右邊，夾在兩個框線接頭之間 | 模式 | 進入模式，看上框右邊 |
| panel-6 | panel.3（圖） | 模式名緊貼兩個接頭，中間不加空白（`┫Drag┣`） | 模式 | 進入模式，看接頭與模式名之間 |
| panel-7 | panel.3 | 模式名的接頭跟框同色 | 模式 | 進入模式，比較接頭與框線的顏色 |
| panel-8 | panel.3 | 接頭的線型跟著框：粗線框（有 focus 的 panel、popup）用 `┫` `┣`，細線框（失焦的 panel）用 `┤` `├` | 模式（在 panel 上）＋多 panel | 在模式裡按 `Tab` 換走，看接頭從粗線換成細線 |
| panel-9 | panel.3 | 模式名用模式色加粗 | 模式 | 進入模式，看模式名的顏色與粗細 |
| panel-10 | panel.3 | 模式名盡量一個詞 | 模式 | 看每一個模式名 |
| panel-11 | panel.3 | 放不下時先截標題，模式名留著 | 模式 | 在模式裡把終端機縮窄，看標題先被截、模式名還在 |
| panel-12 | panel.3 | 在模式裡，膠囊跟著外框換成模式色 | 模式 | 進入模式，看膠囊的顏色 |
| panel-13 | panel.1 | 每個 panel 下框左邊都有 hint；panel 上一個按得動的鍵都沒有時（例：唯讀的 panel，或清單空了、又沒有對整個 panel 的鍵）不寫 hint，只剩框線 | 都要 | 看每個 panel 的左下；讓清單空掉看沒有按得動的鍵的 panel |
| panel-14 | panel.1 | focus 在 panel filter 的打字列上時不寫 hint，focus 回到清單時 hint 回來 | panel filter | 按 `/` 看下框，再按 `Enter` 回清單看下框 |
| panel-15 | panel.1 | focus 在 panel 裡的 PTY 時不寫 hint，離開 PTY 時回來 | PTY | 進 PTY 看下框，按出口鍵離開再看 |
| panel-16 | panel.1 | 框上的字與角之間隔一段線：hint 是 `┗━ ` 開頭、捲動位置是 ` ━┛` 結尾、模式名後面是 `┣━┓`；只有 `[N] label` 膠囊緊接左上角 | 都要 | 看 panel 的四個角 |
| panel-17 | panel.1 | hint 照 popup 的 hint 的順序：`Enter` 第一，有 tab 時接 `h\|l:tab`，再接這個 panel 自己的鍵 | 都要 | 看各 panel 的下框 hint，`Enter` 排第一（例 `Enter:logs .:helm`） |
| panel-18 | panel.1 | hint 寫這個 panel 自己的鍵：`Enter` 在這裡做什麼、常用的熱鍵 | 都要 | 看各 panel 的 hint |
| panel-19 | panel.1 | hint 不寫移動鍵，例外是有兩個以上的 tab 時寫 `h\|l:tab` | 都要 | 看各 panel 的 hint 裡沒有 `j\|k` 這類鍵；有 tab 的 panel 有 `h\|l:tab` |
| panel-20 | panel.1 | hint 不寫 footer 已經有的 core key | 都要 | 比對 hint 與 footer，沒有重複的 core key |
| panel-21 | panel.1 | 有 focus 時 hint 的鍵 Blue、說明 Overlay0 | 都要 | 看有 focus 的 panel 的 hint |
| panel-22 | panel.1 | 失焦時 hint 照樣留著，跟著 panel 一起淡化 | 多 panel | 按 `Tab` 換走，看原本 panel 的 hint 還在、變暗 |
| panel-23 | panel.1 | hint 放不下時從尾端整組捨，捲動位置留著 | 都要 | 把終端機縮窄，看 hint 從尾端少掉整組、`N of M` 還在 |
| panel-24 | panel.1（圖） | panel 的內容左邊離框一格（PTY 例外：貼著框） | 都要 | 看各 panel 第一個字與左框之間 |
| panel-25 | panel.1（圖） | panel 的內容上下不留空白列，第一列緊接上框 | 都要 | 看各 panel 上框下面那一列就是內容 |
| panel-26 | panel.4 | 膠囊串的兩端是斜角：左 U+E0BA、右 U+E0B0 | 都要 | 看 panel 標題膠囊的兩端；讀程式核對 code point |
| panel-27 | panel.4 | 選中的段填滿這串的顏色，字 Base 粗體 | 都要 | 看 panel 的 `[N] label` 膠囊與目前的 tab |
| panel-28 | panel.4 | panel 上這串的顏色是框線色，跟著 focus、失焦、模式換 | 都要 | 按 `Tab` 換 panel、進入模式，看膠囊的顏色跟著框線變 |
| panel-29 | panel.4 | popup 標題後的 tab，這串的顏色是層色 | popup tab | 打開有 tab 的 popup，看選中的 tab |
| panel-30 | panel.4 | `[N] label` 膠囊算選中的 | 都要 | 看 `[N] label` 膠囊是填色的 |
| panel-31 | panel.4 | 沒選中的段底是 Mantle，字用這串的顏色、不加粗 | 多畫面、panel tab、popup tab | 看沒選中的 tab；把終端機底色換成不是 Base 的顏色，沒選中的段照樣是 Mantle |
| panel-32 | panel.4 | 接縫一律是斜線：顏色換的地方用實心的斜角，兩段都沒選中時用細斜線 | 多畫面、panel tab | 換 tab，看接縫的形狀；讀程式核對 code point |
| panel-33 | panel.4 | 選中 → 沒選中的接縫是 U+E0BC，前景這串的顏色、背景 Mantle | 多畫面、panel tab | 看選中的段右邊的接縫 |
| panel-34 | panel.4 | 沒選中 → 選中的接縫是 U+E0BA，前景這串的顏色、背景 Mantle | 多畫面、panel tab | 看選中的段左邊的接縫 |
| panel-35 | panel.4 | 兩段都沒選中的接縫是 U+E0BB，前景這串的顏色、背景 Mantle | 多畫面、panel tab | 看兩個相鄰的沒選中的段之間 |
| panel-36 | panel.4 | 兩端的前景是旁邊那一段的底：旁邊是選中的段時是這串的顏色，是沒選中的段時是 Mantle；外側不塗背景 | 都要 | 看膠囊串頭尾，再換 tab 讓尾端變成沒選中的段；把終端機底色換成不是 Base 也不是 Mantle 的顏色，兩端外側沒有色塊 |
| panel-37 | panel.4 | 斜角與接縫各佔一個 powerline 符號的寬度，換選中的段時字不位移 | 多畫面、panel tab | 換 tab，看各段的字位置不動 |
| panel-137 | panel.4 | 失焦時沒選中的段照樣是 Mantle（串的顏色換成失焦的框線色）；被蓋住時跟整個畫面一起淡化，Mantle 變成 Crust `#11111b` | 多畫面、panel tab、popup tab | 按 `Tab` 換 panel，看失焦的 panel 上沒選中的段底色不變；開一個 popup，量底下沒選中的段的底色 |
| panel-138 | panel.9 | 在一列上按比較鍵進入 K11 的模式，那一列成為 anchor；框與模式名 Yellow | 比較模式 | 按比較鍵，看框與模式名 |
| panel-139 | panel.9 | 只比文字或用文字呈現的內容；`text` 以外的項目沒有比較的動作 | 比較模式 | 在不是文字的項目上開 Space menu，看沒有比較 |
| panel-140 | panel.9 | 模式裡 cursor 停在 anchor 或不能比的項目上時，比較鍵與 `Enter` 停用 | 比較模式 | 停在 anchor 上按 `?`，比較鍵是停用色；按了不作用 |
| panel-141 | panel.9 | anchor 那一列整列 Yellow 底、Base 字、不加粗、沒有右邊的箭頭；cursor 停在上面時畫 cursor | 比較模式 | 進入後移開 cursor 看 anchor，再移回去 |
| panel-142 | panel.9 | 比較鍵或 `Enter` 打開跟 anchor 的比較；關掉後回到模式，anchor 留著 | 比較模式 | 比一次、關掉，看還在模式裡、anchor 還在 |
| panel-143 | panel.9 | 兩邊一模一樣時不打開，跳 Info toast，留在模式裡 | 比較模式 | 比兩個一樣的項目 |
| panel-144 | panel.9 | `Esc` 離開模式、拿掉 anchor；`Tab` 與數字鍵暫停 | 比較模式 | 模式裡按 `Tab`、`Esc` |
| panel-145 | panel.9 | anchor 不在了時離開模式，跳 Warning toast | 比較模式 | 在模式裡讓 anchor 那一項被刪掉 |
| panel-146 | panel.3 | 進入模式時模式名從中間打開：兩個接頭並排出現、往兩邊撐開，名字從中間露出來；離開時倒著播；第一幀是兩個接頭，之後每 32ms 一幀多露出一個字 | 模式 | 進入再離開模式，看上框右邊 |
| panel-147 | panel.3 | 模式名開或關到一半時又切換，從當下的位置轉向，不從頭播 | 模式 | 快速進出模式幾次（例：`D` `Esc` `D`） |
| panel-148 | panel.3 | 模式立刻生效、外框立刻變色；模式名播動畫時照樣收鍵 | 模式 | 進入模式後馬上按模式的鍵；看外框顏色 |
| panel-149 | panel.3 | 模式有好幾層時，模式名把層接在後面，用 `>` 隔開、不加空白（例：`Visual>select`） | 模式 | viewer 的選取模式裡按第二次 `v`，看上框右邊 |
| panel-150 | panel.3 | 多一層時右端不動，層的字從尾巴每 32ms 一幀長出一個字；退一層從尾巴收掉；一半又切換照樣轉向；從某一層直接離開整個模式時，整個標籤從中間關掉 | 模式 | 選取模式裡按 `v`、`Esc`，再按 `v`、`y`，看上框右邊 |
| panel-151 | panel.2 | 有 focus 的清單 cursor 那一列代表畫面上另一個 panel 時，那個 panel 的框是 Lavender 細線直角，不變成 focus，膠囊串跟著換色 | 被指到的 panel | 在清單上移動，看對應的 panel 的框 |
| panel-152 | panel.2 | cursor 換列就換成指那一列的 panel；那一列的 panel 不在畫面上時，沒有 panel 被指到 | 被指到的 panel | 移到 panel 不在畫面上的那一列 |
| panel-153 | panel.2 | 只在那個清單有 focus 時才指：focus 到被指的 panel 上照 focus 畫，focus 到別的 panel 上沒有 panel 被指到；被 popup 蓋住時一起淡化 | 被指到的 panel | 用 `Tab` 換 panel；開一個 popup |
| panel-38 | panel.4 | 膠囊裡的字前後不加空白（`[1] TABS`） | 都要 | 看膠囊的字與兩端之間 |
| panel-39 | panel.4 | 有 tab 的 panel，`[N]` 自己是一段，一直是選中的 | panel tab | 換到第二個 tab，看 `[N]` 還是填色 |
| panel-40 | panel.4 | `[N]` 後面每個 tab 一段，只有目前的 tab 選中 | panel tab | 換 tab，看只有目前的 tab 填色 |
| panel-41 | panel.4 | 有 tab 的 panel 沒有另外的名字，第一個 tab 的名字就是 label | panel tab | 看有 tab 的 panel 上框沒有另外的 label |
| panel-42 | panel.4 | 在第一個 tab 時，`[N]` 與第一個 tab 中間是空白、不畫接縫；那段空白跟接縫一樣佔一個 powerline 符號的寬度（powerline 符號佔兩格時是兩格） | panel tab | 換回第一個 tab，看 `[N]` 與 tab 名字之間；用 `TERMINU__POWERLINE_WIDTH=2` 開，換 tab 時字不位移 |
| panel-43 | panel.4 | 放不下時先把沒選中的縮成第一個字或 glyph | 多畫面、panel tab | 把終端機縮窄，看沒選中的段 |
| panel-44 | panel.4 | 還放不下就從尾端收掉沒選中的，改畫一個 `…` | 多畫面、panel tab | 再縮窄，看串的尾端 |
| panel-45 | panel.4 | 放不下時選中的永遠留著 | 多畫面、panel tab | 縮到最窄，看選中的段還在 |
| panel-46 | panel.4 | 膠囊串絕不把框撐寬 | 都要 | 縮窄終端機，看框沒有超出終端機寬度 |
| panel-47 | panel.5 | cursor 是 Subtext1 底、Base 粗體 | 都要 | 看清單 panel 上 cursor 那一列 |
| panel-48 | panel.5 | cursor 佔滿整個內寬，從框貼到框 | 都要 | 看 cursor 色塊的左右兩端 |
| panel-49 | panel.5 | cursor 那一列整列都是 Base 字，各欄原本的顏色不保留 | 都要 | 把 cursor 移到有上色欄位的那一列 |
| panel-50 | panel.5 | cursor 右邊的留白畫 U+E0B0，Subtext1 | 都要 | 看 cursor 那一列最右邊 |
| panel-51 | panel.5 | 每一列右邊的留白跟箭頭一樣寬（powerline 符號佔兩格時留兩格），箭頭放得進去、字不位移 | 都要 | 用 `TERMINU__POWERLINE_WIDTH=2` 開，看每一列右邊的留白與箭頭 |
| panel-52 | panel.5 | 多欄的一般清單一定有表頭（清單空了時連表頭一起換成空狀態，panel-132） | 都要 | 看每一個多欄的清單 panel，最上面有一列表頭 |
| panel-53 | panel.5 | 一般清單的表頭 Blue | 表頭 | 看清單的表頭 |
| panel-54 | panel.5、panel.12 | 表頭固定在最上面不捲 | 表頭、一列一個值的 panel | 往下捲，看表頭留在最上面 |
| panel-55 | panel.5（圖） | 表頭的字跟項目的字對齊（有標記欄時在標記欄之後） | 表頭 | 看表頭第一欄與各列第一欄的起點 |
| panel-56 | panel.5（圖） | 表頭下面直接接資料，不空列、不畫分隔線 | 表頭 | 看表頭的下一列 |
| panel-57 | panel.5 | 數字的欄靠右、文字的欄靠左 | 表頭 | 看數字欄與文字欄的對齊 |
| panel-58 | panel.5 | 數字的欄照數值排（`9` 在 `10` 前面），文字的欄照文字排 | 排序 | 對數字欄排序，看 `9` 在 `10` 前面 |
| panel-59 | panel.6 | 排序中的欄位，標題後面加 U+F160（升冪）或 U+F161（降冪） | 排序 | 升冪、降冪各排一次，看欄名後面的 glyph |
| panel-60 | panel.6 | 好幾欄一起排序時，在箭頭前加順位（`Name (2)`） | 排序 | 用兩欄排序，看第二欄的欄名 |
| panel-61 | panel.5 | 放不下時下框右邊寫 `N of M`（cursor 在第幾筆、總共幾筆） | 都要 | 讓清單超過 panel 高度，移動 cursor 看右下 |
| panel-62 | panel.5 | 捲動位置用框線的顏色 | 都要 | 看 `N of M` 的顏色跟框線一樣 |
| panel-63 | panel.5 | 全放得下就不寫捲動位置 | 都要 | 讓清單短到放得下，看右下沒有 `N of M` |
| panel-64 | panel.5 | 沒有 cursor 的 panel（預覽、log）寫看得到的行 `N-M of T` | 沒有 cursor 的 panel | 看預覽或 log panel 的右下 |
| panel-65 | panel.7 | 每一列最前面保留一格標記欄 | 標記 | 看沒有標記時各列前面也空著一格 |
| panel-66 | panel.7 | 被標記的列畫 Green 的 U+F0132 | 標記 | 標記一列，看標記欄 |
| panel-67 | panel.7 | 沒標記的留空白，欄寬一直保留，標記、取消時列不左右位移 | 標記 | 標記再取消，看那一列的字位置不動 |
| panel-68 | panel.8 | Drag 拿著的那一列照 cursor 的畫法，Yellow 底、Base 粗體 | Drag | 進 Drag 拿起一列 |
| panel-69 | panel.8 | 拿著的那一列右邊的箭頭也是 Yellow | Drag | 拿起一列，看最右邊 |
| panel-70 | panel.8 | 拿著的那一列標記欄畫 U+F04E2 | Drag | 拿起一列，看標記欄 |
| panel-71 | panel.8 | 放下後回到那一列原本的標記 | Drag | 先標記一列再拿起、放下，看標記回來 |
| panel-72 | panel.8 | 有 Drag 的 panel，每一列都保留標記欄 | Drag | 看有 Drag 的 panel 各列前面空著一格 |
| panel-73 | panel.8 | 拿著時 `Enter` 放下 | Drag | 拿起、搬動後按 `Enter` |
| panel-74 | panel.5 | 太長時截斷、加 `…`：預設從尾端截；路徑、檔名這類尾端比較重要的從前面截；兩端都有意義的（例：pod 的名稱）從中間截（`demo-app…66-gm72n`）；每一欄從哪裡截，app 可以自行決定 | 都要 | 看長名字的欄位 |
| panel-75 | panel.15 | panel 還沒有任何內容時，中間照空狀態的樣子寫一句 loading 的話 | loading | 讓 panel 第一次載入，看中間 |
| panel-76 | panel.15 | 重新載入時舊的內容留著，不清空 | loading | 重新載入，看舊內容還在 |
| panel-77 | panel.15 | panel 讀不到內容時（錯誤、斷線、沒有權限），照空狀態的樣子置中寫兩句，一句事實用 Red | 都要 | 讓沒有內容的 panel 讀取失敗，看中間的第一句 |
| panel-78 | panel.15 | 讀不到內容的另一句是提示，用 Overlay0 | 都要 | 同上，看第二句 |
| panel-79 | panel.15 | 載入失敗時舊的內容還在就留著 | loading | 有內容時讓它重新載入失敗，看內容還在 |
| panel-80 | panel.15 | 舊的內容還在時，錯誤用 toast 報 | loading | 同上，看跳出 toast |
| panel-81 | panel.11 | 分組的清單每組前面一列分組標題 | 分組清單 | 看分組清單 |
| panel-82 | panel.11 | 分組標題 Blue | 分組清單 | 看分組標題的顏色 |
| panel-83 | panel.11 | 分組標題沒有 glyph | 分組清單 | 看分組標題前面 |
| panel-84 | panel.11 | 分組標題離框一格 | 分組清單 | 看分組標題與左框之間 |
| panel-85 | panel.11 | 項目比分組標題多縮兩格 | 分組清單 | 比較項目與分組標題的起點 |
| panel-86 | panel.11 | 分組清單有標記欄時，記號（勾或旗標）畫在項目多縮的那兩格裡：記號離框一格、空一格，字離框三格 | 分組清單＋標記或旗標 | 在分組清單標記一個項目，數標記與字離左框幾格 |
| panel-87 | panel.11 | 分組清單有標記欄時，分組標題那一列不留標記欄 | 分組清單＋標記或旗標 | 看有標記欄時分組標題的起點，跟沒有標記欄時一樣離框一格 |
| panel-88 | panel.11 | cursor 跳過分組標題，`j\|k` 越過它 | 分組清單 | 按 `j\|k` 經過分組標題 |
| panel-89 | panel.11 | `gg\|G` 到第一個、最後一個項目 | 分組清單 | 按 `gg` 與 `G`，看 cursor 停在項目上 |
| panel-90 | panel.11 | 捲動位置的 `N of M` 只算項目 | 分組清單 | 看 `N of M` 的總數等於項目數 |
| panel-91 | panel.11 | 捲動時 cursor 停在一組的第一個項目，這組的標題也留在畫面裡 | 分組清單 | 把終端機拉矮再捲到某組的第一個項目 |
| panel-92 | panel.11 | 組與組之間不空列、不畫分隔線 | 分組清單 | 看兩組之間 |
| panel-93 | panel.11 | 沒有項目的組不畫標題 | 分組清單 | 用 panel filter 篩到某組一項都不剩，看它的標題消失 |
| panel-94 | panel.12 | `Enter` 打開那個值的 input popup | 一列一個值的 panel | 在一個值上按 `Enter` |
| panel-95 | panel.12 | 值在 input popup 確定的那一刻就生效、就存 | 一列一個值的 panel | 改一個值確定後立刻離開 app 再開，看值還在 |
| panel-96 | panel.12 | 開關與 radio 在原地選的那一刻就生效、就存 | 一列一個值的 panel | 切一個開關後立刻離開 app 再開，看值還在 |
| panel-97 | panel.12 | 沒有動作區 | 一列一個值的 panel | 看 panel 裡沒有送出、取消這類按鈕 |
| panel-98 | panel.12 | 沒有「改過了要先問」 | 一列一個值的 panel | 改一個值後離開 panel，看沒有問要不要存 |
| panel-99 | panel.12 | focus 色塊 Subtext1 底、Base 粗體 | 一列一個值的 panel | 看 focus 那一列 |
| panel-100 | panel.12 | focus 色塊右邊的留白是箭頭 | 一列一個值的 panel | 看 focus 那一列最右邊 |
| panel-101 | panel.12 | focus 色塊從值（選項則從那個選項）開始，到 panel 內的右緣 | 一列一個值的 panel | 看 focus 色塊的左右兩端 |
| panel-102 | panel.12 | label 一般 Blue | 一列一個值的 panel | 看 label 欄 |
| panel-103 | panel.12 | 值出錯時 label Red，優先於其他顏色 | 一列一個值的 panel | 讓一個值出錯，看它的 label |
| panel-104 | panel.12 | label 欄寬取 label 與表頭第一欄名裡最長的那一個 | 一列一個值的 panel | 看值欄的起點是最長的 label（表頭第一欄名比較長時是它）加兩格 |
| panel-105 | panel.12 | 一列一個值的 panel 有表頭時，表頭用 Overlay0 | 一列一個值的 panel | 看表頭的顏色 |
| panel-106 | panel.12（圖） | 一列一個值的 panel 有表頭時，表頭的欄名跟下面的 label 欄、值欄對齊 | 一列一個值的 panel | 看表頭兩個欄名的起點 |
| panel-107 | panel.13 | 另一個 panel 的 cursor 一移動，明細立刻換成新的那一筆，不用按 `Enter` | 明細 panel | 在清單上按 `j\|k`，看明細 |
| panel-108 | panel.13 | 明細的 label 寫那一筆的名字時，label 一起換 | 明細 panel | 同上，看明細的膠囊 |
| panel-109 | panel.13 | cursor 移動時 focus 留在原本的 panel | 明細 panel | 同上，看 focus 的框 |
| panel-110 | panel.14 | 按 `/` 在 panel 最上面出現一列打字列 | panel filter | 在清單上按 `/` |
| panel-111 | panel.14 | 清單有表頭時，打字列在表頭上面；有位置列時在位置列下面 | 表頭＋panel filter | 在有表頭的清單按 `/`，打字列出現在表頭上面 |
| panel-112 | panel.14 | panel filter 不開 popup | panel filter | 按 `/`，看沒有 popup |
| panel-113 | panel.14 | 打字列最前面是 U+F105，離框一格 | panel filter | 按 `/` 看打字列最前面 |
| panel-114 | panel.14 | U+F105 在 focus 在打字列時用 panel 框線的顏色、在清單時 Overlay0 | panel filter | 在打字列與清單之間切換，看 glyph 的顏色 |
| panel-115 | panel.14 | focus 在清單時打字列用 Overlay0 畫 | panel filter | 按 `Enter` 到清單，看打字列 |
| panel-116 | panel.14（圖） | 打字列右邊寫篩選的筆數 `符合/總數`（`2/5`），靠右、離框一格 | panel filter | 打字，看打字列右邊 |
| panel-117 | panel.14 | 筆數用 Overlay0 | panel filter | 看筆數的顏色 |
| panel-118 | panel.14（圖） | 打字列下面直接接表頭（沒有表頭時接清單），不空列、不畫分隔線 | panel filter | 看打字列的下一列 |
| panel-119 | panel.14 | 清單上的 `Tab` 到下一個 panel | panel filter | 篩選後到清單按 `Tab` |
| panel-120 | panel.14 | 清單上按 `Enter` 之後 panel filter 不關：清單留著篩選過的樣子，照常操作 | panel filter | 篩選後到清單按 `Enter`，打字列與篩選都還在，清單照常操作 |
| panel-121 | panel.14 | 清單上的 `/` 回到打字列，接著舊的字打 | panel filter | 篩選後在清單按 `/` |
| panel-122 | panel.14 | focus 離開 panel 時篩選留著，往哪個方向離開都一樣 | panel filter | 篩選後用 `Tab` 與數字鍵離開再回來 |
| panel-123 | panel.14 | focus 回到有篩選的 panel 時，直接在打字列上 | panel filter | 篩選後離開再回來，看 focus 在打字列 |
| panel-124 | panel.1 | 清單一項都沒有時（panel filter 篩到空，或本來就是空的），hint 拿掉 `Enter` 與對項目的熱鍵，只留對整個 panel 的 | 都要 | 讓清單篩到空或清空，看下框 hint 沒有 `Enter` 與項目的熱鍵 |
| panel-125 | panel.4 | 選中的那一段自己就太長時，字從尾端截、加 `…`；兩端的斜角照畫，跟框角之間照樣留一段線 | 都要 | 把終端機縮到很窄，看 label 很長的 panel 的膠囊 |
| panel-126 | panel.6 | 排序的群：app 替列指定的群照 app 定的先後排，排序只在同一群裡排，群和群之間不畫標題（例：目錄一律在檔案前面） | 排序 | 對有群的清單換排序，看群的先後不變 |
| panel-127 | panel.5 | 欄放不下時先把可以截短的欄縮到最少寬度，還放不下才整欄收：照 app 標的順序從最不重要的那一欄拿掉（表頭跟著拿掉），名稱欄不收 | 表頭 | 把終端機縮窄，看長欄先截短、再整欄消失，名稱欄一直在 |
| panel-128 | panel.5 | 終端機變大時，收掉的欄照順序回來 | 表頭 | 縮窄後再拉寬，看收掉的欄回來 |
| panel-129 | panel.10 | 位置列是 panel 內的第一列，離框一格；有表頭時在表頭上面，panel filter 的打字列出現時在打字列上面；固定在最上面不捲 | 位置列 | 看位置列的位置；往下捲、按 `/` |
| panel-130 | panel.10 | 位置列太長時從前面截、加 `…`，留住後面（目前所在的那一層） | 位置列 | 走進很深的位置，看位置列的開頭 |
| panel-131 | panel.10 | 位置列只顯示：不能按，cursor 不會停在上面，捲動位置也不算它；panel 失焦時跟著淡化 | 位置列 | 用 `j\|k` 走到最上面，看 cursor 不停在位置列；看 `N of M`；按 `Tab` 換走 |
| panel-132 | panel.5 | 清單空了時空狀態取代整塊，表頭一起不畫，句子置中在整個 panel | 都要 | 讓有表頭的清單空掉，看表頭也不見、句子在 panel 正中間 |
| panel-133 | panel.5 | 清單的順序固定：同一份資料每次打開、重抓都排得一樣；資料本身沒有順序時 app 先排好（預設照名稱、數字照數值） | 都要 | 關掉再打開、重抓幾次，看順序不變；讀程式：沒有順序的資料（例：map）先排序 |
| panel-134 | panel.10 | 清單空了時位置列照樣留著，只有表頭與清單被空狀態取代 | 位置列 | 讓有位置列的清單空掉（例：進一個空目錄），看位置列還在 |
| panel-135 | panel.5 | 可以截短的欄（名稱、網址、一行文字）分剩下的寬度、照自己的截法截；其他短欄照自己最寬的值，不縮 | 表頭 | 讓清單裡有一個很長的名稱，看其他欄照樣完整、名稱被截短 |
| panel-136 | panel.5 | 格子裡的值（檔名、名字這種從檔案或別的程式來的）有控制字元時，照打字列寫成紅色的轉義（`\n`、`\t`、`\x1b`），不丟、不換成空白、不原樣送給終端機 | 都要 | 讓清單裡有一個名字含換行或 `\x1b` 的項目（例：檔名），看那一格；或讀程式 |
| panel-154 | panel.7 | 不能標記的清單，app 可以把一種旗標畫在標記欄，一列最多一個；這時每一列都保留標記欄，沒有旗標的留空白 | 旗標 | 看有旗標與沒有旗標的列字從同一格開始；換一列成為有旗標的，看字不位移 |
| panel-155 | panel.7 | 可以標記的清單，標記欄只放勾，領域旗標寫在內容裡 | 標記 | 看標記欄裡只有勾或空白 |

## layout/popup

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| popup-1 | popup.1 | popup 一律是粗線 `┏━┓`，被蓋在底下、淡化了的也是粗線 | 都要 | 疊兩層 popup，看底下那層的框 |
| popup-2 | popup.1 | 標題是 glyph + 文字，做成一個膠囊，放在上框 `┏━` 後面 | 都要 | 看任何一個 popup 的上框 |
| popup-3 | popup.1 | 標題膠囊兩端是圓角：左 U+E0B6、右 U+E0B4 | 都要 | 看標題膠囊的兩端；讀程式核對 code point |
| popup-4 | popup.1 | 標題膠囊填層色（error popup 填 Red），字 Base 粗體 | 都要 | 看標題膠囊的底與字 |
| popup-5 | popup.1 | 標題文字寫這個 popup 是做什麼的（`RENAME`、`NEW HOST`） | 都要 | 打開各種 popup 看標題 |
| popup-6 | popup.1 | 要寫對哪一個做時，名稱接在標題後面，用 `: ` 隔開（`EDIT: filu`） | 都要 | 對某一個東西打開 popup，看標題 |
| popup-7 | popup.1 | 標題太長從尾端截，加 `…` | 都要 | 對名稱很長的東西打開 popup，或把終端機縮窄 |
| popup-8 | popup.1 | 標題後面接 tab 時，tab 照膠囊串畫 | popup tab | 打開有 tab 的 popup，看標題後面 |
| popup-9 | popup.1 | tab 跟圓角的標題之間隔一段線（`┏━TITLE━CONSOLE…`） | popup tab | 看標題膠囊與第一個 tab 之間 |
| popup-10 | popup.1 | hint 的順序：`Enter` 第一 → 切 tab 的 `h\|l:tab` → 這個 popup 自己的鍵 → 換塊的 `Tab:…` → `Esc` 最後 | 都要 | 打開各種 popup，看 hint 的順序 |
| popup-11 | popup.1 | hint 不寫在項目之間移動的鍵（`j\|k`、`↑\|↓`）；有兩個以上的 tab、`h\|l` 切 tab 時寫 `h\|l:tab` | 都要 | 看各種 popup 的 hint；打開比較的 viewer 看有 `h\|l:tab` |
| popup-12 | popup.1 | 框到了最寬還放不下時，hint 從 `Esc` 前面的那一組開始往前整組捨棄，不截在項目中間；最後的 `Esc` 一定留著 | 都要 | 把終端機縮到很窄，打開寬度到頂的 popup，看下框留著 `Esc` |
| popup-13 | popup.1 | hint 捨棄時，下框右邊的捲動位置留著 | 都要 | 同上，讓內容也放不下，看右下 |
| popup-14 | popup.1 | 框上的字與角之間隔一段線：`┏━TITLE`、`┗━ Enter:run`、`4 of 12 ━┛` | 都要 | 看 popup 的四個角 |
| popup-15 | popup.1 | 內容上下各留一列空白（viewer 也一樣） | 都要 | 看各種 popup 上框下面、下框上面那一列 |
| popup-16 | popup.1 | 內容左右離框一格 | 都要 | 看內容與左右框之間 |
| popup-17 | popup.1 | 清單的 cursor 從框貼到框，蓋住左右的留白 | 都要 | 按 `Space` 看 cursor 色塊的兩端 |
| popup-18 | popup.1 | cursor 色塊上的字照樣離框一格 | 都要 | 同上，看色塊上的字與左框之間 |
| popup-19 | popup.1 | 整列 cursor 右邊的留白畫 U+E0B0，色塊的顏色 | 都要 | 按 `Space` 看 cursor 那一列最右邊 |
| popup-20 | popup.1 | 有整列 cursor 的 popup（含表單的 focus 色塊），每一列右邊的留白跟箭頭一樣寬（powerline 符號佔兩格時留兩格） | 都要 | 用 `TERMINU__POWERLINE_WIDTH=2` 開，看 menu 與表單每一列右邊 |
| popup-21 | popup.1 | 只有整列的 cursor 有箭頭；一格一格的 cursor（datetime picker 的日子、時、分）沒有 | 都要 | 看整列的 cursor 有箭頭；有 datetime picker 時，看日子、時、分的 cursor 旁邊沒有箭頭 |
| popup-22 | popup.1 | 橫的分隔線不接框，左右各留一格空白 | 都要 | 按 `Space` 看區塊之間的分隔線兩端 |
| popup-23 | popup.1 | 直的分隔線不畫進上下的留白 | 都要 | 看直分隔線的上下端 |
| popup-24 | popup.1 | popup 裡的分隔線 Overlay0 | 都要 | 看分隔線的顏色 |
| popup-25 | popup.2 | 內容寬度打開時就確定的 popup，寬是最寬的那一列 + 4（右邊的留白跟箭頭一樣寬時照它的寬） | 都要 | 量 menu、confirm 的框寬 |
| popup-26 | popup.2 | 內容寬度確定的 popup，寬度至少放得下標題 | 都要 | 打開內容很窄、標題較長的 popup，看標題完整 |
| popup-27 | popup.2 | 內容寬度確定的 popup，寬度至少放得下 hint：hint 的寬 + 6（`┗━ ` 與 ` ━┛`） | 都要 | 打開內容很窄、hint 較長的 popup（例：PIN），量框寬 |
| popup-28 | popup.2 | 要捲的 popup 也放得下最寬時的捲動位置：hint 的寬 + 捲動位置最寬時的寬 + 9（`N of M` 照 `M of M`、`N-M of T` 照 `T-T of T`），捲的時候框不忽寬忽窄 | 都要 | 在矮的終端機打開長 menu，從頭捲到尾看框寬不變 |
| popup-29 | popup.2 | 窄的內容靠左，離框一格 | 都要 | 打開 confirm，看內容的位置 |
| popup-30 | popup.3 | 打開的第一段「拉線」4 格：popup 正中間那一列，一條層色的粗線 `━` 從中間往左右延伸，拉到 popup 的寬度 | 都要 | 錄下 popup 打開的過程逐格看 |
| popup-31 | popup.3 | 第二段「停」1 格：拉滿的線停一格 | 都要 | 同上 |
| popup-32 | popup.3 | 第三段「展開」4 格：從中間那一列往上下展開，每一格露出 popup 正中間的那幾列，最後一格是整個 popup | 都要 | 同上 |
| popup-33 | popup.3 | 收起是同樣的 9 格倒著播：往中間壓成一條線，線再往中間縮掉 | 都要 | 錄下 popup 收起的過程逐格看 |
| popup-34 | popup.3 | 打開的第一格起，底下就淡化 | 都要 | 錄下打開的第一格，看底下已經變暗 |
| popup-35 | popup.3 | 開始收起時，底下立刻亮回來 | 都要 | 錄下收起的第一格，看底下已經變亮 |
| popup-36 | popup.3 | 收到一半的 source 壓在 target 底下，照 F8 淡化 | 都要 | 從會被清掉的 source 打開 target，錄下過程，看收到一半的 source 是暗的 |
| popup-37 | popup.3 | toast 與 terminal popup 也用同一種開關動畫 | terminal popup、toast | 錄下 toast、terminal popup 打開與收起 |
| popup-38 | popup.4 | 標題後面接著 tab 時，loading icon 放在整串 tab 的後面 | popup tab | 打開有 tab、會載入的 popup |
| popup-39 | popup.4 | popup 的 loading icon 前後各空一格 | loading | 看 icon 兩邊 |
| popup-40 | popup.4 | loading icon 用 U+F0A9E–U+F0AA5（`nf-md-circle_slice_1` 到 `_8`）八格，一個圓一片一片填滿，滿了再從頭 | loading | 錄下 icon 轉一圈；讀程式核對 code point |
| popup-41 | popup.4 | loading icon 一格 90ms | loading | 讀程式：每格的時間 |
| popup-42 | popup.4 | 哪一格由時鐘決定（`frames[(now / 90ms) % 8]`），不是計數 | loading | 讀程式：取格子的算法 |
| popup-43 | popup.4 | loading 的 tick 只在有東西 loading 時續排 | loading | 讀程式：沒有東西 loading 時不排 tick |
| popup-44 | popup.4 | loading icon 一格寬，跟它取代的靜止 glyph 同寬，換上換下不位移 | loading | 看 loading 開始與結束時旁邊的字不動 |
| popup-45 | popup.4 | 不用 braille 點字當 loading icon | loading | 看 loading icon 的形狀 |
| popup-46 | popup.4 | loading icon 跟旁邊的字同色 | loading | 看 panel 中間「loading」那一句的 icon 顏色 |
| popup-47 | popup.4 | 放在 popup 標題後面的 loading icon 用該層的層色、粗體 | loading | 看標題後面 icon 的顏色 |
| popup-48 | popup.4 | 放在 panel 上框的 loading icon 用框線色（focus 時 Blue、失焦時 Surface2）、不加粗，跟著框一起淡化 | loading | 讓 panel 載入時按 `Tab` 換走，看 icon 的顏色 |
| popup-49 | popup.6 | 只有內容區捲動；上下留白、錯誤列、上下框固定不動 | 都要 | 在放不下的 popup 裡捲動，看留白與錯誤列不動 |
| popup-50 | popup.6 | 跟著 focus 捲，捲最少的量，讓 focus 所在的那一個整個看得到；不把 focus 固定在中間 | 都要 | 在放不下的 menu 裡一路往下移，看 cursor 到底才開始捲 |
| popup-51 | popup.6 | 放不下時下框右邊寫捲動位置 | 都要 | 看放不下的 popup 的右下 |
| popup-52 | popup.6 | popup 的捲動位置用層色 | 都要 | 看右下捲動位置的顏色 |
| popup-53 | popup.6 | 有 cursor 或游標的寫 `N of M`（focus 所在的那一個是第幾個、總數） | 都要 | 在放不下的 menu 移動 cursor，看右下 |
| popup-54 | popup.6 | 沒有 cursor 或游標的（note、選取模式外的 viewer）寫看得到的行 `N-M of T` | 都要 | 打開放不下的 key reference，看右下 |
| popup-55 | popup.6 | 全放得下時不寫捲動位置 | 都要 | 打開放得下的 popup，看右下 |
| popup-56 | popup.6 | 表單與一列一個值的 panel 以欄位為單位：上下式的 label 與值兩列、radio 的幾個選項都算同一欄；M 只算欄位，錯誤列與按鈕不算 | 表單、一列一個值的 panel | 在放不下的表單或一列一個值的 panel 裡移動，看 `N of M` |
| popup-57 | popup.6 | 一段文字裡的游標（textarea、選取模式裡的 viewer）以行為單位：游標所在的行、總行數，跟行號同一套數字 | viewer、textarea | 在長的 textarea 裡移動游標，看 `N of M` 跟行號一樣 |
| popup-58 | popup.6（圖） | 錯誤列下面是一列下留白，再接下框 | input | 打開 input popup，看錯誤列與下框之間 |
| popup-59 | popup.7 | 錯誤列在內容區下面，固定不捲 | input | 打開 input popup 讓它出錯，看錯誤列的位置 |
| popup-60 | popup.7 | 錯誤列跟內容之間空一列 | input | 同上，看錯誤列與內容之間 |
| popup-61 | popup.7 | 只有值可能不合格的 popup 才預留錯誤列 | 都要 | 打開 confirm、menu，看沒有預留的空列 |
| popup-62 | popup.7 | 錯誤列只放值的錯（格式、範圍、必填、名字重複），訊息很短；值錯太多次而暫停收值時的倒數也寫在這裡 | input | 讓值不合格，看錯誤列的訊息 |
| popup-63 | popup.7 | 錯誤列是 Red 字 | input | 看錯誤列的顏色 |
| popup-64 | popup.7 | 錯誤列左緣跟內容對齊；內容置中時錯誤列也置中 | input | 看錯誤列的起點 |
| popup-65 | popup.7 | 有錯誤時框與標題不變色，維持層色 | input | 讓值不合格，看框與標題的顏色 |
| popup-66 | popup.7 | 錯誤列只佔一列，太長從尾端截斷加 `…` | input | 讓一個很長的錯誤出現，看它只有一列 |
| popup-67 | popup.7 | input popup 裡的錯誤列不拿 focus | input | 讓 input popup 出錯，按鍵看 focus 不會到錯誤列 |
| popup-68 | popup.7 | input popup 在 `Enter` 時檢查 | input | 打不合格的值，按 `Enter` 時才出現錯誤 |
| popup-69 | popup.7 | 動作本身失敗（寫檔失敗、遠端拒絕、檔案在底下被改了）不寫錯誤列，開一個 error popup 蓋在當前的 popup 上 | 都要 | 讓送出的動作失敗，看跳出 error popup |
| popup-70 | popup.7 | 值錯太多次而暫停收值時，倒數寫在錯誤列（Red，每秒更新，倒數完清掉）；暫停期間除了 `Esc` 的鍵都吞掉，不進打字列 | input | 連錯到暫停，看錯誤列每秒倒數；暫停時打字，打字列不變；倒數完錯誤列清掉（不會暫停收值的 app 沒有這種情況） |
| popup-71 | popup.8 | app 自己的 popup 的外框、標題、hint、寬度、開關動畫、loading、層色與淡化照 popup | app 自己的 popup | 打開它，看框、標題、hint 與開關動畫；在它上面再開一層 popup |
| popup-72 | popup.8 | app 自己的 popup 內容上的熱鍵揭露在這個 popup 的 `?` | app 自己的 popup | 在那種 popup 上按 `?` |
| popup-73 | popup.8 | app 自己的 popup 裡 focus 在哪裡看得出來；移動照 K12（hjkl 是方向鍵） | app 自己的 popup | 在內容上按 hjkl，看 focus 的位置 |

## dialog/form

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| form-1 | form.1 | 表單只用在好幾個值一起送出：只有一個值時用 input popup，不開表單 | 表單 | 看每一張表單，欄位都不只一個 |
| form-2 | form.1 | 改了就生效、不用送出的值放在 panel 的一列一個值，不做成表單 | 表單 | 看每一張表單，裡面的值都要送出才生效 |
| form-3 | form.1 | 表單上不直接打字：要打字的欄位（text、password…）按 `Enter` 打開那一欄的 input popup，在那裡輸入 | 表單 | focus 在打字的欄位上按 `Enter`，開出 input popup；在表單上直接打字不會改到值 |
| form-4 | form.1 | 選項多到放不下的欄位（select、日期、顏色、選檔）按 `Enter` 打開那一欄的 input popup | 表單 | focus 在 select 之類的欄位上按 `Enter`，開出它的 popup |
| form-5 | form.3 | 標題不寫型別（`number`、`path`、`email`） | 表單 | 看標題文字 |
| form-6 | form.4 | 每個欄位都排成上下式或左右式其中一種 | 表單 | 看表單每一欄的排法 |
| form-7 | form.4 | 上下式：label 一列，值在下一列，值佔滿內寬 | 表單 | 看上下式欄位的兩列 |
| form-8 | form.4 | 左右式：一列裡 label 在左一欄、值在右 | 表單 | 看左右式欄位 |
| form-9 | form.4 | 欄位之間不空行 | 表單 | 看欄位區相鄰兩欄之間沒有空列 |
| form-10 | form.4 | 上下式的 label 與值之間不空行 | 表單 | 看上下式欄位的 label 與值 |
| form-11 | form.4 | 上下式的欄位：label、值、錯誤的左緣對齊 | 表單 | 送出被擋後，看上下式的值、錯誤列與 label 的左緣在同一欄 |
| form-12 | form.4 | 左右式的 label 欄寬取左右式欄位裡最長的 label，上下式的 label 不算進去 | 表單 | 看左右式的值都從最長的左右式 label 後面同一欄開始 |
| form-13 | form.5 | 畫在表單或一列一個值的 panel 上的選項一律直排，一個選項一列 | radio、checkbox | 看選項沒有橫排 |
| form-14 | form.9（圖） | 表單與一列一個值的 panel 上左右式欄位的選項：第一個選項跟 label 同一列，其餘選項接在下面各一列、左緣對齊值，label 欄空白（checkbox 組的選項比 `Select all` 多縮兩格） | radio、checkbox | 看 radio 欄位第二個以後的選項，左緣對齊第一個選項 |
| form-15 | form.6 | 欄位的 focus 色塊從值開始一直到框，蓋住右邊的留白 | 表單 | focus 停在一欄，看色塊從值的左緣到右框 |
| form-16 | form.6 | 表單與一列一個值的 panel 上，選項的 focus 色塊從那個選項的 glyph 開始，一直到框 | radio、checkbox | focus 停在一個選項上看色塊 |
| form-17 | form.6 | 值空著的欄位 focus 時也是一整塊底色 | 表單 | focus 停在空的欄位上看色塊 |
| form-18 | form.6 | 按鈕的 focus 色塊就是按鈕本身，沒有箭頭 | 表單 | `Tab` 到按鈕，看色塊只有按鈕那一塊 |
| form-19 | form.6 | 表單與一列一個值的 panel 上，label 不因 focus 變色 | 表單、一列一個值的 panel | focus 進出一欄，看 label 顏色不變 |
| form-20 | form.6 | 一般的 label 是層色（跟標題膠囊、框線同色） | 表單 | 比較 label 與框線的顏色 |
| form-21 | form.6 | 值出錯的欄位 label 是 Red，優先於其他顏色 | 表單 | 送出被擋後看有問題的 label |
| form-22 | form.6 | 表單與一列一個值的 panel 上，停用的欄位留在原位，不拿掉、不改高度 | 表單、一列一個值的 panel | 讓一欄變成停用，看表單版面不變 |
| form-23 | form.6 | 表單與一列一個值的 panel 上，值在每一個狀態都不跟它的 label 同色 | 表單、一列一個值的 panel | 看一般、focus、停用、出錯時的 label 與值 |
| form-24 | form.7 | 按鈕的文字左右各留一格空白，一塊底色 | 表單 | 看動作區的按鈕 |
| form-25 | form.7 | 按鈕上寫按下去要做的事（`Save`、`Connect`） | 表單 | 看按鈕文字 |
| form-26 | form.7 | 按鈕不畫成方括號（`[ Save ]`） | 表單 | 看按鈕 |
| form-27 | form.7 | 按鈕不畫成膠囊 | 表單 | 看按鈕兩端 |
| form-28 | form.7 | 由上而下是：欄位區 → 空一列 → 錯誤列（沒錯時空白）→ 分隔線 → 動作區 | 表單 | 看表單下半部的列 |
| form-29 | form.7（圖） | 錯誤列、分隔線、每一列按鈕之間都不空行 | 表單 | 看錯誤列到最後一列按鈕之間沒有空列 |
| form-30 | form.7 | 每一列按鈕都靠右，最右邊的按鈕離框一格 | 表單 | 數最右邊按鈕的色塊與右框之間的格數 |
| form-31 | form.7（圖） | 動作區上方的分隔線是實線 `─`（U+2500） | 表單 | 看分隔線用的字元 |
| form-32 | form.7 | 錯誤列、分隔線、動作區固定不捲，欄位放不下時只捲欄位區 | 表單 | 把終端機縮矮到欄位放不下，捲動時看錯誤列與按鈕不動 |
| form-33 | form.7 | focus 在錯誤列或按鈕上時不寫捲動位置，回到欄位就寫回來 | 表單 | 欄位放不下時 `Tab` 到按鈕再回來，看下框右邊 |
| form-34 | form.7 | 一定有一個主要的送出按鈕，放在動作區的右下角（只有一個按鈕時就是它） | 表單 | 看最後一列最右邊的按鈕是主要的送出 |
| form-35 | form.7 | 同一列的按鈕之間隔一格 | 表單 | 數同一列兩顆按鈕色塊之間的格數 |
| form-36 | form.7 | 不關表單的動作按下時，只檢查這個動作需要的欄位 | 表單 | 讓它不需要的欄位空著，按那顆按鈕，不被擋 |
| form-37 | form.7 | 不關表單的動作檢查沒過時跟送出被擋一樣：有問題的 label 轉 Red、錯誤列寫第一個問題、focus 跳到那一欄 | 表單 | 讓它需要的欄位空著，按那顆按鈕 |
| form-38 | form.7 | 不關表單的動作成功時 toast 一句 | 表單 | 讓動作成功，看下方的 toast |
| form-39 | form.7 | 動作的結果是一段要看的內容時開 note | 表單 | 按那顆按鈕，看結果開在 note 裡 |
| form-40 | form.7 | 跑得久的不關表單動作與跑得久的送出（例：`Connect`），還在跑時標題後面放 loading icon | 表單 | 按下後看標題後面有輪轉的 loading icon，跑完消失 |
| form-41 | form.7 | 動作還在跑時，focus 停在那顆按鈕上按 `Enter` 不作用 | 表單 | 按下後馬上再按 `Enter`，不會發出第二次 |
| form-42 | form.7 | 動作還在跑時 hint 拿掉那顆按鈕的 `Enter`，跑完再放回來 | 表單 | 按下後看下框 hint，跑完再看一次 |
| form-43 | form.7 | 跑得久的送出（`Connect`）還在跑時一樣：`Enter` 不作用、hint 拿掉它的 `Enter` | 表單 | 按下送出後馬上再按 `Enter`，看 hint |
| form-44 | form.7 | 動作還沒跑完就關掉表單（`Esc`，或按了另一顆送出）：動作算取消，能停就停 | 表單 | 按下後馬上 `Esc`；讀程式：動作有被停掉 |
| form-45 | form.7 | 表單關掉後，那個動作的結果不顯示（沒有 toast、note、error popup） | 表單 | 按下後馬上 `Esc`，等一下看不到結果 |
| form-46 | form.7 | 不關表單的動作做完後，focus 留在那顆按鈕上 | 表單 | 動作成功後看 focus |
| form-47 | form.7 | 動作把值寫進某一欄時，那一欄算改過 | 表單 | 讓動作寫回一欄後按 `Esc`，先跳 confirm |
| form-48 | form.7 | 動作區不放取消的按鈕 | 表單 | 看動作區沒有 `Cancel` 之類的按鈕 |
| form-49 | form.9 | 表單與一列一個值的 panel 上，focus 的單位是項目：要打字或開 popup 的欄位一個、radio／checkbox 每個選項各一個、checkbox 組的 `Select all` 一個、每個按鈕一個 | 表單、一列一個值的 panel | 用 `j` 走一遍，數停的次數 |
| form-50 | form.9 | 錯誤列有錯誤時也是一個項目，在最後一欄後面；沒錯時不停 | 表單 | 送出被擋前後，各用 `j` 走過最後一欄 |
| form-51 | form.9 | 表單與一列一個值的 panel 上，走到一欄的最後一個選項再往後就到下一欄；在第一個選項再往前就回到上一欄 | radio、checkbox | 在 radio 的最後一個選項按 `j`、第一個選項按 `k` |
| form-52 | form.9 | 動作區照閱讀順序排成一串：一列裡由左到右，再到下一列 | 表單 | 在動作區按 `j` 走過每一顆按鈕 |
| form-53 | form.9 | `gg\|G` 到這一區的第一個、最後一個項目 | 表單 | 在欄位區、動作區各按 `gg`、`G` |
| form-54 | form.9 | `u\|d` 以項目為單位半頁，到頭尾停住 | 表單 | 在欄位很多的表單按 `d` 到底再按，不繞回 |
| form-55 | form.9 | 第一次到動作區時停在主要的送出（右下角） | 表單 | 打開表單後第一次按 `Tab` |
| form-56 | form.9 | 錯誤列屬於欄位區：`j\|k` 與 `e` 到得了，在它上面按 `Tab` 到動作區 | 表單 | 送出被擋後用 `j` 走到錯誤列，再按 `Tab` |
| form-57 | form.9 | 每一區各自頭尾繞回：欄位區最後一項（有錯誤時是錯誤列）往後回到第一欄，最後一個按鈕往後回到第一個按鈕 | 表單 | 在欄位區最後一項、最後一顆按鈕上按 `j` |
| form-58 | form.9 | 表單與一列一個值的 panel 上，停用的欄位與選項跳過，`j\|k` 不停在上面 | 表單、一列一個值的 panel | 用 `j` 經過停用的欄位 |
| form-59 | form.9 | 打開時 focus 在第一個能停的項目（跳過停用的；checkbox 組的 `Select all` 也跳過，停在第一個選項），新增與編輯都一樣 | 表單 | 分別打開新增、編輯的表單看 focus |
| form-60 | form.9 | app 從某一欄打開表單時，focus 停在那一欄 | 表單 | 從 panel 的某一列打開編輯表單，看 focus |
| form-61 | form.9 | 打開時不自動打開任何欄位的 input popup：打開的一定是表單本身，一次 `Esc` 就離開 | 表單 | 打開新增表單，按一次 `Esc` 就回到原處 |
| form-62 | form.9 | 跳進 radio、checkbox 那一欄時（從那一欄打開、送出被擋、錯誤列按 `e`）停在第一個有值的選項：radio 已選的、checkbox 第一個勾的選項，都沒有值停第一個選項（`Select all` 不算） | 表單 | 讓 radio 那一欄出錯後送出，看 focus 停在哪個選項 |
| form-63 | form.10 | 在按鈕上按 `Enter` 按下它：送出，或做那個按鈕的動作 | 表單 | `Tab` 到按鈕按 `Enter` |
| form-64 | form.11 | 送出只有一個方法：focus 在送出的按鈕上按 `Enter`（沒有字母熱鍵或其他送出方式） | 表單 | 在欄位上按 `s` 等字母，都不會送出 |
| form-65 | form.12 | focus 在要打字的欄位（text、password、number、textarea）上，按表單操作鍵以外的可列印字元（含數字、`q`）跳說明的 note | 表單 | 在 text 欄位上打 `s`、`1`、`q` |
| form-66 | form.12 | 說明 note 的標題是那一欄的名稱 | 表單 | 看跳出來的 note 標題 |
| form-67 | form.12（圖） | 說明 note 的內容告訴使用者按 `[Enter]` 編輯這一欄 | 表單 | 看 note 的內文 |
| form-68 | form.12 | 說明 note 按 `Enter`、`Esc` 都能關，關掉後回到表單、focus 不動 | 表單 | 跳出 note 後各按一次 `Enter`、`Esc` |
| form-69 | form.12（圖） | 說明 note 的 hint 是 `Enter\|Esc:close` | 表單 | 看 note 的下框 |
| form-70 | form.12 | 表單的操作鍵（`j` `k` `h` `l`、方向鍵、`Tab\|Shift-Tab`、`u\|d`、`g`、`G`、`e`、`Enter`、`Esc`、`Space`、`?`）在打字欄位上不跳 note | 表單 | 在 text 欄位上逐一按這些鍵 |
| form-71 | form.12 | `e` 只在有問題的欄位與錯誤列上作用，其他地方不作用 | 表單 | 沒有錯誤時按 `e` |
| form-72 | form.12 | 開其他 input popup 的欄位（select、slider、日期、顏色、選檔、reorder、checkbox popup）上按可列印字元，不跳 note、不作用 | 表單 | focus 在 select 之類的欄位上打 `s`、`1`、`q`，沒有 note，什麼都沒變 |
| form-73 | form.12 | 其他可列印字元在選項、按鈕、錯誤列上不跳 note、不作用 | 表單 | focus 在按鈕上打 `s` |
| form-74 | form.13 | focus 在會開 input popup 的欄位上，hint 寫 `Enter:edit` | 表單 | 看下框 hint |
| form-75 | form.13 | 表單與一列一個值的 panel 上，focus 在 radio 的選項上，hint 寫 `Enter:choose` | radio | 看下框 hint |
| form-76 | form.13 | 表單上 focus 在 checkbox 的選項上，hint 寫 `Enter\|Space:toggle` | 表單＋checkbox | 看下框 hint |
| form-77 | form.13 | focus 在按鈕上，hint 寫按鈕的字：動詞小寫，名稱、路徑照原樣（`Save` → `Enter:save`、`Save As` → `Enter:save as`） | 表單 | `Tab` 到每一顆按鈕看 hint |
| form-78 | form.13 | focus 在有問題的欄位上時加 `e:error`（`Enter:edit e:error Tab:actions Esc:cancel`） | 表單 | 送出被擋後看 hint |
| form-79 | form.13 | focus 在錯誤列上，hint 是 `Enter:show e:edit Tab:actions Esc:cancel` | 表單 | 送出被擋後走到錯誤列看 hint |
| form-80 | form.13 | `Tab` 寫要去的那一塊：欄位區（含錯誤列）`Tab:actions`、按鈕上 `Tab:fields`，不寫 `Tab:save` | 表單 | 在欄位與按鈕上各看一次 hint |
| form-81 | form.13 | `Esc` 寫 `Esc:cancel`，不寫 `close` | 表單 | 看下框 hint |
| form-82 | form.15 | 沒改過的表單按 `Esc` 直接關 | 表單 | 打開表單不改，按 `Esc` |
| form-83 | form.15 | 放棄的 confirm 上 `Enter` 放棄並關掉表單；`Esc` 關掉 confirm、回到表單，值都還在 | 表單 | 在那個 confirm 上分別按 `Enter`、`Esc` |
| form-84 | form.15 | 有值寫回表單就算改過：input popup（含 checkbox popup 按 `Enter` 整組寫回）確定了跟打開時不同的值、選了 radio 的選項、翻了 checkbox | 表單 | 各做一次後按 `Esc`，都先跳 confirm |
| form-85 | form.15 | 「改過了」設起來後不清掉：改了又改回原值也算改過 | 表單 | 改一欄再改回原值，按 `Esc` 仍先跳 confirm |
| form-86 | form.15 | 會問要不要放棄的只有表單、textarea、reorder：其他 input popup 按 `Esc` 直接關、不問 | input | 在 text input popup 打了字後按 `Esc` |
| form-87 | form.16 | 牽涉整張表單的規則（必填、依另一欄而定的必填、名字重複）在按下按鈕送出時才檢查 | 表單 | 必填欄空著時走過去不會變紅，按送出才擋 |
| form-88 | form.16 | 檢查沒過：不存，表單留著，值都在 | 表單 | 讓必填空著按送出 |
| form-89 | form.16 | 檢查沒過時，每一個有問題的欄位（不只第一個）label 都轉 Red | 表單 | 讓兩欄出錯後送出 |
| form-90 | form.16 | 錯誤列寫依欄位順序的第一個問題 | 表單 | 讓兩欄出錯後送出，看錯誤列 |
| form-91 | form.16 | 在有問題的欄位上按 `e`：focus 跳到錯誤列，錯誤列換成這一欄的訊息 | 表單 | 兩欄出錯時，在第二欄按 `e` |
| form-92 | form.16 | 在錯誤列按 `Enter` 打開完整訊息的 error popup，標題寫那一欄的名字，`Enter`、`Esc` 都能關 | 表單 | 在錯誤列按 `Enter`，看標題，再各按 `Enter`、`Esc` |
| form-93 | form.16 | 在錯誤列按 `e`：focus 回到這則訊息的那一欄 | 表單 | 在錯誤列按 `e` |
| form-94 | form.16 | 錯誤跟著檢查走：表單的 Red label 與錯誤列一直掛著，值改了也一樣，到下一次檢查（送出、按不關表單的動作）才換掉或清掉 | 表單 | 送出被擋後改好那一欄，label 仍是 Red，再送出才清掉 |
| form-95 | form.12 | 打字說明 note 只收 `Enter`、`Esc`：其他可以打的字（包括 `q`、`?`）都不作用，也不穿過去 | 表單 | 在 text 欄位上打 `a` 跳出 note，再打 `q`、`?`、`j`，note 還在、什麼都沒發生 |
| form-96 | form.16 | input popup 的錯誤列一直掛著，值改了也一樣，到下一次 `Enter` 才換掉或清掉 | input | 讓 input popup 出錯後改值，錯誤還在；再按 `Enter` 才換掉 |

## dialog/menu

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| menu-1 | menu.1 | menu 只用在沒有搜尋、選一列執行的清單：要搜尋的用 finder，選值寫回的用 select，排順序的用 reorder | 都要 | 看每個 menu，選一列就是執行那一列 |
| menu-2 | menu.2 | 每一列的 label 用 Text | 都要 | 按 `Space` 看 menu 的列 |
| menu-3 | menu.2 | 熱鍵標記 `[x]` 跟 label 同色 | 都要 | 看有熱鍵的列 |
| menu-4 | menu.2 | 說明用 Overlay0 | 都要 | 看說明的顏色 |
| menu-5 | menu.2 | 每一列左邊是動作名稱；說明靠右，貼著右邊的留白（一般離右框一格） | 都要 | 看每一列說明的右緣 |
| menu-6 | menu.2 | 說明太長時（框已經到最寬）從尾端截，加 `…`，只佔一列 | 都要 | 把視窗縮窄，看長的說明 |
| menu-7 | menu.2 | label 與說明之間最少兩格 | 都要 | 看最寬的那一列 |
| menu-8 | menu.2 | 區塊標題前面一個 `nf-md-hexagon`（U+F02D8），空一格，再寫標題 | 都要 | 看 Space menu 的區塊標題 |
| menu-9 | menu.2 | 區塊標題大寫 | 都要 | 看區塊標題 |
| menu-10 | menu.2 | 區塊標題 Overlay0、不加粗 | 都要 | 看區塊標題 |
| menu-11 | menu.2 | 區塊標題縮一格（離框一格，跟各列的字同一欄） | 都要 | 看區塊標題的左緣 |
| menu-12 | menu.2 | cursor 跳過區塊標題 | 都要 | 用 `j\|k` 經過區塊標題 |
| menu-13 | menu.2 | 區塊之間的分隔線用虛線 `╌`（U+254C） | 都要 | 看分隔線用的字元 |
| menu-14 | menu.2 | cursor 跳過分隔線 | 都要 | 用 `j\|k` 經過分隔線 |
| menu-15 | menu.2（圖） | 區塊標題、各列、分隔線之間都不空行 | 都要 | 看 Space menu 裡沒有空列 |
| menu-16 | menu.2 | 標題是 `nf-fa-bars`（U+F0C9）加文字，畫成標題膠囊 | 都要 | 看每個 menu 的標題 |
| menu-17 | menu.2 | Space menu 的標題寫 focus panel 的 `[N] label` | 都要 | 在不同 panel 按 `Space` 看標題 |
| menu-18 | menu.2 | `Global operation` 那一列的說明一律是 `actions for the whole app` | 都要 | 看 Space menu 的最後一列 |
| menu-19 | menu.3 | hint 是 `Enter:run Esc:close`，不寫移動鍵 | 都要 | 看 menu 的下框 |
| menu-20 | menu.3 | 工作清單上沒有動作可做的列，`Enter` 打開那一列的全文，hint 寫 `Enter:detail Esc:close` | 工作清單 | cursor 移到沒有動作可做的列，看下框 |
| menu-21 | menu.5 | 工作清單上可以對那一列做事的（例：進行中的傳輸可以取消），`Enter` 打開帶那一列全文的 confirm，hint 寫那個動作（例 `Enter:cancel Esc:close`） | 工作清單 | cursor 移到可以做事的列，看 hint 後按 `Enter` |
| menu-22 | menu.5 | 工作清單開著時，列跟著工作更新（進度、狀態一變那一列就變），不用關掉重開 | 工作清單 | 工作進行中打開工作清單，看列的進度在變 |
| menu-23 | menu.4 | 模式的 Space menu 分兩區：`ITEM OPERATION` 與 `<模式名> MODE`；panel、item、global 的動作不列 | 模式 | 進模式按 `Space` |
| menu-24 | menu.4 | 項目操作跟平常的列一樣能執行，選了等於按那個鍵；現在不能做的停用 | 模式 | 從 menu 執行一項；cursor 停在不能做的地方再開 menu |
| menu-25 | menu.4 | 移動鍵只顯示：鍵 Blue、說明 Overlay0，cursor 跳過，`Enter` 不作用 | 模式 | 在 menu 裡移 cursor |
| menu-26 | menu.4 | 離開模式（字用模式 hint 裡 `Esc` 的動詞，例：`[Esc] Leave`）能從 menu 執行；menu 裡按 `Esc` 只關 menu、回到模式 | 模式 | 選 Leave；另外開一次 menu 按 `Esc` |
| menu-27 | menu.4 | 標題寫模式所在的地方：panel 的 `[N] label`，或 popup 的標題 | 模式 | 在 panel 上與 popup 裡的模式各開一次 |

## dialog/confirm

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| confirm-1 | confirm.2 | 標題 glyph 是 `nf-md-shield_alert`（U+F0ECC） | confirm | 打開一個 confirm（例：離開）看標題 |
| confirm-2 | confirm.2 | 標題文字是動作名（`DELETE`、`QUIT`、`CONNECT`） | confirm | 看標題文字 |
| confirm-3 | confirm.2 | 問句放最後，下面接著就是 hint（中間只有下方的留白） | confirm | 看問句與下框之間 |
| confirm-4 | confirm.2 | 回答前要看的內容放在問句上面 | confirm | 看有內容的 confirm |
| confirm-5 | confirm.2 | 內容跟問句之間空一列 | confirm | 看內容與問句之間 |
| confirm-6 | confirm.2 | 沒有內容時只有問句 | confirm | 看沒有內容的 confirm |
| confirm-7 | confirm.2 | 問句用 Text，不加粗 | confirm | 看問句 |
| confirm-8 | confirm.2 | 內容用 Overlay0 | confirm | 看內容的顏色 |
| confirm-9 | confirm.2 | 內容裡警告的那一句用 Peach | confirm | 看警告的那一句 |
| confirm-10 | confirm.2 | 問句與內容太長時折行，不截斷 | confirm | 把視窗縮窄，看長的問句或內容 |
| confirm-11 | confirm.2 | 內容長時只有內容那一段用 `j\|k` 捲，問句固定在最後 | confirm | 按 `j\|k`，問句不動 |
| confirm-12 | confirm.3 | hint 是 `Enter:<動詞> Esc:cancel`，動詞寫接受會做的事（`Enter:delete Esc:cancel`） | confirm | 看每個 confirm 的下框 |

## dialog/note

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| note-1 | note.2 | 標題是 glyph 加上顯示的東西，畫成標題膠囊 | 都要 | 看 key reference、viewer 的標題 |
| note-2 | note.2 | viewer 的標題：種類大寫；要寫顯示的是哪一個時，接 ` — ` 再接名稱，名稱照原樣（例 `YAML — pod/nginx`） | viewer | 看 viewer 的標題 |
| note-3 | note.2 | viewer 折行時，N 是最上面那一列所屬的行，M 是最下面那一列所屬的行，T 是總行數 | viewer | 把視窗縮窄讓內容折行，對照捲動位置與行號 |
| note-4 | note.2 | viewer 預設折行：一行比框寬時接到下一列畫；要對齊的內容 app 讓它不折行時，比框寬的部分截掉、行尾加 `…` | viewer | 打開有長行的內容，看長行折到下一列、或行尾有 `…` |
| note-6 | note.2 | 每一行的第一列畫行號，靠右對齊、後面空一格 | viewer | 看行號欄 |
| note-7 | note.2 | 折下來的列，行號欄空白 | viewer | 看折行的那幾列 |
| note-8 | note.2（圖） | 行號欄緊接在左邊的留白之後（離框一格），行號與內容之間不畫分隔線 | viewer | 看行號欄的位置 |
| note-9 | note.2（圖） | 折下來的列從內容欄的左緣開始，不跟著原行的縮排 | viewer | 看縮排很深的一行折下來的列 |
| note-10 | note.2 | 行號用 Overlay0 | viewer | 看行號的顏色 |
| note-11 | note.2 | 選取模式裡，游標所在那一行的行號用 Text | viewer | 按 `v` 後看游標那一行的行號 |
| note-12 | note.2 | 複製不含行號 | viewer | 選一段複製後貼出來看 |
| note-13 | note.2 | 行號欄至少三位：打開時就知道行數的取 max(3, 總行數的位數)，打開後不變 | viewer | 打開不到 100 行與超過 1000 行的內容，看行號欄寬 |
| note-14 | note.2 | 串流的 viewer（App Log）行號欄從三位開始，超過 999 行才跳寬 | viewer | 看串流到 1000 行前後的行號欄 |
| note-15 | note.2 | 有 tab 的 viewer，行號欄照看過的頁裡最寬的那一頁，只變寬、不變窄（串流的頁一樣） | viewer | 切到行數多的頁再切回來，看行號欄寬沒有縮回 |
| note-16 | note.2 | 內容有固定格式的 viewer（YAML、JSON、TOML、HTML、XML、Markdown……）照 file-picker 預覽的文字檔上色：chroma 的 catppuccin-mocha、只上前景色；檔案內容照檔名判斷格式 | viewer | 打開 YAML 檢視與一個 `.json` 檔的內容，看語法顏色跟預覽一樣、沒有背景色 |
| note-17 | note.2 | 選取範圍裡不顯示語法顏色 | viewer | 選一段有語法顏色的文字，看範圍裡的字 |
| note-18 | note.2 | viewer 裡的 Tab 畫成 `input_tab_width` 格空白，不對齊 tab 停點 | viewer | 打開有 Tab 的檔案 |
| note-19 | note.2 | 換行前面的 `\r`（CRLF）不畫 | viewer | 打開 CRLF 的檔案 |
| note-20 | note.2 | 其他控制字元畫成名字（`\x07`），Red | viewer | 打開含控制字元的內容 |
| note-21 | note.2 | 複製照原樣：是原本的 Tab 與控制字元，不是畫出來的空白或名字 | viewer | 選含 Tab 的一段複製後貼出來看 |
| note-22 | note.3 | 用 `j\|k`、`u\|d`、`gg\|G` 捲動 | 都要 | 在放不下的 key reference 上按這些鍵 |
| note-23 | note.3 | viewer 折行時以畫面上的一列為單位捲：`j\|k` 一次一列，`u\|d` 半頁照列算 | viewer | 折行時按 `j`，看一次只捲一列 |
| note-24 | note.3 | `Enter` 不關 note（error popup 與表單的打字說明除外） | 都要 | 在 key reference、viewer 上按 `Enter` |
| note-25 | note.4 | 選取模式只有 viewer 有：key reference、error popup、打字說明按 `v` 不作用，`j\|k` 只捲動 | 都要 | 在 key reference 上按 `v` |
| note-26 | note.4 | viewer 平常沒有游標，`j\|k`、`u\|d`、`gg\|G` 捲動畫面 | viewer | 打開 viewer 按 `j` |
| note-27 | note.4 | 有 tab 的 viewer 平常用 `h\|l` 切 tab | viewer | 按 `h`、`l` |
| note-28 | note.4 | 第一次 `v` 進入選取模式：框與模式名換成模式色 Yellow | viewer | 按 `v`，看框與模式名 |
| note-29 | note.4 | 進入選取模式時游標在畫面第一行的行首，還沒開始選 | viewer | 按 `v`，看游標位置 |
| note-30 | note.4 | 選取模式裡 `h\|j\|k\|l`（有 tab 的 viewer 也是，`h\|l` 不切 tab）、`w\|b\|e`、`0\|$`、`u\|d`、`gg\|G` 移動游標，走到畫面邊緣時畫面跟著捲 | viewer | 按 `v` 後逐一按這些鍵，走到底邊 |
| note-31 | note.4 | 還沒開始選時 hint 是 `v:select Esc:cancel` | viewer | 按一次 `v` 後看下框 |
| note-32 | note.4 | 第二次 `v` 從游標所在開始選，移動游標把範圍拉開 | viewer | 按第二次 `v` 後移動游標 |
| note-33 | note.4 | 範圍以字為單位：從起點到游標，含游標那個字 | viewer | 選一段後複製，看頭尾 |
| note-34 | note.4 | 開始選之後模式名是 `Visual>select`，hint 是 `y:copy Esc:unselect` | viewer | 按第二次 `v` 後看下框 |
| note-35 | note.4 | 開始選之後再按 `v` 不作用（不當離開的別名） | viewer | 開始選之後按 `v` |
| note-36 | note.4 | `y` 複製選起來的文字，離開選取模式，範圍與游標都消失；跳一個 Success toast 說複製好了 | viewer | 選一段後按 `y` |
| note-37 | note.4 | `Esc` 一次退一層：開始選之後範圍消失、回到 `Visual`，游標留在原地；還沒開始選時整個離開，游標消失；都不複製 | viewer | 開始選之後按 `Esc`，再按一次 |
| note-38 | note.4 | 游標是一格層色底、Base 字 | viewer | 按 `v` 後看游標 |
| note-39 | note.4 | 範圍是 Yellow 底、Base 字，游標那格維持層色 | viewer | 選一段後看範圍與游標 |
| note-40 | note.4 | 範圍裡的空行畫一格 | viewer | 選一段跨過空行的範圍 |
| note-41 | note.5 | 標題 glyph 是 `nf-fa-question_circle`（U+F059） | 都要 | 按 `?` 看標題 |
| note-42 | note.5 | 標題文字是 `<surface> keys`（`[2] HOSTS KEYS`、`SPACE MENU KEYS`） | 都要 | 在 panel 與 Space menu 上各按 `?` 看標題 |
| note-43 | note.5 | 每一列一個鍵，縮兩格（鍵從框線內第三格開始） | 都要 | 看鍵的左緣 |
| note-44 | note.5 | 鍵補到跟最寬的鍵一樣寬，空兩格，再接說明 | 都要 | 看說明都從同一欄開始 |
| note-45 | note.5 | 說明太長時（框已經到最寬）從尾端截，加 `…`，不折行 | 都要 | 把視窗縮窄，看長的說明 |
| note-46 | note.5 | 從 menu 來的列，說明寫 `label — 說明` | 都要 | 對照 Space menu 的列 |
| note-47 | note.5 | 從 menu 來的列，label 去掉熱鍵標記、大小寫照原樣（`[E]dit` 寫成 `Edit`） | 都要 | 對照 Space menu 的列 |
| note-48 | note.5 | 區塊標題跟 menu 一樣：`nf-md-hexagon`、大寫、Overlay0、縮一格、不加粗 | 都要 | 看區塊標題 |
| note-49 | note.5（圖） | 區塊之間不畫分隔線、不空行：區塊標題直接接在上一區最後一列下面 | 都要 | 看兩個區塊之間 |
| note-50 | note.5 | panel 上的區塊依序是（一列一個值的 panel 有的話）`what each row is`、`item operation`、`panel operation`、`move`、`core keys`、`app-wide` | 都要 | 在 panel 上按 `?` 看區塊順序 |
| note-51 | note.5 | `item operation`、`panel operation` 的內容跟 Space menu 一樣 | 都要 | 對照同一個 panel 的 Space menu |
| note-52 | note.5 | `move` 只列這裡真的能用的移動鍵 | 都要 | 對照 `move` 的每一個鍵在這個 panel 上按得出效果 |
| note-53 | note.5 | `core keys` 列這個 panel 上有作用的 core key：`Space`、`?`、`Tab`、`1–N`、`q\|Ctrl-C` | 都要 | 看 `core keys` 那一段 |
| note-54 | note.5 | `1–N` 只在有好幾個 panel 時列進 `core keys` | 都要 | 看只有一個 panel 的畫面沒有 `1–N` |
| note-55 | note.5 | `Esc` 只在這裡有作用時才列進 `core keys`（例：有篩選可以清） | 都要 | 有篩選與沒有篩選時各按 `?` |
| note-56 | note.5 | `Enter` 不列進 `core keys`（已經在 `item operation` 寫了） | 都要 | 看 `core keys` 沒有 `Enter` |
| note-57 | note.5 | panel 的 key reference 在 `app-wide` 區列出 global 熱鍵；離開的 `q` 已在 `core keys`，不重複 | 都要 | 對照 global operation popup 的熱鍵 |
| note-58 | note.5 | 現在按得了的鍵用 Blue、不加粗（按不了的見 note-60） | 都要 | 看鍵欄的顏色 |
| note-59 | note.5 | 說明用 Text | 都要 | 看說明的顏色 |
| note-60 | note.5 | 現在按不了（對象存在）的鍵照樣列出，鍵與說明都用 Surface2 | 停用 | 讓某個動作停用後按 `?` |
| note-61 | note.5 | hint 是 `?\|Esc:close` | 都要 | 看 key reference 的下框 |
| note-62 | note.6 | 框、文字都是 Red | error popup | 看 error popup 的框與訊息 |
| note-63 | note.6 | 標題膠囊填 Red、字 Base 粗體 | error popup | 看標題膠囊 |
| note-64 | note.6 | 標題 glyph 是 `nf-md-fire`（U+F0238） | error popup | 看標題 |
| note-65 | note.6 | 訊息在框裡折行；太長時 `j\|k` 捲動 | error popup | 讓長的訊息跳出來，按 `j\|k` |
| note-66 | note.6 | 標題寫哪件事失敗了（`RENAME FAILED`、`SAVE FAILED`）；從表單錯誤列打開的寫那一欄的名字（form-92） | error popup | 看標題文字 |
| note-67 | note.6 | `Enter` 與 `Esc` 都能關 | error popup | 各按一次 `Enter`、`Esc` |
| note-68 | note.6 | hint 是 `Enter\|Esc:close` | error popup | 看下框 |
| note-69 | note.6 | 關掉 error popup 之後回到底下的 popup，focus 留在原位（表單的送出或不關表單的動作失敗時，focus 在那顆按鈕上，再按 `Enter` 就是重試），值都還在 | error popup | 關掉後看底下的 popup |
| note-70 | note.4 | 每個 viewer 都有選取模式（`v` 選取、`y` 複製） | viewer | 在每個 viewer 上按 `v` |
| note-71 | note.2 | viewer 的搜尋：命中的字全部加底線、保留原本的顏色；目前那一筆畫成 cursor 色塊；不用 Yellow | viewer | 在有 `/` 的 viewer 搜一個出現好幾次的字，看底線與目前那一筆（沒有搜尋的 viewer 沒有這種情況） |
| note-72 | note.2 | 不折行的 viewer，選取模式的游標走進截掉的部分時，畫面跟著左右捲到看得見，左邊被捲掉的開頭加 `…`；截掉的內容選得到、複製得到 | viewer | 在不折行的 viewer 進選取模式，把游標往右走到截掉的地方 |
| note-73 | note.5 | 「每一列」那一節的說明太長時在右欄折行、名稱欄不動，不截斷；按鍵的各節照舊一列一個鍵、太長截 | 一列一個值的 panel | 讓一列的說明比框寬，按 `?` 看它折行 |
| note-74 | note.2 | viewer 的內容裡，app 一行一行交來的一行夾著 `\n` 時拆成兩行 | viewer | 讓 app 交給 viewer 的一行含 `\n`（例：多行的錯誤訊息），看是兩行 |
| note-75 | note.2 | viewer 的內容裡，顏色碼（SGR）照著上色，一行裡的 `\r` 只留最後的狀態，不是顏色碼的序列畫成紅色的名字 | viewer | 打開含顏色碼、`10%\r100%`、`\x1b[2J` 的內容 |
| note-76 | note.7 | 每個 app 都有 App Log，是 viewer，最新的在最下面，開著時新的一筆照樣進來 | 都要 | 按 `!`，做幾件事，看新的一筆進來 |
| note-77 | note.7 | 記使用者的動作與結果、每一個 toast、app 在背景做的事；動作是 Rules P3 的三種 operation，只看不改的也記，移動 cursor、換 focus、panel filter、比較模式、在 confirm 或表單上取消的不記 | 都要 | 做一個改東西的動作、一個只看的動作（例：開 viewer）、跳一個 toast，移動幾次 cursor，按 `!`；讀程式 |
| note-78 | note.7 | 每一筆：時間 `HH:MM:SS`（Overlay0）、等級（`INFO` Text、`OK` Green、`WARN` Peach、`ERR` Red，四格寬靠左）、發生的事（跟 toast 一樣大寫開頭） | 都要 | 看 App Log 的各種等級 |
| note-79 | note.7 | 只放在記憶體，app 關掉就清空；筆數有上限，滿了丟掉最舊的 | 都要 | 讀程式；或關掉再開，App Log 是空的 |
| note-80 | note.8 | 標題 glyph `nf-md-compare`（U+F018A），`DIFF — <anchor> ↔ <另一個>`，後面接 `UNIFIED`、`SPLIT` 兩個 tab，`h\|l` 切 | 比較模式 | 打開比較，按 `h\|l`；讀程式核對 code point |
| note-81 | note.8 | 只顯示有差異的段落，前後各 3 行沒變的，段落之間一條 Overlay0 的分隔線 | 比較模式 | 比兩個長內容、只差兩處的項目 |
| note-82 | note.8 | UNIFIED：刪掉的行 `-` Red、加上的行 `+` Green、沒變的 Text；anchor 是刪掉的那一邊；行號兩欄、Overlay0 | 比較模式 | 看 UNIFIED |
| note-83 | note.8 | SPLIT：左 anchor、右另一個，各自標行號；刪 Red 在左、加 Green 在右，對應不到的留空列；不折行，太長截掉加 `…` | 比較模式 | 看 SPLIT |
| note-84 | note.8 | 記住上次選的 tab（狀態） | 比較模式 | 換成 SPLIT 後關掉 app、再開、再比一次 |
| note-85 | note.8 | 終端機寬不到 96 時一律 UNIFIED，`SPLIT` 停用 | 比較模式 | 把終端機縮到 96 以下再比 |

## dialog/terminal

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| terminal-1 | terminal.1 | PTY 放在 panel 裡時不是 popup：框照 panel 畫 | PTY | 看放 PTY 的 panel 的框 |
| terminal-2 | terminal.2 | 上面留著 statusbar 或畫面 chip 列（含 chip 列下面的分隔線），框從分隔線的下一列開始 | terminal popup | 打開後看最上面幾列 |
| terminal-3 | terminal.2 | 沒有 statusbar 的 app，框從第一列開始 | terminal popup | 看上框在畫面第一列 |
| terminal-4 | terminal.2 | 標題 glyph 是 `nf-md-console`（U+F018D） | terminal popup | 看標題 |
| terminal-5 | terminal.2 | 標題文字寫跑的是什麼（`SHELL`、`ALTERM: myhost`），名稱與路徑照原樣 | terminal popup | 看標題文字 |
| terminal-6 | terminal.2 | 真的游標藏起來，在子程序的游標位置畫一格 Text 底、Base 字的方塊 | PTY | 在 shell 裡看游標 |
| terminal-7 | terminal.2 | 子程序用 DECSCUSR 要求的游標形狀（底線、直線）不理 | PTY | 在 shell 裡送 `printf '\e[6 q'`，游標仍是方塊 |
| terminal-8 | terminal.3 | hint 裡出口鍵永遠是第一個 | terminal popup | 看下框 hint |
| terminal-9 | terminal.3 | hint 放不下時，出口鍵最後才捨 | terminal popup | 把終端機縮窄，看 hint |
| terminal-10 | terminal.3 | 出口鍵的動詞寫真正會發生的事：結束子程序寫 `Alt-Esc:exit`，離開但子程序還留著寫 `Alt-Esc:leave` | terminal popup | 看 hint，再按出口鍵對照結果 |
| terminal-11 | terminal.3 | 出口鍵不寫 `close` | terminal popup | 看 hint |
| terminal-12 | terminal.3 | 出口鍵後面跟 app 保留的組合鍵（`Alt-t:hide`、`PgUp:history`） | terminal popup | 看 hint 的順序 |
| terminal-13 | terminal.2 | terminal popup 開著時 footer 不畫：最後一列的兩端是空白，不露出 footer 的字 | terminal popup | 打開 terminal popup，看最後一列的兩端 |
| terminal-14 | terminal.2 | PTY 放在 panel 裡時也不留白：panel 的框照畫，PTY 貼著框 | PTY | 看放 PTY 的 panel 裡第一個字與框之間 |
| terminal-15 | terminal.5 | 在 PTY 上按 `PgUp` 捲上去就進入歷史模式：框與模式名換成模式色，模式名是 `History` | 互動 terminal | 在 PTY 上按 `PgUp`，看框與上框右邊 |
| terminal-16 | terminal.5 | 歷史模式裡 `j\|k`、`u\|d`、`gg\|G`、`PgUp\|PgDn` 都捲歷史，不送給子程序 | 互動 terminal | 進歷史模式後按這些鍵，看歷史捲動、shell 沒有收到 |
| terminal-17 | terminal.5 | 歷史模式裡 `Esc` 離開模式，回到即時畫面 | 互動 terminal | 進歷史模式後按 `Esc` |
| terminal-18 | terminal.6 | 互動 terminal 的選取模式用 `Alt-v` 進入（家族的 `v`，PTY 裡加 `Alt` 跳出子程序），跟保留鍵一樣常駐揭露 | 互動 terminal | 看 footer 或 terminal 的下框有 `Alt-v:select`，按下去 |
| terminal-19 | terminal.6 | 進入 PTY 的選取模式時畫面凍住：子程序後來的輸出先不畫上去，游標可以往上走進歷史；離開時回到即時畫面 | 互動 terminal | 讓 shell 一直輸出時進選取模式，看畫面不動、游標能往上走 |
| terminal-20 | terminal.6 | PTY 的選取模式照 note 的選取模式：按鍵、顏色、捲動位置、複製後的 toast 都一樣 | 互動 terminal | 在 PTY 的選取模式選一段複製，對照 viewer 的選取模式 |
| terminal-21 | terminal.4 | app 開一個程式做一件事的 PTY（編輯器、讓 doas 問密碼）沒有歷史模式與選取模式，按鍵全部給那個程式，包括 `PgUp` | PTY | 在開著編輯器的 PTY 按 `PgUp`，看編輯器自己往上翻、框沒有換成模式色 |
| terminal-22 | terminal.4 | 子程序佔滿整個畫面時（vim、less、htop），`PgUp` 送給它，下框不寫 `PgUp:history`；它回到一般畫面後 `PgUp` 又進歷史模式 | 互動 terminal | 在 shell 裡開 `less` 按 `PgUp`，看 less 往上翻、下框沒有 `PgUp:history`；離開 less 再按 `PgUp` |
| terminal-23 | terminal.4 | 使用者把所有鍵都給子程序時（例：sshu 鎖住格子），選取模式暫時讓出去，`PgUp\|PgDn` 直接送進去；解開的鍵常駐揭露，解開後兩種模式回來 | 互動 terminal | 有這種狀態的 app：進去後按 `Alt-v`、`PgUp`，看都送進子程序、下框寫著解開的鍵；解開後再按一次 |
| terminal-24 | terminal.7 | 要提權時先試不用密碼的；要密碼時用 password popup（解鎖）問，交給工具的標準輸入，打錯時 popup 不關、寫 `Wrong password`；密碼不寫進檔案、不進 App Log、不出現在畫面上、不送到網路上，app 拿不到；工具不能從標準輸入讀時（doas）在 terminal popup 裡讓它自己問 | 提權 | 在要密碼的機器上做要提權的動作，先打錯一次再打對；看 App Log 沒有密碼；讀程式：密碼只交給工具 |

## dialog/toast

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| toast-1 | toast.2 | 框是 popup 的框，一律用第 1 層的層色 | toast | 在疊了 popup 時跳 toast，看框色 |
| toast-2 | toast.2 | toast 不被淡化 | toast | toast 開著時打開 popup，看 toast 沒有變暗 |
| toast-3 | toast.2 | 下框一律在畫面倒數第三列，最下面兩列一直看得到（平常是 panel 的下框與 footer；terminal popup 開著時是 PTY 的最後一列與 terminal 的下框；沒有 panel 的畫面也一樣） | toast | 在一般畫面與 terminal popup 裡各跳一次 toast，看下框的列 |
| toast-4 | toast.2 | 文字置中 | toast | 看訊息的位置 |
| toast-5 | toast.2 | 太長時折行，每一列都置中 | toast | 跳一個長的 toast |
| toast-6 | toast.2 | 最多幾列，app 可以自行決定；app 設了上限、訊息超過時，最後一列結尾加 `…` | toast | 跳一個很長的 toast，看列數與結尾 |
| toast-7 | toast.2 | app 設了列數上限時，會被截掉的訊息，完整內容走 error popup 或 app 的 log | toast | 讀程式：長訊息的完整內容另外寫進 error popup 或 log |
| toast-8 | toast.2 | Info：標題 `nf-fa-flag`（U+F024）`INFO`，文字 Text | toast | 跳一個 Info toast |
| toast-9 | toast.2 | Warning：標題 `nf-md-alarm_light`（U+F078F）`WARNING`，文字 Peach | toast | 跳一個 Warning toast |
| toast-10 | toast.2 | Error：標題 `nf-md-fire`（U+F0238）`ERROR`，文字 Red | toast | 跳一個 Error toast |
| toast-11 | toast.2 | Success、Info 顯示 2200ms | toast | 量 Success、Info toast 停留的時間 |
| toast-12 | toast.2 | Warning、Error 顯示 4400ms | toast | 量 Warning、Error toast 停留的時間 |
| toast-13 | toast.2 | 第二個 toast 來時直接取代第一個，重新計時 | toast | 連續跳兩個 toast |
| toast-14 | toast.3 | hint 是 `Esc:close` | toast | 看 toast 的下框 |
| toast-15 | toast.2 | Success：標題 `nf-md-check_circle`（U+F05E0）`SUCCESS`，文字 Green | toast | 跳一個 Success toast |
| toast-16 | toast.2 | 做完的事用 Success 還是 Info，app 可以自行決定；失敗一律 Error | toast | 完成一個動作，看跳的是 Success 或 Info；讓一個動作失敗，看是 Error |
| toast-17 | toast.1 | 跟某個 popup 的動作有關、需要使用者看完再決定的失敗，用 error popup，不用 toast | toast | 讓 popup 裡的動作失敗，看跳的是 error popup |
| toast-18 | toast.2 | 做完了或還能用、但有值得注意的地方用 Warning（例：`3 files skipped`） | toast | 做一個部分略過的動作，看跳的是 Warning |
| toast-19 | toast.2 | 動作失敗一律用 Error，不用 Warning | toast | 讓一個動作失敗，看跳的是 Error（或 error popup） |
| toast-20 | toast.2 | toast 每一列的第一個字母大寫，其他照原樣；一列從名稱或路徑開始時，名稱照原樣不改大小寫 | toast | 讓 app 跳幾個 toast（含開頭是檔名的），看每一列的第一個字 |

## input/README

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| input-1 | input.1 | 從表單或一列一個值的 panel 的欄位打開的 input，錯誤要點名值時用那一欄的名字、不用標題；能直接指出錯在哪裡的照指出的寫 | 表單、一列一個值的 panel | 讓值不合格按 `Enter`，看錯誤列點名的是欄位名或錯的那一處，不是標題 |
| input-2 | input.1 | 自己打開的 input（標題寫在做什麼，例 `RENAME`、`SAVE AS`），錯誤點名 app 另外給的值的名字（例 `Name`），不拿標題當名字 | input | 在 `SAVE AS` 之類的 popup 貼上控制字元按 `Enter`，錯誤寫 `Name can't …`，不是 `Save as can't …` |
| input-3 | input.1 | `Esc`：關掉，值不變 | input | 改了值按 `Esc`，欄位還是舊值 |
| input-4 | input.1 | 有按鈕的 input popup：hint 在欄位上寫 `Tab:actions`、在按鈕上寫 `Tab:fields` | input | 看兩處的下框 hint |
| input-5 | input.2 | 有說明列：一句話說要輸入什麼，Overlay0（password 的解鎖樣式例外，見 password-24） | text、password、number | 打開 text／number／password popup，看打字列上面那一句 |
| input-6 | input.2（圖） | 說明列在打字列上面 | text、password、number | 看內容的列序 |
| input-7 | input.2 | 說明列跟打字列之間空一列 | text、password、number | 數兩列之間的空列 |
| input-8 | input.2 | 要改的對象是誰，寫進說明列那一句（例 `New name for assets`） | text、password、number | 打開 rename 之類的 popup，看說明列寫出對象 |
| input-78 | input.2 | 說明太長時折行、popup 跟著長高；長到最高還放不下，最後一列結尾加 `…` | text、password、number | 讓說明比框寬（例：網頁 prompt 的長問題），看它折行 |
| input-9 | input.2 | 打字列最前面是 `nf-fa-angle_right`（U+F105），離框一格（password 解鎖方案除外） | text、password、number | 看打字列第一個字元與左框的距離 |
| input-10 | input.2 | 單行 input popup 的 `nf-fa-angle_right` 一直是層色 | text、password、number | 打開後與打字中各看一次 glyph 的顏色 |
| input-11 | input.2 | 值是 Lavender | text、password、number | 打幾個字看顏色 |
| input-12 | input.2 | 游標是一格 Lavender 底、Base 字 | text、password、number | 把游標移到字上看 |
| input-13 | input.2 | hint 是 `Enter:<動詞> Esc:cancel`，動詞寫按下去做什麼（rename、create、save） | text、password、number | 看下框 hint |
| input-14 | input.3 | 值比框長時，框裡顯示游標附近的那一段 | text、password、number | 打一串比框長的字 |
| input-15 | input.3 | 被截掉的那一邊補 `…` | text、password、number | 打長值，再按 `Home`，看兩端 |
| input-16 | input.3 | 游標一定看得到 | text、password、number | 長值裡按 `Home`、`End`、`←`、`→` |
| input-17 | input.3 | 游標移動時只捲剛好夠的量，不把游標固定在中間 | text、password、number | 長值裡從尾端一路按 `←`，看捲動 |
| input-18 | input.3 | 截斷照顯示寬度算（中文一個字 2 格） | text、password、number | 打長的中文值，框線不歪 |
| input-19 | input.3 | 截斷時一個字不切成兩半，紅色的 `\n`、`\x1b` 也一樣 | text、password、number | 貼上含 `\x1b` 的長值，捲動時看邊緣 |
| input-20 | input.4 | 字元、`Space` 插在游標處（password 除外） | input、panel filter | 游標移到中間再打字 |
| input-21 | input.4 | `←\|→` 游標往左、往右移一個字（password 除外） | input、panel filter | 按 `←`、`→` |
| input-22 | input.4 | `Backspace` 刪游標前面的字（password 除外） | input、panel filter | 游標在中間按 `Backspace` |
| input-23 | input.4 | `Delete` 刪游標上的字（password 除外） | input、panel filter | 游標在中間按 `Delete` |
| input-24 | input.4 | 一個字是看起來的一個字：中文、emoji 各一個，組合字元連同前面的字算一個（password 除外） | input、panel filter | 打中文、emoji、組合字元後按 `←`、`Backspace` |
| input-25 | input.4 | 貼上進來的控制字元各算一個字（`←\|→`、`Delete` 一次跨過或刪掉整個 `\x1b`）（password 除外） | input、panel filter | 貼上含 `\x1b` 的字，按 `←`、`Delete` |
| input-26 | input.4 | `Ctrl-U`、`Ctrl-W` 不收 | input、panel filter | 打字後按 `Ctrl-U`、`Ctrl-W`，值不變 |
| input-27 | input.4 | 其他 `Ctrl-`、`Alt-` 組合在打字列上沒有作用、不打出字 | input、panel filter | 按 `Ctrl-A`、`Alt-b`，值不變 |
| input-28 | input.5 | 灰字提議只用在 text、number（password 用灰點、textarea 直接帶入舊值） | input | 打開有舊值的 text、number，有灰字提議；打開有舊值的 textarea、password，沒有 |
| input-29 | input.5 | 改已有的值時，框打開是空的，舊值用灰字（Overlay0）顯示 | text、number | 打開一個有舊值的欄位 |
| input-30 | input.5 | 灰字從游標那一格開始：游標壓在第一個字上（Lavender 底、Base 字），後面接灰字 | text、number | 看打開時游標與灰字的位置 |
| input-31 | input.5 | 舊值第一個字是控制字元時，游標那一格照控制字元畫（Red 底、Base 字） | text、number | 打開舊值以 `\x1b` 開頭的欄位 |
| input-32 | input.5 | `Tab` 把舊值收進框裡，游標在尾端 | text、number | 有灰字時按 `Tab`，再按 `←` 改 |
| input-33 | input.5 | 直接打字：重打一個新的值，灰字隱藏 | text、number | 有灰字時打一個字 |
| input-34 | input.5 | 把打的字刪光，灰字再出現 | text、number | 打字後按 `Backspace` 刪光 |
| input-35 | input.5 | 框是空的時按 `Backspace`：灰字消失（不要這個值） | text、number | 打開後直接按 `Backspace` |
| input-36 | input.5 | 灰字消失後按 `Enter` 存成空的（欄位不能空時照錯誤處理） | text、number | `Backspace` 後按 `Enter`，看欄位變空或出錯誤 |
| input-37 | input.5 | 有灰字、什麼都沒碰就按 `Enter`：保留舊值、關掉（不是存成空的） | text、number | 打開後直接按 `Enter` |
| input-38 | input.5 | 有灰字時 hint 加 `Tab:edit Backspace:clear`（例 `Enter:rename Tab:edit Backspace:clear Esc:cancel`） | text、number | 看有灰字時的下框 hint |
| input-39 | input.5 | 灰字提議只有兩種來源：舊值，與沒有舊值時 app 給的建議值（沒有歷史、補完之類的提議） | input、panel filter | 打幾個字，看有沒有其他灰字 |
| input-40 | input.7 | input popup 裡不放 placeholder（空的打字列不寫灰字說明） | input | 打開沒有舊值的 input，打字列除了 glyph 什麼都沒有 |
| input-41 | input.7 | 打字列前面的 `nf-fa-angle_right` 不是字：不會被收進值，打字時也不會消失 | input、panel filter | 在空的打字列打字，glyph 留著 |
| input-42 | input.8 | 只算貼上的文字：按下去的 `Tab`、`Enter`、`Ctrl-J` 照原本的作用，不打成控制字元 | input、panel filter | 在打字列按 `Ctrl-J`，值裡沒有多出 `\n` |
| input-43 | input.8 | 貼上的控制字元一個都不丟，也不換成空白，留在值裡 | input、panel filter | 貼上多行文字 |
| input-44 | input.8 | 控制字元照實畫成紅字（Red），不切開（password 除外） | input、panel filter | 貼上多行文字看顏色 |
| input-45 | input.8 | `\r`、`\n`、`\t` 寫名字（2 格）（password 除外） | input、panel filter | 貼上含換行與 Tab 的文字 |
| input-46 | input.8 | 其他 C0、DEL、C1 寫 `\xNN`（4 格，例 `\x1b`、`\x7f`、`\x85`）（password 除外） | input、panel filter | 貼上從終端機複製、帶顏色的字 |
| input-47 | input.8 | `\r\n` 照實畫成 `\r\n` 兩個（password 除外） | input、panel filter | 貼上 CRLF 換行的文字 |
| input-48 | input.8 | 整列畫成灰色的列（沒有 focus 的打字列、提議）裡，控制字元跟著灰（password 除外） | input、panel filter | 打字列含 `\n` 時把 focus 移到清單；或看舊值含控制字元的灰字 |
| input-49 | input.8 | 游標停在控制字元上：整個控制字元畫成 Red 底、Base 字（一般的字照舊 Lavender 底）（password 除外） | input、panel filter | 按 `←` 移到 `\x1b` 上 |
| input-50 | input.8 | `Backspace` 一次刪一整個控制字元（password 除外） | input、panel filter | 游標在 `\x1b` 後面按一次 `Backspace` |
| input-51 | input.8 | 遮罩的值照樣遮罩（password 貼上控制字元也只畫遮罩） | password | 在 password 貼上含 `\n` 的文字 |
| input-52 | input.8 | 不是使用者打字進來的值（原本的名字、檔案或別的程式給的、清單填回來的、啟動目錄來的預設值、提議…）走同一個過濾 | input、panel filter | 帶入含 `\x1b` 的舊值，看畫成紅字、確定時擋下；或讀程式 |
| input-53 | input.8 | 值會被拿去用的（送出、存、執行、交給別的程式）：有控制字元時按 `Enter` 擋下 | input | 貼上多行後按 `Enter`，popup 不關 |
| input-54 | input.8 | 擋下時錯誤列寫原因並點名值（例 `Name can't have control characters`） | input | 看擋下時的錯誤列 |
| input-55 | input.8 | 控制字元的檢查在去掉前後空白字元之前（`Icon\r` 也擋得到） | input | 貼上 `Icon\r` 按 `Enter`，被擋下 |
| input-56 | input.8 | 搜尋與篩選的打字列只畫，不擋 | panel filter、finder | 在 finder 打字列貼上含 `\n` 的字，照樣篩選、畫紅字 |
| input-57 | input.9 | 一行的值確定時去掉前後的空白字元（password 不去） | text、number | 打 `  x ` 確定，存成 `x` |
| input-58 | input.9 | 去掉的是所有 Unicode 空白字元（一般空格、全形空格 U+3000、NBSP…） | text、number | 打全形空格加 `x` 加 NBSP 確定，存成 `x` |
| input-59 | input.10 | 值的顏色是 Text | 表單、input | 看表單或 panel 上的值 |
| input-60 | input.10 | 空的值用灰字（Overlay0）寫出「空著代表什麼」（例 `not set`），不是一片空白 | 表單、input | 清空一個欄位後看 |
| input-61 | input.10 | 空值的灰字不寫教人按鍵的字（例：不寫 `enter to browse ~/.ssh`） | 表單、input | 看每個空值的字 |
| input-62 | input.10 | 值太長從尾端截，加 `…` | 表單、input | 填一個很長的值 |
| input-63 | input.10 | 路徑太長從前面截（`…/.ssh/id_ed25519`） | file-picker | 填一個很長的路徑 |
| input-64 | input.10 | text 顯示值本身；number 顯示值本身，有單位時空一格接單位、寫完整的字（`10 seconds`） | text、number | 看表單或 panel 上的值 |
| input-65 | input.10 | password 設了是固定 8 個 `•`，沒設照空值 | password | 各看一個設了、沒設的密碼欄 |
| input-66 | input.10 | textarea 顯示第一行，後面還有就加 `…` | textarea | 填多行後看欄位 |
| input-67 | input.10 | select 顯示選中那一項的文字 | select | 看欄位 |
| input-68 | input.10 | checkbox popup 的值是選中的項目用 `, ` 接起來，太長加 `…` | checkbox | 勾幾項後看欄位 |
| input-69 | input.10 | reorder 的值照目前的順序用 `, ` 接起來，太長加 `…` | reorder | 排過順序後看欄位 |
| input-70 | input.10 | 畫在表單上的 radio、checkbox 顯示選項本身 | radio、checkbox | 看表單 |
| input-71 | input.10 | date／datetime picker 顯示格式化的日期（時間） | datetime picker | 看欄位 |
| input-72 | input.10 | color picker 的值顯示成 3 格的色塊（`███`）、空一格、hex（`███ #2A2A3C`，hex 一律大寫） | color picker | 看欄位 |
| input-73 | input.10 | file-picker 顯示路徑，家目錄寫成 `~` | file-picker | 選一個家目錄下的檔案後看欄位 |
| input-74 | input.6 | 沒有舊值、app 有建議值時，用灰字提議顯示建議值（長相、`Tab`、直接打字、`Backspace`、hint 都跟舊值的提議一樣） | text、number | 打開有建議值的新建欄位（沒有建議值的 app 沒有這種情況） |
| input-75 | input.6 | 有建議值、什麼都沒碰就按 `Enter`：用建議值，寫回去、照常檢查（不能空的欄位也不跳「不能空」） | text、number | 打開有建議值的欄位直接按 `Enter` |
| input-76 | input.10 | 表單與 panel 上的值有控制字元時，照打字列寫成紅色的轉義（`\n`、`\t`、`\x1b`），不丟、不換成空白 | input | 讓一個欄位的值含 Tab 或 `\x1b`，看表單或 panel 上的值 |
| input-77 | input.2 | 打字列的 `nf-fa-angle_right` 後面空一格才接值 | text、password、number | 看打字列 glyph 與值之間 |

## input/text

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| text-1 | text.1 | 多行文字用 textarea，不用 text | text、textarea | 找出要輸入多行的欄位，看打開的是 textarea |
| text-2 | text.1 | 只收數字的值用 number，不用 text | text、number | 找出 port、秒數之類的欄位，看打開的是 number |
| text-3 | text.1 | 不顯示出來的值（密碼、PIN、passphrase）用 password | text、password | 找出密碼類的欄位，看打開的是 password |

## input/password

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| password-1 | password.2 | 遮罩方案照用途挑：表單裡、一般的密碼框用一般；整個框只為這一個值的（螢幕解鎖、PIN、驗證碼）用解鎖 | password | 對照每個 password 的用途與方案 |
| password-2 | password.2 | 一般方案：每個字一個 `•`，靠左 | password | 打幾個字看 |
| password-3 | password.2 | 解鎖方案：每個字一顆 `●`，顆與顆之間空一格 | password | 打幾碼看 |
| password-4 | password.2 | 解鎖方案：整串置中，往兩側長 | password | 一碼一碼打，看點往兩側長 |
| password-5 | password.2 | 遮罩用值的顏色（Lavender） | password | 打幾個字看顏色 |
| password-6 | password.2 | 已經有密碼的 8 個灰點用同一個方案的字（一般 `•`、解鎖 `●`） | password | 打開有舊密碼的欄位 |
| password-7 | password.2 | 遮罩放不下框時照「值比框長時」，游標那一端看得到 | password | 打到比框長 |
| password-8 | password.2 | 解鎖的游標在下一顆 `●` 會出現的位置（最後一顆後面空一格） | password | 打 3 碼看游標 |
| password-9 | password.2 | 打滿最後一碼時，游標停在最後一顆上（Lavender 底、Base 的 `●`），不再多一格 | password | 打滿上限 |
| password-10 | password.2 | 置中連游標一起算：打了 n 碼（沒滿）是 2n + 1 格，打滿 N 碼是 2N − 1 格 | password | 量左右留白是否相等 |
| password-11 | password.2 | 解鎖方案沒有 `nf-fa-angle_right` | password | 看打字列前面 |
| password-12 | password.3 | 有舊密碼時框打開是空的，畫固定 8 個灰點，不照實際長度 | password | 打開舊密碼長度不是 8 的欄位 |
| password-13 | password.3 | 灰點從游標那一格開始：游標壓在第一顆上（Lavender 底、Base 的點），其他 7 顆 Overlay0 | password | 打開有舊密碼的欄位看第一顆 |
| password-14 | password.3 | 解鎖方案的 8 顆灰點間隔一格、整串置中（15 格） | password | 打開有舊 PIN 的框 |
| password-15 | password.3 | 什麼都沒打，`Enter` 或 `Esc` 都保留舊密碼 | password | 打開後直接 `Enter`，再用舊密碼驗證 |
| password-16 | password.3 | 直接打字：換成新密碼，灰點隱藏 | password | 有灰點時打一個字 |
| password-17 | password.3 | hint 不寫 `Tab` | password | 看下框 hint |
| password-18 | password.4 | 有打字時 `Backspace` 一次清掉打的全部，回到灰點（保留舊密碼） | password | 打幾個字後按一次 `Backspace` |
| password-19 | password.4 | 框是空的時 `Backspace` 清掉舊密碼，灰點消失 | password | 打開後直接按 `Backspace` |
| password-20 | password.4 | 灰點消失後 `Enter` 存成沒有密碼 | password | `Backspace` 後按 `Enter`，欄位變成空值 |
| password-21 | password.4 | hint 加 `Backspace:clear` | password | 看下框 hint |
| password-22 | password.4 | 字元一律接在尾端 | password | 打字時按 `←` 再打，字照樣接在最後 |
| password-23 | password.4 | `←\|→`、`Home\|End`、`Delete` 沒有作用 | password | 打字後按這幾個鍵 |
| password-24 | password.2 | 解鎖方案沒有說明列，要輸入什麼由標題講（例：`UNLOCK`、`CURRENT PIN`、`NEW PIN`、`CONFIRM PIN`） | password | 打開解鎖方案的框，看說明列與標題（沒有解鎖方案的 app 沒有這種情況） |
| password-25 | password.2（圖） | 解鎖方案的框裡是兩列空白、打字列、一列空白、錯誤列，連框 7 列 | password | 數解鎖方案的框的列數 |

## input/number

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| number-1 | number.1 | 範圍小、用點選比打字快的值用 slider，不用 number | number、slider | 找出範圍小的數值欄位，看用的是 slider |
| number-2 | number.2 | 說明列寫出範圍（例 `Port, 1-65535`） | number | 看說明列 |
| number-3 | number.3 | 打字只收數字，其他鍵按了沒反應 | number | 打字母、符號 |
| number-4 | number.3 | 欄位允許負數才收 `-` | number | 在不允許負數的欄位打 `-` |
| number-5 | number.3 | 欄位允許小數才收 `.` | number | 在整數欄位打 `.` |
| number-6 | number.3 | 貼上時只留下會收的字 | number | 貼上 `a1b2` |
| number-7 | number.3 | 不做 `↑\|↓` 加減 | number | 按 `↑`、`↓`，值不變 |
| number-8 | number.4 | 範圍錯了寫錯誤列，點名值（例 `Port must be 1-65535`） | number | 打範圍外的數按 `Enter` |
| number-9 | number.4 | 欄位可以空時，空的值不做範圍檢查，存成空的 | number | 清空一個可以空的數字欄位按 `Enter`（沒有可以空的數字欄位的 app 沒有這種情況） |
| number-10 | number.2 | 有單位時，打字列下面多一列單位列：寫完整的字（`seconds`，不寫 `s`）、Overlay0、跟值的第一格對齊、不跟著打的字移動 | number | 打開有單位的數字欄位，打幾個字看單位列（沒有單位的 app 沒有這種情況） |
| number-11 | number.2 | 有單位列時，寬度把單位列也算進最寬的那一列 | number | 量有單位的數字欄位的框寬 |

## input/select

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| select-1 | select.2 | finder 的骨架，沒有預覽 | select | 打開 select |
| select-2 | select.2 | 打字列一直顯示，短清單也是 | select | 打開選項很少的 select |
| select-3 | select.3 | 打開時 focus 在清單上 | select | 打開後看 hint 是清單的 hint |
| select-4 | select.3 | 打開時 cursor 停在目前的值 | select | 打開有值的欄位 |
| select-5 | select.3 | 清單的 hint 是 `Enter:choose Tab\|/:filter Esc:cancel` | select | 看下框 hint |

## input/radio

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| radio-1 | radio.1 | 選項五個以內的單選，直接畫在表單或 panel 上（radio） | radio、select | 找出五個以內的單選欄位 |
| radio-2 | radio.1 | 選項超過五個的單選用 select | radio、select | 找出超過五個的單選欄位 |
| radio-3 | radio.2 | 選中 `nf-md-radiobox_marked`（U+F043E）、沒選 `nf-md-radiobox_blank`（U+F043D） | radio | 看選項前面的 glyph |
| radio-4 | radio.2 | 選中那一個的字是 Green，其他是 Text | radio | 看選項的顏色 |
| radio-5 | radio.2 | 一律直排，一個選項一列 | radio | 看選項排法 |
| radio-6 | radio.2（圖） | 第二個以後的選項跟第一個選項同一欄起頭（glyph 上下對齊） | radio | 看選項的左緣 |
| radio-7 | radio.3 | 每個選項是一個項目，`j\|k`（或 `h\|l`）在選項之間移 | radio | 在選項上按 `j`、`k` |
| radio-8 | radio.3 | `Enter` 選它，focus 不動 | radio | 在沒選的選項上按 `Enter` |
| radio-9 | radio.3 | 選了馬上生效，不用另外確定 | radio | 按 `Enter` 後看效果 |

## input/checkbox

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| checkbox-1 | checkbox.1 | 開關與五個以內的一組，直接畫在表單或 panel 上，在原地翻 | checkbox | 找出開關與五個以內的多選欄位 |
| checkbox-2 | checkbox.1 | 超過五個的多選開 checkbox popup | checkbox | 找出超過五個的多選欄位 |
| checkbox-3 | checkbox.2 | 勾了 `nf-md-checkbox_marked`（U+F0132），沒勾 `nf-md-checkbox_blank_outline`（U+F0131）；表單、panel 上與 checkbox popup 的每一列都是 | checkbox | 看選項前面的 glyph |
| checkbox-4 | checkbox.2 | 勾了的字是 Green | checkbox | 看勾了的選項顏色 |
| checkbox-5 | checkbox.2 | 不可用的選項照樣畫在原位，不藏起來（不可用的選項不是停用） | checkbox | 看不可用的選項還在清單裡 |
| checkbox-6 | checkbox.2 | 不可用的選項整列 Surface2，勾也是（勾著也不是 Green）（不可用的選項不是停用） | checkbox | 看勾著與沒勾的不可用選項 |
| checkbox-7 | checkbox.2 | cursor 停在不可用的選項上時照 cursor 色塊畫，跟其他列一樣（不可用的選項不是停用） | checkbox | 移到不可用的選項上 |
| checkbox-8 | checkbox.2 | checkbox popup 是 finder 的骨架，沒有預覽 | checkbox | 打開 checkbox popup |
| checkbox-9 | checkbox.4 | 表單或 panel 上 `Enter` 在原地翻，focus 不動 | checkbox | 在 checkbox 上按 `Enter` |
| checkbox-10 | checkbox.4 | 表單或 panel 上翻了馬上生效 | checkbox | 翻了之後看效果 |
| checkbox-11 | checkbox.4 | checkbox popup 打開時 focus 在清單上 | checkbox | 打開後看 hint 是清單的 hint |
| checkbox-12 | checkbox.4 | 打開時 cursor 停在 app 指定的那一項，沒指定就是第一個選項（不是 `Select all`） | checkbox | 打開後看 cursor；或讀程式 |
| checkbox-13 | checkbox.4 | `Space` 只改畫面上的勾，不寫回、不生效 | checkbox | 按 `Space` 後看底下的畫面沒變 |
| checkbox-14 | checkbox.4 | `Enter` 把目前勾的整組一次寫回、popup 關掉，這時才生效 | checkbox | 勾兩項後按 `Enter` |
| checkbox-15 | checkbox.4 | 單獨打開的，`Enter` 時才套用 | checkbox | 按 `Enter` 前後看套用的對象 |
| checkbox-16 | checkbox.4 | `Esc` 取消：勾的都不算，值維持打開時的樣子 | checkbox | 改勾後按 `Esc`，再打開看 |
| checkbox-17 | checkbox.4 | 不可用的選項 cursor 照樣停（不可用的選項不是停用） | checkbox | 用 `j\|k` 走過不可用的選項 |
| checkbox-18 | checkbox.4 | 不可用的選項照樣能勾或取消（popup 的 `Space`、表單或 panel 上的 `Enter`）（不可用的選項不是停用） | checkbox | 在不可用的選項上翻 |
| checkbox-19 | checkbox.4 | popup 的 `Enter` 照畫面上的勾寫回，不可用的選項也一樣（不可用的選項不是停用） | checkbox | 勾不可用的選項後按 `Enter`，看值 |
| checkbox-20 | checkbox.4 | 篩選時不可用的選項照樣列在結果裡（不可用的選項不是停用） | checkbox | 打字篩選出不可用的選項 |
| checkbox-21 | checkbox.4 | 清單的 hint 是 `Enter:apply Space:toggle Tab\|/:filter Esc:cancel` | checkbox | 看下框 hint |
| checkbox-22 | checkbox.4 | 篩到沒有結果時，清單上的 `Enter` 照樣把勾好的整組寫回（被篩掉的勾也算） | checkbox | 勾兩項後打到沒有結果，到清單按 `Enter`，兩項都寫回 |
| checkbox-23 | checkbox.4 | 篩到沒有結果時，清單的 hint 拿掉 `Space`：`Enter:apply Tab\|/:filter Esc:cancel` | checkbox | 打到沒有結果後到清單看下框 |
| checkbox-24 | checkbox.4 | checkbox popup 什麼都沒改就按 `Enter`：不改，關掉 | checkbox | 打開 checkbox popup 不動就按 `Enter` |
| checkbox-25 | checkbox.4 | 一列一個值的 panel 上 focus 在 checkbox 時，hint 寫 `Enter:toggle`（panel 上的 `Space` 開 Space menu，不翻） | 一列一個值的 panel＋checkbox | 看 panel 的下框 hint |
| checkbox-26 | checkbox.3 | 一組選項（表單、panel 上與 checkbox popup 裡）第一列是 `Select all`，glyph 與顏色照選項畫，focus 與 cursor 能停；一個開關沒有 | checkbox | 看每一組的第一列，走上去 |
| checkbox-27 | checkbox.3 | `Select all` 不是選項：不算進值、不算在五個以內；app 沒有另外代表全部的選項 | checkbox | 全勾後寫回，看值裡沒有它；找有沒有「All」之類的選項 |
| checkbox-28 | checkbox.3 | 勾 `Select all` 每一個選項都勾上，取消就都取消，不可用的選項也算；生效的時機跟選項一樣（popup 裡 `Enter` 才寫回） | checkbox | 在 `Select all` 上翻兩次，看每一列 |
| checkbox-29 | checkbox.3 | `Select all` 只在每一個選項都勾著時勾著：取消一個它跟著取消，一個一個勾滿它跟著勾上，打開時全勾著它也勾著 | checkbox | 全勾後取消一列，再勾回來 |
| checkbox-30 | checkbox.3 | checkbox popup 的打字列有字時不畫 `Select all`，清掉才回來 | checkbox | 打一個字看第一列，再清掉 |
| checkbox-31 | checkbox.3 | 選項比 `Select all` 多縮兩格；篩選時它藏起來，選項照樣縮著、不位移 | checkbox | 看選項的左緣；打一個字看選項有沒有移動 |
| checkbox-32 | checkbox.3 | 停用的選項不跟著 `Select all` 改，也不算進「每一個都勾著」；每一個選項都停用時它也停用 | checkbox | 有停用的選項時翻 `Select all` |
| checkbox-33 | checkbox.3 | focus 與 cursor 不從 `Select all` 開始：表單打開時、popup 沒指定時、跳進那一欄時都停在選項上 | checkbox | 打開第一欄是 checkbox 組的表單、打開 checkbox popup，看停在哪裡 |

## input/slider

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| slider-1 | slider.1 | 要打精確數字的值用 number，不用 slider | number、slider | 找出要精確數字的欄位，看用的是 number |
| slider-2 | slider.2 | 表單與 panel 上畫一條軌道加數字 | slider | 看欄位 |
| slider-3 | slider.2 | 軌道用粗線 `━` | slider | 看軌道的字元 |
| slider-4 | slider.2 | 值的位置畫 `●`（在軌道上，值越大越右） | slider | 改值看 `●` 移動 |
| slider-5 | slider.2（圖） | 軌道後面空一格接數字 | slider | 看軌道與數字之間 |
| slider-6 | slider.3 | `Enter` 打開 select，選項是 bottom 到 top、每 step 一個的數字 | slider | 在 slider 上按 `Enter`，看清單的頭尾與間隔 |
| slider-7 | slider.3 | 沒有原地拉的鍵：`h\|l`、`←\|→` 不改值 | slider | 在 slider 上按 `h`、`l` |
| slider-8 | slider.4 | 每個 slider 都有 bottom、top、step 三個屬性 | slider | 讀程式 |
| slider-9 | slider.4 | step 沒設時是 `(top − bottom) / 10` | slider | 讀程式；或打開沒設 step 的 select 數項數 |

## input/textarea

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| textarea-1 | textarea.1 | 程式碼、設定檔這種「一行就是一行」的內容交給使用者的 `$EDITOR`，不用 textarea | textarea | 找出編輯這類內容的地方，看開的是 `$EDITOR` |
| textarea-2 | textarea.2 | 一行太長時自動折行，不左右捲 | textarea | 打一行比框寬的字 |
| textarea-3 | textarea.2 | 折行只在畫面上，值裡不多出換行 | textarea | 存了之後看值；或讀程式 |
| textarea-4 | textarea.2 | 折行的寬度照顯示寬度算（寬字一個字 2 格） | textarea | 打一行長的中文，看每一列都不超出框、框線不歪 |
| textarea-5 | textarea.2 | 每一行的第一列畫行號 | textarea | 打幾行看左邊 |
| textarea-6 | textarea.2 | 行號靠右對齊、後面空一格 | textarea | 打到第 10 行看對齊 |
| textarea-7 | textarea.2 | 折下來的列行號欄空白 | textarea | 看折行的第二列 |
| textarea-8 | textarea.2 | 行號 Overlay0，游標所在那一行的行號 Text | textarea | 移動游標看行號顏色 |
| textarea-9 | textarea.2 | 行號欄寬取 max(2, 最大行號的位數)：1–99 行不跳 | textarea | 打到第 10 行，內容不往右移 |
| textarea-10 | textarea.2 | 行數沒有上限 | textarea | 貼上很多行；或讀程式 |
| textarea-11 | textarea.2 | 框高取 Rules F7 的上限（畫面高度 − 2），舊值很短也一樣 | textarea | 打開舊值只有一行的欄位，量框高 |
| textarea-12 | textarea.2 | 內容超過框時在框裡捲，游標一直看得到 | textarea | 貼上比框高的內容，上下移動 |
| textarea-13 | textarea.2 | 「寫」的游標是一格 Lavender 底、Base 字 | textarea | 打開後看游標 |
| textarea-14 | textarea.2 | 「移」的游標是一格層色底、Base 字 | textarea | 按 `Esc` 後看游標 |
| textarea-15 | textarea.2 | 值的字都是 Lavender | textarea | 看內容顏色 |
| textarea-16 | textarea.2 | 兩種狀態的游標停在控制字元上時，整個控制字元畫成 Red 底、Base 字 | textarea | 貼上 `\x1b` 後在「寫」與「移」各移到它上面 |
| textarea-17 | textarea.2 | 值裡的 `\t` 畫成 `input_tab_width` 格空白，不對齊到 tab stop | textarea | 貼上含 `\t` 的字 |
| textarea-18 | textarea.3 | 打開時在「寫」 | textarea | 打開後直接打字 |
| textarea-19 | textarea.3 | 「寫」的 hint 是 `Esc:move` | textarea | 看下框 hint |
| textarea-20 | textarea.3 | 「移」裡 `i` 在游標前、`a` 在游標後開始寫，`o` 在下面開新的一行再寫（照 vim） | textarea | 在「移」裡各按一次 |
| textarea-21 | textarea.3 | 「移」的 hint 是 `Enter:save i:write Esc:cancel` | textarea | 看下框 hint |
| textarea-22 | textarea.3 | 打開時舊值直接帶進來，游標在最後 | textarea | 打開有舊值的欄位 |
| textarea-23 | textarea.3 | 「移」裡 `Esc` 關掉 | textarea | 沒改內容時在「移」裡按 `Esc` |
| textarea-24 | textarea.3 | 「寫」裡 `↑\|↓` 換到上一列、下一列（照畫出來的列，折行也算一列） | textarea | 在折行的那一行按 `↓` |
| textarea-25 | textarea.3 | 「寫」裡 `←\|→` 到行頭、行尾時跨到上一行、下一行 | textarea | 在行尾按 `→` |
| textarea-26 | textarea.3 | 行首的 `Backspace` 跟上一行合併 | textarea | 在第二行行首按 `Backspace` |
| textarea-27 | textarea.3 | 「寫」裡 `Home`、`End` 到整篇的開頭、結尾 | textarea | 在中間的行按 `Home`、`End` |
| textarea-28 | textarea.3 | 貼上的 `\n`、`\r\n`、單獨的 `\r` 都是真的換行 | textarea | 貼上三種換行的文字 |
| textarea-29 | textarea.3 | 貼上的其他控制字元留在值裡、畫成紅字 | textarea | 貼上帶顏色的終端機文字 |
| textarea-30 | textarea.3 | `Backspace` 一次刪一整個控制字元 | textarea | 在 `\x1b` 後面按一次 `Backspace` |
| textarea-31 | textarea.3 | 值裡有控制字元時，確定（「移」裡的 `Enter`）擋下、不存 | textarea | 貼上 `\x1b` 後在「移」裡按 `Enter` |
| textarea-32 | textarea.3 | 擋下時錯誤列點名值（例 `Notes can't have control characters`） | textarea | 看擋下時的錯誤列 |
| textarea-33 | textarea.3 | 換行與 `\t` 不算控制字元，不擋 | textarea | 貼上含 `\t` 的多行文字後確定，存得進去 |
| textarea-34 | textarea.3 | `Tab` 插入的空白 `Backspace` 一次刪一個 | textarea | 按 `Tab` 後按一次 `Backspace` |
| textarea-35 | textarea.3 | 貼上的 `\t` 照存，不換成空白 | textarea | 貼上含 `\t` 的字存了之後看值 |
| textarea-36 | textarea.3 | 「移」的移動照 Rules K12：`h\|j\|k\|l`、`w\|b\|e`、`0\|$`、`u\|d`、`gg\|G` | textarea | 在「移」裡逐一按 |

## input/color-picker

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| color-picker-1 | color-picker.2 | 一整列由左到右是 old、new、R、G、B | color picker | 打開 color picker |
| color-picker-2 | color-picker.2 | old、new 色塊 8 格寬、2 列高 | color picker | 量色塊 |
| color-picker-3 | color-picker.2 | old 是打開時的顏色，一直不變 | color picker | 改 R 之後看 old |
| color-picker-4 | color-picker.2 | new 跟著 R、G、B 即時變 | color picker | 改 R 之後看 new |
| color-picker-5 | color-picker.2 | old、new 下面寫 `old`、`new` 與各自的 hex | color picker | 看色塊下面兩列 |
| color-picker-6 | color-picker.2 | R、G、B 是小色塊（3 格寬、1 列高），不是 slider | color picker | 量色塊 |
| color-picker-7 | color-picker.2 | R、G、B 色塊畫那個色版自己的顏色（R 是 `#RR0000`） | color picker | 看三個小色塊的顏色 |
| color-picker-8 | color-picker.2 | R、G、B 下面寫它的值，一律用 hex | color picker | 看色版下面的值 |
| color-picker-9 | color-picker.2（圖） | R、G、B 的小色塊跟 old、new 色塊的第二列在同一列（下緣對齊） | color picker | 看小色塊在哪一列 |
| color-picker-10 | color-picker.2（圖） | 色塊下面是名稱一列、hex 一列，各自跟自己的色塊左緣對齊 | color picker | 看名稱與 hex 的左緣 |
| color-picker-11 | color-picker.2 | 動作區：內容下面一條分隔線，右邊一個按鈕 `Choose` | color picker | 看框的下半部 |
| color-picker-12 | color-picker.2（圖） | hex 那一列跟分隔線之間空一列 | color picker | 數 hex 列與分隔線之間的空列 |
| color-picker-13 | color-picker.2 | `Choose` 靠右，離框一格 | color picker | 看按鈕與右框的距離 |
| color-picker-14 | color-picker.3 | 可以 focus 的是 R、G、B 與 `Choose` 四個 | color picker | 按 `Tab` 與 hjkl 走一遍，focus 只停在這四個 |
| color-picker-15 | color-picker.3 | hjkl 只在 R、G、B 之間移：`h\|l` 左右，`j\|k` 也是前後 | color picker | 在 R、G、B 上按 `h`、`l`、`j`、`k` |
| color-picker-16 | color-picker.3 | `Choose` 只用 `Tab` 到：hjkl 不會移到 `Choose` | color picker | 在 B 上按 `l`，回到 R、不到 `Choose`；按 `Tab` 才到 `Choose` |
| color-picker-17 | color-picker.3 | 打開時 focus 在 R | color picker | 打開後看 |
| color-picker-18 | color-picker.3 | focus 在色版上時，下面的名稱與 hex 兩列照 cursor 畫（層色底、Base 粗體） | color picker | focus 在 G 上看 |
| color-picker-19 | color-picker.3 | 色版的 cursor 跟上面的色塊一樣寬（3 格 × 2 列） | color picker | 量 cursor 色塊 |
| color-picker-20 | color-picker.3 | R、G、B 上 `Enter` 打開數字的 select：00–FF、step 1、cursor 在目前的值 | color picker | 在 R 上按 `Enter` |
| color-picker-21 | color-picker.3 | 那個 select 的每一列寫 hex、括號附十進位（`2A (42)`） | color picker | 看清單的列 |
| color-picker-22 | color-picker.3 | 打 hex 或十進位都篩得到 | color picker | 打 `2A`，再打 `42` |
| color-picker-23 | color-picker.3 | 選完回來，new 跟著變 | color picker | 選一個值後看 new |
| color-picker-24 | color-picker.3 | 選完回來，focus 留在那個色版 | color picker | 選一個值後看 focus |
| color-picker-25 | color-picker.3 | `Choose` 上 `Enter`：確定，寫回去，關掉 | color picker | 在 `Choose` 上按 `Enter` |
| color-picker-26 | color-picker.3 | R、G、B 上的 hint 是 `Enter:edit Tab:actions Esc:cancel` | color picker | 看下框 hint |
| color-picker-27 | color-picker.3 | `Choose` 上的 hint 是 `Enter:choose Tab:fields Esc:cancel` | color picker | 看下框 hint |
| color-picker-28 | color-picker.2 | 原本沒有值時，old 不畫色塊，文字寫 `none`（Overlay0）；new 從 `#000000` 起 | color picker | 打開一個沒有設的顏色欄位（沒有可以不設的顏色的 app 沒有這種情況） |
| color-picker-29 | color-picker.3 | 原本沒有值時，`Choose` 一律算改了：new 是 `#000000` 也照樣寫回去 | color picker | 打開沒有設的顏色欄位，不動就按 `Choose`，看值變成 `#000000` |
| color-picker-30 | color-picker.4 | hex 一律寫大寫，不管檔案裡怎麼存：color picker 裡、表單與 panel 上都是 | color picker | 讓設定檔存小寫的 hex，看 color picker 與 panel 上的 hex |

## input/datetime-picker

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| datetime-picker-1 | datetime-picker.2（日期）（圖） | 月年一列在最上面，下面緊接星期一列，再緊接日曆，中間不空列 | datetime picker | 看內容的列序 |
| datetime-picker-2 | datetime-picker.2（日期）（圖） | 星期那一列 Overlay0 | datetime picker | 看星期的顏色 |
| datetime-picker-3 | datetime-picker.2（日期） | 日曆靠左、離框一格，前面不另外縮 | datetime picker | 看日曆左緣與框的距離 |
| datetime-picker-4 | datetime-picker.2（日期） | 每一天佔 4 格：日期 2 格靠右，加間距 2 格 | datetime picker | 看個位數與兩位數日期的對齊 |
| datetime-picker-5 | datetime-picker.2（日期） | 星期照同一個 4 格的格子 | datetime picker | 看星期與日期上下對齊 |
| datetime-picker-6 | datetime-picker.2（日期） | 日曆固定畫 6 列，用不到的列照樣留著 | datetime picker | 翻到只佔 4 或 5 週的月份，框高不變 |
| datetime-picker-7 | datetime-picker.2（日期） | cursor 停在哪一天，就是要寫回去的那一天（沒有「選了還沒確定」的狀態） | datetime picker | 移到一天後確定，寫回的就是那一天 |
| datetime-picker-8 | datetime-picker.2（日期） | 欄位原本的值字用 Green | datetime picker | 打開有值的欄位，移開 cursor 看原本那天 |
| datetime-picker-9 | datetime-picker.2（日期） | 打開時 cursor 停在原本的值；沒有值就停在今天 | datetime picker | 各打開有值與沒值的欄位 |
| datetime-picker-10 | datetime-picker.2（日期） | 今天加底線，不另外上色 | datetime picker | 看今天 |
| datetime-picker-11 | datetime-picker.2（日期） | 週末不另外上色 | datetime picker | 看週六、週日 |
| datetime-picker-12 | datetime-picker.2（日期） | 範圍外的日子用 Surface2 | datetime picker | 翻到範圍邊界的月份 |
| datetime-picker-13 | datetime-picker.2（日期加時間） | 日期加時間：右邊用一條直的分隔線切出時間塊 | datetime picker | 打開 datetime picker |
| datetime-picker-14 | datetime-picker.2（日期加時間） | 只選日期的沒有時間塊 | datetime picker | 打開 date picker |
| datetime-picker-15 | datetime-picker.2（日期加時間） | 分隔線左右各空兩格 | datetime picker | 數分隔線兩邊的空格 |
| datetime-picker-16 | datetime-picker.2（日期加時間） | 時間分成「時」與「分」兩欄 | datetime picker | 看時間塊 |
| datetime-picker-17 | datetime-picker.2（日期加時間） | 時是 00–23 | datetime picker | 在時那一欄走一圈 |
| datetime-picker-18 | datetime-picker.2（日期加時間） | 分每 5 分鐘一格（00–55） | datetime picker | 在分那一欄走一圈 |
| datetime-picker-19 | datetime-picker.2（日期加時間） | 時間塊沒有搜尋（不是 finder） | datetime picker | 在時間塊打數字，沒有篩選 |
| datetime-picker-20 | datetime-picker.2（日期加時間） | 時與分目前的值是 Green | datetime picker | 打開有值的欄位看 |
| datetime-picker-21 | datetime-picker.2（日期加時間）（圖） | 時間兩欄跟左邊一樣高（從月年那一列到日曆第 6 列），放不下的捲 | datetime picker | 看時間欄的頭尾列 |
| datetime-picker-22 | datetime-picker.2（日期加時間）（圖） | 時、分兩欄各自捲：打開時各自只捲最少的量讓目前的值看得到（例：10:05 是時 03–10、分 00–35），欄不畫成環（55 後面不接 00） | datetime picker | 打開值是 10:05 的欄位，看兩欄的第一列與最後一列 |
| datetime-picker-23 | datetime-picker.2（日期加時間） | 目前的值不在格子上時（10:07），打開時 cursor 停在它之前最近的那一格（10:05） | datetime picker | 打開值是 10:07 的欄位 |
| datetime-picker-24 | datetime-picker.2（日期加時間） | 有 focus 的那一塊 cursor 是層色底，沒有 focus 的那一塊 cursor 是層色 cursor 再淡化一次 | datetime picker | 在日曆與時間之間 `Tab`，看兩塊的 cursor |
| datetime-picker-25 | datetime-picker.2（日期加時間） | 時間塊裡沒有 focus 的那一欄 cursor 也再淡化一次（整個 picker 只有一個亮的 cursor） | datetime picker | 在時間塊按 `h`、`l`，看兩欄的 cursor |
| datetime-picker-26 | datetime-picker.3 | 可以拿 focus 的是月、年、日曆、時間（只選日期的沒有時間） | datetime picker | 按 `Tab` 走一圈 |
| datetime-picker-27 | datetime-picker.3 | picker 自己的操作只用 `Tab`、hjkl（方向鍵）、`Enter`、`Esc`、`t`，換月換年不另外設鍵（core key `?`、`q`／`Ctrl-C` 另照 input/README） | datetime picker | 按 `p`、`n` 等其他字母，沒有換月，也沒有其他作用 |
| datetime-picker-28 | datetime-picker.3 | `Tab` 照畫面順序換 focus：月 → 年 → 日曆 → 時間 → 回到月 | datetime picker | 從日曆一路按 `Tab` |
| datetime-picker-29 | datetime-picker.3 | 打開時 focus 在日曆 | datetime picker | 打開後看 hint |
| datetime-picker-30 | datetime-picker.3 | 月、年上 `h\|l`（`←\|→`）換上一個、下一個月或年 | datetime picker | 在月上按 `l` |
| datetime-picker-31 | datetime-picker.3 | 換月或年時日曆跟著翻，cursor 停在同一天；那個月沒有這一天就停在最後一天 | datetime picker | 在 31 號時換到 2 月 |
| datetime-picker-32 | datetime-picker.3 | 日曆上 `h\|l` 前後一天，`j\|k` 前後一週 | datetime picker | 在日曆按 `h`、`l`、`j`、`k` |
| datetime-picker-33 | datetime-picker.3 | 日曆上走過月底自然換月 | datetime picker | 在月底按 `l` |
| datetime-picker-34 | datetime-picker.3 | 範圍外的日子跳過，停在那個方向下一個範圍內的日子 | datetime picker | 往中間隔著範圍外日子的方向移 |
| datetime-picker-35 | datetime-picker.3 | 那個方向已經沒有範圍內的日子，就不動 | datetime picker | 在最晚那一天按 `l` |
| datetime-picker-36 | datetime-picker.3 | 時間上 `j\|k` 在一欄裡移，`h\|l` 在「時」與「分」之間換 | datetime picker | 在時間塊按 `j`、`l` |
| datetime-picker-37 | datetime-picker.3 | 各欄自己繞：分繞回不帶動時，時繞回不帶動日期 | datetime picker | 分在 55 按 `j`，看時；時在 23 按 `j`，看日期 |
| datetime-picker-38 | datetime-picker.3 | 月、年上 `Enter`：focus 移到日曆，不選 | datetime picker | 在月上按 `Enter` |
| datetime-picker-39 | datetime-picker.3 | 只選日期的，日曆上 `Enter` 確定（寫回去、關掉） | datetime picker | 在日曆上按 `Enter` |
| datetime-picker-40 | datetime-picker.3 | datetime 的日曆上 `Enter`：focus 移到時間 | datetime picker | 在日曆上按 `Enter` |
| datetime-picker-41 | datetime-picker.3 | 時間上 `Enter`：確定，寫回日曆 cursor 那一天加時間 cursor 那一格，關掉 | datetime picker | 在時間上按 `Enter`，看寫回的值 |
| datetime-picker-42 | datetime-picker.3 | `t`：日期跳到今天，每一塊都能用 | datetime picker | 在月、年、日曆上各按一次 `t` |
| datetime-picker-43 | datetime-picker.3 | 在時間上按 `t`，時間的 cursor 也跳到現在（分往前取最近的 5 分鐘） | datetime picker | 在時間上按 `t` |
| datetime-picker-44 | datetime-picker.3 | 日曆（datetime）上的 hint 是 `Enter:time t:today Tab:time Esc:cancel` | datetime picker | 看下框 hint |
| datetime-picker-45 | datetime-picker.3 | 日曆（只選日期）上的 hint 是 `Enter:choose t:today Tab:month Esc:cancel` | datetime picker | 看下框 hint |
| datetime-picker-46 | datetime-picker.3 | 月上的 hint 是 `Enter:days h\|l:month t:today Tab:year Esc:cancel` | datetime picker | 看下框 hint |
| datetime-picker-47 | datetime-picker.3 | 年上的 hint 是 `Enter:days h\|l:year t:today Tab:days Esc:cancel` | datetime picker | 看下框 hint |
| datetime-picker-48 | datetime-picker.3 | 時間上的 hint 是 `Enter:choose t:today Tab:month Esc:cancel` | datetime picker | 看下框 hint |

## input/finder

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| finder-1 | finder.2 | 上面是打字列，下面是清單 | finder | 打開 finder |
| finder-2 | finder.2 | 打字列與清單中間一條分隔線，不接框 | finder | 看分隔線兩端 |
| finder-3 | finder.2（圖） | 打字列、分隔線、清單緊接著，中間不空列 | finder | 看內容的列序 |
| finder-4 | finder.2 | 打字列最前面是 `nf-fa-angle_right`（U+F105），離框一格 | finder | 看打字列第一個字元 |
| finder-5 | finder.2 | glyph 的顏色：focus 在清單時 Overlay0，focus 在打字列時是該層的層色 | finder | 按 `Tab` 來回，看 glyph |
| finder-6 | finder.2 | 打字列右邊寫篩選的筆數 `符合/總數`（`3/41`） | finder | 打字篩選後看 |
| finder-7 | finder.2 | 筆數是 Overlay0 | finder | focus 在打字列時看筆數顏色 |
| finder-8 | finder.2（圖） | 筆數靠右，離框一格 | finder | 看筆數與右框的距離 |
| finder-9 | finder.2 | 一般的 finder 一定有預覽 | 有預覽的 finder | 打開一般的 finder |
| finder-10 | finder.2 | 預覽跟著 cursor 那一筆 | 有預覽的 finder | 移動 cursor，看預覽換 |
| finder-11 | finder.2 | 預覽的不是檔案或目錄時，沒有 metadata | 有預覽的 finder | 看預覽框 |
| finder-12 | finder.2 | 清單與預覽加起來是一個 popup 的寬（Rules F7 的上限） | 有預覽的 finder | 量兩框加起來的寬 |
| finder-13 | finder.2 | terminal 寬 ≥ 96：清單與預覽左右並排、各佔一半 | 有預覽的 finder | 在 96 欄以上打開 |
| finder-14 | finder.2 | terminal 寬 ≥ 96、有 metadata：右框是「預覽／分隔線／metadata」 | 有預覽的 finder | 在 96 欄以上打開 |
| finder-15 | finder.2（圖） | 右框裡預覽佔上面剩下的高度，分隔線與 metadata 四列在最下面 | 有預覽的 finder | 看右框的列序 |
| finder-16 | finder.2 | 不到 96、有 metadata：上面一列是清單框與 metadata 框，左右各一半 | 有預覽的 finder | 在 80 欄打開 |
| finder-17 | finder.2 | 不到 96、有 metadata：下面是整條寬的預覽框 | 有預覽的 finder | 在 80 欄打開 |
| finder-18 | finder.2 | 不到 96、有 metadata：上下各一半高 | 有預覽的 finder | 量上下兩排的高 |
| finder-19 | finder.2 | metadata 自己一個框時，標題是 `INFO` | 有預覽的 finder | 在 80 欄打開看標題 |
| finder-20 | finder.2（圖） | `INFO` 框的下框不寫字 | 有預覽的 finder | 在 80 欄打開看 `INFO` 的下框 |
| finder-21 | finder.2 | 80×24 時清單 5 筆、預覽 7 列 | 有預覽的 finder | 在 80×24 打開數列數 |
| finder-22 | finder.2 | 不到 96、沒有 metadata：上下疊，清單在上、預覽在下，各一半 | 有預覽的 finder | 在 80 欄打開 |
| finder-23 | finder.2（圖） | 並排的兩個框中間隔一格空白 | 有預覽的 finder | 看兩框之間 |
| finder-24 | finder.2（圖） | 並排時寬度分不平，右框多一格（96 寬：46 + 1 + 47；80 寬：38 + 1 + 39） | 有預覽的 finder | 量兩框的寬 |
| finder-25 | finder.2（圖） | 上下疊的兩排框中間不空列 | 有預覽的 finder | 在 80 欄打開看上下之間 |
| finder-26 | finder.2 | 預覽框的標題是選中那一筆的名字（或它在哪裡） | 有預覽的 finder | 看預覽框的標題 |
| finder-27 | finder.2 | 預覽不拿 focus | 有預覽的 finder | 按 `Tab` 來回，focus 不到預覽 |
| finder-28 | finder.2 | 預覽框的框線與標題膠囊用該層的層色 | 有預覽的 finder | 看預覽框的顏色 |
| finder-29 | finder.2 | 預覽內容不淡化 | 有預覽的 finder | focus 在打字列與清單時各看預覽內容 |
| finder-30 | finder.2 | 預覽框的下框不寫字（沒有 hint、沒有捲動位置） | 有預覽的 finder | 看預覽框的下框 |
| finder-31 | finder.2 | 邊找邊列：結果陸續到時照樣列出 | finder | 打開大的搜尋範圍 |
| finder-32 | finder.2 | 還在找時標題後面放 loading icon | finder | 搜尋中看標題 |
| finder-33 | finder.2 | 一筆都還沒到時寫 `(indexing…)` | finder | 剛打開時看清單 |
| finder-34 | finder.2 | 有預覽的 finder 高度一律取 Rules F7 的最高（畫面高度 − 2），清單短時下面空著 | 有預覽的 finder | 結果很少時量框高 |
| finder-35 | finder.3 | select 每一列前面放 radio glyph：選中 U+F043E、沒選 U+F043D | select | 看清單每一列前面 |
| finder-36 | finder.3 | 目前的值字是 Green | select、checkbox | 看目前的值那一列 |
| finder-37 | finder.3 | 所有列的字對齊 | select、checkbox | 看各列文字的左緣 |
| finder-38 | finder.3 | cursor 停在目前的值上時，底色照 cursor、字照 cursor 的 Base | select、checkbox | cursor 移到目前的值上 |
| finder-39 | finder.3 | checkbox popup 裡 Green 跟著畫面上的勾：`Space` 勾了就是 Green、取消就不是，還沒按 `Enter` 也一樣 | checkbox | 按 `Space` 後看字色 |
| finder-40 | finder.4 | focus 在打字列時，打字列照 input 的打字列畫：值 Lavender、有游標 | finder | focus 在打字列時看 |
| finder-41 | finder.4 | focus 在打字列時，清單的 cursor 是層色 cursor 再淡化一次 | finder | focus 在打字列時看清單 |
| finder-42 | finder.4 | focus 在清單時，打字列整列 Overlay0（含筆數），沒有游標 | finder | focus 在清單時看打字列 |
| finder-43 | finder.5 | 一般的 finder 打開時 focus 在打字列 | 有預覽的 finder | 打開一般的 finder 直接打字，字進到打字列 |
| finder-44 | finder.6 | 打字時清單即時篩選 | panel filter、finder | 打字看清單 |
| finder-45 | finder.6 | 打字列上 `↑\|↓` 在結果之間移 cursor | panel filter、finder | 在打字列按 `↓` |
| finder-46 | finder.7 | 比對不分大小寫 | panel filter、finder | 打 `READ` 找得到 `README` |
| finder-47 | finder.7 | 打的字要連續出現在那一項裡（只是依序含有那幾個字母不算） | panel filter、finder | 打 `prod`，`db-replica-tokyo-ap-northeast-1` 不在結果裡 |
| finder-48 | finder.7 | 用空白分開的每個詞都要出現，順序不拘 | panel filter、finder | 打 `me read` |
| finder-49 | finder.7 | 結果保持清單本來的順序，不重排 | panel filter、finder | 打字後看結果的順序跟清單一樣 |
| finder-50 | finder.7 | 清單的順序裡數字照數值排（`9` 在 `10` 前面），文字照文字排 | panel filter、finder | 看含數字的清單的順序（清單裡沒有數字時，這一條沒有可以判的情況） |
| finder-51 | finder.8 | 清單上 `Enter`：去那裡（select 選定、checkbox popup 套用、file-picker 選檔或進目錄） | finder | 在清單按 `Enter` |
| finder-52 | finder.8 | 沒有結果時（包括邊找邊列、一筆都還沒到時），清單上的 `Enter` 不作用（checkbox popup 例外） | select、finder、file-picker | 打到沒有結果，`Tab` 到清單按 `Enter`，什麼都沒發生 |
| finder-53 | finder.8 | 清單上 `Tab\|/`：回打字列 | finder | 在清單按 `Tab`、`/` |
| finder-54 | finder.8 | 回打字列時接著舊的字打（不清掉） | finder | 篩選後到清單，再按 `/` 打字 |
| finder-55 | finder.9 | 打字列的 hint 是 `Enter\|Tab:list Esc:cancel` | finder | focus 在打字列時看下框 |
| finder-56 | finder.9 | 清單的 hint 是 `Enter:<去那裡的動詞> Tab\|/:filter Esc:cancel` | finder | focus 在清單時看下框 |
| finder-57 | finder.9 | 沒有結果時（包括邊找邊列、一筆都還沒到時），打字列的 hint 拿掉 `Enter`：`Tab:list Esc:cancel`，有結果時再放回來 | select、checkbox、finder、file-picker | 打到沒有結果看下框，再刪字回到有結果看一次 |
| finder-58 | finder.9 | 沒有結果時，清單的 hint 拿掉 `Enter`：`Tab\|/:filter Esc:cancel` | select、finder、file-picker | 打到沒有結果後 `Tab` 到清單看下框 |
| finder-59 | finder.2 | 打字列的 `nf-fa-angle_right` 後面空一格才接打的字 | finder | 打幾個字，看 glyph 與字之間 |
| finder-60 | finder.2 | select、checkbox popup 的寬度照選項確定（打開時就知道）；邊找邊列、結果要等搜尋的才用 F7 的上限 | select、checkbox | 在很寬的終端機打開 select、checkbox popup，量框寬 |
| finder-61 | finder.7 | 搜尋要花時間時（讀每個檔、交給搜尋工具或遠端），照邊找邊列：標題後面放 loading icon、結果陸續列出、打字列照常能打 | finder | 在要花時間的搜尋裡連續打字，看打字不卡、結果陸續出來（搜尋都很快的 app 沒有這種情況） |
| finder-62 | finder.2 | 從某一行開始的預覽（例：用內容找到的檔，從找到的那一行看起）：那一行放在預覽的第三列、上面兩行前文、不另外標；行號照檔案 | 有預覽的 finder | 用內容找到一個檔，看預覽（沒有這種預覽的 app 沒有這種情況） |

## input/file-picker

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| file-picker-1 | file-picker.1 | 值是目錄的欄位用 file-picker 的「選目錄」 | file-picker | 找出值是目錄的欄位，看打開的是選目錄 |
| file-picker-2 | file-picker.2 | 一定有四塊：打字列、清單、預覽、metadata | file-picker | 打開 file-picker |
| file-picker-3 | file-picker.2 | 打開時清單顯示 app 給的根目錄 | file-picker | 打開後看標題與清單 |
| file-picker-4 | file-picker.2 | 根目錄只是起點：清單最上面一列是 `..`，可以往上走 | file-picker | 在 `..` 上按 `Enter` |
| file-picker-5 | file-picker.2 | 在 `/` 時沒有 `..` | file-picker | 走到 `/` 看清單 |
| file-picker-6 | file-picker.2 | 目前的目錄寫在標題：欄位名稱（大寫）後面接 ` · ` 再接目錄（`IDENTITY FILE · ~/.ssh`） | file-picker | 看標題 |
| file-picker-7 | file-picker.2 | 標題的路徑太長從前面截（`…/sideproj/terminu`） | file-picker | 走進很深的目錄看標題 |
| file-picker-8 | file-picker.2 | 打開時 focus 在清單上 | file-picker | 打開後看 hint 是清單的 hint（`Enter:… Tab\|/:filter Esc:cancel`） |
| file-picker-9 | file-picker.2 | 打字列打開時是空的 | file-picker | 打開有值的欄位看打字列 |
| file-picker-10 | file-picker.2 | 清單的順序：`..` → 目錄 → 檔案 | file-picker | 看清單 |
| file-picker-11 | file-picker.2 | 目錄、檔案各自照名字排，不分大小寫 | file-picker | 看大小寫混合的名字 |
| file-picker-12 | file-picker.2 | 隱藏檔（`.` 開頭）預設不列 | file-picker | 打開家目錄 |
| file-picker-13 | file-picker.2 | 篩選字（路徑的最後一段）是 `.` 開頭時才列隱藏檔（`.ss`、`~/.ss` 會出現 `.ssh`） | file-picker | 打 `.ss` |
| file-picker-14 | file-picker.2 | wildcard 的 `*` 不比對隱藏檔、`**` 不走進隱藏目錄，寫 `.` 開頭才會 | file-picker | 在家目錄打 `~/*` |
| file-picker-15 | file-picker.2 | 每一列前面放 icon：目錄 `nf-md-folder`（U+F024B）、檔案 `nf-md-file`（U+F0214） | file-picker | 看清單每一列前面；讀程式核對 code point |
| file-picker-16 | file-picker.2 | 欄位原本有值時，打開時 cursor 停在那個檔案上 | file-picker | 打開有值的欄位 |
| file-picker-17 | file-picker.2 | 欄位原本的值字用 Green | file-picker | 打開有值的欄位，移開 cursor 看 |
| file-picker-18 | file-picker.3 | 預覽最多讀 64 KB | 有檔案預覽 | 讀程式；或預覽大檔看尾端 |
| file-picker-19 | file-picker.3 | 目錄預覽成樹 | 有檔案預覽 | cursor 移到目錄上 |
| file-picker-20 | file-picker.3 | 壓縮檔（zip、tar、tar.gz、tar.bz2）照目錄的樹列出裡面 | 有檔案預覽 | cursor 移到壓縮檔上 |
| file-picker-21 | file-picker.3 | 文字檔畫內容，加語法顏色（chroma 的 catppuccin-mocha，只上前景色） | 有檔案預覽 | cursor 移到原始碼檔上 |
| file-picker-22 | file-picker.3 | 文字檔有行號：Overlay0，靠右對齊、後面空一格 | 有檔案預覽 | 看文字檔預覽的左邊 |
| file-picker-23 | file-picker.3 | 文字檔的 Tab 畫成 `input_tab_width` 格空白 | 有檔案預覽 | 預覽含 Tab 的檔 |
| file-picker-24 | file-picker.3 | 文字檔裡 CRLF 的 `\r` 不畫 | 有檔案預覽 | 預覽 CRLF 換行的檔 |
| file-picker-25 | file-picker.3 | 文字檔裡其他控制字元畫成 Red 的名字 | 有檔案預覽 | 預覽含 `\x1b` 的檔 |
| file-picker-26 | file-picker.3 | PDF：第一列灰字寫頁數（`12 pages`），空一列，接前 20 頁的文字（最多 128 KB） | 有檔案預覽 | 預覽 PDF |
| file-picker-27 | file-picker.3 | PDF 抽不出文字時寫 `(no extractable text)` | 有檔案預覽 | 預覽掃描的 PDF |
| file-picker-28 | file-picker.3 | 圖片（png、jpg、gif、bmp、webp、tiff、ico、avif、heic）：第一列灰字 `data:image/png · 12.4 KB`，空一列，接 base64 的 data URI，照預覽寬折行 | 有檔案預覽 | 預覽小圖片 |
| file-picker-29 | file-picker.3 | 圖片超過 1 MB 時只寫 `(1.4 MB — too large to inline as a data URI)` | 有檔案預覽 | 預覽超過 1 MB 的圖片 |
| file-picker-30 | file-picker.3 | 其他檔案畫十六進位：一律一列 8 bytes，後面接 ASCII（`89 50 4e 47 0d 0a 1a 0a  .PNG....`，33 格） | 有檔案預覽 | 預覽二進位檔，並排與上下疊各看一次 |
| file-picker-31 | file-picker.3 | 讀不到寫 `(unreadable)` | 有檔案預覽 | 預覽沒有讀權限的檔 |
| file-picker-32 | file-picker.3 | 目錄的樹最多三層 | 有檔案預覽 | 預覽很深的目錄 |
| file-picker-33 | file-picker.3 | 樹的第一層不畫樹枝，第二層起用 `├─`、`└─`、`│` 連起來 | 有檔案預覽 | 看樹 |
| file-picker-34 | file-picker.3 | 樹枝 Overlay0 | 有檔案預覽 | 看樹枝的顏色 |
| file-picker-35 | file-picker.3（圖） | 第二層的樹枝從第一層名字那一欄開始（縮 2 格），每深一層再縮 3 格（`│  ` 或 3 格空白） | 有檔案預覽 | 看三層的樹 |
| file-picker-36 | file-picker.3（圖） | 樹枝後面空一格接 icon | 有檔案預覽 | 看樹枝與 icon 之間 |
| file-picker-37 | file-picker.3 | 樹的每一項 icon、顏色、順序跟清單一樣 | 有檔案預覽 | 對照樹與走進去後的清單 |
| file-picker-38 | file-picker.3 | 樹不列隱藏檔 | 有檔案預覽 | 預覽含隱藏檔的目錄 |
| file-picker-39 | file-picker.3 | 樹不能捲，畫到預覽區滿為止，最後一列寫 `…` | 有檔案預覽 | 預覽很大的目錄 |
| file-picker-40 | file-picker.3 | 空的目錄寫 `(empty)`，灰字 | 有檔案預覽 | 預覽空目錄 |
| file-picker-41 | file-picker.3 | 讀不到的目錄寫 `(permission denied)`，灰字 | 有檔案預覽 | 預覽沒有讀權限的目錄 |
| file-picker-42 | file-picker.3 | 一個子目錄展開到底才輪到下一個 | 有檔案預覽 | 預覽有好幾個子目錄的目錄 |
| file-picker-43 | file-picker.4 | 固定四列（`TYPE`、`SIZE`、`MODIFIED`、`MODE`），檔案與目錄都一樣 | 有檔案預覽 | 在檔案與目錄之間移動，預覽區高度不跳 |
| file-picker-44 | file-picker.4 | label 大寫、層色 | 有檔案預覽 | 看 label |
| file-picker-45 | file-picker.4 | 值是 Text | 有檔案預覽 | 看值的顏色 |
| file-picker-46 | file-picker.4 | label 欄寬取最長的 label，跟值隔兩格 | 有檔案預覽 | 看值的左緣 |
| file-picker-47 | file-picker.4 | 檔案的 `TYPE` 寫預覽的種類：`text`、`private key`、`image`、`PDF`、`archive`、`binary` | 有檔案預覽 | 各種檔各看一次 |
| file-picker-48 | file-picker.4 | symlink 的 `TYPE` 寫 `link → <目標>` | 有檔案預覽 | cursor 移到 symlink 上 |
| file-picker-49 | file-picker.4 | 目錄的 `TYPE` 寫 `directory` | 有檔案預覽 | cursor 移到目錄上 |
| file-picker-50 | file-picker.4 | 檔案的 `SIZE` 寫 `411 B`、`4.2 KB`、`3.4 MB`（1024 進位，一位小數） | 有檔案預覽 | 看幾個大小不同的檔 |
| file-picker-51 | file-picker.4 | 目錄的 `SIZE` 寫 `12 items`，一項時 `1 item`（不算隱藏檔） | 有檔案預覽 | 看含隱藏檔的目錄與只有一項的目錄 |
| file-picker-52 | file-picker.4 | `MODIFIED` 寫 `2026-09-30 14:02`（本地時間，到分） | 有檔案預覽 | 對照 `ls -l` |
| file-picker-53 | file-picker.4 | `MODE` 照 `ls -l` 的寫法（`-rw-------`、`drwx------`） | 有檔案預覽 | 對照 `ls -l` |
| file-picker-54 | file-picker.4 | 第一行是私鑰標頭的檔案 `TYPE` 是 `private key`，跟 `hide_secrets_in_preview` 開不開無關 | 有檔案預覽 | 開關設定各看一次私鑰 |
| file-picker-55 | file-picker.4 | symlink 的 `SIZE`、`MODIFIED`、`MODE` 寫目標的 | 有檔案預覽 | 看 `/etc/localtime` 之類的 link |
| file-picker-56 | file-picker.4 | 讀不到的目錄 `SIZE` 寫 `—`，修改時間、權限照樣寫 | 有檔案預覽 | 看沒有讀權限的目錄 |
| file-picker-57 | file-picker.4 | 斷掉的 link 的 `SIZE`、`MODIFIED`、`MODE` 寫 `—` | 有檔案預覽 | 看斷掉的 link |
| file-picker-58 | file-picker.4 | 拿不到值時四列照樣固定，不少畫一列，也不寫成 `0 items` | 有檔案預覽 | 看斷掉的 link 與讀不到的目錄 |
| file-picker-59 | file-picker.4 | 不寫路徑、擁有者、存取與建立時間 | 有檔案預覽 | 看 metadata 只有四列 |
| file-picker-60 | file-picker.5 | 打開時，第一行是私鑰標頭（開頭 `-----BEGIN` 且含 `PRIVATE KEY`，或開頭 `PuTTY-User-Key-File-`）的檔只露第一行，下面灰字 `(sensitive content not shown)` | 有檔案預覽 | 打開設定，預覽改過檔名的私鑰 |
| file-picker-61 | file-picker.5 | 打開時，只有擁有者能讀的檔案（group、other 都沒有讀權限）一行都不露，只有那句灰字，什麼種類都一樣 | 有檔案預覽 | 打開設定，預覽 `600` 的文字檔 |
| file-picker-62 | file-picker.5 | 目錄不算（`700` 的目錄照常預覽） | 有檔案預覽 | 打開設定，預覽 `~/.ssh` |
| file-picker-63 | file-picker.5 | 其他檔案照常預覽 | 有檔案預覽 | 打開設定，預覽 `644` 的文字檔 |
| file-picker-64 | file-picker.5 | metadata 不管開關都照常顯示 | 有檔案預覽 | 打開設定，看私鑰的 metadata |
| file-picker-65 | file-picker.6 | 清單上在目錄按 `Enter`：進去 | file-picker | 在目錄上按 `Enter` |
| file-picker-66 | file-picker.6 | 進目錄時打的篩選字清掉 | file-picker | 篩選後在目錄上按 `Enter` |
| file-picker-67 | file-picker.6 | 進目錄後 focus 留在清單，cursor 停在 `..` 下面的第一項 | file-picker | 進目錄後看 cursor |
| file-picker-68 | file-picker.6 | 在檔案上 `Enter`：選中，寫回去、關掉 | file-picker | 在檔案上按 `Enter` |
| file-picker-69 | file-picker.6 | 選檔時目錄永遠不會被選中 | file-picker | 試著用任何方式選目錄 |
| file-picker-70 | file-picker.6 | 打字列打一般的字：照 finder 的「比對」篩選目前這一層 | file-picker | 打 `ed25` |
| file-picker-71 | file-picker.6 | 打路徑（`/` 或 `~/` 開頭）時，路徑一直留在打字列上 | file-picker | 打 `~/.ssh/` 後看打字列 |
| file-picker-72 | file-picker.6 | 路徑以最後一個 `/` 切開：前面是目錄（清單列出它、標題寫它），後面是篩選字 | file-picker | 打 `~/.ssh/id_` |
| file-picker-73 | file-picker.6 | 路徑打到一半也有用，打字與貼上的結果一樣 | file-picker | 一個字一個字打，與貼上同一串比較 |
| file-picker-74 | file-picker.6 | 路徑的目錄不存在時清單是空的，跟「沒有結果」一樣 | file-picker | 打 `~/nope/x` |
| file-picker-75 | file-picker.6 | 路徑裡有 `..` 這一段時不往上解析，清單是空的 | file-picker | 打 `~/../x` |
| file-picker-76 | file-picker.6 | 有 `*`、`?` 時是 wildcard：`*` 只比對同一層，`**` 往下找所有子目錄 | file-picker | 打 `~/Downloads/*.png`、`~/.ssh/**/*.pem` |
| file-picker-77 | file-picker.6 | wildcard 的結果每一列寫相對於起點的路徑（起點是第一個 `*`、`?` 前面的目錄） | file-picker | 打 `**` 的路徑看結果 |
| file-picker-78 | file-picker.6 | wildcard 時標題寫起點 | file-picker | 打 wildcard 後看標題 |
| file-picker-79 | file-picker.6 | wildcard 的結果沒有 `..` | file-picker | 打 wildcard 後看清單第一列 |
| file-picker-80 | file-picker.6 | 清單上在目錄的 hint 是 `Enter:into Tab\|/:filter Esc:cancel` | file-picker | cursor 在目錄上看下框 |
| file-picker-81 | file-picker.6 | 清單上在檔案的 hint 是 `Enter:choose Tab\|/:filter Esc:cancel` | file-picker | cursor 在檔案上看下框 |
| file-picker-82 | file-picker.7 | 清單只列目錄，檔案不列 | file-picker | 打開選目錄 |
| file-picker-83 | file-picker.7 | 順序是 `.` → `..` → 目錄 | file-picker | 看清單 |
| file-picker-84 | file-picker.7 | 最上面一列是 `.`，寫成 `. (this directory)` | file-picker | 看清單第一列 |
| file-picker-85 | file-picker.7 | `.` 的 icon 是 `nf-md-folder_move`（U+F0252） | file-picker | 看 `.` 前面的 icon |
| file-picker-86 | file-picker.7 | 在 `.` 上 `Enter`：選目前這個目錄，寫回去、關掉 | file-picker | 在 `.` 上按 `Enter` |
| file-picker-87 | file-picker.7 | 在其他目錄上 `Enter`：走進去 | file-picker | 在目錄上按 `Enter` |
| file-picker-88 | file-picker.7 | 打字列上有篩選字或 wildcard 時，`.` 那一列不出現 | file-picker | 打篩選字後看清單 |
| file-picker-89 | file-picker.7 | wildcard 的結果只列目錄 | file-picker | 打 `~/*` |
| file-picker-90 | file-picker.7 | 在 `.` 上的 hint 是 `Enter:choose Tab\|/:filter Esc:cancel` | file-picker | cursor 在 `.` 上看下框 |
| file-picker-91 | file-picker.4 | 列出之後才不見的檔（被刪掉、搬走），拿不到的每一列寫 `—` | 有檔案預覽 | 列出後在別的地方刪掉一個檔，cursor 移過去看 metadata |
| file-picker-92 | file-picker.3 | 預覽與 metadata 在背景讀：打字、移動 cursor 不等它；讀取中預覽框標題後面放 loading icon、框裡灰字 `(loading…)`、metadata 的值先空著；讀過的照路徑記住，不重讀 | 有檔案預覽 | 在慢的（例：遠端）檔案系統上快速移動 cursor，看打字不卡、讀取中的樣子；讀程式：不在畫的時候讀檔 |
| file-picker-93 | file-picker.3 | 文字檔裡的顏色碼照著上色，一行裡的 `\r` 只留最後的狀態 | 有檔案預覽 | 預覽含顏色碼與 `10%\r100%` 的檔 |

## input/reorder

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| reorder-1 | reorder.1 | 沒有打字列、沒有搜尋 | reorder | 打開 reorder |
| reorder-2 | reorder.2 | 每一列：列首一格放 glyph，空一格，再寫項目 | reorder | 看每一列的開頭 |
| reorder-3 | reorder.2 | 項目是 Text | reorder | 看沒有 cursor 的列 |
| reorder-4 | reorder.2 | 只有拿著的那一項畫 glyph，其他列那一格留空白 | reorder | 按 `D` 前後看列首 |
| reorder-5 | reorder.2 | glyph 那一格一直保留，拿起、放下時字不位移 | reorder | 按 `D`、`Enter`，看字的位置不動 |
| reorder-6 | reorder.2 | 拿著的那一項 Yellow 底、Base 粗體，箭頭也是 Yellow | reorder | 按 `D` 後看 |
| reorder-7 | reorder.2 | 拿著的那一項列首畫 `nf-md-swap_vertical`（U+F04E2） | reorder | 按 `D` 後看列首 |
| reorder-8 | reorder.3 | 打開時 focus 在清單上，沒拿東西 | reorder | 打開後看 hint |
| reorder-9 | reorder.3 | `D` 拿起 cursor 那一項，進入 Drag mode | reorder | 按 `D` |
| reorder-10 | reorder.3 | 沒拿東西時 `Enter`：把整個順序寫回去、popup 關掉，這時才生效 | reorder | 搬過後按 `Enter` |
| reorder-11 | reorder.3 | 沒拿東西時 `Esc`：順序沒改過，直接關 | reorder | 打開後直接按 `Esc` |
| reorder-12 | reorder.3 | 放棄的 confirm 上 `Enter`：放棄、popup 關掉 | reorder | 在 confirm 上按 `Enter` |
| reorder-13 | reorder.3 | 放棄的 confirm 上 `Esc`：關掉 confirm、回到清單，順序還在 | reorder | 在 confirm 上按 `Esc` |
| reorder-14 | reorder.3 | 「改過了」：放下的位置跟拿起前不同就算，之後不清掉（搬走又搬回原位也算） | reorder | 搬走再搬回原位後按 `Esc`，照樣先問 |
| reorder-15 | reorder.3 | 沒拿東西時 hint 是 `Enter:apply D:drag Esc:cancel` | reorder | 看下框 hint |
| reorder-16 | reorder.3 | 拿著時 `j\|l` 把它跟下一項交換、`h\|k` 跟上一項交換，cursor 跟著它 | reorder | 拿著按 `k`、`l` |
| reorder-17 | reorder.3 | 拿著時 `Enter`：放下，離開 Drag mode，cursor 留在那一項 | reorder | 拿著按 `Enter` |
| reorder-18 | reorder.3 | 拿著時 `Esc`：放回拿起前的位置，離開 Drag mode（不關 popup） | reorder | 拿著搬兩格後按 `Esc` |
| reorder-19 | reorder.3 | 拿著時 `Space` 打開 Drag mode 的 Space menu，其他鍵不作用，`D` 不是放下的別名 | reorder | 拿著按 `Space`、`D` |
| reorder-20 | reorder.3 | 拿著時 hint 是 `Enter:drop Esc:cancel` | reorder | 拿著看下框 hint |

## project

| 編號 | 出處 | 檢查什麼 | 適用 | 怎麼驗 |
|---|---|---|---|---|
| project-1 | project.2 | `family.mk` 照範本原樣複製到 `family.mk`，不改 | 都要 | 讀檔案：跟 app 跟的那一版 tdp 的 `project/family.mk` diff，沒有差 |
| project-2 | project.2 | `release.yml` 照範本複製到 `.github/workflows/release.yml`，只有出 Windows 版時在測試的 matrix 加 `windows-latest` | 都要 | 讀檔案：跟同一版範本 diff，只差 matrix 的 `windows-latest`（出 Windows 版時） |
| project-3 | project.2 | `goreleaser.yaml` 照範本複製到 `.goreleaser.yaml`，只改 `<app>`、標著 `app:` 的幾行、出 Windows 版時打開標著 `Windows` 的註解 | 都要 | 讀檔案：把 app 名換回 `<app>` 跟同一版範本 diff，只差這些地方 |
| project-4 | project.2 | `install.sh` 照範本複製，只改 `<app>`、`WINDOWS`、標著 `app's own` 的段落 | 都要 | 讀檔案：把 app 名換回 `<app>` 跟同一版範本 diff，只差這些地方 |
| project-5 | project.2 | `uninstall.sh` 照範本複製，只改 `<app>`、標著 `app's own` 的段落 | 都要 | 讀檔案：把 app 名換回 `<app>` 跟同一版範本 diff，只差這些地方 |
| project-6 | project.2 | `version.go` 照範本複製到 `internal/version/version.go`，只改 `<app>` | 都要 | 讀檔案：把 app 名換回 `<app>` 跟同一版範本 diff，沒有其他差 |
| project-7 | project.2 | `gitignore` 照範本複製到 `.gitignore`，只改 `<app>`，app 自己的行接在最後 | 都要 | 讀檔案：把 app 名換回 `<app>` 跟同一版範本 diff，只差最後加的行 |
| project-8 | project.2 | 出 Windows 版時，`release.yml` 測試的 matrix 加了 `windows-latest` | 出 Windows 版 | 讀檔案：`.github/workflows/release.yml` 的 matrix |
| project-9 | project.2 | 出 Windows 版時，`.goreleaser.yaml` 標著 `Windows` 的註解都打開 | 出 Windows 版 | 讀檔案：`.goreleaser.yaml` |
| project-10 | project.2 | 出 Windows 版時，`install.sh` 的 `WINDOWS` 設成 `yes`（範本註解） | 出 Windows 版 | 讀檔案：`install.sh` 的 `WINDOWS` |
| project-11 | project.3 | app 本身的 Go 程式只在 `cmd/<app>/` 與 `internal/`；開發用的小工具可以放頂層的 `tools/` | 都要 | 讀檔案：`tools/` 以外的 `.go` 檔都在這兩個目錄底下 |
| project-12 | project.3（圖） | main package 在 `cmd/<app>/main.go` | 都要 | 讀檔案 |
| project-13 | project.3 | `go install github.com/<帳號>/<app>/cmd/<app>@latest` 裝得起來（家族成員的帳號是 `vulcanshen`，照 tdp 做的 app 是自己的帳號） | 都要 | 讀檔案：`go.mod` 的 module 是 `github.com/<帳號>/<app>`，`cmd/<app>` 是 main package |
| project-14 | project.3（圖） | README 的 demo gif 放在 `docs/` | 都要 | 讀檔案：README 引用的 gif 在 `docs/` 底下 |
| project-15 | project.3（圖） | 根目錄有 `go.mod`、`go.sum` | 都要 | 讀檔案 |
| project-16 | project.3（圖） | 根目錄有 `LICENSE` | 都要 | 讀檔案 |
| project-18 | project.3 | 家族 mark 的正本是 `docs/icon.svg`；splash 用的那一份在程式裡（`internal/` 裡的副本檔，或寫死的格子） | 都要 | 讀檔案：有 `docs/icon.svg`；讀程式：splash 畫的是 `internal/` 裡的副本檔或寫死的格子 |
| project-19 | project.3 | 出 Windows 版的 app 另有 `install.ps1`、`uninstall.ps1` | 出 Windows 版 | 讀檔案 |
| project-20 | project.4 | `<app> version` 與 splash 的版本印的是 `internal/version` 的 `Display()` | 都要 | 讀程式：兩處都呼叫 `Display()` |
| project-21 | project.4 | 發布版的版本是 tag 去掉 v 注入的，印出來帶 v（例：tag `v0.2.0` 印 `v0.2.0`） | 都要 | 讀檔案：`.goreleaser.yaml` 把 tag 去掉 v 注入、`internal/version` 印出時帶 v；發過版的，裝發布版跑 `<app> version`，印的跟 tag 一樣 |
| project-22 | project.4 | 本機 `make build`、`go build` 不注入版本，版本是 `dev` | 都要 | 本機 `make build` 後跑 `./<app> version`，印 `dev` |
| project-23 | project.5 | `Makefile` 只設變數、`include family.mk`，app 自己的 target 全寫在最後一段 `##@ <app> 自己的` | 都要 | 讀檔案；跑 `make help`，家族共用的段照 family.mk 的順序、app 自己的段在最後 |
| project-24 | project.5 | 變數在 `include family.mk` 之前設 | 都要 | 讀檔案 |
| project-25 | project.5 | `BINARY` 設成 app 的名字，也是 `cmd/` 底下那個目錄的名字 | 都要 | 讀檔案 |
| project-26 | project.5 | Makefile 開頭的兩行註解照範本（`<app> — build / run / test / package（家族共用的 target 在 family.mk）`、「跑 make（或 make help）列出所有指令。」） | 都要 | 讀檔案的開頭 |
| project-27 | project.5 | app 自己的 target 名字不跟 family.mk 的重複 | 都要 | 讀檔案：比對兩邊的 target 名 |
| project-28 | project.6 | `CHANGELOG.md` 開頭照範本：`# Changelog`，接著 `Each release names the version of terminu design (tdp) it follows.` | 都要 | 讀檔案的開頭 |
| project-29 | project.6 | 每一版的標題是 push 的 tag（帶 v）接 ` — tdp <版本>` | 發過版 | 讀檔案：tdp v0.7.0 之後發的每一版標題 |
| project-30 | project.6 | 還沒發版的改動寫在最上面的 `## Unreleased` | 都要 | 讀檔案與最新 tag 之後的 commit：改動都記在最上面的 `## Unreleased` |
| project-31 | project.6 | tdp v0.7.0 以前發的版本，標題照當時的寫法、不改 | 發過版 | 讀檔案：`git log -p CHANGELOG.md`，舊版的標題沒被改寫 |
| project-32 | project.6 | CHANGELOG 用英文寫 | 都要 | 讀檔案 |
| project-33 | project.6 | GitHub release 的內文就是 CHANGELOG 裡這一版的那一段 | 發過版 | `gh release view <tag>` 對照 CHANGELOG 那一段 |
| project-34 | project.7 | 發版的 tag 是 `vX.Y.Z` | 發過版 | `git tag` |
| project-35 | project.7 | 現在的 repo 上 `make check` 通過 | 都要 | 在現在的 repo 跑 `make check` |
| project-36 | project.7 | 出 Windows 版的發布時另推 scoop bucket | 出 Windows 版 | 看 scoop bucket 有這一版 |

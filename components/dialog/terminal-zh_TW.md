# terminal（框裡跑子程序）

**Language**: [English](terminal.md) · 繁體中文

## terminal.1 用途

框裡跑的子程序（shell、編輯器、遠端 session）：按鍵都給它，只有出口鍵、app 保留的組合鍵，以及互動 terminal 的 `Alt-v`、`PgUp`（見下面的「哪些 PTY 有這兩種模式」）屬於 app（Rules F1、K10）。PTY 放在
panel 裡時（例：sshu 的格子）不是 popup：框照 [`layout/panel`](../layout/panel-zh_TW.md)，PTY 的鍵寫在 footer（[`layout/screen`](../layout/screen-zh_TW.md)）。

## terminal.2 長相

```
[M]ANAGE[F]ILE TRANSFER[S]SH        2 live sessions    ← statusbar／畫面 chip 列：留著
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   ← chip 列下面的分隔線：留著（傳檔時是進度條）
┏━󰆍 ALTERM: myhost━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃$ kubectl get pods                                      ┃   ← PTY 貼著框，上下左右都不留白
┃NAME          READY   STATUS    RESTARTS   AGE          ┃
┃nginx-7d4f    1/1     Running   0          3d           ┃
┃$ █                                                     ┃
┗━ Alt-Esc:exit Alt-t:hide Alt-v:select PgUp:history ━━━━┛   ← 一直到畫面最後一列；footer 不畫
```

- **大小**（Rules F7 的 terminal 例外）：寬度 `terminal 寬 − 2`，不受 120 欄上限。上面留著 statusbar 或畫面 chip 列（含 chip 列下面的
  分隔線）；下面一直到畫面最後一列。沒有 statusbar 的 app，從第一列開始。
- **footer 不畫**：terminal popup 開著時 footer 整列不畫。框左右各空一欄，最後一列的兩端是空白，不露出 footer 的字。
- **不留白**：子程序需要每一列、每一欄，內容從框裡第一列畫到最後一列、第一欄畫到最後一欄，上下左右都貼著框。這是 terminal
  這種 popup 的特殊情況（[`layout/popup`](../layout/popup-zh_TW.md) 的留白）。PTY 放在 panel 裡時也一樣不留白：panel 的框照畫，
  PTY 貼著框（[`layout/panel`](../layout/panel-zh_TW.md) 的留白不適用）。
- **標題**：`nf-md-console`（U+F018D）加上跑的是什麼（`SHELL`、`ALTERM: myhost`、`EDIT: pod/x`；名稱與路徑照原樣）。
- **子程序的游標**：真的游標藏起來，在子程序的游標位置畫一格 Text 底、Base 字的反白方塊；子程序用 DECSCUSR 要求的形狀（底線、
  直線）不理。PTY 放在 panel 裡時也一樣。這是終端機預設的游標；家族的游標顏色各有意思（Lavender 是正在編輯的值、層色是在文字
  裡移動的游標），PTY 裡是子程序自己的畫面，兩個都不對；直線在一格一格畫的畫面上畫不出來，會蓋掉那個字。

**為什麼**：statusbar 上有正在進行的狀態（kbu 的 context、sshu 的傳檔進度），在 shell 裡工作時照樣會想瞄一眼。footer 不需要：
focus 在 PTY 裡時，footer 上的 `Space`、`?`、`q` 都送給子程序，照常顯示反而誤導；PTY 的鍵只出現在一個地方，就是這個框的下框，
不會有兩列 hint。

## terminal.3 按鍵

- 按鍵都送給子程序（Rules K10）。
- **hint**：出口鍵永遠是第一個，放不下時最後才捨。動詞寫按下去真正會發生的事：
  - `Alt-Esc:exit`：結束子程序。
  - `Alt-Esc:leave`：離開，子程序還留著。
  - 不寫 `close`。
- 出口鍵後面跟 app 保留的組合鍵（例：`Alt-t:hide`），互動 terminal 再接 `Alt-v:select`、`PgUp:history`（見下面）。
- `Alt-Esc` 一律先 confirm（Rules K10）。
- `Home`、`End` 屬於子程序（Rules K10）；要到歷史的頭尾，用歷史模式的 `gg|G`（見下面）。

## terminal.4 哪些 PTY 有這兩種模式

下面的歷史模式與選取模式看 PTY 拿來做什麼，不是看它是不是 PTY：

- **互動 terminal**：使用者在裡面打自己指令的 PTY（shell、ssh 連線、`kubectl exec`），一定有這兩種模式。
- **app 開一個程式做一件事的 PTY**（`$EDITOR` 編檔、讓 doas 問密碼）：沒有這兩種模式，按鍵全部給那個程式，包括 `PgUp`。捲動、
  移動、選取是那個程式自己的事。
- **子程序佔滿整個畫面時**（在互動 terminal 裡開了 vim、less、htop，它們切到終端機的另一個畫面）：`PgUp` 送給它，下框不寫
  `PgUp:history`；它回到一般畫面後，`PgUp` 又進歷史模式。選取模式照常，選的是凍住的那個畫面。
- **使用者把所有鍵都給子程序時**（例：sshu 鎖住格子，給在裡面再開的 sshu 用）：選取模式暫時讓出去；`PgUp|PgDn` 直接送進去，
  由最裡面的 PTY 捲它自己的歷史，就像直接在那個 terminal 裡操作。解開的鍵照 Rules K10 常駐揭露，解開後兩種模式回來。

**為什麼**：要顧的是使用者自己的指令：在 shell 裡打的指令，輸出要捲得回去、選得起來。編輯器與佔滿畫面的程式自己管捲動與選取，
我們沒有重寫它們，就不搶它們的鍵。它們的畫面也不會留進歷史，攔下 `PgUp` 只會讓 vim 翻不了頁，換來一個空的歷史。

## terminal.5 歷史模式

互動 terminal 的即時畫面上，字母都屬於子程序（shell 要 `j`、`k`、`g`），所以捲上去看歷史就是一個模式（Rules K11），裡面才用家族的移動鍵。

- **進入**：`PgUp` 捲上去就進入。框與模式名照 K11 換成模式色，模式名是 `History`（`┫History┣`）。
- **模式裡**：`j|k`、`u|d`、`gg|G`、`PgUp|PgDn` 都捲歷史，不送給子程序。
- **`Esc`**：離開模式，回到即時畫面。
- **其他鍵**：先離開模式回到即時畫面，再照常送給子程序 —— 看完歷史直接打字，字就落在 shell 裡。
- **揭露**：照 K11，模式裡能按的鍵寫在下框的 hint 與 `?` 的 key reference。

**為什麼**：到頭到尾在家族裡是 `gg|G`，PTY 的歷史也一樣；但即時畫面上每個字母都要送給子程序，家族的移動鍵只能在模式裡用。
`PgUp` 是終端機裡捲歷史的老習慣，按下去就進得來；打字的人不用先按 `Esc`，打下第一個字就回到即時畫面。

## terminal.6 選取模式

互動 terminal 的選取模式照 [`dialog/note`](note-zh_TW.md) 的選取模式：按鍵、顏色、捲動位置、複製後的 toast 都一樣。

- **進入**：選取模式在家族一律用 `v` 進入；PTY 裡的字母都屬於子程序，`v` 會打進 shell，所以加 `Alt` 跳出來：`Alt-v`。不是 app
  挑的鍵，跟保留鍵一樣常駐揭露（Rules K10、M1）。
- **畫面凍住**：進入時，子程序後來的輸出先不畫上去，選的範圍不會被新的輸出推走；游標可以往上走進歷史。離開時回到即時畫面。
- **離開之後**：按鍵照常送給子程序。

**為什麼**：在 shell 裡最常想複製的就是一段輸出；跟 viewer 同一套鍵，學一次在家族哪裡都能選。

## terminal.7 要提權時

app 要寫系統檔（例：hostu 寫 `/etc/hosts`）時，交給系統的提權工具：

- 先試不用密碼的（例：`sudo -n`）；成功就直接寫，不開任何東西。
- 要密碼時，開 password popup 問（[`input/password`](../input/password-zh_TW.md) 的解鎖方案，標題 `PASSWORD`），交給工具從標準
  輸入讀（例：`sudo -S`）。密碼不對：popup 不關，點清掉，錯誤列寫 `Wrong password`；按 `Esc` 取消，什麼都不寫。
- **密碼只交給提權工具**：除了交給工具的標準輸入，不寫進任何檔案、不進 App Log、不出現在畫面上（toast、錯誤訊息）、不送到網路上，
  交出去就丟。用 lib 的 app 只給要跑的指令：問密碼、交給工具都由 lib 做，app 碰不到密碼（Rules E8）。
- 工具不能從標準輸入讀密碼時（例：`doas`），開 terminal popup 跑它，讓它自己問；跑完 popup 自己關。這個 PTY 是 app 開一個程式做
  一件事，沒有歷史模式與選取模式（上面的「哪些 PTY 有這兩種模式」）。
- 用哪個工具，app 可以依平台自行決定（例：sudo，沒有時 doas；Windows 用 gsudo 或內建的 sudo，由系統跳 UAC）。

**為什麼**：問一行密碼，用不著撐滿畫面的終端機；問密碼的樣子跟家族其他 password popup 一樣。密碼因此經過 app，但家族是開源的，
密碼拿去做了什麼，看程式就知道；lib 把它關在「問」與「交出去」之間，app 拿不到，就不會被存下來、記進 App Log 或送出去
（user 2026-10-27，hostu）。sudo 記住多久照樣有效（先試 `sudo -n`）；指紋解鎖這類要工具自己問的設定用不到。

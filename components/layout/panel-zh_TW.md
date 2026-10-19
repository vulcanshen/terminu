# panel（框、清單、值與 filter）

**Language**: [English](panel.md) · 繁體中文

panel 的框、一般清單（含位置列、分組）、一列一個值的 panel、明細、panel filter。整個畫面的排法見 [`screen`](screen-zh_TW.md)。

## 框

- **線型與顏色**：有 focus 是 Blue 粗線 `┏━┓`，失焦是 Surface2 細線 `┌─┐`（直角），兩者同寬，切換時不位移（Rules L5、[`color`](../color-zh_TW.md)）。
  失焦時內容淡化，串流內容除外（Rules T2）。
- **上框左邊：`[N] label` 膠囊**，緊接著框的角。`N` 同時是直接跳到該 panel 的數字鍵（只在目前的畫面裡，Rules K1）。panel 有
  tab 時，`[N]` 自己是一段，tab 接在後面，第一個 tab 的名字就是 label（見下面的膠囊串）。label 裡的名稱照原樣，跟 popup 的標題一樣
  （`[2] PODS: nginx-7d4f`、`[1] prod-web-01`；[components](../README-zh_TW.md) 的「大寫」）。panel 在 loading 時，loading icon 放在整串膠囊（含 tab）的後面，前後各空一格
  （例：`┏[2] PODSEVENTSYAML 󰪞 ━━━┓`；[`popup`](popup-zh_TW.md) 的 loading）。
- **上框右邊：模式名**（Rules K11），夾在兩個框線接頭之間，像框上嵌了一個標籤：`┏[1] KINDS━━━┫Drag┣━┓`、
  `┏━YAML━━━━┫Visual┣━┓`。接頭跟框同色、線型跟著框 —— 粗線框（有 focus 的 panel、popup）用 `┫` `┣`，細線框（失焦的
  panel）用 `┤` `├`；模式名用模式色加粗，大小寫照原樣。
  模式名盡量一個詞（`Drag`、`Visual`、`Select`：窄的 panel 放不下兩個詞，右上角的字會整個被丟掉）；放不下時先截標題，
  模式名留著。膠囊跟著外框換成模式色。
- **下框左邊：hint**，每個 panel 都要有 —— 例外是 focus 在 panel filter 的打字列上時、focus 在 panel 裡的 PTY 時：不寫，focus 回到清單、
  離開 PTY 時回來；panel 上一個按得動的鍵都沒有時也不寫（見下面的 hint）。下框右邊：
  捲動位置（見下面的「一般清單」）。
- **框上的字與角之間一律隔一段線**，只有 `[N] label` 膠囊緊接著左上角：hint 是 `┗━ Enter:logs`、捲動位置是 `3 of 40 ━┛`、
  模式名是 `┫Drag┣━┓`。

```
┏[2] PODS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ ...                                             ┃
┗━ Enter:logs .:helm ━━━━━━━━━━━━━━━━━━━ 3 of 40 ━┛
```

**hint**：寫法與順序同 [`popup`](popup-zh_TW.md) 的 hint（`Enter` 第一）。內容是這個 panel 自己的鍵 —— `Enter` 在這裡做什麼、
常用的熱鍵；不寫移動鍵，也不寫 footer 已經有的 core key；全部的鍵在 Space menu 與 `?`。清單一項都沒有時（panel filter
篩到空，或本來就是空的），拿掉 `Enter` 與對項目的熱鍵，只留對整個 panel 的 —— 跟 finder、表單的按鈕一樣，hint 只寫按得動的鍵
（[`input/finder`](../input/finder-zh_TW.md)、[`dialog/form`](../dialog/form-zh_TW.md)）。拿掉之後一個鍵都不剩時（例：唯讀的
panel，或清單空了、又沒有對整個 panel 的鍵），下框左邊不寫 hint，只剩框線。有 focus 時鍵 Blue、說明 Overlay0；
失焦時照樣留著，跟著 panel 一起淡化。放不下時從尾端整組捨，捲動位置留著。

**為什麼**：panel 下框的 hint 告訴使用者「在這個 panel 上按什麼會怎樣」，footer 只管全畫面通用的鍵；兩者各管一層，
每個 panel 都有，使用者換 panel 時眼睛知道去哪裡找。panel filter 打字時不寫：hint 列的是 panel 自己的熱鍵，打字時都是字元
（Rules K8），列出來會教使用者按錯；打字時的鍵 footer 已經寫了。PTY 裡也一樣：panel 的鍵都送給子程序，不會送進去的出口鍵 footer 已經寫了
（[`screen`](screen-zh_TW.md) 的 footer）。框上的字都跟角隔一段線，只有膠囊例外 —— 四個角的規則一樣，
不用記哪個角不同；膠囊是這個 panel 的名字，貼著角最好找。loading icon 接在整串膠囊後面：膠囊串是一個整體（這是哪裡），
loading 是狀態，不切斷一串 tab。

## 膠囊串

panel 標題的膠囊、panel 的 tab、[`screen`](screen-zh_TW.md) 的畫面 chip、popup 標題後的 tab，用同一套畫法：

- **兩端**：斜角，左 U+E0BA（`nf-ple-lower_right_triangle`）、右 U+E0B0（`nf-pl-left_hard_divider`）。popup 的標題不在這串裡：
  它自己是一個圓角的膠囊（[`popup`](popup-zh_TW.md) 的標題）；popup 標題後面的 tab 照這串畫。
- **選中的**：填滿這串的顏色，字 Base 粗體。panel 上這串的顏色是框線色（跟著 focus、失焦、模式換）；popup 裡是層色；
  畫面 chip 是 Blue。`[N]` 膠囊與目前的 tab 都算選中的。
- **沒選中的**：不填底色，字用這串的顏色、不加粗。
- **接縫**：顏色換的地方用 U+E0B0（`nf-pl-left_hard_divider`），同色之間用 U+E0B1（`nf-pl-left_soft_divider`）。
- **斜角與接縫的顏色**（照 Powerline）：前景是左邊那一段的底、背景是右邊那一段的底；沒選中的段的底當作 Base（實心的三角形靠它畫出沒填色的那一邊；兩段都沒選中的細線不塗背景，見下），串外面是終端機的底。
  - 選中 → 沒選中：U+E0B0，前景這串的顏色、背景 Base；沒選中 → 選中：U+E0B0，前景 Base、背景這串的顏色。
  - 兩段都沒選中：U+E0B1，前景這串的顏色，不塗背景；兩段都選中：U+E0B1，前景 Base、背景這串的顏色（只有 `[N]` 與第一個 tab
    會兩段都選中，那裡照下面的「panel 的 tab」：一個 powerline 符號寬的空白、不畫接縫）。
  - 兩端的斜角畫成旁邊那一段的底：頭或尾是沒選中的段時，那一端是 Base（終端機的底是 Base 時看不見，只留一個 powerline 符號寬的空）。
  - 斜角與接縫一律各佔一個 powerline 符號的寬度（Rules E5：多半是一格；佔兩格的終端機上是兩格），看不見時也照樣佔著，換選中的段時
    字不位移。
- 膠囊裡的字前後不加空白：`[1] TABS`。字一律大寫，名稱照原樣（`[2] PODS: nginx-7d4f`），熱鍵標記裡的字母照原樣
  （[components](../README-zh_TW.md) 的「大寫」）。
- **panel 的 tab**：`[N]` 自己是一段，一直是選中的；後面每個 tab 一段，只有目前的 tab 選中。panel 沒有另外的名字，第一個 tab 的
  名字就是 label。`[N]` 與第一個 tab 都選中時（在第一個 tab），中間是空白、不畫接縫，看起來跟沒有 tab 的 panel 一樣；這段空白
  跟接縫一樣佔一個 powerline 符號的寬度（powerline 符號佔兩格的終端機上是兩格空白），換 tab 時字不位移：

  ```
  ┏[2] PODSEVENTSYAML━━━━━━━━━┓   ← 在 PODS：「[2] PODS」填色
  ┏[2]PODSEVENTSYAML━━━━━━━━━┓   ← 在 EVENTS：「[2]」與「EVENTS」填色
  ```

- **popup 標題後的 tab**：跟圓角的標題之間隔一段線（[`popup`](popup-zh_TW.md) 的標題）。
- **放不下時**：先把沒選中的縮成第一個字或 glyph（`[M] [F] [S]`）；還放不下，就從尾端收掉沒選中的、改畫一個 `…`。
  選中的永遠留著，絕不把框撐寬（Rules L4）。選中的那一段自己就太長時，字從尾端截、加 `…`；兩端的斜角照畫，跟框角之間
  照樣留一段線（例：`┏[2] DEPLOYM…━┓`）。

**為什麼**：膠囊在家族裡的意思是「名稱」—— panel 叫什麼、在哪一頁、在哪個畫面（Principle P4）。這幾種用途共用一套，
使用者認得一次就認得全部。沒選中的不用 Surface2：Surface2 是停用，沒選中的頁面看起來會像不能切。接縫用原始 Powerline
的兩個符號，字型支援最普遍；上色也照 Powerline，色塊只出現在選中的段，一眼看得出選了哪一個，沒選中的段旁邊不會冒出色塊的尖角。
兩段都沒選中的細線不塗背景：細線的形狀不靠背景，只有實心的三角形要用 Base 畫出沒填色的那一邊。
`[N]` 自己一段：除了編號，只有目前的 tab 亮，不會有兩塊看起來都是目前的；在第一個 tab 時用空白接，跟沒有 tab 的 panel 一樣，
也不用幫有 tab 的 panel 另外取名字；那段空白跟接縫一樣寬，在第一個 tab 與其他 tab 之間換，字才不會跳一格。選中的段太長時
截字不截斜角：斜角是「這是膠囊」的形狀，截掉了就看不出是名稱。兩端用斜角、popup 的標題用圓角：固定在畫面上的 panel 與浮在上面的 popup，看膠囊的兩端就分得出來。

## 一般清單

kbu 的資源清單、filu 的檔案清單這種一列一筆的 panel。

```
┏[2] PODS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃   NAME          READY  STATUS     RESTARTS  AGE ┃  ← 表頭：Blue，固定不捲
┃   nginx-7d4f    1/1    Running           0   3d ┃
┃ 󰄲 web-a8k2      0/1    CrashLoo…        12   2h ┃  ← 標記的列：Green 的勾
┃▓▓▓coredns-7w9z▓▓1/1▓▓▓▓Running▓▓▓▓▓▓▓▓▓▓▓0▓▓▓9d┃  ← cursor：Subtext1 底、Base 粗體
┃   prome-er-0    0/2    Pending           0   5m ┃
┗━ Enter:logs ━━━━━━━━━━━━━━━━━━━━━━━━━━ 3 of 40 ━┛
```

- **cursor**：Subtext1 底、Base 粗體，佔滿整個內寬；cursor 那一列整列都是 Base 字，各欄原本的顏色不保留。右邊的留白
  畫 U+E0B0（`nf-pl-left_hard_divider`），Subtext1，像一個箭頭指著這一列。留白跟箭頭一樣寬（Rules E5 的 powerline 符號寬度：
  多半是一格；佔兩格的終端機上，每一列右邊都留兩格），箭頭剛好放得進去，字不位移。panel 失焦時
  整塊淡化（Rules T2），cursor 跟著淡化，不另外換顏色。
- **表頭**：多欄的清單一定有表頭，單欄的由 app 決定。Blue、不加粗、大寫，固定在最上面不捲。每一欄是數字或文字：數字靠右、
  照數值排（`9` 在 `10` 前面），文字靠左、照文字排。
  欄與欄之間兩格（[components](../README-zh_TW.md) 的「圖與間距」）。排序中的欄位，標題後面加 `nf-fa-sort_amount_asc`（U+F160，
  升冪）或 `nf-fa-sort_amount_desc`（U+F161，降冪）；好幾欄一起排序時，在箭頭前加順位，例：`Name (2)` 後面接箭頭。
  **排序的群**：app 可以替每一列指定一個群，群的先後由 app 定，排序只在同一群裡排，群和群之間不畫標題（例：filu 的目錄一律在
  檔案前面，照名稱排時目錄與檔案各自排）。
- **清單的順序要固定**：每次打開、每次重抓，同一份資料排出來都一樣。資料本身沒有順序時（例：kubeconfig 的 contexts，讀出來的
  順序每次可能不同），app 先排好再顯示，預設照名稱、數字照數值；資料本身有順序的（例：照時間的歷史、使用者自己排過的），照它
  本來的順序。
- **欄放不下時**：先整欄收掉，再縮。app 替每一欄標收掉的順序，最重要的那一欄（名稱）永遠不收；放不下時從最不重要的那一欄整欄
  拿掉（表頭跟著拿掉），直到放得下、或只剩不能收的欄，還放不下才照比例縮各欄的寬。終端機變大時，收掉的欄照順序回來。
- **捲動位置**：放不下時，下框右邊寫 `N of M`（cursor 在第幾筆、總共幾筆），框線的顏色；全放得下就不寫。沒有 cursor 的
  panel（預覽、log）寫看得到的行 `N-M of T`。
- **標記的列**（Principle P3 的「整批標記」）：每一列最前面保留一格標記欄。被標記的列畫 Green 的 `nf-md-checkbox_marked`
  （U+F0132）；沒標記的留空白，欄寬一直保留，標記、取消時列不會左右位移（Rules L2）。收藏、釘選這類領域的旗標屬於內容，
  由 app 決定。
- **Drag mode 拿著的那一列**（Rules K11；進入 Drag 的鍵由 app 決定，例：展示場與 kbu 的 `D`）：照 cursor 的畫法，Subtext1 換成模式色 ——
  Yellow 底、Base 粗體，右邊的箭頭也是 Yellow；標記欄畫 `nf-md-swap_vertical`（U+F04E2），放下後回到那一列原本的標記。有 Drag 的
  panel，每一列也保留標記欄。按鍵跟 [`input/reorder`](../input/reorder-zh_TW.md) 拿著一項時一樣：`j|k` 搬（到頭尾繞回，Rules K12）、
  `Enter` 放下、`Esc` 放回。
- **截斷**：從尾端截，加 `…`。路徑、檔名這類尾端比較重要的，可以從前面截（`…/.ssh/id_ed25519`）；兩端都有意義的（例：pod
  的名稱，前面是 deployment、後面是辨識那一個的亂碼），從中間截，`…` 放在中間（`demo-app…66-gm72n`）。從哪裡截由 app 替每一欄
  決定。
- **空的**：照 [`screen`](screen-zh_TW.md) 的空狀態。空狀態取代整塊，連表頭一起不畫，句子置中在整個 panel；有位置列時位置列照樣留著（見「位置列」）。

**loading 與錯誤**：

- **loading**：loading icon 放在整串膠囊（含 tab）的後面，前後各空一格，用框線色（[`popup`](popup-zh_TW.md) 的 loading）。panel 還沒有任何內容時，中間照空狀態的樣子寫一句，例：`󰪞 loading pods…`。
  重新載入時，舊的內容留著，不清空。
- **錯誤、斷線、沒有權限**：照空狀態的樣子置中寫兩句：一句事實用 Red（例：`Forbidden: pods in kube-system`），一句提示用
  Overlay0（例：`Press [R] to retry`）。舊的內容還在就留著，錯誤照 Rules F5 用 toast 報。

**為什麼**：cursor 是「`Enter` 會作用的那一列」，整列一塊實心底、尾端一個箭頭，形狀與顏色都說得出來（L5）。標記用 checkbox 的勾：標記
就是「選起來的」，跟 checkbox 勾著的是同一件事、同一個顏色。多欄的清單一定有表頭：欄的意思與排序的箭頭都靠它。表頭固定，
捲到哪裡都看得到每一欄是什麼。欄放不下時整欄收：每一欄都縮一點，每一欄都讀不完；拿掉最不重要的一欄，剩下的照樣讀得完，
名稱一直在，認得出是哪一筆。排序的群讓「目錄在前面」這種固定的先後不被排序打散。清單空了時連表頭一起拿掉：沒有資料時，
欄名沒有東西可以對，置中的一句話最清楚。

### 位置列

清單上面一列寫目前的位置（路徑、drill 到的層），例：filu 的目錄、sshu 的遠端路徑、kbu 從 Deployment 進到 Pods 的那一層。
**要不要有這一列由 app 決定**。

```
┏[2] FILES━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ …/sideproj/terminu/components/layout          ┃  ← 位置列：Lavender，太長從前面截
┃   NAME              SIZE  MODIFIED            ┃
┃   panel.md         12 KB  2026-10-19 14:02    ┃
┗━ Enter:open ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **位置**：panel 內的第一列，離框一格；有表頭時在表頭上面，panel filter 的打字列出現時在打字列上面。固定在最上面，不捲。
- **顏色**：Lavender（[`color`](../color-zh_TW.md) 的使用者足跡、麵包屑）；panel 失焦時跟著淡化（Rules T2）。
- **太長**：從前面截、加 `…`，留住後面（目前所在的那一層在最後面）。
- **只顯示**：不能按，cursor 不會停在上面，捲動位置也不算它。
- **清單空了時照樣留著**：空狀態取代的是表頭與清單，位置列不在其中 —— 它說的是「你在哪裡」，不是清單的內容；空目錄更要知道是哪一個。

**為什麼**：「我現在在哪」寫在 label 裡，label 會越來越長、被膠囊的截斷吃掉；寫在 panel 裡自己的一列，放得下整條路徑，
label 也照樣是這個 panel 的名字。用 Lavender：使用者走到這裡留下的足跡，跟 statusbar 上「你現在在哪」的值是同一個意思。
不是每個 app 都有「位置」可言，所以這一列可有可無。

### 分組

清單的項目分成幾組時（kbu 的資源種類、locku 的側欄），每組前面一列分組標題。

```
┏[1] KINDS━━━━━━━━━━━━━┓
┃ WORKLOADS              ┃  ← 分組標題：Blue、大寫、不加粗，cursor 跳過
┃   pods                 ┃
┃▓▓▓deployments▓▓▓▓▓▓▓▓▓┃  ← cursor
┃   statefulsets         ┃
┃ NETWORK                ┃
┃   services             ┃
┃   ingresses            ┃
┗━ Enter:open ━━ 2 of 5 ━┛
```

- **分組標題**：Blue、大寫（[components](../README-zh_TW.md) 的「大寫」）、不加粗，沒有 glyph；離框一格。跟表頭同一類：說的是
  「下面這些是什麼」，不是一筆資料。
- **項目**：比分組標題多縮兩格。清單有標記欄時（上面的「標記的列」），標記就畫在多縮的那兩格裡：標記離框一格、空一格，字離框
  三格；分組標題那一列不留標記欄。
- **cursor 跳過分組標題**，只停在項目上：`j|k` 越過它；`gg|G` 到第一個、最後一個項目；捲動位置的 `N of M` 只算項目。捲動時
  cursor 停在一組的第一個項目，這組的標題也留在畫面裡。
- **組與組之間**：不空列、不畫分隔線。
- **沒有項目的組不畫標題**：panel filter 篩選後一項都沒剩，或 app 給的組本來就是空的。
- **失焦**：跟著 panel 一起淡化（Rules T2）。

**為什麼**：分組標題跟表頭一樣說「下面這些是什麼」，所以用表頭的畫法（Blue、大寫、不加粗）；項目多縮兩格，一眼看得出屬於哪一組，
不用另外畫分隔。標記畫在多縮的那兩格裡：字跟沒有標記時、跟一般清單有標記時一樣離框三格，不位移。cursor 只停在能做事的列上，
跟 menu 的區塊標題一樣。沒有項目的組還留著標題，看起來像還沒載入。

## 一列一個值

設定畫面這種一列一個值的 panel（locku 的 preference、webu 的 Settings、webu 頁面上的欄位）。

```
┏[2] PREFERENCE━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ PROPERTY            VALUE                     ┃
┃ PIN                 not set                   ┃
┃ PROFILE             clock                     ┃
┃ SHOW_STATUS         on                        ┃
┃ PIN_PROMPT_TIMEOUT  30                        ┃
┗━ Enter:edit ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **照 [`dialog/form`](../dialog/form-zh_TW.md) 的規則**：focus 一個項目一個項目移動（`j|l|↓|→` 往後、`h|k|↑|←` 往前；
  放在有 tab 的 panel 裡時 `h|l` 給 tab，Rules K12）；`Enter` 打開那個值的 input popup，radio、checkbox 在原地選；確定後
  focus 留在同一列（Rules K3）；值的顯示照 [`input/README`](../input/README-zh_TW.md)。
- **不一樣的地方：沒有送出。** 每個值在 input popup 確定的那一刻就生效、就存；開關與 radio 在原地選的那一刻也是。
  所以沒有動作區、也沒有「改過了要先問」。
- **focus 色塊**：Subtext1 底、Base 粗體，跟一般清單的 cursor 同一個畫法（右邊的留白是箭頭）；範圍跟表單一樣，從項目開頭到
  panel 內的右緣（欄位從值開始、選項從那個選項開始）。
- **label**：大寫；一般 Blue，停用 Surface2，它的值出錯時 Red（優先於其他顏色）。panel 失焦時跟著淡化（T2）。label 欄寬取最長的
  label 與表頭第一欄名裡最長的那一個（例：表頭 `SETTING` 7 格、最長的 label `DRAWER` 6 格時取 7 格），label 欄與值之間兩格；
  表頭的第二欄名跟值對齊。
- **表頭**（範例的 `PROPERTY  VALUE`）：要不要有由 app 決定。有的話用 Overlay0（[`color`](../color-zh_TW.md) 的暗字）；其他照
  一般清單的表頭（大寫、不加粗、固定在最上面不捲）。
- **捲動位置**：照表單，以欄位為單位 —— `N of M` 的 N 是 focus 所在的欄位，M 是欄位數；radio 的幾個選項算同一欄
  （[`popup`](popup-zh_TW.md) 的「內容放不下時」）。
- **`?` 的「每一列」一節**（要不要有由 app 決定）：key reference 最前面可以有一節說明每一列是什麼 —— 左欄是設定的名稱（一般字色），
  右欄是說明；按鍵的節接在後面（[`dialog/note`](../dialog/note-zh_TW.md) 的 key reference）。

**為什麼**：設定畫面跟表單是同一件事 —— 一列一個值、一個一個改 —— 只差在改了就生效。用同一套規則，使用者在表單學會的
在設定畫面照樣能用。label 用 Blue，跟有 focus 的框同色：表單的 label 用層色，也就是 popup 框的顏色，同一個道理。
表頭不用 Blue：底下的 label 已經是 Blue，表頭再用 Blue 會跟 label 連成一片，看不出是標題；一般清單的表頭底下是 Text 的資料，
才分得出來。表頭說的是「這一欄是什麼」、不能操作，跟 menu 的區塊標題一樣用暗字。表頭可有可無：每一列的 label 已經說了
它是什麼。label 欄連表頭一起算寬：表頭比 label 寬時只照 label 算，表頭的第二欄就對不上值。捲動位置照欄位算，跟表單一樣：
使用者數的是第幾個設定，不是第幾列字。label 只有一兩個字，說不清楚一列管什麼時，`?` 最前面的「每一列」一節補上；設定少、
名字就說清楚的 app 不用這一節。

## 明細

顯示另一個 panel 裡 cursor 那一筆的 panel：locku 的 `[2]` 屬性表、filu 的預覽、kbu 的詳細資料。

- **跟著 cursor 即時換**：那個 panel 的 cursor 一移動，明細的內容立刻換成新的那一筆，不用按 `Enter`；label 寫那一筆的名字時
  （locku 的 `[2] clock`），label 一起換。
- **focus 不動**：cursor 移動時 focus 留在原本的 panel；要操作明細，用 `Tab` 或數字鍵過去（Rules K2、K1）。app 也可以讓清單上的
  `Enter` 把 focus 送到明細，要不要、在哪些項目上由 app 決定（Rules K3 唯一可以用 `Enter` 換 panel 的地方）。
- 明細本身照它的種類畫：一般清單、一列一個值、預覽。

**為什麼**：明細回答的是「cursor 那一筆長什麼樣」。要按 `Enter` 才換，使用者一邊移動、看到的一直是上一筆；即時換，移到哪就看到哪。

## panel filter

按 `/` 之後在 panel 最上面出現一列打字列（有位置列時在位置列下面；清單有表頭時在表頭上面），打字的同時清單即時篩選，不開 popup（kbu 的 panel 搜尋、
sshu 的 Hosts、webu 的清單篩選）。

```
┏[2] HOSTS━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  prod                                   2/5 ┃   ← 打字列：前面是 `nf-fa-angle_right`，右邊是篩選的筆數
┃ NAME         USER      HOSTNAME              ┃   ← 表頭：在打字列下面
┃ prod-web-01  deploy    10.0.3.14             ┃
┃ prod-db      postgres  10.0.3.20             ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

打字列的按鍵、比對的方式跟 finder 的打字列一樣（[`input/finder`](../input/finder-zh_TW.md)）：篩選後的清單保持 panel 本來的排序。
打字列最前面是 `nf-fa-angle_right`（U+F105），離框一格（跟 finder 的打字列一樣），後面空一格才接打的字；顏色跟著打字列的亮暗：focus 在
打字列時用 panel 框線的顏色，在清單時 Overlay0。右邊的筆數寫 `符合/總數`（`2/5`），Overlay0。
不一樣的地方都來自 panel 在畫面那一層：

| | panel filter |
|---|---|
| 清單上的 `Tab` | 下一個 panel（Rules K2） |
| 清單上的 `Esc` | 清掉篩選（Rules K4：一次一層） |
| 選了一項之後 | 清單留著篩選過的樣子，照常操作；打字列用灰色畫（Overlay0） |
| 清單上的 `/` | 回到打字列，接著舊的字打；要從頭開始，先 `Esc` 清掉再按 `/` |

focus 離開與回來：

- **focus 離開 panel 時篩選留著**，往哪個方向離開都一樣：篩選是這個 panel 目前的樣子，到別的 panel 看一眼回來不該不見。
- **focus 回到有篩選的 panel 時，直接在打字列上**，不用再按 `/`；要操作篩選過的清單，按 `Enter` 或 `Tab` 到清單。
  所以有篩選的 panel 用 `Tab` 經過時會停兩下：打字列一下、清單一下。

**為什麼**：panel filter 跟 finder 做的事不一樣 —— finder 是「到某一項」，選了就關掉；panel filter 是「把清單縮小、留著繼續用」
（kbu 留下名字有 api 的 pod 看它們的狀態、sshu 打 `prod` 把整群 host 列出來一台一台連）。兩者的打字列用同一套鍵，
只有跟層級有關的 `Tab`、`Esc` 不同。

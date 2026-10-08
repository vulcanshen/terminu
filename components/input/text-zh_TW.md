# text（一行文字）

**Language**: [English](text.md) · 繁體中文

## 用途

輸入一行文字：名稱、網址、指令、路徑。單行 input popup 的骨架（說明列、值、錯誤列）在這裡定，password、number 共用。

## 長相

單行 input popup 的骨架，text、password、number 共用（user 2026-10-07 定）。

```
╭─ Rename ─────────────────────────────────╮
│                                          │
│ New name for assets                      │   ← 說明列：一句話，Overlay0
│                                          │
│ assets█                                  │   ← 值：Lavender；游標 Lavender 底、Base 字
│                                          │
│                                          │   ← 錯誤列（layout/popup）
│                                          │
╰─ Enter:rename Esc:cancel ────────────────╯
```

- **說明列**：一句話說要輸入什麼（`New name for assets`），Overlay0。跟值之間空一列。要改的對象是誰，寫進這一句。
- **值**：Lavender —— [`color`](../color-zh_TW.md) 裡 Lavender 是「正在編輯的東西」，input popup 裡正在編輯的就是這個值。游標是
  一格 Lavender 底、Base 字。
- **hint**：`Enter:<動詞> Esc:cancel`，動詞寫按下去做什麼（rename、create、save）。
- 現況：locku、sshu、webu 就是這樣；filu 要改（拿掉 Peach 的 `❯` 與輸入列下的底線，值從預設前景改成 Lavender，說明列從
  「被改名那一項的 icon 與名字」改成一句話）。
- 從表單搬來、原本留給 input 檔的三點：「上下式也適合只有一個欄位、label 是一句說明」就是這個樣子（說明列在上、值在下）；
  「單一欄位的 label 一直是 Lavender 粗體」與「focus 的值字不是 Lavender」不用了 —— 那是值在表單上直接打字時定的，現在
  Lavender 只給值，說明列是 Overlay0。

**值比框長時**（user 2026-10-07 定）：框裡顯示游標附近的那一段，被截掉的那一邊補 `…`。

```
│ …/sideproj/terminu/components/layout█ │   ← 打字中：游標在尾端，前面截掉
│ █/Users/vulcan/Documents/sideproj/te… │   ← Home 之後：游標在開頭，後面截掉
```

- 游標一定看得到；移動時只捲剛好夠的量，不把游標固定在中間（跟 popup 內容放不下時同一個捲法）。
- 寬度照顯示寬度算（中文一個字 2 格；sshu 現在照字數算，要改）。一個字不切成兩半，紅色的 `\n` 也一樣。
- 現況：webu 保留尾端；sshu 保留開頭、正在打的那一端看不到（盤點翻出的 bug）。

## 狀態

**改一個已經有的值：舊值是提議，不是預填**（user 2026-10-07 定）。

```
│ report-2025.pdf                      │   ← 框是空的；游標後面的舊值是灰字（Overlay0）
```

- 框打開時是空的，舊值用灰字（Overlay0）顯示在游標後面。
- `Tab`：把舊值收進框裡，游標在尾端，接著用 `←`/`→` 改（K2：單一輸入框有灰字提議時 `Tab` 接受提議）。
- 直接打字：重打一個新的值，灰字隱藏；把打的字刪光，灰字再出現。
- 值是空的時候按 `Backspace`：不要這個值，灰字消失；這時按 `Enter` 存成空的（欄位不能空時照錯誤處理）。
- 什麼都沒碰就按 `Enter`：不改，關掉。
- 有灰字時 hint 加 `Tab:edit Backspace:clear`（例：`Enter:rename Tab:edit Backspace:clear Esc:cancel`）。
- 為什麼：不要 `Ctrl-U` 之後，預填的長值要整個換掉得按住 `Backspace` 刪到底；提議讓「重打」不用先刪、「小改」多一下
  `Tab`、「不改」直接 `Enter`。
- 現況：locku 的設定檔路徑、webu 的 Location 是這樣；filu、sshu、webu 的 Rename 與 locku 的 profile 名稱是預填，要改。

**input popup 裡不放 placeholder**（user 2026-10-07 定）：要輸入什麼由說明列講；灰字只留給提議。兩種灰字長得一樣，一種按 `Tab`
會收進來、一種不會，會分不出來。

## 按鍵

user 2026-10-07 定。輸入態（K8）：字元、`Space`、`?`、`q` 都是字元。

| 鍵 | 作用 |
|---|---|
| 字元、`Space` | 插在游標處 |
| `←` / `→` | 游標往左、往右移一個字 |
| `Home` / `End` | 游標跳到最前面、最後面 |
| `Backspace` / `Delete` | 刪游標前面的字 / 游標上的字 |

- **一個字是看起來的一個字**：中文一個字、emoji 一個、組合字元連同前面的字算一個；貼上進來的換行與 Tab 各算一個（見「貼上的
  換行與 Tab」）。
- **不做 shell 的刪字快捷鍵**（user：`Ctrl-U`、`Ctrl-W` 不要）。locku、webu 現在的 `Ctrl-U` 清空要拿掉。其他 `Ctrl-`、`Alt-`
  組合在輸入框裡沒有作用、不打出字（kbu、webu 現在按 `Alt-b` 會打出 `b`）。
- 現況：只有 sshu 能移游標；filu、kbu、locku、webu 只能從尾端打字與刪字，要改。

## 貼上的換行與 Tab

2026-10-06 發版前定、五個 app 已照做（user 否決「換成空白」，理由是要明確顯示）；各 app 修的時候補了幾點。

- **範圍**：一行的值（textarea 不算）。只收數字的欄位照它原本的過濾。
- **只算貼上的文字**：按下去的 `Tab`、`Enter`、`Ctrl-J` 照它們原本的作用。
- **換行與 Tab 留在值裡**，畫成紅色的 `\n`、`\t`（Red `#f38ba8`，2 格，不切開）；整列畫成灰色的列（沒在打的篩選列、提議）裡跟著灰。
  `\r\n` 算一個換行，原樣存或存成 `\n` 都可以。其他控制字元（C0、DEL、C1）丟掉。
- **`Backspace` 一次刪整個 `\n` 或 `\t`。**
- **遮罩的值照樣遮罩**（password）。
- **預填的值走同一個過濾**：預填 = 每一個不是使用者打字進來的地方（原本的名字、檔案或別的程式給的值、選單填回來的值、從啟動
  目錄來的預設值、提議…），不一一列舉（sshu 的回饋）。
- **值會被拿去用的（送出、存、執行、交給別的程式）**：按 `Enter` 時擋下，錯誤列寫原因並點名欄位（例：`Name can't have line
  breaks or tabs`）；原本不會失敗的 input 照 F7 補上錯誤列。**在 trim 之前檢查**（filu：`Icon\r` + `Enter` 曾被改名成 `Icon`）。
- **搜尋與篩選列只畫，不擋。**

## 值

- **送出時去掉前後空白**，password 不去；換行與 Tab 的檢查在去空白之前（見上面的貼上規則）。sshu、locku、webu 現在就是這樣
  （2026-10-07 照現況寫下）。

## 在表單與 panel 上怎麼顯示

- **空的值**（user 2026-10-07 定，每一種 input 都一樣）：用灰字（Overlay0）寫出「空著代表什麼」，由 app 寫（`not set`、
  `ssh decides`、`none`）。一片空白看不出是沒設、設成空字串、還是還沒載入。locku 的 `not set` 現在是 Yellow，要改成灰
  （Yellow 是「選取、模式」，[`color`](../color-zh_TW.md)）。不寫教人按鍵的字（sshu 的 `enter to browse ~/.ssh`）：hint 會寫
  `Enter:browse`。

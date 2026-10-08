# input（共用的規則）

**Language**: [English](README.md) · 繁體中文

所有 input popup 共用的規則；各 input 檔只寫跟這裡不同的地方。

## 什麼是 input

一種 popup：輸入或選出一個值，確定後寫回去；一個 popup 一個值（Rules F1）。

- **打字列上是輸入態**（Rules K8）：字母、`Space`、`?`、`q` 都是字元。不打字的部分（select 的清單、picker）不是輸入態，core key
  照 Rules K1：`?` 打開 key reference，`q`／`Ctrl-C` 進離開流程，`Space` 不作用（K5），`hjkl` 移動（K12）。
- **`Enter`**（Rules K3）：focus 在值上時確定這個值 —— 寫回去、popup 關掉。值不合格就不寫回，錯誤寫在錯誤列，popup 不關。值跟打開時
  一樣，就不寫回、直接關掉。
- **`Esc`**：關掉，值不變。
- **從表單打開的**：確定之後 focus 留在表單的同一欄（Rules K3）。

## 單行 input popup 的骨架

text、password、number 共用。

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
- **值**：Lavender —— [`color`](../color-zh_TW.md) 裡 Lavender 是「正在編輯的東西」，input popup 裡正在編輯的就是這個值。游標是一格
  Lavender 底、Base 字。
- **錯誤列**：照 [`layout/popup`](../layout/popup-zh_TW.md)。
- **hint**：`Enter:<動詞> Esc:cancel`，動詞寫按下去做什麼（rename、create、save）。這種 popup 只有打字列，`?` 是字元，所以 hint 要列出
  全部操作（Rules M3）。
- **寬度**：自由打字的值，寬度不確定，用 Rules F7 的上限；有長度上限的值（例：PIN、範圍已知的數字），寬度確定，照
  [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」。

## 值比框長時

框裡顯示游標附近的那一段，被截掉的那一邊補 `…`。

```
│ …/sideproj/terminu/components/layout█ │   ← 打字中：游標在尾端，前面截掉
│ █/Users/vulcan/Documents/sideproj/te… │   ← Home 之後：游標在開頭，後面截掉
```

- 游標一定看得到；移動時只捲剛好夠的量，不把游標固定在中間（跟 popup 內容放不下時同一個捲法）。
- 寬度照顯示寬度算（中文一個字 2 格）。一個字不切成兩半，紅色的 `\n` 也一樣。

## 編輯鍵

打字列上：

| 鍵 | 作用 |
|---|---|
| 字元、`Space` | 插在游標處 |
| `←` / `→` | 游標往左、往右移一個字 |
| `Home` / `End` | 游標跳到最前面、最後面 |
| `Backspace` / `Delete` | 刪游標前面的字 / 游標上的字 |

- **一個字是看起來的一個字**：中文一個字、emoji 一個、組合字元連同前面的字算一個；貼上進來的換行與 Tab 各算一個。
- **不做 shell 的刪字快捷鍵**：`Ctrl-U`、`Ctrl-W` 不收。其他 `Ctrl-`、`Alt-` 組合在打字列上沒有作用、不打出字。

**為什麼**：編輯鍵只收鍵帽上寫著的那幾個，看得到就知道怎麼用。`Ctrl-U`、`Ctrl-W` 在不同 shell 裡行為不一樣，收進來反而要記
「這裡是哪一種」；改掉長值靠下面的灰字提議（重打一個值不用先刪）。

## 改一個已經有的值：舊值是灰字提議

```
│ report-2025.pdf                      │   ← 框是空的；游標後面的舊值是灰字（Overlay0）
```

- 框打開時是空的，舊值用灰字（Overlay0）顯示在游標後面。
- `Tab`：把舊值收進框裡，游標在尾端，接著用 `←`/`→` 改（Rules K2）。
- 直接打字：重打一個新的值，灰字隱藏；把打的字刪光，灰字再出現。
- 值是空的時候按 `Backspace`：不要這個值，灰字消失；這時按 `Enter` 存成空的（欄位不能空時照錯誤處理）。
- 什麼都沒碰就按 `Enter`：不改，關掉。
- 有灰字時 hint 加 `Tab:edit Backspace:clear`（例：`Enter:rename Tab:edit Backspace:clear Esc:cancel`）。
- 灰字提議只有這一種來源：舊值。沒有提議時 `Tab` 不作用。

**為什麼**：預填的長值要整個換掉時，得按住 `Backspace` 刪到底；提議讓「重打」不用先刪、「小改」多一下 `Tab`、「不改」直接 `Enter`。

## 不放 placeholder

input popup 裡不放 placeholder：要輸入什麼由說明列講；灰字只留給提議。

**為什麼**：兩種灰字長得一樣，一種按 `Tab` 會收進來、一種不會，會分不出來。

## 貼上的換行與 Tab

- **範圍**：一行的值（textarea 不算）。只收數字的欄位照它原本的過濾。
- **只算貼上的文字**：按下去的 `Tab`、`Enter`、`Ctrl-J` 照它們原本的作用。
- **換行與 Tab 留在值裡**，畫成紅色的 `\n`、`\t`（Red，2 格，不切開）；整列畫成灰色的列（沒有 focus 的打字列、提議）裡跟著灰。
  `\r\n` 算一個換行，原樣存或存成 `\n` 都可以。其他控制字元（C0、DEL、C1）丟掉。
- **`Backspace` 一次刪整個 `\n` 或 `\t`。**
- **遮罩的值照樣遮罩**（password）。
- **不是使用者打字進來的值走同一個過濾**：原本的名字、檔案或別的程式給的值、清單填回來的值、從啟動目錄來的預設值、提議……
  不一一列舉。
- **值會被拿去用的（送出、存、執行、交給別的程式）**：按 `Enter` 時擋下，錯誤列寫原因並點名欄位（例：`Name can't have line
  breaks or tabs`）。**在去掉前後空白之前檢查**：`Icon\r` 去掉空白會變成 `Icon`，先去空白就檢查不到。
- **搜尋與篩選的打字列只畫，不擋。**

**為什麼**：換成空白會悄悄改掉使用者貼進來的東西；明確畫出來，使用者看得到、自己決定要不要刪。

## 值

- **一行的值確定時去掉前後空白**，password 不去；換行與 Tab 的檢查在去空白之前（見上面）。

## 在表單與 panel 上怎麼顯示

- **顏色**：Text。
- **空的值**：用灰字（Overlay0）寫出「空著代表什麼」，由 app 寫（`not set`、`ssh decides`、`none`）。一片空白看不出是沒設、設成空字串、
  還是還沒載入。不寫教人按鍵的字（例：`enter to browse ~/.ssh`）：hint 會寫 `Enter:edit`。
- **太長**：從尾端截，加 `…`；路徑從前面截（`…/.ssh/id_ed25519`）。
- **各種 input**：

  | input | 顯示 |
  |---|---|
  | text、number | 值本身 |
  | password | 設了：固定 8 個 `•`；沒設：照空值 |
  | textarea | 第一行；後面還有就加 `…` |
  | select | 選中那一項的文字 |
  | checkbox popup（多選） | 選中的項目用 `, ` 接起來，太長加 `…` |
  | radio、checkbox（畫在表單上） | 選項本身（[`radio`](radio-zh_TW.md)、[`checkbox`](checkbox-zh_TW.md)） |
  | slider | 軌道加數字（[`slider`](slider-zh_TW.md)） |
  | datetime picker | 格式化的日期（時間），格式由 app 決定（`2026-10-15`、`2026-10-15 10:05`） |
  | color picker | 一小格色塊加 hex（`███ #2A2A3C`） |
  | file-picker | 路徑，家目錄寫成 `~` |

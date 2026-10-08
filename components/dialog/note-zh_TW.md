# note（唯讀內容）

**Language**: [English](note.md) · 繁體中文

## 用途

唯讀的內容，可以捲動，可以有自己的熱鍵與模式（Rules F1）：key reference、viewer（YAML 檢視、App Log、檔案內容）、error popup、
表單上的打字說明（[`dialog/form`](form-zh_TW.md)）。有可以用 `Enter` 執行的選項清單時，它是 menu，不是 note。

## 長相

- 框照 [`layout/popup`](../layout/popup-zh_TW.md)：上下留白一律有，viewer 也一樣。
- **標題**：glyph 加上顯示的東西（例：`YAML — pod/nginx`）。glyph 由 app 選；key reference 與 error popup 的 glyph 見下面。
- **捲動位置**：放不下時，下框右邊寫看得到的行 `N-M of T`。
- **寬度**：內容打開時就確定的（key reference、error popup、說明）照內容；viewer 的內容寬度不確定，用 Rules F7 的上限。

## 按鍵

- 捲動：`j/k`、`u/d`、`gg/G`（Rules K12）；文字的選取模式裡再加 `w/b/e`、`0/$`。
- **只用 `Esc` 關**。`Enter` 不關；`Space` 也不關（Rules K5）。
- **例外：自己跳出來的** error popup 與表單上的打字說明，`Enter` 也能關。
- **hint**：note 自己的熱鍵寫在前面，`Esc:close` 放最後。例：`y:copy /:search v:visual Esc:close`。

**為什麼**：使用者自己打開的 note，看完按 `Esc` 是最直覺的；`Space` 在 `less`、`man` 這類閱讀器裡是往下翻頁，熟的人在 note 上按
`Space` 想往下翻，note 卻關掉了。自己跳出來的那兩個，出現時使用者的手正在打字或正要送出，`Enter` 是反射動作；讓 `Enter` 也能關，
那一下不會落空，而它們上面也沒有別的東西會被 `Enter` 觸發。

## key reference

`?` 打開的「這裡能按什麼鍵」（Rules K6、M4）。

```
╭─ [2] Hosts keys ──────────────────────────────╮
│                                               │
│ item operation                                │  ← 區塊標題
│  Enter    connect — what it is, then in       │
│  E        edit — change this host             │
│  X        delete — remove from hosts.yaml     │
│ panel operation                               │
│  A        add — a new host                    │
│  /        search — name, user, host, port, …  │
│ core keys                                     │
│  Space    what you can do here                │
│  ?        this list                           │
│ app-wide                                      │
│  M        manage — hosts, credentials, …      │
│                                               │
╰─ ?/Esc:close ──────────────────── 1-12 of 20 ─╯
```

- **標題**：`nf-fa-question_circle`（U+F059）加 `<surface> keys`，例：`[2] Hosts keys`、`Space menu keys`。
- **每一列一個鍵**：縮兩格，鍵補到跟最寬的鍵一樣寬，空兩格，再接說明。說明太長從尾端截，加 `…`，不折行。鍵的寫法照 Rules M5
  （不加括號、不加冒號）。
- **從 menu 來的列**：說明寫 `label — 說明`。
- **區塊**：區塊標題跟 menu 一樣（Overlay0、縮一格、不加粗）。panel 上依序是 `item operation`、`panel operation`（跟 Space menu 一樣）、
  `core keys`、`app-wide`（global 熱鍵）；popup 上只列這個 popup 自己的鍵（Rules K6）。
- **顏色**：鍵 Blue、不加粗；說明 Text。現在按不了的鍵，鍵與說明都用 Surface2（Rules M6）。
- **按鍵**：捲動照上面；`?` 或 `Esc` 關，`Enter` 不作用。hint `?/Esc:close`。

## error popup

popup 的動作失敗時（[`layout/popup`](../layout/popup-zh_TW.md) 的錯誤列），蓋在那個 popup 上的 note。表單錯誤列 `Enter` 打開的完整訊息
也是它。

```
╭─ Save failed ───────────────────────────────────╮
│                                                 │
│ hosts.yaml changed on disk since it was opened. │
│                                                 │
╰─ Enter/Esc:close ───────────────────────────────╯
```

- **樣子**：框、標題、文字都是 Red。標題 glyph 跟 Error toast 一樣是 `nf-md-fire`（U+F0238）。訊息在框裡折行；太長時 `j`/`k` 捲動。
- **標題**：寫哪件事失敗了（`Rename failed`、`Save failed`）。從表單錯誤列打開的，標題寫那一欄的名字（`Port`）。
- **關掉**：`Enter` 與 `Esc` 都能關，hint `Enter/Esc:close`。
- **關掉之後**：回到底下的 popup，focus 留在原位，值都還在（Rules F4）。連按 `Enter` 時，第一下關掉它，下一下等於在原來的位置再按
  一次 —— 在表單的按鈕上就是重試。失敗的動作沒有改變任何東西，重試最多再看到一次錯誤。

**為什麼**：error popup 整個就是錯誤，框與字都是 Red；它一定在最上層、一個鍵就關掉，少了層色也不會讓人搞不清第幾層。有錯誤列的
popup 本身不是錯誤，只是裡面有一個值不合格，所以那裡的框維持層色。

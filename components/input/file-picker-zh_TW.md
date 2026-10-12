# file-picker（選檔）

**Language**: [English](file-picker.md) · 繁體中文

## 用途

選一個**檔案**，當成值交回去：sshu 的 Identity file、webu 的 Upload 與 Import。file-picker 是 finder 的一種（[`input/finder`](finder-zh_TW.md)）：
骨架、兩塊、`Tab`、打字列上 `Enter` 進清單、亮暗、預覽都照 finder；這裡只寫不同的地方。

## 長相

```
╭─ Identity file · ~/.ssh ─────────────╮ ╭─ id_ed25519 ────────────────────╮
│                                      │ │                                 │
│                                  5/5 │ │ -----BEGIN OPENSSH PRIVATE KEY  │   ← 打字列：打開時是空的
│ ──────────────────────────────────── │ │ (key, 411 B)                    │
│ 󰉋 ..                                 │ │                                 │
│ 󰉋 work                               │ │                                 │
│ 󰈔 config                             │ │                                 │
│ 󰈔 id_ed25519                         │ │                                 │   ← cursor：原本的值，字 Green
│ 󰈔 id_ed25519.pub                     │ │                                 │
│                                      │ │                                 │
╰─ Enter:choose Tab:filter Esc:cancel ─╯ ╰─────────────────────────────────╯
```

- **根目錄**：app 給，就是打開時清單顯示的那個目錄（例：sshu `~/.ssh`、webu `~/Downloads`）。只是起點、不是邊界：清單最上面一列
  是 `..`，可以往上走。根目錄 `/` 沒有 `..`。
- **目前的目錄寫在標題**，欄位名稱後面（`Identity file · ~/.ssh`）；路徑太長從前面截（`…/sideproj/terminu`）。
- **打字列打開時是空的**（[`input/README`](README-zh_TW.md) 的 placeholder 規則）。
- **每一列前面放 icon**：目錄一個、檔案一個，顏色照檔案類型（內容的顏色，由 app 決定；例：filu 用 eza 的顏色）。欄位原本有值的話，
  打開時 cursor 停在那個檔案上，字用 Green（目前的值）。
- **預覽的內容**：目錄列出裡面、文字檔顯示內容（行號 Overlay0）、其他寫類型與大小。

## 按鍵

- **清單上按 `Enter`**：在目錄上是**進去** —— 打的篩選字清掉，focus 留在清單，cursor 停在 `..` 下面的第一項；在檔案上才是**選中**，
  寫回去、關掉。**目錄永遠不會被選中**。
- **打字列打的字**：
  - 一般的字（`ed25`）：篩選目前這一層，照 [`finder`](finder-zh_TW.md) 的「比對」（包含、不分大小寫）。
  - 路徑（`/` 或 `~/` 開頭）：**路徑一直留在打字列上，以最後一個 `/` 切開** —— 前面是目錄（清單列出它、標題寫它），後面是篩選字
    （照「比對」）。路徑打到一半也有用，打字與貼上的結果一樣：

    | 打的字 | 清單 |
    |---|---|
    | `~/.ss` | 列出 `~`、篩 `.ss`：留下 `.ssh`，`Enter` 進去 |
    | `~/.ssh/` | 整個 `~/.ssh` |
    | `~/.ssh/id_` | `~/.ssh` 裡的 `id_ed25519`、`id_ed25519.pub` |
    | `~/.ssh/id_ed25519` | 那個檔在第一列，`Enter` 選中 |
    | `~/nope/x` | 目錄不存在：清單是空的，跟「沒有結果」一樣 |

    **路徑裡不支援 `..`**：有 `..` 這一段時不往上解析，當成不存在的目錄，清單是空的。往上走用清單的 `..` 列，或用 `Backspace`
    刪掉路徑的最後一段。
  - 有 `*`、`?`：wildcard。`*` 只比對同一層，`**` 往下找所有子目錄（一般 shell glob 的規則）：`~/Downloads/*.png` 列出 Downloads 裡
    所有的 png，`~/.ssh/**/*.pem` 找出 `.ssh` 底下所有的 pem。每一列寫相對於起點的路徑（起點是第一個 `*`、`?` 前面的目錄；例：
    `keys/a.pem`、`old/b.pem`），標題寫起點；結果是搜尋出來的、不是一層目錄，沒有 `..`。
- **hint**：清單上，在目錄是 `Enter:into Tab:filter Esc:cancel`、在檔案是 `Enter:choose Tab:filter Esc:cancel`；打字列 `Enter/Tab:list Esc:cancel`。

**為什麼**：這個欄位要的是檔案；在目錄上按 `Enter`，最直觀的動作是進去看裡面。目錄寫在標題，打字列就能留給篩選。路徑留在打字列上、
以最後一個 `/` 切開，清單永遠列出打字列上的那個目錄，不用另外定「什麼時候跳過去」：一個字一個字打 `~/Documents/sideproj`，不會打到
`~/Documents` 就跳走、清空，再把接著打的 `/sideproj` 當成根目錄底下的路徑；`Backspace` 刪掉最後一段就退回上一層。

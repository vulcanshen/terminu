# file-picker（選檔）

**Language**: [English](file-picker.md) · 繁體中文

## 用途

選一個**檔案**，當成值交回去（sshu 的 Identity file、webu 的 Upload 與 Import）。**它是 finder 的一種**（user 2026-10-07）：
骨架、兩區、`Tab`、打字時 `Enter` 進清單、亮暗、預覽都照 [`search`](search-zh_TW.md) 的 finder；這裡只寫不一樣的地方。照 filu 的
Search 做（user：filu 在上面花了很大功夫）。

## 長相

```
╭─ Identity file ──────────────────────────────╮ ╭─ id_ed25519 ─────────────────────╮
│  ~/.ssh/█                                    │ │ -----BEGIN OPENSSH PRIVATE KEY-- │
│──────────────────────────────────────────────│ │ (key, 411 B)                     │
│ 󰉋 ..                                         │ │                                  │
│ 󰉋 work                                       │ │                                  │
│ 󰈔 config                                     │ │                                  │
│ 󰈔 id_ed25519                                 │ │                                  │
│ 󰈔 id_ed25519.pub                             │ │                                  │
╰─ Enter:list Tab:list Esc:cancel ─────────────╯ ╰──────────────────────────────────╯
```

- **根目錄**：app 給，就是打開時清單顯示的那個目錄（sshu `~/.ssh`、webu `~/Downloads`）。只是起點、不是邊界：清單最上面一列
  是 `..`，可以往上走。
- **每一列前面放 icon**：目錄一個、檔案一個，顏色照檔案類型（filu 用 eza 色）。欄位原本有值的話，打開時 cursor 停在那個
  檔案上，字用 Green（[`color`](../color-zh_TW.md)「選中的值」）。
- **預覽的內容**：目錄列出裡面、文字檔顯示內容（行號 Overlay0）、其他寫類型與大小。

## 按鍵

- **清單上按 `Enter`**：在目錄上是**進去**；在檔案上才是**選中**，寫回去、關掉。**目錄永遠不會被選中**（user）。這是跟一般
  finder 不一樣的地方：finder 的 `Enter` 是「去那裡」，目錄也可以去。
- **輸入區打的字**（wildcard 是 user 要的，家族還沒人做過；其餘細節我補、user 沒異議）：
  - 一般的字（`ed25`）：模糊篩選目前這一層，比對照 filu（字首、分隔字元後、camelCase、連續、落在檔名本身加分）。
  - 路徑（`/` 或 `~/` 開頭）：清單跳到那個目錄。
  - 有 `*`、`?`：wildcard。`*` 只比對同一層，`**` 往下找所有子目錄（一般 shell glob 的規則）：`~/Downloads/*.png` 列出
    Downloads 裡所有的 png，`~/.ssh/**/*.pem` 找出 `.ssh` 底下所有的 pem。

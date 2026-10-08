# toast（短訊息）

**Language**: [English](toast.md) · 繁體中文

## 用途

從下方彈出的短訊息，`Esc` 或時間到就收掉；除了 `Esc`，按鍵都穿過它（Rules F1、F3）：「已複製」、操作失敗。跟某個 popup
的動作有關、需要使用者看完再決定的失敗，用 error popup（[`dialog/note`](note-zh_TW.md)），不用 toast。

## 長相

```
╭─ Info ────────────────────────────╮
│                                   │
│          Copied 3 paths           │
│                                   │
╰─ Esc:close ───────────────────────╯
```

- **框**：popup 的框，一律用第 1 層的層色。toast 不算一層（Rules F1）：不觸發淡化，也不被淡化。
- **位置**：畫面下方、水平置中；下框貼在 panel 下框的上面，panel 的下框（hint、捲動位置）與 footer 都留著看得到。
- **寬度**：訊息打開時就確定，照 [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」。
- **文字**：置中。太長時折行，每一列都置中；最多三列，超過的話第三列結尾加 `…`。完整的訊息應該走 error popup 或 app 的 log。
- **三種**：標題寫種類。

  | 種類 | 標題 | 文字 |
  |---|---|---|
  | Info | `nf-fa-flag`（U+F024）`Info` | Text |
  | Warning | `nf-md-alarm_light`（U+F078F）`Warning` | Peach |
  | Error | `nf-md-fire`（U+F0238）`Error` | Red |

- **時間**：Info 2200ms；Warning、Error 4400ms。
- **第二個 toast 來時**：直接取代第一個，重新計時。

**為什麼**：toast 是順便告訴你一聲，不該擋住任何東西 —— 所以在下方、不收鍵、時間到自己走；它也不該蓋掉 panel 的下框與 footer，
那裡是使用者接下來要按什麼的地方。Warning、Error 的時間加倍，因為要讀的東西比較重要。

## 按鍵

- `Esc` 立刻收掉它（Rules F3），在關掉其他 popup 之前先收它（Rules K4）；其他鍵都穿過它，送到底下。focus 在 PTY 裡時，`Esc`
  屬於子程序，toast 只能等時間到收掉。
- **hint**：`Esc:close`。

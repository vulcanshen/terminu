# color-picker（顏色）

**Language**: [English](color-picker.md) · 繁體中文

選一個顏色的 input popup（webu 網頁上的顏色欄位；locku 的配色設定可以照用）。user 2026-10-07 定。

## 用途

選一個顏色。

## 長相

```
╭─ Background ─────────────────────────────────╮
│                                              │
│  ████████  ████████                          │
│  ████████  ████████   ███   ███   ███        │   ← R/G/B：小色塊，畫那個色版的顏色（#2A0000、#002A00、#00003C）
│  old       new        R     G     B          │   ← focus 的項目，下面的字照 cursor 畫
│  #1E1E2E   #2A2A3C    2A    2A    3C         │   ← 一律寫 hex
│                                              │
╰─ Enter:edit Esc:cancel ──────────────────────╯
```

- **一整列由左到右**：old、new、R、G、B（user）。版面小，不佔一大塊。
- **old、new 兩個色塊畫大一點**（user）：old 是打開時的顏色，一直不變；new 是調整中的顏色，跟著 R/G/B 即時變。下面寫
  `old`、`new`（字是我挑的）與各自的 hex。並排比較，看得出改了多少。
- **R、G、B 是小色塊**，不是 slider（user：slider 太佔版面）。色塊畫那個色版自己的顏色（R 是 `#RR0000`，跟 locku 現在軌道的
  畫法一樣）；下面寫它的值，**一律用 hex**（user）。
- 先定過「三條 slider 上下排」與「兩個色塊在上、slider 在下」，user 改成這一列。

## 按鍵

- **可以 focus 的是 new、R、G、B 四個**，`h`/`l` 左右移動（一維：`j`/`k` 也是前後）；**old 不拿 focus**（user：不改就 `Esc`）。
  打開時 focus 在 R。focus 的那一項，下面的字照 cursor 畫（層色底、深色粗體）。
- **`Enter`** 對 focus 的項目做最直觀的動作（K3）：
  - R、G、B：開數字的 [`select`](select-zh_TW.md)（00–FF、step 1、cursor 在目前的值），每一列寫 hex、括號裡附十進位：`2A (42)`
    （user：呈現一律用 hex，十進位只在 select 上附註）；`/` 打字篩選，打 hex 或十進位都篩得到。選完回來，new 跟著變。
  - new：確定，寫回去，關掉。
- **`Esc`**：關掉，不改。
- **hint**：R/G/B 上 `Enter:edit Esc:cancel`；new 上 `Enter:choose Esc:cancel`。
- 不用 `Ctrl-S`、不加新的鍵：確定就是 new 上的 `Enter`。

## 值

- **表單與 panel 上**：一小格色塊加 hex（`███ #2A2A3C`）；空的照 text 的空值規則。
- 現況：webu 讓使用者打 `#RRGGBB`，要改成這個 picker。

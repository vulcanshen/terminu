# checkbox（開關，或勾好幾個）

**Language**: [English](checkbox.md) · 繁體中文

## 用途

一個開關，或從一組裡勾好幾個。開關與五個以內的一組，直接畫在表單或 panel 上、在原地翻；超過五個，開 checkbox popup
（例：kbu 的 namespace picker）。checkbox popup 是 finder 的一種（[`input/finder`](finder-zh_TW.md)）：這裡只寫不同的地方。

## 長相

- glyph：勾了 `nf-md-checkbox_marked`（U+F0132，實心打勾）、沒勾 `nf-md-checkbox_blank_outline`（U+F0131）。勾了的字是 Green（生效中）。
- **checkbox popup**：finder 的骨架，沒有預覽；每一列前面放 checkbox glyph（finder 的「清單的標記」）；寬度照選項確定。

**為什麼**：方框打勾、圓框一點（radio），是 GUI 表單的慣例，誰都看得懂（Principle P1）。打勾用實心的那一個：TUI 裡 outline 的
glyph 線條可能太細，看不清楚。

## 按鍵

**表單或 panel 上**：`Enter` 在原地翻，focus 不動，馬上生效。

**checkbox popup**：

- 打開時 focus 在清單上。
- **`Space`**：勾或取消勾 cursor 那一列 —— 只改畫面上的勾，不寫回、不生效（Rules K5 的例外）。
- **`Enter`**：把目前勾的整組一次寫回去、popup 關掉，這時才生效。從表單打開的，寫回那一欄、表單記成改過、focus 留在那一欄；
  單獨打開的，這時才套用（例：kbu 的 panel 2 這時才重抓）。什麼都沒改就按 `Enter`：不改，關掉。
- **`Esc`**：取消，勾的都不算，值維持打開時的樣子。不先問：一個 popup 只有一個值。
- 打字列照 finder；選項多時打字篩選。
- **hint**：清單 `Enter:apply Space:toggle Tab:filter Esc:cancel`；打字列 `Enter/Tab:list Esc:cancel`。

例：打開時勾的是 `default`。依序按 `j` `Space`（勾 `kube-system`）、`j` `Space`（勾 `monitoring`），這時 panel 2 還沒變。按 `Enter`，
三個一起生效；按 `Esc`，還是只有 `default`。

**為什麼**：`Space` 勾選是大家熟的做法（GUI 的核取方塊、很多 TUI 的多選清單）；`Enter` 留給確定整組，跟其他 input popup 一樣；
`Esc` 也就回到「取消」。

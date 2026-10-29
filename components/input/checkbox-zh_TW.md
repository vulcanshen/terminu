# checkbox（開關，或勾好幾個）

**Language**: [English](checkbox.md) · 繁體中文

## checkbox.1 用途

一個開關，或從一組裡勾好幾個。開關與五個以內的一組，直接畫在表單或 panel 上、在原地翻；超過五個，開 checkbox popup
（例：kbu 的 namespace picker）。checkbox popup 是 finder 的一種（[`input/finder`](finder-zh_TW.md)）：這裡只寫不同的地方。

一組選項一定帶一列全選 `Select all`，是元件自己的一列，不是選項（見下面的「全選」）；一個開關沒有。

一個開關也可以畫成 `off`、`on` 兩個選項的 [`radio`](radio-zh_TW.md)，app 可以自行決定。

## checkbox.2 長相

- glyph：勾了 `nf-md-checkbox_marked`（U+F0132，實心打勾）、沒勾 `nf-md-checkbox_blank_outline`（U+F0131）。勾了的字是 Green（生效中）；popup 裡跟著畫面上的勾，`Space` 勾了就是 Green（[`finder`](finder-zh_TW.md) 的「清單的標記」）。
- **不可用的選項**（not available，例：ccdrawu 要靠還拿不到的 API 的項目）：照樣畫在原位，整列 Surface2，勾也是（[`color`](../color-zh_TW.md)
  的「用不到」優先於「生效中」）；勾著的靠實心打勾的形狀看得出來。只畫出狀態，不擋操作（見下面的按鍵）；cursor 停在上面時照
  cursor 色塊畫，跟其他列一樣。表單、panel 上與 checkbox popup 裡都一樣。
- **checkbox popup**：finder 的骨架，沒有預覽；每一列前面放 checkbox glyph（finder 的「清單的標記」）；寬度照選項確定。

**為什麼**：方框打勾、圓框一點（radio），是 GUI 表單的慣例，誰都看得懂（Principle P1）。打勾用實心的那一個：TUI 裡 outline 的
glyph 線條可能太細，看不清楚。不可用的選項整列用 Surface2、勾也不用 Green：Green 說的是「生效中」，不可用的選項勾著也拿不到
效果；實心打勾的形狀已經說了它勾著。

## checkbox.3 全選

- 一組選項（一個開關不算）一定帶一列 `Select all`，畫在第一列：表單與 panel 上在 label 那一列，選項接在下面；checkbox popup
  裡是清單的第一列，跟著清單捲。glyph 與顏色照選項畫，勾著是 Green；focus 與 cursor 照樣能停。
- **選項比它多縮兩格**：看得出它管著下面這些（跟 panel 分組的項目一樣多縮兩格，[`layout/panel`](../layout/panel-zh_TW.md)）。
  篩選時它藏起來，選項照樣縮著、不位移。
- **它不是選項**：不算進值，也不算在「五個以內」裡；寫回的只有選項的勾。app 不另外放一個代表全部的選項（例：kbu 舊的
  `All Namespaces`），那是用錯了；每一個都勾著代表什麼，app 可以自行決定（例：kbu 讀成整個 cluster，之後新建的 namespace 也算）。
- **翻它**：勾起來，每一個選項都勾上；取消，每一個都取消；不可用的選項也算，停用的不算（表單上現在不能改的選項，
  [`dialog/form`](../dialog/form-zh_TW.md) 的「停用的欄位與選項跳過」，照樣維持原樣）。鍵與生效的時機都跟選項一樣：表單、panel 上
  馬上生效；checkbox popup 裡只改畫面上的勾，`Enter` 才寫回。
- **它反映現在的狀態**：每一個選項都勾著，它才勾著（停用的選項不算；每一個選項都停用時，它也停用）。取消任何一個，
  它跟著取消；一個一個勾滿了，它跟著勾上；打開時就全勾著，它也勾著。
- **篩選時藏起來**：checkbox popup 的打字列有字時不畫這一列，清掉才回來。
- **focus 與 cursor 不從它開始**，移動才到得了它：表單打開時第一個項目是它，停在第一個選項；checkbox popup 沒指定時停第一個
  選項；跳進表單上的 checkbox 組時停第一個勾起來的選項。

```
┃ Tags   󰄱 Select all                  ┃
┃          󰄲 web                       ┃
┃          󰄱 db                        ┃
┃          󰄲 cache                     ┃
```

例：`default`、`kube-system`、`kube-public`、`monitoring`，勾著 `kube-system`、`kube-public`：`Select all` 沒勾。在 `Select all`
上按 `Space`，四個都勾上，它也勾上；再到 `default` 上按 `Space`，`default` 取消，`Select all` 跟著取消，其他三個照舊。

**為什麼**：勾一組，全選與全取消是一定會用到的操作（GUI 的慣例）；放在元件裡，每個 app 都一樣，也不用自己做。app 自己放的
「全部」選項會跟其他勾打架：先勾它再勾 `default`，寫回的還是全部，`default` 被默默吃掉（來自 kbu）。這一列反映的是整組真實
的狀態；篩選時看不到被篩掉的選項，它不管怎麼畫都不是當下真實的狀態，所以藏起來（user 2026-10-24）。

## checkbox.4 按鍵

**表單或 panel 上**：`Enter` 在原地翻，focus 不動，馬上生效。表單上 `Space` 也能翻（Rules K5 的例外，跟 checkbox popup 一樣）；
panel 上的 `Space` 照樣打開 Space menu。hint：表單上 `Enter|Space:toggle`（[`dialog/form`](../dialog/form-zh_TW.md)）；panel 上只有 `Enter` 翻，
寫 `Enter:toggle`。

**checkbox popup**：

- 打開時 focus 在清單上，cursor 停在 app 指定的那一項（從哪一項開始，app 可以自行決定，沒指定就是第一個選項，不是 `Select all`）。
- **`Space`**：勾或取消勾 cursor 那一列（在 `Select all` 上是整組，見「全選」）—— 只改畫面上的勾，不寫回、不生效（Rules K5 的例外）。
- **`Enter`**：把目前勾的整組一次寫回去、popup 關掉，這時才生效。從表單打開的，寫回那一欄、表單記成改過、focus 留在那一欄；
  單獨打開的，這時才套用（例：kbu 的 panel 2 這時才重抓）。什麼都沒改就按 `Enter`：不改，關掉。
- **`Esc`**：取消，勾的都不算，值維持打開時的樣子。不先問：一個 popup 只有一個值。
- **不可用的選項跟其他選項一樣操作**：cursor 照樣停，`Space` 照樣勾或取消，`Enter` 照畫面上的勾寫回。不可用代表什麼、勾著的
  要怎麼處理（例：drawer 上寫 `api unavailable`），app 可以自行決定；tdp 只畫出狀態。
- 打字列照 finder；選項多時打字篩選，不可用的選項照樣列在結果裡。
- **hint**：清單 `Enter:apply Space:toggle Tab|/:filter Esc:cancel`；打字列 `Enter|Tab:list Esc:cancel`。篩到沒有結果時：
  清單上的 `Enter` 照樣把勾好的整組寫回去（篩選不改勾了哪些，被篩掉的勾也算），`Space` 沒有東西可以勾，hint 拿掉 `Space`：
  `Enter:apply Tab|/:filter Esc:cancel`；打字列的 `Enter` 照 finder 不作用：`Tab:list Esc:cancel`。

例：打開時勾的是 `default`。依序按 `j` `Space`（勾 `kube-system`）、`j` `Space`（勾 `monitoring`），這時 panel 2 還沒變。按 `Enter`，
三個一起生效；按 `Esc`，還是只有 `default`。

**為什麼**：`Space` 勾選是大家熟的做法（GUI 的核取方塊、很多 TUI 的多選清單）；`Enter` 留給確定整組，跟其他 input popup 一樣；
`Esc` 也就回到「取消」。不可用的選項照樣畫出來、能停、能勾：勾著的停不上去，使用者就拿不掉它（舊設定開著的 Account 只能
手改設定檔）；它能不能用、勾了怎麼辦是 app 的事，tdp 只讓人看得出它現在不可用。藏起來，使用者會以為沒有這一項（跟 Rules M6
同一個道理）。

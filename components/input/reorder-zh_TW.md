# reorder（自己搬動項目，排出順序）

**Language**: [English](reorder.md) · 繁體中文

## reorder.1 用途

把一組項目一項一項搬，排出它們的順序（例：ccdrawu 的 drawer 項目顯示的順序）；值是整個順序，`Enter` 確定後寫回去（Rules F1 的
input）。它就是 panel 的 Drag mode 放進 popup：拿起、搬、放下的按鍵與樣子都一樣（[`layout/panel`](../layout/panel-zh_TW.md)）。

跟 menu 的排序選擇器（[`dialog/menu`](../dialog/menu-zh_TW.md)）不同：排序選擇器選依哪一欄排，只決定怎麼顯示；reorder 是使用者自己
搬動項目，改掉的是順序本身。

沒有搜尋：篩選之後，畫面上的上一項不一定是真正的上一項，搬的時候說不清跟誰交換。所以它不是 finder；要排的通常是挑好的少數幾項，
`j|k`、`u|d`、`gg|G` 就找得到。

## reorder.2 長相

沒拿東西時：

```
┏━ORDER━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                 ┃
┃   Usage                         ┃   ← 每一列前面留一格給 glyph
┃▓▓▓Cost▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃   ← cursor：層色底、Base 粗體
┃   Model                         ┃
┃   Context                       ┃
┃   Git                           ┃
┃                                 ┃
┗━ Enter:apply D:drag Esc:cancel ━┛
```

拿著 Cost 按一次 `k`（Cost 跟 Usage 交換）：

```
┏━ORDER━━━━━━━━━━━━━━━━━━┫Drag┣━┓   ← Drag mode：框與模式名換成 Yellow
┃                                 ┃
┃▓󰓢▓Cost▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃   ← 拿著的一項：Yellow 底、Base 粗體，列首 `nf-md-swap_vertical`
┃   Usage                         ┃
┃   Model                         ┃
┃   Context                       ┃
┃   Git                           ┃
┃                                 ┃
┗━ Enter:drop Esc:cancel ━━━━━━━━━┛
```

- **每一列**：列首一格放 glyph，空一格，再寫項目（Text）。只有拿著的那一項畫 glyph，其他列留空白；這一格一直保留，拿起、放下時
  字不位移（Rules L2）。
- **cursor**：照 menu —— 層色底、Base 粗體，從框貼到框，右邊的留白是箭頭 U+E0B0（[`dialog/menu`](../dialog/menu-zh_TW.md)）。
- **拿著的那一項**（Drag mode，Rules K11）：照 cursor 的畫法，層色換成模式色 —— Yellow 底、Base 粗體，箭頭也是 Yellow；列首畫
  `nf-md-swap_vertical`（U+F04E2）。框與模式名換成 Yellow，上框右側嵌 `┫Drag┣`（[`layout/panel`](../layout/panel-zh_TW.md) 的模式名）。
- **標題**：照 [`layout/popup`](../layout/popup-zh_TW.md)，寫排的是什麼（例：`ORDER`）。
- **寬度**：打開時就確定（[`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」）：最寬的項目加列首兩格，再 + 4；
  至少放得下 hint `Enter:apply D:drag Esc:cancel`（29 + 6 = 35 格）。

**為什麼**：拿著的一項用模式色、加上下箭頭：看得出「這一項被拿起來了，可以往上往下搬」，而 Yellow 在家族裡就是「在模式裡」。
glyph 那一格每一列都留：拿起時只有那一列換色、多一個 glyph，其他列一格都不動。

## reorder.3 按鍵

- 打開時 focus 在清單上。
- **沒拿東西時**：
  - `j|l` 往後、`h|k` 往前移動 cursor（一維清單，Rules K12），到頭尾繞回；`u|d` 半頁、`gg|G` 頭尾。
  - **`D`**：拿起 cursor 那一項，進入 Drag mode。`D` 是這個 popup 自己的熱鍵；`Space` 照 Rules K5 不作用。
  - **`Enter`**：把整個順序寫回去、popup 關掉，這時才生效（從表單打開的，照 [`input/README`](README-zh_TW.md)）。順序跟打開時一樣：
    不改，關掉。
  - **`Esc`**：順序沒改過，直接關。改過，先開 confirm 問要不要放棄（例：`Discard changes to Order?`）：`Enter` 放棄、popup 關掉；
    `Esc` 關掉 confirm、回到清單，順序還在（Rules F3、F6、K4；跟 [`dialog/form`](../dialog/form-zh_TW.md) 的「取消」一樣）。
    「改過了」：放下的位置跟拿起前不同就算，之後不清掉 —— 搬走又搬回原位也算改過。
  - **hint**：`Enter:apply D:drag Esc:cancel`。
- **拿著一項時**（Drag mode，Rules K11）：
  - `j|l`、`h|k`：把它跟下一項、上一項交換，cursor 跟著它。到頭尾繞回：拿著最後一項往下，它到第一項、其他各往下一格；拿著第一項往上，
    它到最後一項（Rules K12）。
  - **`Enter`**：放下，離開 Drag mode，cursor 留在那一項。
  - **`Esc`**：放回拿起前的位置，離開 Drag mode（K11：回到進入前的狀態；Rules K4 一次一層）。再按一次 `Esc` 才是上面的取消。
  - `Space` 打開 Drag mode 的 Space menu（K11）；其他鍵不作用，`D` 不是放下的別名。
  - **hint**：`Enter:drop Esc:cancel`。
- **`?`**：這個 popup 的 key reference（Rules K6）；拿著時是 Drag mode 的鍵（K11）。

例：ccdrawu 的順序是 Usage、Cost、Model。cursor 在 Cost 上按 `D`、`k`、`Enter`：Cost 搬到最上面、放下；再按 `Enter`，新的順序
Cost、Usage、Model 寫回去。拿著 Cost 時按 `Esc`，Cost 回到第二項；放下之後按 `Esc`，先問要不要放棄。

**為什麼**：panel 上排順序已經有 Drag mode，popup 裡照搬，學一次兩處都會用。拿起用 `D` 而不是 `Space`：`D` 是 popup 自己的熱鍵，
K5 不用多一個例外。`Enter` 一次只做一件事：拿著時放下，沒拿東西時確定整個順序。`Esc` 一次退一層：先放回拿著的那一項，再取消整個
popup。順序改過才先問：搬過好幾項的順序一次丟掉，重排的代價跟表單一樣高。

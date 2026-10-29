# toast（短訊息）

**Language**: [English](toast.md) · 繁體中文

## toast.1 用途

從下方彈出的短訊息，`Esc` 或時間到就收掉；除了 `Esc`，按鍵都穿過它（Rules F1、F3）：「已複製」、操作失敗。跟某個 popup
的動作有關、需要使用者看完再決定的失敗，用 error popup（[`dialog/note`](note-zh_TW.md)），不用 toast。inspect toast
（toast.4）是例外：它說游標那一項是什麼，只在游標停在那一項時存在。

## toast.2 長相

```
┏━󰗠 SUCCESS━━━━┓
┃                ┃
┃ Copied 3 paths ┃
┃                ┃
┗━ Esc:close ━━━━┛
```

- **框**：popup 的框，一律用第 1 層的層色。toast 不算一層（Rules F1）：不觸發淡化，也不被淡化。
- **位置**：畫面下方、水平置中；下框一律在畫面倒數第三列，不管底下是什麼，最下面兩列一直看得到：平常是 panel 的下框（hint、
  捲動位置）與 footer；terminal popup 開著時是 PTY 的最後一列（shell 的提示列）與 terminal 的下框（出口鍵）；沒有 panel 的畫面也是
  同一個位置。
- **寬度**：訊息打開時就確定，照 [`layout/popup`](../layout/popup-zh_TW.md) 的「內容的寬度打開時就確定」。
- **文字**：置中。可以好幾列，app 一列一列給（[components](../README-zh_TW.md) 的「控制字元」），每一列另起一列。太長時折行（照 [components 的「折行」](../README-zh_TW.md)），每一列都置中。最多幾列，app 可以自行決定，規範不設上限；app 設了上限、
  訊息超過時，最後一列結尾加 `…`，完整的訊息走 error popup 或 app 的 log。
- **開頭大寫**：每一列的第一個字母大寫，其他照原樣（`Copied`、`Can't save filu: permission denied`）。一列從名稱或路徑開始時，
  名稱照原樣，不改大小寫（`kbu.yaml saved`；[components](../README-zh_TW.md) 的「大寫」：名稱是內容）。App Log 的每一筆也照這條
  （[`dialog/note`](note-zh_TW.md) 的 App Log）。
- **四種**：標題寫種類。

  | 種類 | 標題 | 文字 |
  |---|---|---|
  | Success | `nf-md-check_circle`（U+F05E0）`SUCCESS` | Green |
  | Info | `nf-fa-flag`（U+F024）`INFO` | Text |
  | Warning | `nf-md-alarm_light`（U+F078F）`WARNING` | Peach |
  | Error | `nf-md-fire`（U+F0238）`ERROR` | Red |

- **用哪一種，跟著顏色的意思走**（[`color`](../color-zh_TW.md)）：

  | 種類 | 什麼時候用 | 例 |
  |---|---|---|
  | Success | 一個動作成功做完（Green：成功完成的） | `Copied 3 paths`、`Connected to web-01` |
  | Info | 中性的告知，沒有好壞 | `Switched to context prod`、`Nothing to paste` |
  | Warning | 做完了或還能用，但有值得注意的地方（Peach：值得注意、但沒壞） | `3 files skipped`、`Unknown key in config.yaml` |
  | Error | 動作失敗（Red：錯誤） | `Can't connect to cluster` |

  做完的事用 Success 還是 Info，app 可以自行決定：Success 本來就是告知的一種，要不要特別標成成功，看 app。失敗一律用 Error，不用 Warning；跟某個 popup 的動作有關、要使用者看完再決定的失敗，照「用途」用 error popup。
- **時間**：Success、Info 2200ms；Warning、Error 4400ms。
- **第二個 toast 來時**：直接取代第一個，重新計時。

**為什麼**：toast 是順便告訴你一聲，不該擋住任何東西 —— 所以在下方、不收鍵、時間到自己走；它也不該蓋掉 panel 的下框與 footer，
那裡是使用者接下來要按什麼的地方。terminal popup 開著時，toast 在 PTY 裡按 `Esc` 關不掉（Rules K10、F3）；蓋住提示列的話，有幾秒
看不到自己打的字，而 terminal 的下框寫著出口鍵，跟 footer 一樣是「接下來能按什麼」。一個位置涵蓋所有情況，toast 也不會因為
畫面不同而跳來跳去。Warning、Error 的時間加倍，因為要讀的東西比較重要；Success 跟 Info 一樣，只是順便說一聲做完了。Success 用
圓圈裡一個勾，不用方框打勾：方框打勾是 checkbox，同一個樣子不能有兩個意思（Principle P4）。

## toast.3 按鍵

- `Esc` 立刻收掉它（Rules F3），在關掉其他 popup 之前先收它（Rules K4）；其他鍵都穿過它，送到底下。focus 在 PTY 裡時，`Esc`
  屬於子程序，toast 只能等時間到收掉。
- **hint**：`Esc:close`。

## toast.4 inspect toast

說游標那一項是什麼的 toast，游標在那一項上它就在（user 2026-10-29，來自 webu）：例：webu 的 Focus mode 裡，連結會去的
網址。哪些項目有、寫什麼，app 可以自行決定；沒有東西可看的項目就沒有。

```
┏━󰈈 INSPECT━━━━━━━━━━━━┓
┃                         ┃
┃ go.dev/doc/effective_go ┃
┃                         ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **長相**：跟一般 toast 一樣（toast.2 的位置、框、寬度、文字），標題 `nf-md-eye`（U+F0208）`INSPECT`，文字 Text。
  **沒有 hint**：沒有鍵關它。
- **什麼時候在**：游標停到有 inspect toast 的項目上就出現，離開那一項就消失；移到另一個有的項目，直接換成那一項的。
  **沒有計時。**
- **按鍵**：所有鍵都穿過它，`Esc` 也是（toast.3、Rules K4、F3 的例外）：`Esc` 照底下的意思做（例：離開 webu 的 Focus
  mode），toast 跟著游標消失。
- **其他 toast 來時**：一般 toast 照 toast.2 取代它；那個走了以後，游標還在那一項上，inspect toast 就回來。
- **底下那一項**：inspect toast 會蓋到游標那一項時，畫面捲動，讓那一項露在它上面。

**為什麼**（user 2026-10-29）：連結會去哪，只有停在連結上時才要看，所以不佔自己的一列或一格 —— panel 下框右邊照樣是
捲動位置（[`layout/panel`](../layout/panel-zh_TW.md)）。note popup 會收鍵，`j|k` 就移不了游標；toast 本來就讓 `Esc` 以外
的鍵穿過。`Esc` 也讓它穿過：游標一走它就自己走，攔下 `Esc` 只會讓每個連結上都要按兩下才離開，而移到下一個連結它又會
出現。用眼睛不用放大鏡：家族裡放大鏡是搜尋（webu、filu 的搜尋框），同一個樣子不能有兩個意思（Principle P4）。標題自己
一種、不用 Info 的：Info 過一會兒自己走，inspect toast 不會。

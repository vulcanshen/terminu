# file-picker（選檔）

**Language**: [English](file-picker.md) · 繁體中文

## file-picker.1 用途

選一個**檔案**，當成值交回去：sshu 的 Identity file、webu 的 Upload 與 Import。值是目錄時用下面的「選目錄」。file-picker 是 finder 的一種（[`input/finder`](finder-zh_TW.md)）：
骨架、兩塊、`Tab`、打字列上 `Enter` 進清單、亮暗、預覽都照 finder；這裡只寫不同的地方。

## file-picker.2 長相

```
┏━IDENTITY FILE · ~/.ssh━━━━━━━━━━━━━━━━━━━┓ ┏━id_ed25519━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                            ┃ ┃                                             ┃
┃                                       6/6 ┃ ┃ -----BEGIN OPENSSH PRIVATE KEY-----         ┃
┃ ────────────────────────────────────────── ┃ ┃ (sensitive content not shown)               ┃
┃ 󰉋 ..                                       ┃ ┃                                             ┃
┃ 󰉋 work                                     ┃ ┃                                             ┃
┃ 󰈔 config                                   ┃ ┃                                             ┃
┃▓󰈔▓id_ed25519▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃ ┃                                             ┃
┃ 󰈔 id_ed25519.pub                           ┃ ┃                                             ┃
┃ 󰈔 known_hosts                              ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃ ─────────────────────────────────────────── ┃
┃                                            ┃ ┃ TYPE      private key                       ┃
┃                                            ┃ ┃ SIZE      411 B                             ┃
┃                                            ┃ ┃ MODIFIED  2026-09-30 14:02                  ┃
┃                                            ┃ ┃ MODE      -rw-------                        ┃
┃                                            ┃ ┃                                             ┃
┗━ Enter:choose Tab|/:filter Esc:cancel ━━━━━┛ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

上圖是 `hide_secrets_in_preview` 打開時的樣子；預設是關的，關的時候私鑰也照文字檔整個顯示（見下面的「藏起秘密」）。

- **四塊**：打字列、清單、預覽、metadata。左框是「打字列／分隔線／清單」，右框是「預覽／分隔線／metadata」；terminal 寬不到 96 時
  metadata 搬到清單旁邊自己一個框，預覽在下面整條寬（[`finder`](finder-zh_TW.md) 的「排法」）。
- **根目錄**：app 給，就是打開時清單顯示的那個目錄（例：sshu `~/.ssh`、webu `~/Downloads`）。只是起點、不是邊界：清單最上面一列
  是 `..`，可以往上走。根目錄 `/` 沒有 `..`。
- **目前的目錄寫在標題**：欄位名稱（大寫）後面接 ` · ` 再接目錄（例：`IDENTITY FILE · ~/.ssh`）；路徑太長從前面截（`…/sideproj/terminu`）。
- **打開時 focus 在清單上**，跟 select、checkbox popup 一樣。
- **打字列打開時是空的**（[`input/README`](README-zh_TW.md) 的 placeholder 規則），前面照 finder 有 `nf-fa-angle_right`。
- **清單的順序**：`..` → 目錄 → 檔案，各自照名字排、不分大小寫。
- **隱藏檔**（`.` 開頭）預設不列；打字列的篩選字（路徑的最後一段）是 `.` 開頭時才列（`.ss`、`~/.ss` 會出現 `.ssh`）。跟 shell 的 glob
  一樣：`*` 不比對隱藏檔、`**` 不走進隱藏目錄，要寫 `.` 開頭才會。
- **每一列前面放 icon**：目錄 `nf-md-folder`（U+F024B）、檔案 `nf-md-file`（U+F0214），顏色照檔案類型（內容的顏色，app 可以
  自行決定；例：filu 用 eza 的顏色）。欄位原本有值的話，打開時 cursor 停在那個檔案上，字用 Green（目前的值）。

**為什麼**：家目錄有幾十個隱藏檔，全列出來會塞滿清單最上面；要找隱藏檔的人自然會打 `.`，跟 shell 同一個規矩，不用多學一個切換鍵。

### file-picker.3 預覽

cursor 那一筆的內容，照種類畫。最多讀 64 KB。

**在背景讀**：預覽與 metadata 不在畫畫面的時候讀，打字、移動 cursor 不等它（遠端、慢的檔案系統也一樣）。還在讀的時候，預覽框的
標題後面放 loading icon（跟 finder 的邊找邊列一樣），框裡寫灰字 `(loading…)`，metadata 的值先空著（不寫 `—`：`—` 是拿不到）；讀到了
再畫。讀過的照路徑記住，popup 開著時 cursor 回到同一筆不再讀。

| 種類 | 預覽 |
|---|---|
| 目錄 | 樹（見下面） |
| 壓縮檔（zip、tar、tar.gz、tar.bz2） | 照目錄的樹列出裡面 |
| 文字檔 | 內容，加語法顏色（chroma 的 catppuccin-mocha，只上前景色）與行號（Overlay0，靠右對齊、後面空一格）；Tab 與控制字元照 [`dialog/note`](../dialog/note-zh_TW.md) 的 viewer（Tab 畫成 `input_tab_width` 格空白、CRLF 的 `\r` 不畫、顏色碼照著上色、一行裡的 `\r` 只留最後的狀態、其他控制字元畫成 Red 的名字） |
| PDF | 第一列灰字寫頁數（`12 pages`），空一列，接前 20 頁的文字（最多 128 KB）；抽不出文字時寫 `(no extractable text)` |
| 圖片（png、jpg、gif、bmp、webp、tiff、ico、avif、heic） | 第一列灰字 `data:image/png · 12.4 KB`，空一列，接 base64 的 data URI，照預覽寬折行；超過 1 MB 時只寫 `(1.4 MB — too large to inline as a data URI)` |
| 其他 | 十六進位，一律一列 8 bytes，後面接 ASCII（`89 50 4e 47 0d 0a 1a 0a  .PNG....`，33 格）；並排時預覽最寬只有 56 格，放不下 16 bytes |
| 讀不到 | `(unreadable)` |

**目錄的樹**：最多三層。第一層不畫樹枝，第二層起用 `├─`、`└─`、`│` 連起來，樹枝 Overlay0；每一項前面的 icon、顏色、順序跟清單一樣，
隱藏檔不列。預覽拿不到 focus、不能捲，畫到預覽區滿為止，最後一列寫 `…`。空的目錄寫 `(empty)`，讀不到寫 `(permission denied)`，
都是灰字。

```
󰉋 keys
  ├─ 󰈔 a.pem
  └─ 󰉋 old
     └─ 󰈔 b.pem
󰈔 config
󰈔 id_ed25519.pub
…
```

一個子目錄會展開到底才輪到下一個：大的子目錄可能塞滿預覽區，看不到第一層後面的項目。

### file-picker.4 metadata

固定四列，檔案與目錄都一樣，換一筆時預覽區的高度不跳。label 大寫、層色，值 Text；label 欄寬取最長的 label，跟值隔兩格（跟
[`layout/panel`](../layout/panel-zh_TW.md) 的一列一個值一樣）。

| label | 檔案 | 目錄 |
|---|---|---|
| `TYPE` | 預覽的種類：`text`、`private key`、`image`、`PDF`、`archive`、`binary`；symlink 是 `link → <目標>` | `directory` |
| `SIZE` | `411 B`、`4.2 KB`、`3.4 MB`（1024 進位，一位小數） | `12 items`，一項時 `1 item`（跟清單一樣，不算隱藏檔） |
| `MODIFIED` | `2026-09-30 14:02`（本地時間，到分） | 同左 |
| `MODE` | `ls -l` 的寫法：`-rw-------` | `drwx------` |

- `private key`：第一行是私鑰的標頭（見下面）。跟 `hide_secrets_in_preview` 開不開無關，種類不是秘密。
- **symlink**：`SIZE`、`MODIFIED`、`MODE` 都寫**目標**的，跟預覽一致 —— 選下去拿到的就是它，`MODE` 也是真正有作用的權限。例：
  `/etc/localtime` 寫 `761 B`、`-rw-r--r--`，不是 link 本身的 `37 B`、`lrwxr-xr-x`（`ls -l` 的寫法）。是不是 link、指向哪裡，`TYPE` 已經寫了。
- **拿不到的值寫 `—`**：讀不到的目錄的 `SIZE`（數不出幾項；修改時間、權限照樣寫）；斷掉的 link 的 `SIZE`、`MODIFIED`、`MODE`；
  列出之後才不見的檔（被刪掉、搬走）拿不到的每一列。四列照樣固定，不少畫一列，也不寫成 `0 items`（會被讀成空的）。
- 不寫路徑（標題與清單已經有）、擁有者、存取與建立時間：選檔時用不到。

**為什麼**：選檔時要確認的是「是不是這個檔」—— 種類、大小、修改時間；權限對私鑰很重要（ssh 要求 `600`）。`TYPE` 跟預覽同一套分類，
看 `TYPE` 就知道預覽會畫什麼；寫法給人看，不寫 MIME 或八進位。

### file-picker.5 藏起秘密

使用者的設定 **`hide_secrets_in_preview`**，放在每個 app 的設定檔（Rules E3），預設 `false`：全部照常顯示。打開（`true`）時：

| 檔案 | 預覽 |
|---|---|
| 第一行是私鑰的標頭：開頭是 `-----BEGIN`、而且含有 `PRIVATE KEY`（OpenSSH、RSA、EC、PKCS#8、PGP），或開頭是 `PuTTY-User-Key-File-` | 露第一行，下面灰字 `(sensitive content not shown)` |
| 只有擁有者能讀的檔案（group、other 都沒有讀權限，例：`600`、`400`），什麼種類都一樣；目錄不算（`~/.ssh` 本身就是 `700`） | 一行都不露，只有那句灰字 |
| 其他 | 照常 |

metadata 不管開關都照常顯示。這個設定管的是 popup 的預覽：file-picker，與預覽檔案或目錄的 finder。

**為什麼**：在本地端的 TUI 裡，要不要藏由使用者決定（分享螢幕、錄 demo 時打開），預設不打擾。判斷不靠檔名清單（清單外的全漏）、
也不靠內容關鍵字（`password_min_length` 會誤擋、`pw:` 會漏掉）：私鑰看第一行，改了檔名也抓得到；其他秘密檔看權限 —— 只有擁有者
能讀是檔案的主人或工具自己標上的「別人不能看」（ssh 私鑰、`~/.aws/credentials`、`~/.kube/config`、`.netrc`、`.pgpass` 都是 `600`）。
誤判的方向是安全的：普通的檔被擋下來只是看不到預覽。私鑰的標頭本身不是秘密，露出來看得出是哪一種鑰匙。

## file-picker.6 按鍵

- **清單上按 `Enter`**：在目錄上是**進去** —— 打的篩選字清掉，focus 留在清單，cursor 停在 `..` 下面的第一項；在檔案上才是**選中**，
  寫回去、關掉。**選檔時目錄永遠不會被選中**（選目錄見下面）。
- **打字列打的字**：
  - 一般的字（`ed25`）：篩選目前這一層，照 [`finder`](finder-zh_TW.md) 的「比對」（包含、不分大小寫）。
  - 路徑（`/` 或 `~/` 開頭）：**路徑一直留在打字列上，以最後一個 `/` 切開** —— 前面是目錄（清單列出它、標題寫它），後面是篩選字
    （照「比對」）。路徑打到一半也有用，打字與貼上的結果一樣：

    | 打的字 | 清單 |
    |---|---|
    | `~/.ss` | 列出 `~`、篩 `.ss`：留下 `.ssh`（`Enter` 到清單、再 `Enter` 進去） |
    | `~/.ssh/` | 整個 `~/.ssh` |
    | `~/.ssh/id_` | `~/.ssh` 裡的 `id_ed25519`、`id_ed25519.pub` |
    | `~/.ssh/id_ed25519` | 那個檔在第一列（`Enter` 到清單、再 `Enter` 選中） |
    | `~/nope/x` | 目錄不存在：清單是空的，跟「沒有結果」一樣 |

    **路徑裡不支援 `..`**：有 `..` 這一段時不往上解析，當成不存在的目錄，清單是空的。往上走用清單的 `..` 列，或用 `Backspace`
    刪掉路徑的最後一段。
  - 有 `*`、`?`：wildcard。`*` 只比對同一層，`**` 往下找所有子目錄（一般 shell glob 的規則）：`~/Downloads/*.png` 列出 Downloads 裡
    所有的 png，`~/.ssh/**/*.pem` 找出 `.ssh` 底下所有的 pem。每一列寫相對於起點的路徑（起點是第一個 `*`、`?` 前面的目錄；例：
    `keys/a.pem`、`old/b.pem`），標題寫起點；結果是搜尋出來的、不是一層目錄，沒有 `..`。
- **hint**：清單上，在目錄是 `Enter:into Tab|/:filter Esc:cancel`、在檔案是 `Enter:choose Tab|/:filter Esc:cancel`；打字列 `Enter|Tab:list Esc:cancel`。

**為什麼**：這個欄位要的是檔案；在目錄上按 `Enter`，最直觀的動作是進去看裡面。目錄寫在標題，打字列就能留給篩選。路徑留在打字列上、
以最後一個 `/` 切開，清單永遠列出打字列上的那個目錄，不用另外定「什麼時候跳過去」：一個字一個字打 `~/Documents/sideproj`，不會打到
`~/Documents` 就跳走、清空，再把接著打的 `/sideproj` 當成根目錄底下的路徑；`Backspace` 刪掉最後一段就退回上一層。

## file-picker.7 選目錄

值是目錄的欄位（例：下載到哪裡、專案的路徑）用 file-picker 的「選目錄」。其他都照上面：標題寫目前的目錄、打字列打路徑、隱藏目錄的
規則、預覽畫 cursor 那一列的目錄樹、metadata 四列。

```
┏━DOWNLOAD TO · ~/Downloads━━━━━━━━━━━━━━━━┓ ┏━Downloads━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                            ┃ ┃                                             ┃
┃                                       4/4 ┃ ┃ 󰉋 music                                     ┃
┃ ────────────────────────────────────────── ┃ ┃   ├─ 󰈔 a.flac                               ┃
┃▓󰉒▓. (this directory)▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃ ┃   └─ 󰈔 b.flac                               ┃
┃ 󰉋 ..                                       ┃ ┃ 󰉋 papers                                    ┃
┃ 󰉋 music                                    ┃ ┃   └─ 󰈔 tdp.pdf                              ┃
┃ 󰉋 papers                                   ┃ ┃ 󰈔 invoice.pdf                               ┃
┃                                            ┃ ┃ 󰈔 photo.jpg                                 ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃                                             ┃
┃                                            ┃ ┃ ─────────────────────────────────────────── ┃
┃                                            ┃ ┃ TYPE      directory                         ┃
┃                                            ┃ ┃ SIZE      4 items                           ┃
┃                                            ┃ ┃ MODIFIED  2026-10-12 21:40                  ┃
┃                                            ┃ ┃ MODE      drwxr-xr-x                        ┃
┃                                            ┃ ┃                                             ┃
┗━ Enter:choose Tab|/:filter Esc:cancel ━━━━━┛ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- **清單只列目錄**，檔案不列：目錄裡有什麼，看預覽的樹。順序是 `.` → `..` → 目錄。
- **最上面一列是 `.`**（`. (this directory)`），icon 是 `nf-md-folder_move`（U+F0252）；其他目錄的 icon 照舊。在 `.` 上按 `Enter` 選
  目前這個目錄 —— 寫回去、關掉；在其他目錄上按 `Enter` 走進去，跟選檔一樣。
- **打字列上有篩選字或 wildcard 時，`.` 那一列不出現**：wildcard 的結果只列目錄、沒有 `.`（跟沒有 `..` 一樣）。在結果的目錄上
  `Enter` 走進去，那一層的 `.` 就回來；要選目前的目錄，清掉篩選字（或把路徑打到 `/` 結尾）。
- **hint**：在 `.` 上 `Enter:choose Tab|/:filter Esc:cancel`，在目錄上 `Enter:into Tab|/:filter Esc:cancel`。

**為什麼**：`Enter` 在選檔與選目錄裡都是「走進目錄」，不用另外學一個「選這個目錄」的鍵；清單最上面已經有 `..`（上一層），再加一列
`.`（這一層）很好懂。檔案不列：清單留給選得到的東西，要確認選對了，看預覽。

# terminu design

**Language**: [English](README.md) · 繁體中文

**不看文件就能用的 terminal UI。**

terminu design 是一套 terminal UI 的設計語言：一組跨畫面、跨 app 意義不變的按鍵，
加上兩個永遠找得到的入口 —— `Space` 告訴你「這裡能做什麼」，`?` 告訴你「整個 app
能做什麼」。學一次，家族裡每個 app 都一樣。

---

## 六個鍵

| 鍵 | 意義 |
|---|---|
| `Tab` | 換到同一層的下一塊：panel 之間、表單欄位之間 |
| `Enter` | 對選中的東西做那件理所當然的事；在表單裡是送出 |
| `Esc` | 取消、關掉最上層，一次一層，永遠不會把 app 關掉 |
| `Space` | 這裡能做什麼 |
| `?` | 整個 app 能做什麼；在 popup 裡是這個框怎麼用 |
| `q` | 離開 app（`Ctrl-C` 也是） |

迷路了就按 `Space`。

## 設計精神

- **揭露，而不是文件。** 使用者能做的每件事，都在一個按得出來、可以直接執行的清單裡。
- **操作分三種範圍。** 對這一項（item）、對這一塊（panel）、對整個 app（global）——
  menu 永遠照這個順序排。
- **一個元素、一個意義。** 一個顏色、一個鍵、一種框線，只代表一件事。
- **規則服務 UX。** 規則擋住了好的 UX 時，擴充規則，而不是犧牲 UX。
- **固定的與交給 app 的分清楚。** core key 的行為寫死；其餘只規定要達成什麼，
  怎麼做由各 app 決定；配色與熱鍵是可以直接套用的家族預設。

完整內容在 **[terminu design principle（tdp）](principle/README-zh_TW.md)**：

| | |
|---|---|
| [Principle](principle/README-zh_TW.md) | 精神：要達成什麼、為什麼 |
| [Rules](principle/rules-zh_TW.md) | 必須遵守的規則，每條附理由，分固定區與概念區 |
| [Family defaults](principle/defaults-zh_TW.md) | 通用預設建議：色彩系統、popup、menu、熱鍵參考、文件骨架 |

## terminu family

| App | 是什麼 |
|---|---|
| [kbu](https://github.com/vulcanshen/kbu) | Kubernetes TUI dashboard |
| [filu](https://github.com/vulcanshen/filu) | 不用學的 terminal 檔案管理員 |
| [sshu](https://github.com/vulcanshen/sshu) | ssh 與 sftp 的 terminal 前端 |
| [webu](https://github.com/vulcanshen/webu) | 把網頁當文件讀的 terminal 瀏覽器 |
| [locku](https://github.com/vulcanshen/locku) | 帶 PIN 鎖的 terminal 螢幕保護程式 |

## 歷史

terminu design 的前身是 VTP，一份先長在 kbu 裡、後來抽出來的 TUI 設計原則。
它怎麼一路演變成現在的樣子，記錄在 [vtp/](vtp/)。

## License

[CC BY 4.0](LICENSE)

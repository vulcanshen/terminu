# radio（幾個選一個）

**Language**: [English](radio.md) · 繁體中文

## 用途

幾個選一個，選項五個以內：直接畫在表單或 panel 上（[`dialog/form`](../dialog/form-zh_TW.md) 的「選項畫在表單上」）。超過五個用
[`select`](select-zh_TW.md)。

**一個開關也可以畫成 radio**：`off`、`on` 兩個選項，跟 [`checkbox`](checkbox-zh_TW.md) 二選一，由 app 選（例：ccdrawu 的 Drawer，
跟同一頁 `off`、`on`、`on when narrow` 的設定排法一樣）。

**為什麼**：`off`、`on` 兩個狀態都寫出來，比一個勾直觀；同一頁有多個選項的同類設定時，開關跟著畫成 radio，排法也一致。

## 長相

```
Auth        󰐾 password
            󰐽 privatekey
            󰐽 credential
```

- glyph：選中 `nf-md-radiobox_marked`（U+F043E）、沒選 `nf-md-radiobox_blank`（U+F043D）。select 也用這一組。
- 選中那一個的字是 Green（生效中），其他是 Text。
- 一律直排，一個選項一列：focus 色塊從選項一直到框，橫排時會蓋住後面的選項、看不出它們選了沒；也不留給 app 判斷「多短算可以橫排」。

## 按鍵

- 每個選項是一個項目，`j|k`（或 `h|l`）在選項之間移（Rules K12）。
- `Enter`：選它，focus 不動，馬上生效。

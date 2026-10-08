# radio（幾個選一個）

**Language**: [English](radio.md) · 繁體中文

## 用途

幾個選一個，選項五個以內：直接畫在表單或 panel 上（[`dialog/form`](../dialog/form-zh_TW.md) 的「選項畫在表單上」）。超過五個用
[`select`](select-zh_TW.md)。

## 長相

```
Auth        󰐾 password
            󰐽 privatekey
            󰐽 credential
```

- glyph：選中 `nf-md-radiobox_marked`（U+F043E）、沒選 `nf-md-radiobox_blank`（U+F043D）。select 也用這一組。
- 選中那一個的字是 Green（生效中），其他是 Text。
- 預設直排；選項都很短、一列放得下時，可以橫排（`󰐾 asc  󰐽 desc`）。

## 按鍵

- 每個選項是一個項目，`j`/`k`（或 `h`/`l`）在選項之間移（Rules K12）。
- `Enter`：選它，focus 不動，馬上生效。

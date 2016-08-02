# ページの構造とレイアウト
## 36. 内在的なサイズ設定

```html
<p>Some Text [...]</p>
<figure>
  <img src="path/to/image"/>
  <figcaption>
    The great Sir Adam Catlace was named after
    Countess Ada Lovelace, the first programmer.
  </figcaption>
</figure>
<p>More text [...]</p>
```

```css
figure {
  max-width: 300px;
  max-width: min-content;
  margin: auto;
}

figure > img {
  max-width: inherit;
}
```

:arrow_forward: [Intrinsic sizing](http://dabblet.com/gist/82eb1575806f6eff9c37)
:arrow_forward: [Design From the Inside Out With CSS Min-Content](http://thenewcode.com/662/Design-From-the-Inside-Out-With-CSS-MinContent)

## 37. テーブルの列幅を自在に指定する
テーブルを行儀よくふるまわせる方法はあるのでしょうか
### 解決策
- `table-layout: fixed` を指定すると、より予測しやすいレイアウトが行われるようになります

```css
table {
  table-layout: fixed;
  width: 100%;
}
```

:arrow_forward: [Taming table column widths](http://dabblet.com/gist/7979af102a991cecfcdf)
:arrow_forward: [Fixed Table Layout](https://css-tricks.com/fixing-tables-long-strings/)

## 38 兄弟要素の個数にもとづくスタイル指定



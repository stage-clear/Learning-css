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

## 38. 兄弟要素の個数にもとづくスタイル指定
### 解決策

```css
li:only-child {
  /* 項目が1つだけの場合に適用されるスタイル */
  /* li:first-child:last-child と同義 */
  /* li:first-child:nth-last-child(1)  */
}

li:first-child:nth-last-child(4),
li:first-child:nth-last-child(4) ~ li {
  /* 項目数が4つのリストで、各項目に適用されるスタイル */
}
```

```scss
// mixin 
@mixin n-items($n) {
  &:first-child:nth-last-child($n),
  &:first-child:nth-last-child($n) ~ & {
    @content;
  }
}

// usage
li {
  @include n-items(4) {
    /* properties and values */
  }
}
```

:arrow_forward: [styling-sibiling-count](http://dabblet.com/gist/70c434a6e802b062f494)

### 項目数の範囲を指定して選ぶ

> ここでの __n__ はゼロから（理論上は）正の無限大まで1つずつ増加していく変数を表します

```css
li:first-child:nth-last-child(n+4),
li:first-child:nth-last-child(n+4) ~ li {
  /* 項目数が4つ以上のリストで、各項目に適用される
   * [ ] [ ] [ ] 
   * [ ] [ ] [ ] [✔︎]
   * [ ] [ ] [ ] [✔] [✔] [✔] [✔]
   */
}
```

```css
li:first-child:nth-last-child(-n+4),
li:first-child:nth-last-child(-n+4) ~ li {
  /* 項目数が4つ以下のリストで、各項目に適用されるスタイル 
   * [✔] [✔] [✔]
   * [✔] [✔] [✔] [✔]
   * [ ] [ ] [ ] [ ] [ ] [ ]
   */
}
```

```css
li:first-child:nth-last-child(n+2):nth-last-child(-n+6),
li:first-child:nth-last-child(n+2):nth-last-child(-n+6) ~ li {
  /* 項目数が2つ以上6つ以下で、各項目に適用されるスタイル
   * [ ]
   * [✔] [✔] [✔]
   * [✔] [✔] [✔] [✔] [✔] [✔]
   * [ ] [ ] [ ] [ ] [ ] [ ] [ ]
   */
}
```

## 39. 流動的な幅の背景と固定幅のコンテンツ
### 課題

```html
<footer>
  <div class="wrapper">

  </div>
</footer>
```

```css
footer {
  background: #333;
}

.wrapper {
  max-width: 900px;
  margin: 0 auto;
  /* margin: 1em calc(50% - 450px); clac を使うと */
}
```

### 解決策
```html
<footer>

</footer>
```

```css
footer {
  /* max-width: 900px; */
  padding: 1em; /* 後方互換正 */
  padding: 1em calc(50% - 450px); /* 450px = 900 ÷ 2 */
  background: #333;
}
```

:arrow_forward: [Fluid background, fixed content](http://dabblet.com/gist/763229b68fa27c5c1bfa)

## 40. 縦方向の中央揃え
```html
<main>
  <h1>Am I centered yet?</h1>
  <p>Center me, Please!</p>
</main>
```

### 絶対位置指定を使った解決策
もっとも古いテクニックは以下のようなものです

```css
main {
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -3em; /* 6 ÷ 2 = 3 */
  margin-left: -9em; /* 18 ÷ 2 = 9 */
  width: 18em;
  height: 6em;
}
```

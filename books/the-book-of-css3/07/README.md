# 段組み

[CSS Multi-column Layout モジュール](http://www.w3.org/TR/css3-multicol/)


## 7.1 カラムのレイアウト方法

コンテンツを複数カラムへと分割する方法は2つあります。

1. カラムの数を厳密に指定します
2. カラムの数についてはブラウザに任せます


### 7.1.1 `column-count` カラム数の厳密な指定

__基本構文__

```css
E {
  column-count: [columns];
}
```

__簡単な例__

```css
div {
  column-count: 2;
}
```

__より具体的な例__

```css
div[class*='-2'] { column-count: 2; }
div[class*='-3'] { column-count: 3; }
```

```html
<div class="column-2">
  <p>A young man...</p>
</div>
<div class="column-3">
  <p>A young man...</p>
</div>
```

### 7.1.2 `column-width` 動的なカラム指定

- より柔軟なレイアウトの指定
- `column-width` プロパティを使ってそれぞれのカラムの幅を指定します

__基本構文__

```css
E {
  column-width: [lenght];
}
```

__簡単な例__

```css
div {
  colomn-width: 150px;
}
```

__より擬態的な例__

```css
.columns {
  column-width: 150px;
  width: 710px;
}
```

### 7.1.3 各カラムへのコンテンツの分配

- デフォルトでは、段組みされたコンテンツは可能な限り各カラムに等分されます

```css
E {
  column-fill: [keyword]; /* balance | auto */
}
```

`auto` に指定した場合、`column-count` で指定したのとは異なるカラム数となることがあります


### 7.1.4 `column-count` と `column-width` の併用

- 同じ要素に `column-count` と `column-width` をともに指定することも可能です
- 実はここでの `column-count` は__最大値__として機能します

```css
.columns {
  column-count: 3;
  column-width: 150px;
}
```

__短縮記法__

```css
E {
  columns: [column-width] [column-cont]
}
```

__短縮記法の記述例__

```css
div {
  columns: 150px 3;
}
```


## 7.2 カラム間の余白と区切り線

- カラム数を指定したレイアウトでは、各カラムの間に幅 `1em` の余白が置かれます
- デフォルトを変更するために `column-gap` と　`column-rule` が用意されています

__基本構文__

```css
E {
  column-gap: [length];
}
```

__簡単な例__

```css
div {
  column-gap: 2em;
}
```

- `column-rule` を指定すると、各カラムの中間に線が表示されます

__基本構文__

```css
E {
  column-rule-width: [length];
  column-rule-style: [border-style];
  column-rule-color: [color];
}
```

__簡単な例__

```css
div {
  column-rule-width: 0.3em;
  column-rule-style: double;
  column-rule-color: silver;
}
```

__短縮記法__

```css
.columns {
  column-rule: 0.3em double silver;
}
```


## 7.3 カラム内の要素

- カラム幅を超える大きな要素（画像など）が含まれた場合どうなるか
- この問題への対策として `max-width: 100%` というものがあります


## 7.4 複数カラムにまたがる要素

- 場合によっては特定の要素を複数のカラムにまたがって表示させたいということも考えられます
- 例えば、記事の小見出しごとにダングムをやり直すといったケース

```css
E {
  column-span: [value];
}
```

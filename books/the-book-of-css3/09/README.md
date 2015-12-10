# ボーダーとボックスの効果

## 9.1 ボーダーの角を丸める

![border-radius](https://developer.mozilla.org/files/3638/border-radius-sh.png)

__基本構文__

```css
/*
 * border-radius
 * v : [top | bottom]
 * h : [left | right]
 *
 */
E {
  border-[v]-[h]-radius: [x] [y];
}
```

__簡単な例__

```css
div {
  border-top-right-radius: 20px 20px;
}
```

__四隅を丸める__

```css
div {
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
  border-bottom-right-radius: 20px;
  border-bottom-left-radius: 20px;
}
```

__非対称な曲線__

```css
div {
  border-top-left-radius: 10px 20px;
  border-top-right-radius: 10px 20px;
  border-bottom-left-radius: 10px 20px;
  border-bottom-right-radius: 10px 20px;
}
```

### 9.1.1 `border-radius` を使った短縮記法

```css
/* 値が4つ */
E {
  border-radius: [top-left] [top-right] [bottom-right] [bottom-left];
}
/* 値が3つ */
E {
  border-radius: [top-left] [top-right & bottom-left] [bottom-right];
}
/* 値が2つ */
E {
  border-radius: [top-left & bottom-right] [top-right & bottom-left];
}
/* 値が1つ */
E {
  border-radius: [top-left & top-right & bottom-right & bottom-left]
}
```

__短縮記法で非対称な曲線__

```css
E {
  border-radius: [horizontal-radius] / [vertical-radius];
}
```


### 9.1.2 パーセンテージを使った設定

- どんな大きさの要素でも `50%` と指定すれば円形や楕円形のボーダーになります

```css
div {
  border-radius: 50%;
  height: 100px;
}
.ellipse { width: 200px; }
.circle { width: 100px; }
```


## 9.2 画像を使ったボーダー

### 9.2.1 `border-image-source`

__基本構文__

```css
E {
  border-image-source: url('foo.png');
}
```

### 9.2.2 `border-image-slice`

```css
E {
  border-image-slice: [value] [fill];
}
```


### 9.2.3 `border-image-width`

- スライスの太さは `border-width` の太さにより伸縮します
- このふるまいは `border-iamge-width` を使って変更できます
- このボーダーは表示のみで、ボックスモデルには影響しません

```css
E {
  border-image-width: [value];
}
```


### 9.2.4 `border-image-outset`

ボーダーの画像はボーダーを表すボックスの外周から始まって内側へと描画されていきます。この描画の開始位置は、ボーダーのボックスよりも外側に変更できます。

```css
E {
  border-image-outset: 15px 30px;
}
```


### 9.2.5 `border-image-repeat`

ボーダーの各辺に表示される際の描画方法を指定できます

```css
E {
  border-image-repeat: [keyword];
}
```


### 9.2.6 `border-image` を使った短縮記法

```css
E {
  border-image: [source] [slice]  / [width] / [outset] [repeat]
}
```


## 9.3 ドロップシャドウ

```css
/*
 * box-shadow
 * inset 影が要素の内側か外側か (省略可能)
 * [horizontal] 左右方向の影の距離
 * [vertical] 上下方向の影の距離
 * [blur-radius] ぼかしの半径 (省略可能)
 * [spread] 影が広がる距離 (省略可能)
 * [color] 影の色
 */
E {
  box-shadow: inset [horizontal] [vertical] [blur-radius] [spread] [color];
}
```

## 9.4 内側の影

- `box-shadow` に `inset` を追加


## 9.5 まとめ

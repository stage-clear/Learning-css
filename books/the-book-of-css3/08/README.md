# 背景画像

[CSS Backgrounds and Borders モジュール](http://www.w3.org/TR/css3-background/)


## 8.1 既存のプロパティへの変更

CSS3のモジュールの多くは新たなプロパティあるいは概念を定義していますが、CSS Backgrounds and Borders モジュール
の強みは既存のプロパティを強力で使いやすいものへと拡充しているところです。


### 8.1.1 `background-position`

CSS3では、このプロパティに最大4つの値を指定できるようになりました。辺とともに、そこから
の距離を表す長さまたはパーセンテージを指定できます。

```css
.foo {
  background-position: right 10em bottom 50%;
}
```

### 8.1.2 `background-attachment`

CSS2.1 では `scroll` と `fixed` のいずれかを指定できました。
CSS3 では、`local` という新しい値が追加されました。
これを指定すると、背景画像は適用対象の要素とビューポートの双方に対して連動するようになります。


### 8.1.3 `background-repeat`

CSS2.1 では、 `no-repeat` `repeat` `repeat-x` `repeat-y` のいずれかを指定できました。
CSS3 では、2つのキーワードが追加されました。

- `space` : 適用対象の要素からはみ出ない範囲で画像が繰り返し表示されます。それぞれの画像の間には同じ大きさの余白が追加されます
- `round` : 画像がはみ出ないように繰り返されますが、余白を追加する代わりに画像が拡大縮小されます。

```css
.space {
  background-repeat: space;
}
.round {
  background-repeat: round;
}
```

上下方向と左右方向で、それぞれ異なる繰り返し方法を指定できるようになりました。

```css
.foo {
  background-repeat: round space;
}
```


## 8.2 複数の背景画像

それぞれ背景画像ごとにレイヤーが用意され、`background-*` プロパティを個別に指定できます

```css
E {
  background-image: [value], [value];
}
```

__簡単な例__

```css
h2 {
  background-image: url('monkey.svg'), url('landscape.jpg');
  background-position: 95% 85%, 50% 50%;
  background-repeat: no-repeat;
}
```

__短縮記法__

```css
h2 {
  background:
    url('monkey.svg') no-repeat 95% 85%,
    url('landscape.jpg') no-repeat 50% 50%;
}
```

`background-color` だけは複数値を指定できず、最も下にあるレイヤーのものが適用されます。


## 8.3 画像サイズの動的な変更

CSS3 では `background-size` という新しいプロパティも追加されています。
`value` には、長さまたはパーセンテージを1つか2つ指定できるほか、定められたキーワードを指定することもできます。

__基本構文__

```css
E {
  background-size: [value];
}
E {
  background-size: [width] [height];
}
E {
  background-size: [keyword];
}
```

- `contain` : 背景画像と対象の要素の高さが一致
- `cover` : 背景画像と対象の要素の幅が一致


## 8.4 `background-clip` と `background-origin`

__`background-clip`__

背景の色や画像が表示される範囲をボックスモデルとして指定します。

```css
E {
  background-clip: [box];
}
```

- `border-box` : ボーダーの背後まで背景を描画
- `padding-box` : ボーダーの直前まで背景を描画
- `content-box` : `padding` の内周まで背景を描画


__`background-origin`__

背景を描画する際の起点を指定できます。

```css
E {
  background-origin: [box];
}
```

- `border-box` : ボーダーの外周を起点とする
- `padding-box` : ボーダーの内周を起点とする
- `content-box` : `padding` の内周を起点とする


## 8.5 `background` プロパティを使った短縮記法の変更

`background` プロパティは、`background-size` と `background-origin` そして `background-clip` の各プロパティの値も含められるように変更されました

`background-size` は、対応する `background-position` の直後に `/` で区切って記述します


__短縮記法の例__

```css
/* background-size */
E {
  background: url('bar.png') no-repeat 50% 50% / 50% auto;
}
/* background-clip background-origin */
E {
  background: url('bar.png') no-repeat padding-box content-box;
}
```

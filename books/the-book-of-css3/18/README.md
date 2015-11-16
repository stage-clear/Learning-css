# ブレンドモード、フィルター効果、マスキング

- CSSから利用できるSVGの機能が3つあります
- ブレンドモード、フィルター効果、マスキング
- これらは非破壊的な効果であり、元の画像を改変することなくページ上に対してのみ作用します


## 18.1 ブレンドモード

CSSで利用可能なブレンドモードのリストは [Compositing and Blending モジュール](https://drafts.fxtf.org/compositing/) で定義されています

- [Getting to Know CSS Blend Modes](https://dev.opera.com/articles/getting-to-know-css-blend-modes)


### 18.1.1 `background-blend-mode`

- デフォルト値: `normal`
- 要素の背景にあるレイヤーをブレンドするために使われます
- 対象の要素が持つ背景レイヤーだけがブレンドされます
- このプロパティは要素というコンテキストの中でのみ機能します
- 要素自体は他のどの部分ともブレンドされません

```css
E {
  background-blend-mode: multiply;
}
```

#### 18.1.1.1 背景画像と背景色のブレンド

背景画像と背景色を指定しブレンドモードを適用します。

```css
E {
  background: url(foo.png) #f00;
  background-blend-mode: screen;
}
```

#### 18.1.1.2 2つの画像のブレンド

複数の背景画像を指定しブレンドモードを適用します。

```css
E {
  background-color: transparent;
  background-image: url(foo.png), url(bar.png);
  background-blend-mode: multiply;
}
```

### 18.1.1.3 複数回のブレンド

`foo.png` に `multiply` が適用され、その後 `bar.png` に `screen` が適用される

```css
# {
  background-color: #fff;
  background-image: url(foo.png), url(bar.png);
  background-blend-mode: multiply, screen;
}
```

### 18.1.2 `mix-blend-mode`

- ある要素と別の要素をブレンドする
- 指定された要素の背後にあるすべての要素に対してコンテンツや背景がブレンドされます


```css
E {
  background-image: url(foo.png);
}
F {
  mix-blend-mode: multiply;
}
```

### 18.1.3 isolation

- デフォルト値: `auto`
- 対象の要素でスタックコンテキストを指定します（レイヤーの最背面をリセットする）
- [スタック文脈](https://developer.mozilla.org/ja/docs/Web/Guide/CSS/Understanding_z_index/The_stacking_context)
- 新しいスタックコンテキストを作成するには、`isolate` という値を指定します

```css
E {
  isolation: isolate;
}
```


## 18.2 フィルター効果

- 要素が描画される前にその外見を変化させるための仕組み
- 加工の際に他のコンポーネントの影響を受けないという点は、ブレンドモードと異なります
- [Filter Effects Modules](http://www.w3.org/TR/filter-effects/) で定義され、`filter` プロパティを使います

```css
E {
  filter: FUNCTION;
}
```

### 18.2.1 `blur()`

- 要素に対してぼかしの効果を適用します
- ぼかしの半径を単位つきの値で指定します
- この効果はガウスぼかしと呼ばれ、画像のノイズを減らすために使われます

```css
E {
  filter: blur(10px);
}
```

### 18.2.2 `brightness()` と `contrast()`

- `brightness()` は要素の明るさを変更し、`contrast()` は要素の明るい部分と暗い部分のコントラストを変更します。
- どちらの要素も `100%` ではまったく変化しません
- `brightness()` に `0%` を指定すると真っ黒になり、`contrast()` に `0%` を指定すると完全なグレーになります
- `100%` 以上を指定して明るさやコントラストを増加させることもできます
- 単位なしでも指定でき、`1` は `100%` を意味し、`1.5` は　`150%` を意味します

```css
E {
  filter: brightness(50%);
}
E {
  filter: contrast(50%);
}
```

### 18.2.3 `grayscale()` `sepia()` `saturate()`

- この3つは色に関する関数です
- `grayscale()` を使うとすべての色がグレーの濃淡で表現され、白黒の画像になります
- `sepia()` も `grayscale()` と似ていますが、ゴールド系の色によって古い写真のような効果を得られます
- `saturate()` は色の強さをコントロールするために使われます

```css
/**
 * grayscale()
 * 100% を指定すると、画像は完全な白黒になります
 */
E {
  filter: grayscale(100%);
}

/**
 * sepia() 
 * 100% を指定すると、完全なセピア調になります
 */
E {
  filter: sepia(100%);
}


/**
 * saturate()
 * 値の意味は他とは異なります
 * 0% を指定すると彩度は完全になくなりグレースケールになります
 * 100% 以上をしていすると過剰な彩度の画像になります
 */
E {
  filter: saturate(200%);
}
```

### 18.2.4 `hue-rotate()`

- 要素の色相を回転によって変換します

```css
E {
  filter: hue-rotate(45deg);
}
```

### 18.2.5 `opacity()`

- `100%` 以上を指定しても `100%` とみなされます

```css
E {
  filter: opacity(25%);
}
```

__なぜ opacity プロパティとは別に opacity() が用意された？__

他のフィルターとの組み合わせを可能にするためです。


### 18.2.6 `drop-shadow()`

- 引数は `box-shadow` と同じ
- `box-shadow` とは違い、画像の__輪郭__に沿って影が表示されます

```css
E {
  filter: drop-shadow(5px 5px 3px gray);
}
```

### 18.2.7 複数のフィルターの組み合わせ

- フィルターのリストをスペース区切りで記述するだけで、簡単に複数のフィルターを適用できます
- 関数を記述する順序は重要で、指定された順番に、それぞれ関数が適用されていきます

```css
E {
  filter: blur(5px) drop-shadow(5px 5px 3px gray);
}
```

- フィルターが複数回指定されると先に指定されたものはデフォルト値に戻ります

```css
E {
  filter: sepia(100%) blur(2px);
}
E:hover {
  filter: blur(5px);
}
```


### 18.2.8 SVG を使ったフィルターの記述

- CSS のフィルターは、SVG でのいくつかのフィルターを簡単に呼び出せるようにしたものにすぎません
- Filter Effects オジュールで、CSS のそれぞれの関数を SVG のマークアップとして表現した例が紹介されています

__例) blur() 関数をSVGで書く場合__

`blur-radius` には単位なしの値が指定されます

```xml
<filter>
  <feGaussianBlur stdDeviation="blur-radius">
</filter>
```

__例) SVG を使ってフィルターを自分で定義し、CSS の中から ID 値を通じで参照する__

```xml
<filter id="blur">
</filter>
```

```css
E {
  filter: url(#blur);
}


/**
 * SVG が外部のファイルに記述されているなら、
 * そのパスに続けてID値を指定します 
 */
E {
  filter: url(filters.svg#blur);
}
```


## 18.3 マスキング

- マスキングとは、要素の一部を隠して表示されないようにすることを意味します
- マスキングには、クリッピングとイメージマスキングという2つのアプローチがあります
- クリッピングでは、非表示にする領域を図形として要素に重ね合わせるのに対し、イメージマスキングでは画像のアルファチャンネルを使って非表示の領域を指定します


### 18.3.1 クリッピング

- クリッピングはイメージマスキングよりもシンプルです
- [clip-path | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/clip-path)

```css
E {
  clip-path: [shape];
}
```

- `shape` では形状を関数として指定します。
- 基本的な形状は4種類あり( `circle()` `ellipse()` `inset()` `polygon()` )、円、楕円、長方形、多角形を表します

__円__

```css
/**
 * circle()
 * @param {Number} r 円の半径
 * @param {Number} cx 円の中心のX座標
 * @param {Number} cy 円の中心のY座標
 */
E {
  clip-path: circle([r] at [cx] [cy]);
}
```

__楕円__

```css
/**
 * ellipse()
 * @param {Number} rx X軸方向の半径
 * @param {Number} ry Y軸方向の半径
 * @param {Number} cx 楕円の中心のX座標
 * @param {Number} cy 楕円の中心のY座標
 */
E {
  clip-path: ellipse([rx] [ry] at [cx] [cy]);
}
```

__長方形__

```css
/**
 * inset()
 * @param {Number} o1 上辺からの距離
 * @param {Number} o2 右辺からの距離
 * @param {Number} o3 下辺からの距離
 * @param {Number} o4 左辺からの距離
 * @param {Number} r 角の丸み
 */
E {
  clip-path: inset([o1] [o2] [o3] [o4] round [r]);
}
```

![clip-path](https://cdn.css-tricks.com/wp-content/uploads/2011/09/clip-visual.jpeg)

__多角形__

```css
/**
 * polygon()
 * @param {nx} パス上の点 n のX座標
 * @param {ny} パス上の点 n のY座標
 */
E {
  clip-path: polygon(0% 100%, 100% 0%, 0% 0%);
}
```

### 18.3.1.1 Safari での `clip-path` の実装

- Safari はバージョン7 で、ベンダー接頭辞つきで `clip-path` プロパティを実装しました
- しかし、ここでは古い構文が使われています（Safari 8 ではより新しい構文が実装されました）

```css
/* circle() */
E {
  -webkit-clip-path: circle([cx], [cy], [r]);
}

/* ellipse() */
E {
  -webkit-clip-path: ellipse([cx], [cy], [rx], [ry]);
}

/* inset() は inset-rectangle() とう名前になっている */
E {
  -webkit-clip-path: inset-rectangle([o1], [o2], [o3], [o4]);
  /* 角を丸める場合 */
  -webkit-clip-path: inset-rectangle([o1], [o2], [o3], [o4], [rx], [ry]);
}

/* 最大の違いは rectangle() 関数です */
E {
  -webkit-clip-path: rectangle([x], [y], [w], [h], [rx], [ry]);
}
```


#### 18.3.1.2 クリップパスのトランジション

- クリップパスは数値として表現されるため、この値を変えるトランジションを定義して印象的な効果を発生することができます

```css
E {
  clip-path: polygon(0% 0%, 0% 100%, 100% 0);
  transition: clip-path 1s;
}
E:hover {
  clip-path: polygon(100% 100%, 0% 100%, 100% 0);
}
```

#### 18.3.1.3 SVG を使ったクリップパスの定義

```xml
<xml>
  <defs>
    <clipPath id="clipping">
      <circle cx="0.5" cy="0.5" r="0.5" />
    </clipPath>
  </defs>
</xml>
```

```css
E {
  clip-path: url(#clipping);
}
```

この方法は参考書籍執筆時点では Firefox しか対応しておらず、アニメーションを行う場合には JavaScript の助けが必要です


### 18.3.2 イメージマスキング

- ある画像を使ってもう1つの画像をマスキングする
- [Mask - CSS](https://developer.mozilla.org/ja/docs/Web/CSS/mask)

```css
/**
 * mask
 * 主なプロパティ
 * @param {url} [image] マスキングに使われる画像
 * @param {Number|keyword} [position] (background-position と同様)
 * @param {Number|keyword} [size] (background-size と同様) 
 */
E {
  mask: [image] [position] / [size];
}

/**
 * mask
 * すべてのプロパティ
 * @param {} mode マスキングにアルファチャンネルを使うかそれとも明度を使うか
 * @param {} repeat (backgrond-repeat と同様)
 * @param {} origin (backgrond-origin と同様)
 * @param {} clip (background-clip と同様)
 * @param {} composite 複数の画像を使ってマスキングする場合の重なり有った部分の処理方法
 */
E {
  mask: [image] [mode] [position] / [size] [repeat] [origin] [clip] [composite];
}
```

__例)__

```css
E {
  mask: url(masi.png) 50% 50% / 100% auto;
}
```


### 18.3.3 ボーダーのマスキング

```css
E {
  mask-border: url(mask.png) 40px repeat;
}
```

- 参考書籍執筆時点で仕様に準拠しているブラウザはありません


### 18.3.4 SVG を使ったマスキング

```xml
<xml>
  <defs>
    <mask id="masking">
      <rect y="0.3" width="1" height=".7" fill="black" />
      <circle cx=".5" r=".35" fill="white" />
    </mask>
  </defs>
</xml>
```

```css
E {
  mask: url(#masking);
}
```

- [CSS Masking](http://www.html5rocks.com/en/tutorials/masking/adobe/?redirect_from_locale=ja)


## 18.4 フィルター効果とマスキングの併用

```css
E {
  clip-path: circle(50% at 50% 50%);
  filter: drop-shadow(5px 5px black);
}
```

`drop-shadow` が消えてしまう。これを避けるには

```css
/* 親要素 */
D {
  filter: drop-shadow(5px 5px black);
}
/* 子要素 */
E {
  clip-path: circle(50% at 50% 50%);
}
```

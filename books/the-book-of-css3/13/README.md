# 3次元の変形

## 13.1 CSSでの3次元の要素

![x軸とy軸そしてz軸からなる直行座標系](https://upload.wikimedia.org/wikipedia/commons/thumb/6/69/Coord_system_CA_0.svg/620px-Coord_system_CA_0.svg.png)

- [Westcivのチームが作成したテストページ](http://westciv.com/tools/3Dtransforms/)

__基本的なマークアップ__

```html
<div class="d3-parent">
  <div class="d3-child">
    <h2>The Book of</h2>
    <h1>CSS3</h1>
  </div>
</div>
```

- ほとんどの変形は `.d3-child` に対して行われる
- 親要素に対する指定が必要なものもあるため `.d3-parent` も用意しています


## 13.2 変形の関数

### 13.2.1 軸を中心とした回転

3次元空間では、回転の軸は3つあります

__構文__

```css
E {
  transform: rotateX([angle]);
}
E {
  transform: rotateY([angle]);
}
E {
  transform: rotate([angle]);
}
E {
  transform: rotateX([angle]) rotateY([angle]) rotateZ([angle]);
}
E {
  transform: rotate3d([x], [y], [z], [angle]);
}
```

### 13.2.2 奥行き

- `perspective()` は、オブジェクトに対する視点を3次元空間の中で仮想的に定義する
- `depth` には、単位つきの長さか `none` というキーワードを指定します
- 小さい値(`50px`など)を指定すると、要素は目の前にあるかのようにとても大きく表示されます
- `1000px` 程度が通常の表示となります

__構文__

```css
E {
  transform: perspective([depth]);
}
```

### 12.2.3 軸に沿った移動

- 3つ目の次元への移動には `translateZ()` を使います
- `length` には任意の単位の長さを指定します
- `translate3d()` という短縮記法のための関数も定義されています

```css
E {
  transform: translateZ([length]);
}

E {
  transform: translate3d([x], [y], [z]);
}
```


### 13.2.4 拡大と縮小

- `number` には倍率を指定します
- `scaleZ()` に指定する値を増やしてもそれだけでは要素に変化はありません。この値には、
`translateZ()` で指定された値を増減させるという効果があります
- ``

```css
E {
  transform: scaleZ([number]);
}

E {
  transform: scale3d([x], [y], [z]);
}
```

### 13.2.5 変形の行列

```css
E {
  transform: matrix3d(
    [m01], [m02], [m03], [m04],
    [m05], [m06], [m07], [m08],
    [m09], [m10], [m11], [m12],
    [m13], [m14], [m15], [m16],
  );
}
```

- [入門記事](https://dev.opera.com/articles/understanding-the-css-transforms-matrix/)


## 13.3 `perspective` プロパティと `perspective-origin` プロパティ

- `perspective` プロパティは、奥行きを定義する
- `perspective-origin` プロパティは、3次元空間での視点の位置を定義する

```css
E {
  perspective: [depth];
}

E {
  perspective-origin: [x-position] [y-position];
}
```

```css
.d3-parent { perspective: 200px; }
.d3-child { transform: rotateX(45deg) rotateZ(90deg); }
.trans-1 { perspective-origin: left center; }
.trans-2 { perspective-origin: 100% 100%; }
.trans-3 { perspective-origin: 75% 75%; }
```


## 13.4 変形の原点

- 3次元の変形では z軸が追加されています

__構文__

```css
E {
  transform-origin: [x], [y], [z];
}
```

__サンプル__

```css
.d3-child { transform: rotateX(45deg) rotateZ(90deg); }
.trans-1 { transform-origin: 50% 0 0; }
.trans-2 { transform-origin: 50% 100% 0; }
.trans-3 { transform-origin: center bottom 50px; }
```

## 13.5 `transform-style` プロパティ

- 3次元の変形が行われている要素を入れ子にすると、デフォルトでは子孫の要素に指定された変
形は無視され、親要素と同一の平面に子孫要素が配置されます
- `flat` `preserve-3d` `none`

```css
E {
  transform-style: [keyword];
}
```


## 要素の裏側の表示

- 3次元上で要素の裏側を透過するかどうか
- `visible` `hidden`
- `hidden` の場合、ボーダーや背景色も含めてなにも表示されません

__構文__

```css
E {
  backface-visibility: [state];
}
```

__サンプル__

```css
.d3-child {
  backface-visibility: visible;
  transform: rotateY(180deg);
}
.bf-hidden {
  backface-visibility: hidden;
}
```

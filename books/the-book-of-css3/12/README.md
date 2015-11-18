# 2次元の変形

- [CSS Transforms Module Level 1](https://drafts.csswg.org/css-transforms/)


## 12.1 `transform` プロパティ

```css
E {
  transform: function([value]);
}

/* 複数指定する場合 */
E {
  transform: function([value]) function([value]);
}
```

### 12.1.1 `rotate`

要素を回転する

```css
E {
  transform: rotate([value]);
}

h2 {
  transform: rotate(15deg);
}
```

#### 12.1.1.1 ドキュメントフロー上での配置

要素への変形はページ上での描画のみに作用し、ドキュメントのレイアウトには影響しません


#### 12.1.1.2 `transform-origin`

変形が行われる原点

__構文__

```css
E {
  transform-origin: [value];
}
```

```css
E { transform-origin: 0 0; }
E { transform-origin: left top; }
E { transform-origin: 200px 50px; }
E { transform-origin: 100% 100%; }
E { transform-origin: center center; } /* デフォルト */
```

### 12.1.2 `translate`

要素を移動する

__構文__

```css
E {
  transform: translateX([value]) translateY([value]);
}
```

__サンプル__

```css
E {
  transform: translateX(20px) translateY(15%);
}
```

#### 12.1.2.1 `translate()` を使った短縮記法

__構文__

```css
E {
  transform: translate([x], [y]);
}
```

__サンプル__

```css
E {
  transform: translate(20px, 15%);
}

/*
 * 1つだけ引数を指定した場合
 * 値はx軸として解釈され、y軸は 0 が指定されたものとして扱われます
 */
E {
  transform: translate(20px);
  /* 以下と同等 */
  transform: translate(20px, 0);
  transform: translateX(20) translateY(0);
}
```

### 12.1.3 `scale`

要素を拡大縮小する

__構文__

```css
E {
  transform: scaleX([value]) scaleY([value]);
}
```

__サンプル__

```css
E {
  transform: scaleX(2) scaleY(2);
}
```

#### 12.1.3.1 `scale()` を使った短縮記法

値を1つだけ指定した場合、同じ値が2つ指定されたものとして扱われます

```css
/* すべて同等 */
E { transform: scale(2); }
E { transform: scale(2, 2); }
E { transform: scaleX(2) scaleY(2); }
```

### 12.1.4 `skew`

要素を傾斜させる

__構文__

値には角度を指定します

```css
E {
  transform: skewX([value]) skewY([value]);
}
```

__サンプル__

```css
E { transform: skewX(15deg); }
E { transform: skewY(5deg); }
E { transform: skewX(15deg) skewY(-15deg); }
```

### 12.1.4.1 `skew` を使った回転

```css
/* 次のコードは同じ意味となる */
E {
  transform: rotate(15deg);
  transform: skewX(15deg) skewY(-15deg);
}
```

### 12.1.5 `skew()` を使った短縮記法

この関数は利用しないことを強くおすすめします。


## 12.2 変形の際の注意

- `transform` に値をセットすると、指定されていない関数についてはデフォルト値にリセットされます


## 12.3 行列を使った変形

```css
E {
  transform: matrix([a], [b], [c], [d], [X], [Y]);
}
```

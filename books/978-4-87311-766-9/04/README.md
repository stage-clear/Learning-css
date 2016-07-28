# 視覚効果
## 15. 単方向の影
### 1辺に影を適用する
ぼかしの半径に続けて、「広がりの半径(spread radius)」と呼ばれる長さのパラメーターを記述します。  
ぼかしの半径にマイナス1を掛けた値を広がりの半径として指定すれば、影は元の要素とぴったり同じサイズになるはずです。

```css
E {
  box-shadow: box-shadow: 0 5px 4px -4px black;
}
```
:arrow_forward: [One-side shadow](http://dabblet.com/gist/cc055dadf493c15723cf)

### 隣接する2辺での影

```css
E {
  box-shadow: 3px 3px 6px -3px black;
}
```
:arrow_forward: [2-Side Shadow](http://dabblet.com/gist/d29d19ab66177b18bd64)

### 向かい合う2辺での影

```css
E {
  box-shadow: 5px 0 5px -5px black,
             -5px 0 5px -5px black;
}
```
:arrow_forward: [Opposite-sides shadow](http://dabblet.com/gist/a23e445fca36293d12f6)

## 16. 不規則な形状のドロップシャドウ
### 解決策

```css
E {
  color: deeppink;
  border: 2px solid;
  text-shadow: .1em .2em yellow;
  filter: drop-shadow(.05em .05em .1em gray);
}
```

:arrow_forward: [drop-shadow](http://dabblet.com/gist/d8a2376c79906d68f3d1)

## 17. 色調の調整
### フィルターを使った解決策 
:warning: Lmited Support

```css
/**
 * 1. sepia() ほとんどのピクセルで色相の値は 35 から 40 になります
 * 2. saturate() 再度を調節します
 * 3. hue-rotate() すべてのピクセルの色相を指定された角度だけ移動します
 */
img {
  filter: sepia() saturate(4) hue-rotate(295deg);
}
img:hover,
img:focus {
  filter: none;
}
```
:arrow_forward: [colot-tint-filter](http://dabblet.com/gist/b338c9940a31b727b7a9)

### ブレンドモードを使った解決策
:warning: Limited Support

__例) `<img>` に対してブレンドモードを適用する__
```html
<a href="#something">
  <img src="path/to/image">
</a>
```

```css
a {
  display: block;
  background: hsl(335, 100%, 50%);
}
img {
  mix-blend-mode: luminosity;
}
```

__例) 背景にブレンドモードを適用する__
```html
<div class="tinted-image" style="background-image: url(path/to/image)">
</div>
```

```css
.tinted-image {
  width: 640px;
  height: 440px;
  background-size: cover;
  background-color: hsl(335, 100%, 50%);
  background-blend-mode: luminosity;
  transition: .5s background-color;
}
.tinted-image:hover {
  background-color: transparent;
}
```
:arrow_forward: [color-tint](http://dabblet.com/gist/0dced2852818c0f555e9)

> Dubley Storey は、ブレンドモードとアニメーションを組み合わせたトリックを考案しました。
> [Create Monochromatic Color-Tinted Images With CSS blend](http://thenewcode.com/888/Create-Monochromatic-Color-Tinted-Images-With-CSS-blend-modes)

## 18. 曇りガラスの効果
### 解決策
```html
<main>
  <blockquote>
    "The only way to get rid of a temptation[...]"
    <footer>---
      <cite>
        Oscar Wilde,
        The Picture of Drian Gray
      </cite>
    </footer>
  </blockquote>
</main>
```

```css
body, main::before {
  background: url(path/to/image) 0 / cover fixed;
}

main {
  position: relative;
  background: hsla(0,0%,100%,.3);
  overflow: hidden;
}

main::before {
  content: '';
  position: absolute;
  top: 0; right: 0; bottom: 0; left: 0;
  filter: blur(20px);
  margin: -30px;
}
```

:arrow_forward: [Frosted glass](http://dabblet.com/gist/d9f243ddd7dbffa341a4)

## 19. 角の折り返し
### 45度の場合の解決策

```css
E {
  background: #58a;
  background: 
    linear-gradient(to left bottom,
      transparent 50%, rgba(0,0,0,.4) 0
    ) no-repeat 100% 0 / 2em 2em,
    linear-gradient(-135deg,
      transparent 1.5em, #58a 0
    );
}
```
- 斜め方向のサイズを `2em` に保つなら `background-size` を √2倍します
- 縦横のサイズを `2em` に保つならカラーストップの位置を √2分の1にします

:arrow_forward: [Folded corner](http://dabblet.com/gist/83b4d6bc907aa5ab576a)

### 他の角度での解決策

```css
E {
  background:#58a;
  background:
    linear-gradient(to left bottom,
      transparent 50%, rgba(0,0,0,.4) 0
    ) no-repeat 100% 0 / 3em 1.73em,
    linear-gradient(-150deg,
      transparent 1.5em, #58a 0
    );
}
```

```css
.note {
  position: relative;
  background: #58a;
  background: linear-gradient(-150deg,
    transparent 1.5em, #58a 0
  );
  border-radius: .5em;
}
.note::before {
  content: '';
  position: absolute;
  top: 0; right: 0;
  background: linear-gradient(to left bottom,
    transparent 50%, rgba(0,0,0,.2) 0, rgba(0,0,0,.4)
  ) 100% 0 no-repeat;
  width: 1.73em;
  height: 3em;
  transform: translateY(-1.3em) rotate(-30deg);
  transform-origin: bottom right;
  border-bottom-left-radius: inherit;
  box-shadow: -.2em .2em .3em -.1em rgba(0,0,0,.15);
}
```

:arrow_forward: [folded-corner-realistic](http://dabblet.com/gist/bc32dc20adea2261c731)

```scss
@mixin folded-corner($background, $size, $angle: 30deg) {
  position: relative;
  background: #background;
  background: linear-gradient($angle - 180deg,
    transparent $size, $background 0
  );
  border-radius: .5em;
  
  $x: $size / sin($angle);
  $y: $size / cos($angle);
  
  &::before {
    content: '';
    position: absolute;
    top: 0; right: 0;
    background: linear-gradient(to left bottom,
      transparent 50%, rgba(0,0,0,.2) 0, rgba(0,0,0,.4)
    ) 100% 0 no-repeat;
    width: $y;
    height: $x;
    transform: translateY($y - $x) rotate(2 * $angle - 90deg);
    transform-origin: bottom right;
    border-bottom-left-radius: inherit;
    box-shadow: -.2em .2em .3em -.1em rgba(0,0,0,.2);
  }
}

// Usage:
.note {
  @include folded-corner(#58a, 2em, 49deg);
}
```

:arror_forward: [folded-corner-mixin](http://codepen.io/leaverou/pen/raGaNR)

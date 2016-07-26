# 形状
## 9. さまざまな楕円形

```css
E {
  border-radius: 50% / 50%;
}
```

:arrow_forward: [ellipse](http://dabblet.com/gist/aada0b96b21ae3e45c1b)

### 半楕円形
```css
E {
  border-radius: 50% / 100% 100% 0 0;
}
```

:arrow_forward: [half-ellipse](http://dabblet.com/gist/e98d11da331bd9482bb0)

### 4分割された楕円形

```css
E {
  border-radius: 100% 0 0 0;
}
```

:arrow_forward: [quarter-ellipse](http://dabblet.com/gist/2b75df0e72c9804e8abe)  
:arrow_forward: [BonBon](http://simurai.com/archive/buttons/) - `border-radius` を駆使した様々なボタン

## 10. 平行四辺形
コンテナだけをトランスフォームし、コンテンツはそのままにすることは可能でしょうか?

### 入れ子を使った解決策
```html
<a href="" class="button">
  <div>Click me</div>
</a>
```
```css
.button {
  transform: skewX(45deg);
}
.button > div {
  transform: skewX(-45deg);
}
```

:arrow_forward: [parallelograms](http://dabblet.com/gist/e1f72639c34a5578dda3)

### 擬似要素を使った解決策
```css
.button {
  position: relative;
}
.button::before {
  content: '';
  position: absolute;
  top: 0; right: 0; bottom: 0; left: 0;
  z-index: -1;
  transform: skewX(45deg);
}
```

:arrow_forward: [parallelograms-pseudo](http://dabblet.com/gist/f2d98791ab1f0b238aa9)
:arrow_forward: [multiple-backgrounds-and-borders-with-css2](http://nicolasgallagher.com/multiple-backgrounds-and-borders-with-css2/) - IE8 で複数の背景を適用できます  
:arrow_forward: [css-background-image-hacks](http://nicolasgallagher.com/css-background-image-hacks/) - 背景に対して opacity などのプロパテイィを個別に指定できます

## 11. ひし形の画像
### トランスフォームを使った解決策

```html
<div class="picture">
  <img src="path/to/image" alt=""/>
</div>
```
```css
.picture {
  width: 400px;
  transform: rotate(45deg);
  overflow: hidden;
}
.picture > img {
  max-width: 100%;
  transform: rotate(-45deg) scale(1.42);
}

/** NOTE:
 * これは確かに機能しますが、あくまでハックです
 * - HTMLの要素を1つ余分に記述しなければならず、美しくありません
 * - 正方形以外の画像ではひどい表示になってしまいます
 */
```

:arrow_forward: [diamond-image](http://dabblet.com/gist/7563400)

### クリッピングパスを使った解決策

```css
img {
  clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);
  transition: 1s clip-path;
}
img:hover {
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}
```
:arrow_forward: [diamond-clip](http://dabblet.com/gist/c62456fed36a524b8273)

## 12. 角の切り落とし
### 解決法

```css
/* 右下の角を切り落とす*/
E {
  background: #58a;
  background: linear-gradient(-45deg, transparent 15px, #58a 0);
}

/* 右下と左下の角を切り落とす */
E {
  background: #58a;
  background:
    linear-gradient(-45deg, transparent 15px, #58a 0) right,
    linear-gradient( 45deg, transparent 15px, #58a 0) left;
  background-size: 50% 100%;
  background-repeat: no-repeat;
}

/* 四隅の角を切り落とす */
E {
  background: #58a;
  background: 
    linear-gradient(135deg, transparent 15px, #58a 0) top left,
    linear-gradient(-135deg, transparent 15px, #58a 0) top right;
    linear-gradient(-45deg, transparent 15px, #58a 0) bottom right,
    linear-gradient(45deg, transparent 15px, #58a 0) bottom left,
  background-size: 50% 50%;
  background-repeat: no-repeat;
}
```

```scss
@mixin baveled-corners($bg,
  $tl:0, $tr:$tl, $br: $tl, $bl:$tr) {
  background: $bg;
  background: 
    linear-gradient(135deg, transparent $tl, $bg 0) top left, 
    linear-gradient(-135deg, transparent $tr, $bg 0) top right,
    linear-gradient(-45deg, transparent $br, $bg 0) bottom right,
    linear-gradient(45deg, transparent $bl, $bg 0) bottom left;
  background-size: 50% 50%;
  background-repeat: no-repeat;
}

// Usage:
@include baveled-corners(#58a, 15px, 5px);
```

:arrow_forward: [bevel-corner-gradients](http://dabblet.com/gist/2937c990d6bfad274740)

### 曲線による切り落とし

```css
E {
  background: #58a;
  background: 
    radial-gradient(circle at top left, transparent 15px, #58a 0) top left,
    radial-gradient(circle at top right, transparent 15px, #58a 0) top right,
    radial-gradient(circle at bottom right, transparent 15px, #58a 0) bottom right,
    radial-gradient(circle at bottom left, transparent 15px, #58a 0) bottom left;
  background-size: 50% 50%;
  background-repeat: no-repeat;
}
```

:arrow_forward: [scoop-corners](http://dabblet.com/gist/24484257bc6cf7076a8e)

### インラインの SVG と border-image を使った解決策

```css
E {
  border: 20px solid #58a; /* 20px = 15 × √2 */
  border-image: 1 url('data:image/svg+xml,\
    <svg xmlns="http://www.w3.org/2000/svg" width="3" height="3" fill="%2358a">\
      <polygon points="0,1 1,0 2,0 3,1 3,2 2,3 1,3 0,2"/>\
    </svg>');
  background: #58a;
  background-clip: padding-box;
}
```

:arrow_forward: [bevel-corners](http://dabblet.com/gist/365c867441f3ee298212)

### クリッピングパスを使った解決策

```css
E {
  background:  #58a;
  clip-path: polygon(
    20px 0, calc(100% - 20px) 0, 100% 20px,
    100% calc(100% - 20px), calc(100% - 20px) 100%,
    20px 100%, 0 calc(100% - 20px), 0 20px
  );
}
```

:arrow_forward: [baveld-corners-clipped](http://dabblet.com/gist/4a88c463afdb0778e973)

### 13. 台形のタブ
#### 解決策

```css
E {
  transform: scaleY(1.3) perspective(.5em) rotateX(5deg);
  transform-origin: bottom;
}
```

```html
<nav>
  <a href="">Home</a>
  <a href="" class="selected">Projects</a>
  <a href="">About</a>
</nav>
```

```css
nav {
  position: relative;
  z-index: 1;
  padding-left: 1em;
}

nav > a {
  position: relative;
  display: inline-block;
  margin: 0 -.3em;
  padding: .3em 1em 0;
  text-decoration: none;
}

nav > a::before {
  position: absolute;
  top: 0; right: 0; bottom: 0; left: 0;
  z-index: -1;
  background: #ccc;
  background-image: linear-gradient(
    hsla(0, 0%, 100%, .6),
    hsla(0, 0%, 100%, 0)
  );
  border: 1px solid rgba(0,0,0,.4);
  border-bottom: none;
  border-radius: .5em .5em 0 0;
  transform: scale(1.3) perspective(.5em) rotateX(5deg);
  transform-origin: bottom;
}

nav a.selected { 
  z-index: 2;
}

nav.left > a::before {
  transform: scale(1.2, 1.3) perspective(.5em) rotateX(5deg);
  transform-origin: bottom left;
}

nav.right > a::before {
  transform: scale(1.2, 1.3) perspective(.5em) rotateX(5deg);
  transform-origin: bottom right;
}
```
:arror_forward: [trapezoid-tabs](http://dabblet.com/gist/1345dc9399dc8e794502)

### 14. シンプルな円グラフ

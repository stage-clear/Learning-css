# タイポグラフィー
## 20. ハイフンの追加

```css
E {
  hyphens: auto;
}
```
:arrow_forward: [hyphenation](http://dabblet.com/gist/e370ba333ae95116e212)

## 21. 改行の挿入
```html
<dl>
  <dt>Name:</dt>
  <dd>Super man</dd>
  <dt>Email:</dt>
  <dd>super@man.me</dd>
  <dt>Location:</dt>
  <dd>Earth</dd>
</dl>
```

```css
dt, dd {
  display: inline;
}
dd {
  margin: 0;
  font-weight: bold;
}
```

```css
dd::after {
  content: '\A';
  white-space: pre;
}
```

`dd::after` では、1つの `<dt>` に対して複数の `<dd>` がある場合に対応できません。  
`dt::before` を使います。

```css
dd + dt::before {
  content: '\A';
  white-space: pre;
}

dd + dd::before {
  content: ', ';
  font-weight: normal;
}
```

:arrow_forward: [line-breaks](http://dabblet.com/gist/7eb242f4e8f078cadbca)

## 22. ゼブラストライプ
```html
<pre>
while (true) {
  var d = new Date();
  if (d.getDate() === 1 &&
      d.getMonth() === 3) {
    alert('TROLOLOL');
  }
}
</pre>
```
```css
pre {
  padding: .5em;
  line-height: 1.5;
  background: beige;
  background-image: linear-gradient(
    rgba(0,0,0,.2) 50%, transparent 0;
  );
  background-size: auto 3em;
  background-origin: content-box; /* <- */
}
```

:arrow_forward: [zebra-lines](http://dabblet.com/gist/cf30f5d442533b32600d)

## 23. タブのインデント幅の調整
```css
pre, code {
  font-family: monospace;
}

pre {
  display: block;
  margin: 1em 0;
  white-space: pre;
  tab-size: 2; /* <- */
}
```

:arrow_forward: (tab-size)[http://dabblet.com/gist/88c1523dfd1284950b4d]

## 24 リガチャー

```css
/* すべてのリガチャーを利用する場合 */
E {
  font-variant-ligatures: common-ligatures
                          discretionary-ligatures
                          histrical-ligatures;
}

/* 常用リガチャーのみ適用する場合 */
E {
  font-variant-ligatures: common-ligatures;
}

/* no-に続けて記述すると明示的に無効化できる */
E {
  font-variant-ligatures: common-ligatures
                          no-discreationary-ligatures
                          no-historical-ligatures;
}
```
:arrow_forward: [ligatures](http://dabblet.com/gist/f9f078a639e5cad002d4)

## 25. しゃれた「&」

```css
@font-face {
  font-family: Ampersand;
  src: local('Baskerville-Italic'),
       local('GoundyOldStyleT-Italic'),
       local('Palatino-Italic'),
       local('BookAntiqua-Italic');
  unicode-range: U+26; /* '&'.charCodeAt(0).toString(16) => 26 */
}

h1 {
  font-family: Ampersand, Helvetica, sans-serif;
}
```

:arrow_forward: [Ampersands](http://dabblet.com/gist/42898081c1f7cf8750f9)

## 26. 下線のカスタマイズ
```css
E {
  background: linear-gradient(gray, gray) no-repeat;
  background-size: 100% 1px;
  background-position: 0 1.15em;
  text-shadow: .05em 0 white, -05em 0 white;
}

/* 破線を作る */
E {
  background: linear-gradient(90deg, gray 66%, transparent 0) repeat-x;
  background-size: .2em 2px;
  background-position: 0 1em;
}
```
:arrow_forward: [underlines](http://dabblet.com/gist/58f3d67d5bb0f8338776)

### 波線

```css
E {
  background: 
    linear-gradient(-45deg, transparent 40%, red 0, red 60%, transparent 0) 0 1em,
    linear-gradient( 45deg, transparent 40%, red 0, red 60%, transparent 0) .1em 1em;
  background-repeat: repeat-x;
  background-size: .2em .1em;
  text-shadow: .05em 0 white, -.05em 0 white;
}
```

:arrow_forward: [wavy underline](http://dabblet.com/gist/c9184f634e9e9efde6e8)

## 27. リアルなテキストの表示効果
### 活版印刷風の効果

```css
E {
  background: hsl(210, 13%, 60%);
  color: hsl(210, 13%, 30%);
  text-shadow: 0 .03em .03em hsla(0,0%,100%,.8);
}

/**/
E {
  background: hsl(210,13%,30%);
  color: hsl(210,13%,75%);
  text-shadow: 0 -1px 1px black;
}
```

:arrow_forward: [Contrast Ratio](http://leaverou.github.io/contrast-ratio/) - Accesibility tool  
:arrow:forward: [Letterpress](http://dabblet.com/gist/80eafefae35d26979972)

### フチ付きのテキスト
#### text-shadow
```css
E {
  background: deeppink;
  color: white;
  text-shadow: 1px 1px black, -1px -1px black,
               1px -1px black, -1px 1px black;
}

/* オフセットを指定しない記述 */
E {
  text-shadow: 0 0 1px black, 0 0 1px black,
               0 0 1px black, 0 0 1px black,
               0 0 1px black, 0 0 1px black;
}
```

#### svg を使う方法
```html
<h1>
  <svg width="2em" height="1.2em">
    <use xlink:href="#css"/>
    <text id="css" y="1em">CSS</text>
  </svg>
</h1>
```

```css
h1 {
  font: 500%/1 Rockwell, serif;
  background: deeppink;
  color: white;
}
h1 text {
  fill: currentColor;
}
h1 svg {
  overflow: visible;
}
h1 use {
  stroke: black;
  stroke-width: 6;
  stroke-linejoin: round;
}
```

:arrow_forward: [stroked-text](http://dabblet.com/gist/7a665ce85190f9cb201e)

### 発行の表示効果
```css
E {
  background: #203;
  color: #ffc;
  text-shadow: 0 0 .1em, 0 0 .3em;
}

/* ホバージにトランジションさせる */
a {
  background: #203;
  color: white;
  transition: 1s;
}

a:hover {
  text-shadow: 0 0 .1em, 0 0 .3em;
}

/* filter() をつかう */
a {
  background: #203;
  color: white;
  transition: 1s;
}

a:hover {
  filter: blur(.1em);
}
```

:arrow_forward: [glow](http://dabblet.com/gist/4af6d5c3b22395543cb8)

### 飛び出すテキスト

```css
E {
  background: #58a;
  color: white;
  text-shadow: 0 1px hsl(0,0%,85%),
               0 2px hsl(0,0%,80%),
               0 3px hsl(0,0%,75%),
               0 4px hsl(0,0%,70%),
               0 5px hsl(0,0%,65%),
               0 5px 10px black;
}
```

:arrow_forwards: [Extruded](http://dabblet.com/gist/ba8161d038b9c13b99ac)

```scss
@mixin text-3d($color: white, $depth: 5) {
  $shadows: ();
  $shadow-color: $color;
  
  $for $i from 1 through $depth {
    $shadow-color: darken($shadow-color, 10%);
    $shadows: append($shadows,
      0 ($i * 1px) $shadow-color, comma
    );
    
    color: $color;
    text-shadow: append($shadows, 0 ($depth * 1px) 10px black, comma);
  }
}

// use
h1 {
  @include text-3d(#eee, 4);
}
```

```css
E {
  color: white;
  background: hsl(0,50%,45%);
  text-shadow: 1px 1px black, 2px 2px black,
               3px 3px black, 4px 4px black,
               5px 5px black, 6px 6px black,
               7px 7px black, 8px 8px black;
}
```

```scss
@function text-retro($color: black, $depth: 8) {
  $shadows: (1px 1px $color,);
  
  @for $i from 2 through $depth {
    $shadows: append($shadows,
      ($i * 1px) ($i * 1px) $color, comma
    );
  }
  
  $return $shadows;
}

h1 {
  color: #fff;
  background: hsl(0,50%,45%);
  text-shadow: text-retro();
```

## 28. 円に沿ったテキスト

```html
<div class="circular">
  <svg viewBox="0 0 100 100">
    <path d="M 0,50 a 50,50 0 1,1 0,1 z" id="circle"/>
    
    <text>
      <textpath xlink:href="#circle">
        curculat reasoning works because
      </textpath>
    </text>
  </svg>
</div>
```

```css
.circlar  {
  width: 30em;
  height: 30em;
  margin: 3em auto 0;
}

.circlar svg {
  display: block;
  overflow: visible;
}

.circlar path {
  fill: none;
}
```

#### 抽象化する

```html
<div class="circlar">
  circular reasoning works because
</div>
```

```js
$$('.circlar').forEach(function(el) {
  var NS = 'http://www.w3.org/2000/svg';
  var xlinkNS = 'http://www.w3.org/1999/xlink';
  var svg = document.createElementNS(NS, 'svg');
  var circle = document.createElementNS(NS, 'path');
  var text = document.createElementNS(NS, 'text');
  var textPath = document.createElementNS(NS, 'textPath');
  
  svg.setAttribute('viewBox', '0 0 100 100');
  
  circle.setAttribute('d', 'M 0,50 a 50,50 0 1,1 0,1 z');
  circle.setAttribute('id', 'circle');
  
  textPath.textContent = el.textContent;
  textPath.setAttribute(xlinkNS, 'xlink:href', '#circle');
  
  text.appendChild(textPath);
  svg.appendChild(circle);
  svg.appendChild(text);
  el.textContent = '';
  el.appendChild(svg);
});
```

:arror_forwards: [Text on a circle](http://dabblet.com/gist/bda1bf6b0c4adbcea63d)

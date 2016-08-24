# トランジションとアニメーション
## 42. 弾むような動きのトランジション
### 弾むアニメーション

```css
@keyframes bounce {
  60%, 80%, to {
    transform: translateY(350px);
    animation-timing-function: ease;
  }
  70% {
    transform: translateY(250px);
  }
  90% {
    transform: translateY(300px);
  }
}

.ball {
  animation: bounce 3s cubic-bezier(.1,.25,1,.25) forwards;
}
```

:arrow_forward: [bounce](http://dabblet.com/gist/1b37089310d0a5a2d8e6)  
:arrow_forward: [animate.css](https://daneden.github.io/animate.css/)

### 弾むようなトランジション
```html
<label>
  Your username: <input id="username"/>
  <span class="callout">
    Only letters, numbers, underscores (_) and hyphens (-)  allowed!
  </span>
</label>
```

```css
@keyframes elastic-grow {
  from {
    transition: scale(0);
  }
  70% {
    transform: scale(1.1);
    animation-timing-function; 
      cubic-bezier(.1,.25,1,.25); /* ease の反転 */
  }
}

input:not(:focus) + .callout {
  transform: scale(0);
}

input:focus + .callout {
  animation: elastic-grow .5s;
}

.callout {
  display: block;
  transition: transform;
  transform-origin: 1.4em -.4em;
}
```

```css
input:not(:focus) + .callout {
  transform: scale(0);
  transition: .25s transform;
  transition-timing-function: ease;
}

.callout {
  display: block;
  transform-origin: 1.4em -.4em;
  transition: .5s cubic-bezier(.25,.1,.3,1.5) transform;
}
```

## 43. コマ送りのアニメーション
### 解決策

```html
<div class="loader">Loading...</div>
```

```css
@keyframes loader {
  to { background-position: -800px 0; }
}

.loader {
  width: 100px;
  height: 100px;
  background: url(path/to/image) 0 0;
  animation: loader 1s infinite steps(8);
  
  text-indent: 200%;
  white-space: nowrap;
  overflow: hidden;
}
```

:arrow_forward: [frame-by-frame](http://dabblet.com/gist/bcc082518391f45b41dc)  
:arrow_forward: [Sprite sheet animation with steps()](http://simurai.com/blog/2012/12/03/step-animation) - スプライトと steps()  を組み合わせた便利なテクニック

## 44. 点滅
### 解決策
```css
@keyframes blink-smooth {
  50% {
    color: transparent;
  }
}
.highlight {
  animation: 1s blink-smooth 3;
}
```

`animation-direction` を使う場合
```css
@keyframes blink-smooth {
  to {
    color: transparent;
  }
}

.highlight {
  animation: .5s blink-smooth 3 alternate;
}
```

従来の `<blink>` のような（スムーズではない）点滅
```css
@keyframes blink {
  to {
    color: transparent;
  }
}

.highlight {
  animation: 1s blink 3 steps(1); /* または step-end */
}
```

:arrow_forward: [blink](http://dabblet.com/gist/46fe09e5f2b97d6f282d)  
:arrow_forward: [CSS Animations](https://w3.org/TR/css-animations) - W3

## 45. キー入力のアニメーション
### 解決策

- フォントサイズに `ch` という単位を使います。`1ch` は `0` という文字（グリフ）の幅を表します
- 等幅フォントでの `0` の幅は、他のすべてのグリフの幅と一致します

```css
@keyframes typing {
  from {
    width: 0;
  }
}

E {
  font-family: Consolas, Monaco, monospace;
  width: 15ch;
  animation: typing 8s steps(15), caret 1s steps(1) infinite;
  border-right: .05em solid;
  white-space: nowrap;
  overflow: hidden;
}
```

JavaScript で動的にテキストの幅を取得する場合
```js
var elems = [].slice.call(document.querySelectorAll('.typing'));
elems.forEach((el) => {
  var len = el.textContent.length;
  var style = el.style;
  
  style.width = len + 'ch';
  style.animationTimingFunction = 'steps('+ len +'), steps(1)';
});
```

CSSアニメーションに対応していないブラウザ
```css
@keyframes caret {
  50% {
    border-color: currentColor;
  }
}

E {
  /* 略 */
  border-right: .05em solid transparent;
  animation: typing 6s steps(15), caret 1s steps(1) infinite;
}
```

:dizzy_face: 複数行のテキストに対応できません

:arrow_forward: [typing](http://dabblet.com/gist/b04ab9f41084b0a66960)

## 46. アニメーションのスムーズな中断
### 解決策

```css
@keyframes panoramic {
  to {
    background-position: 100% 0;
  }
}
.panoramic {
  width: 150px;
  height: 150px;
  background: url(path/to/image);
  background-size: auto 100%;
  animation: panoramic 10s linear infinite alternate;
  animation-play-state: paused;
}

.panoramic:hover, .panoramic:focus {
  animation-play-state: running;
}
```

:arrow_forward: [state-animations](http://dabblet.com/gist/b7b53efcc2f933ca6d54)

## 47. 円に沿って動くアニメーション

```html
<div class="path">
  <img src="path/to/image"/ class="avatar"/>
</div>
```

```css
@keyframes span {
  to {
    transform: rotate(1turn);
  }
}
.avatar {
  display: block;
  animation: spin 3s infinite linear;
  transform-origin: 50% 150px; /* 150px = パスの半径 */
  
  /* styles */
  width: 50px;
  height: 50px;
  margin: 0 auto;
  border-radius: 50%;
  overflow: hidden;
}

.path {
  width: 300px;
  height: 300px;
  padding: 20px;
  margin: 0 auto;
  border-radius: 50%;
  background: #fb3;
}
```

### 2つの要素を使った解決策

```html
<div class="path">
  <div class="avatar">
    <img src="path/to/image"/>
  </div>
</div>
```

```css
@keyframes span {
  to {
    transform: rotate(1turn);
  }
}

@keyframes span-reverse {
  from {
    transform: rotate(1turn);
  }
}

.avatar {
  animation: spin 3s infinite linear;
  transform-origin: 50% 150px; /* 150px = パスの半径 */
  
  /* styles */
  width: 50px;
  height: 50px;
  border-radius: 50%;
  overflow: hidden;
}

.avatar > img {
  animation: inherit;
  animation-name: spin-reverse;
  width: 100%;
}
```

反転するためだけの `keyfremas` を用意する必要はありません
```css
.avatar > img {
  animation: inherit;
  animation-direction: reverse;
  transform-origin: center center;
  width: 100%;
}
```

:arrow_forward: [circular-2elements](http://dabblet.com/gist/87d80a51a5294ec07aea)

### 要素を1つしか使わない解決策

```html
<div class="path">
  <img srr="path/to/image" class="avatar"/>
</div>
```

```css
@keyframes spin {
  from {
    transform: translate(50%, 150px)
               rotate(0turn)
               translate(-50%, -150px);
  }
  to {
    transform: translate(50%, 150px)
               rotate(1turn)
               translate(-50%, -150px);
  }
}

@keyframes spin-reverse {
  from {
    transform: translate(50%, 50%)
               rotate(1turn)
               translate(-50%, -50%);
  }
  to {
    transform: translate(50%, 50%)
               rotate(0turn)
               translate(-50%, -50%)
  }
}

.avatar {
  animation: spin 3s infinite linear;
}
```

2つの `keyframes` を1つにまとめます
```css
@keyframes spin {
  from {
    transform: translate(50%, 150px)
               rotate(0turn)
               translate(-50%, -150px)
               translate(50%, 50%)
               rotate(1turn)
               translate(-50%, -50%);
  }
  to {
    transform: translate(50%, 150px)
               rotate(1turn)
               translate(-50%, -150px)
               translate(50%, 50%)
               rotate(0turn)
               translate(-50%, -50%);
  }
}
```

`.avatar` が初期状態で中心に置かれているなら、先頭の2つの `translateY` は削除できます
```css
@keyframes spin {
  from {
    transform: rotate(0turn)
               translateY(-150px) translateY(50%)
               rotate(1turn);
  }
  to {
    transform: rotate(1turn)
               translateY(-150px) translateY(50%)
               rotate(0turn);
  }
}
.avatar {
  animation: spin 3s infinite linear;
  margin: calc(50% - 50px + 20px) auto 0;
}
```

:arrow_forward: [circular](http://dabblet.com/gist/6c647a5599dc11145f2c)

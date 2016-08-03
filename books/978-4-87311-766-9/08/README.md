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


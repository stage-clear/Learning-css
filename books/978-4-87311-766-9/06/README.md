# ユーザーエクスペリエンス
## 29. 適切なマウスカーソルの選択
### 解決策
#### 無効化されている状態を示す

```css
:disabled, [disabled], [aria-disabled="true"] {
  cursor: not-allowed;
}
```
:arrow_forwad: [disabled](http://dabblet.com/gist/41c8da81742e1ab1d07f)

#### マウスカーソルを隠す
不特定多数向けのマルチスクリーン端末など

```css
video {
  cursor: url(transparent.gif); /* for `cursor:none` not supported */
  cursor: none;
}
```

## 30. クリック可能な範囲を広げる

> __フィッツの法則__
> ターゲットの領域に移動するための時間は、ターゲットまでの距離をターゲットのお大きさで割った値の対数に比例するとされています。  
> _T_ = _a_ + _b_ log<sub>2</sub>(1 + _D_ / _W_)

[参考: フィッツの法則](https://ja.wikipedia.org/wiki/%E3%83%95%E3%82%A3%E3%83%83%E3%83%84%E3%81%AE%E6%B3%95%E5%89%87)

#### ボーダーを使う
```css
E {
  background: gray;
  background-clip: padding-box;
  border: 20px solid transparent;
  
  /* 本当にボーダーが必要になった場合 */
  box-shadow: 0 0 0 1px rgba(0,0,0,.3) inset;
}
```

:arrow_forward: [Extending the hit area](http://dabblet.com/gist/df5686d4047307991f73)

#### before を使う
```css
E {
  position: relative;
  background: gray;
  border: 1px solid rgba(0,0,0,.3);
}
E::before {
  position: absolute;
  top: -10px;
  right: -10px;
  bottom: -10px;
  left: -10px;
}
```

:arrow_forwards: [Extending the hit area](http://dabblet.com/gist/d76ac0acc80923d47106)

## 31. チェックボックスのカスタマイズ
### 解決策

```html
<input type="checkbox" id="awesome"/>
<label for="awesome">Awesome</label>
```

```css
input[type="checkbox"] + label::before {
  content: '\a0'; /* 改行しない空白文字 */
  display: inline-block;
  vertical-align: .2em;
  width: .8em;
  height: .8em;
  margin-right: .2em;
  border-radius: .2em;
  background: silver;
  text-indent: .15em;
  line-height: .65;
}

input[type="checkbox"]:checked + label::before {
  content: '\2713';
  background: yellowgreen;
}

input[type="checkbox"]:focus + label::before {
  box-shadow: 0 0 .1em .1em #58a;
}

input[type="checkbox"]:disabled + label::before {
  background: gray;
  box-shadow: none;
  color: #555;
}

/* `display:none` を使ず非表示にする */
/* `display: none` ではキーボード操作の対象から外れてしまうため */
input[type="checkbox"] {
  position: absolute;
  clip: rect(0,0,0,0);
}
```

:arrow_forward: [Custom checkboxes](http://dabblet.com/gist/e269f10328615254e29e)
:arrow_forward: [Custom radio and checkbox inputs using css](https://www.thecssninja.com/css/custom-inputs-using-css)
:arrow_forward: [Bootleg.css](http://labs.thecssninja.com/bootleg/)

### トグルボタン

```css
input[type="checkbox"] {
  position: absolute;
  clip: rect(0,0,0,0);
}

input[type="checkbox"] + label {
  display: inline-block;
  padding: .3em .5em;
  background: #ccc;
  background-image: linear-gradient(#ddd, #bbb);
  border: 1px solid rgba(0,0,0,.2);
  border-radius: .3em;
  box-shadow: 0 1px white inset;
  text-align: center;
  text-shadow: 0 1px 1px white;
}

input[type="checkbox"]:checked + label,
input[type="checkbox"]:active + label {
  box-shadow: .05em .1em .2em rgba(0,0,0,.6) inset;
  border-color: rgba(0,0,0,.3);
  background: #bbb;
}
```

:arrow_forward: [Toggle buttons](http://dabblet.com/gist/fa5c622180b232043891)

## 32. 背景を暗くして重要度を下げる
- Lightbox やクイックツアーなど  
- `<div class="overlay">` はよく使われますが、HTML要素が余分に必要となります

### 擬似要素を使った解決策
- :astonished: すでに `::before` が指定されている場合にはこのテクニックは適用できません
- :astonished: 擬似要素にはイベントハンドラを設定できない

```css
body.dimmed::before {
  content: '';
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 0;
  background: rgba(0,0,0,.8);
}
```

### box-shadow を使った解決策
```css
E {
  box-shadow: 0 0 0 999px rgba(0,0,0,.8);
  box-shadow: 0 0 0 50vmax rgba(0,0,0,.8);
}
```

- :astonished: スクロールするとオーバーレイ表示の橋を超えてしまう
- :astonished: マウスイベントを補足できません

:arrow_forward: [Rudimetary overlay](http://dabblet.com/gist/91538b2131d3545035ca)

###f ::backdrop を使った解決策
:warning: Limited Support

```css
dialog::backdrop {
  background: rgba(0,0,0,.8);
}
```

- :astonished: サポートされているブラウザが非常に限られています

:arrow_forward: [Native modal dialog](http://dabblet.com/gist/bb2121aea259be94c35d)

## 33. 背景をぼかして重要度を下げる

```html
<main>Bacon Ipsum dolor sit amet...</main>
<dialog>
  O Hai, I'm a dialog. Click on me to dismiss.
</dialog>
```

```css
main {
  transition: .6s filter;
}
main.de-emphasized {
  filter: blur(5px) contrast(.8) brightness(.8);
}
```

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

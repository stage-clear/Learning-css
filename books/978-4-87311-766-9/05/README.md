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

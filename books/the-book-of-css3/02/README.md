# 2 メディアクエリ

## 2.2 構文

1. link要素に指定

```html
<link href="file" rel="stylesheet" media="login cmedia and  (expression)">
```

2. import で外部スタイルシートを呼び出す

```css
@import url(file) login media and (expression);
```

3. @media を使う

```css
@media login media and (expression) {
  /* rules... */
}
```

__例__  

```css
/* 800ピクセル以下に適用 */
@media only screen and (max-width: 800px) {}

/* 400ピクセル以上に適用*/
@media only screen and (min-width: 400px) {}

/* AND (and区切り) */
@media (max-device-aspect-ratio: 15/10) and (max-width: 800px) {}

/* OR (,区切り)  */
@media screen (orientation: landscape), print (orientation: portrait) {}
```

### 2.3 メディアフューチャー

|名前|説明|
|:--|:--|
|width|幅|
|height|高さ|
|resolution|ピクセル比 <dpx>,<dpi>|
|device-pixel-ratio|ピクセル比(safari)|
|orientaion|<landscape><portrait>|
|aspect-ratio|ブラウザのアスペクト比|
|device-aspect-ratio|デバイスのアスペクト比|

* それぞれ max-, min- 接頭辞で最大値最小値を指定できる

# Webフォント


```css
@font-face {
  font-family: 'Gentium Basic';
  src: url('GenBkBasR.eot');
  src: url('GenBasR.eot.?#iefix') format('embeded-opentype'),
       url('GenBkBasR.woff') format('woff'),
       url('GenBkBasR.ttf') format('truetype');
```

1. IE8以前のためのEOT形式のフォントを指定
2. IE9での互換性の問題のために再びEOT形式のフォントを指定。（互換性の問題は重要ではなくなっているので各自の判断で削除してしまっても構わない）
3. 大多数のブラウザで使われるWOFF形式のフォントを指定
4. Android 4.3以前の古いブラウザ向けにTTF形式のフォントを指定

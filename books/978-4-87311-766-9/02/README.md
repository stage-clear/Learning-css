# 背景とボーダー
## 1. 半透明なボーダー
```css
E {
  border: 10px solid hsla(0,0%,100%,.5);
  background: white;
  background-clip: paddin-box;
}
```
- [Demo: translucent-borders](http://dabblet.com/gist/012289cc14106a1bd7a5)

## 2. 複数のボーダー
### box-shadow を使った解決策
```css
E {
  background: yellowgreen;
  box-shadow: 
    0 0 0 10px #655,
    0 0 0 15px deeppink,
    0 2px 5px 15px rgba(0,0,0,.6);
}
```

- [Demo: multiple-borders](http://dabblet.com/gist/525eb8e9cdade71723c1)

### アウトラインを使った解決策
- ボーダーは2つまでしか表示できません
- outline では角丸は考慮されません

```css
E {
  background: yellowgreen;
  border: 10px solid #655;
  outline: 15px solid deeppink;
}
```

## 3. 柔軟な背景の位置指定
### background-position 拡張を使った解決策
```css
E {
  background: url(path/to/image.svg) 
    no-repeat bottom right #58a;
  background-position: right 20px bottom 10px;
}
```

- [Demo: extended-bg-position](http://dabblet.com/gist/0f226e63595d1bef88cb)

### background-origin を使った解決策
```css
E {
  padding: 10px;
  background: url(path/to/image.svg) no-repeat #58a bottom right;
  background-origin: content-box;
}
```

- [Demo: background-origin](http://dabblet.com/gist/0f19ac5d28d0aa7b6c60)

### calc() を使った解決策
```css
E {
  background: url(path/to/image.svg) no-repeat;
  background-position: calc(100% - 20px) calc(100% - 10px);
}
```

## 4. 角の内側を丸める
### 解決策
```html
<div class="something-meaningful">
  I have a nice subtle innerrounding,
  don't I look pretty?
</div>
```

```css
.something-meaningful {
  background: tan;
  border-radius: .8em;
  padding: 1em;
  box-shadow: 0 0 0 .6em #655;
  outline: .6em solid #655;
}
```

- [Demo: inner-rounding](http://dabblet.com/gist/170fe436f290083cc24c)

## 5. ストライプ模様の背景
### 解決策
```css
E {
  background: linear-gradient(#fb3 50%, #58a 0);
  background-size: 100% 30px;
}

/* 3色のストライプ */
F {
  background: linear-gradient(#fb3 50%, #58a 0, #58a 66.6%, yellowgreen 0);
  background-size: 100% 30px;
}
```

- [Demo: horizontal-stripes](http://dabblet.com/gist/119dbf7f0c76dba7b7ee)

### 縦のストライプ
```css
E {
  background: linear-gradient(to right, /* or 90deg */ #fb3 50%, #58a 0);
  background-size: 30px 100%;
}
```

- [Demo: vertical-stripes](http://dabblet.com/gist/1b4983062fd2b4d7e60e)

### 斜めのストライプ
```css
E {
  background: linear-gradient(45deg, 
    #fb3 25%, #58a 0, #58a 50%,
    #fb3 0, #fb3 75%, #58a 0);
  background-size: 30px 30px;
}

/** NOTE:
 * 実際にストライプの太さを 15px にしたい場合、2 × 15√2  
 * JavaScript で計算する = `(2 * (15 * Math.sqrt(2))).toFixed(9)`
 * 半端な数字は切り捨てて 42.4px またはシンプルに 42px にすることを
 * 強くおすすめします
 */

E {
  background: linear-gradient(45deg,
    #fb3 25%, #58a 0, #58a 50%,
    #fb3 0, #fb3 75%, #58a 0);
  background-size 42.4px 42.4px;
}
```

- [Demo: diagonal-strips](http://dabblet.com/gist/abeab80934fc26e6538e)

### よりよい斜めのストライプ
```css
E {
  background: repeating-linear-gradient(
    #fb3, #fb3 15px, #58a 0, #58a 30px
  );
}
```

- [Demo: diagonal-stripes-60deg](http://dabblet.com/gist/5646121210b0c99c94a7)

45度の場合は、`linear-gradient` と `repeating-linear-gradient` の両方の
アプローチを組み合わせることでカラーストップを減らせます
```css
E {
  background: repeating-linear-gradient(45deg,
    #fb3 0, #fb3 25%, #58a 0, #58a 100%
  );
  background-size: 42.4px 42.4px;
}
```

### 似た色のストライプを柔軟に指定する
濃い色を背景色にし、これに半透明の白のストライプを重ねます
```css
E {
  background: #58a;
  background-image: repeating-linear-gradient(30deg,
    hsla(0,0%,100%,.1),
    hsla(0,0%,100%,.1) 15px,
    transparent 0, transparent 30px
  );
}
```

- [Demo: subtle-stripes](http://dabblet.com/gist/aa50d296a8ec07cf7334)

## 6. 複雑な背景のパターン
### 格子模様
```css
E {
  background: white;
  background-image: 
    linear-gradient(90deg, rgba(200,0,0,.5) 50%, transparent 0), 
    linear-gradient(       rgba(200,0,0,.5) 50%, transparent 0);
  background-size: 30px 30px;
}
```

格子のサイズが変わっても、線の幅は一定に保ちたいケース
```css
E {
  background: #58a;
  background-image: 
    linear-gradient(white 1px, transparent 0),
    linear-gradient(90deg, white 1px, transparent 0);
  background-size: 30px 30px;
}

/* 異なる幅や色の線を組み合わせると、よりリアルな格子を作成できます */
E {
  background: #58a;
  background-image: 
    linear-gradient(white 2px, transparent 0),
    linear-gradient(90deg, white 2px, transparent 0),
    linear-gradient(hsla(0,0%,100%,.3) 1px, transparent 0),
    linear-gradient(90deg, hsla(0,0%,100%,.3) 1px, transparent 0);
  background-size: 75px 75px, 75px 75px,
                   15px 15px, 15px 15px;
}
```

- [Demo: bluepring](http://dabblet.com/gist/43bde2086e9d549fb844)

### 水玉模様
```css
E {
  background: #655;
  background-image: radial-gradient(tan 30%, transparent 0);
  background-size: 30px 30px;
}
```

```css
E {
  background: #655;
  background-image: 
    radial-gradient(tan 30%, transparent 0),
    radial-gradient(tan 30%, transparent 0);
  background-size: 30px 30px;
  background-position: 0 0, 15px 15px;
}
```

- [Demo: polka](http://dabblet.com/gist/cd33da5d1a48046746cd)

正しく表示されるためには、2つ目のグラデーションの `background-position` はタイルのサイズの半分にする必要があります

```scss
@mixin polka($size, $dot, $base, $accent) {
  background: $base;
  background-image:
    linear-gradient($accent, $dot, transparent 0),
    linear-gradient($accent, $dot, transparent 0);
  background-size: $size $size;
  background-position: 0 0, $size/2 $size/2;
}

@include polka(30px, 30%, #655, tan);
```
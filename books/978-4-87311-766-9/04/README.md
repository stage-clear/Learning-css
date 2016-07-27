# 視覚効果
## 15. 単方向の影
### 1辺に影を適用する
ぼかしの半径に続けて、「広がりの半径(spread radius)」と呼ばれる長さのパラメーターを記述します。  
ぼかしの半径にマイナス1を掛けた値を広がりの半径として指定すれば、影は元の要素とぴったり同じサイズになるはずです。

```css
E {
  box-shadow: box-shadow: 0 5px 4px -4px black;
}
```
:arrow_forward: [One-side shadow](http://dabblet.com/gist/cc055dadf493c15723cf)

### 隣接する2辺での影

```css
E {
  box-shadow: 3px 3px 6px -3px black;
}
```
:arrow_forward: [2-Side Shadow](http://dabblet.com/gist/d29d19ab66177b18bd64)

### 向かい合う2辺での影

```css
E {
  box-shadow: 5px 0 5px -5px black,
             -5px 0 5px -5px black;
}
```
:arrow_forward: [Opposite-sides shadow](http://dabblet.com/gist/a23e445fca36293d12f6)

## 16. 不規則な形状のドロップシャドウ
### 解決策

```css
E {
  color: deeppink;
  border: 2px solid;
  text-shadow: .1em .2em yellow;
  filter: drop-shadow(.05em .05em .1em gray);
}
```

:arrow_forward: [drop-shadow](http://dabblet.com/gist/d8a2376c79906d68f3d1)

## 17. 色調の調整
### フィルターを使った解決策 
[:warning: Lmited Support]

```css
/**
 * 1. sepia() ほとんどのピクセルで色相の値は 35 から 40 になります
 * 2. saturate() 再度を調節します
 * 3. hue-rotate() すべてのピクセルの色相を指定された角度だけ移動します
 */
img {
  filter: sepia() saturate(4) hue-rotate(295deg);
}
img:hover,
img:focus {
  filter: none;
}
```

### ブレンドモードを使った解決策
[:warning: Limited Support]

```html
<a href="#something">
  <img src="path/to/image">
</a>
```

```css
a {
  background: hsl(335, 100%, 50%);
}
```

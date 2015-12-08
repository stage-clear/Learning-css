# テキストの効果とスタイル

[CSS Text Level 3 モジュール](http://www.w3.org/TR/css3-text/)


## 6.1 軸と座標を理解する

- CSS3 では軸（axis、複数形は axes）という概念が取り入れられています
- CSS では直交座標系が使われます

![直交座標系による平面上の点の座標と四つの象限](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Cartesian_coordinates_2D.svg/360px-Cartesian_coordinates_2D.svg.png)


CSSではすべての要素に幅と高さがあり、これらの値はピクセル単位で表現されます。`em` や
パーセントなどの単位が使われている場合でも、内部的にはピクセルが単位となっています。


## 6.2 `text-shadow` （立体的効果）

```css
/*
 * text-shadow
 * @param {x-offset} x 横方向の距離
 * @param {y-offset} y 縦方向の距離
 * @param {color} 色の指定
 * @param {blur-radius} ぼかしの半径
 */
E {
  text-shadow: [x] [y];
}

E {
  text-shadow: [x] [y] [color];
}

E {
  text-shadow: [x] [y] [blur-radius] [color];
}
```

### 6.2.1 複数の影

```css
E {
  text-shadow: [value], [value], [value];
}
```


## 6.3 オーバーフローの制御

```css
/*
 * text-overflow
 * @param {keyword} clip | ellipsis
 * 2つ目のプロパティは逆方向にインデントしたテキストが
 * コンテナからはみ出るような場合に適用される
 */
E {
  text-overflow: [keyword];
}
E {
  text-overflow: [keyword] [keyword];
}
```


## 6.4 テキストの配置

- `text-align-last` は、最終行（あるいは1行だけのテキスト）の配置を指定できます

```css
/*
 * text-align-last
 * @param {keyword} left | right
 */
E {
  text-align-last: [keyword];
}
```


## 6.5 行の折り返しのコントロール

### 6.5.1 単語の分割

- `word-wrap` は長い単語を分割して、親要素にフィットするように指定できます

```css
/*
 * word-wrap
 * @param {keywrod} normal | break-word
 * - `normal` は `<br>` を除いて単語の間でしか改行しません
 * - `break-word` は、必要であれば単語の途中でも改行されます
 */
E {
  word-wrap: [keyword];
}
```


### 6.5.2 ハイフン区切り

- 単語を複数行に区切る際に、ハイフンを追加することもできます

```css
/*
 * hyphens
 * @param {keyword} none | manual | auto
 */
E {
  hyphens: [keyword];
}
```


## 6.6 要素のサイズ変更

```css
/*
 * resize
 * ドラッグ可能な方向を指定します
 * @param {keyword} horizontal | vertical | both | none
 */
E {
  resize: [keyword];
}
```

# 値と長さ

## 16.1 相対的な長さ

- [CSS Values and Units Module Level 3](http://www.w3.org/TR/css-values/)


### 16.1.1 ルートを基準とした単位

- `rem` (root em) は、ドキュメントルート(`html`要素)での `font-size` の値を基準とする

### 16.1.2 ビューポートを基準とした単位

|単位|説明|
|:--|:--|
|`vw`|ビューポートに対する相対的な幅の値|
|`vh`|ビューポートに対する相対的な高さの値|
|`vmax`|`vw` `vh` のうち大きいほうの値を表す|
|`vmin`|`vw` `vh` のうち小さいほうの値を表す|

- iOS7 までの Safari では `vh` の解釈にバグがある


## 16.2 計算による値

- 計算を行わせるには `calc()` 関数を使います
- `calc()` 関数が威力を発揮するのは、異なる単位が混在する場合です
- 乗算と除算を行う場合には、演算子の前後にスペースを1つずつ記述する必要があります


## 16.3 要素のサイズ

### 16.3.1 ボックスのサイズ

- [CSS Basic User Interface Module Level 3](http://www.w3.org/TR/css3-ui/)

```css
E {
  box-sizing: [keyword]
}
```

|値|説明|
|:--|:--|
|`content-box`|デフォルト|
|`border-box`|`width` や `height` にパディングとボーダーが含まれるようになる|


### 16.2.3 内部的なサイズ指定と外部的なサイズ指定

- [CSS Intrinsic & Extrinsic Sizing Module Level 3](https://drafts.csswg.org/css-sizing/)
- CSS3 では内部的なサイズ指定(intrinsic sizing) と外部的なサイズ指定(extrinsic sizing)
という概念が取り入れられました


```css
E {
  width: [keyword]
}
```


|値|説明|
|:--|:--|
|`max-content`|内部コンテンツの中で最も大きいものに合わされます|
|`min-content`|内部コンテンツの中で最も小さいものに合わされます|
|`fit-content`|コンテンツをすべて含むことができるまで幅が広げられます|
|`fill`||


#### 16.3.2.1 `max-content` と `min-content`

- 内部的なサイズを表します
- コンテンツがテキストの場合には、最も内外単語の幅が基準になります


#### 16.3.2.2 `fit-content`

- 内部的なサイズを表します
- コンテンツをすべて含むことができるサイズまで幅が広げられます


#### 16.3.2.3 `fill`

- 外部的なサイズを表します
- 親要素の幅または高さいっぱいに要素が広がります
- Firefox では `available`、Chrome では `fill-available` という名前になっています

# Flexbox レイアウト

- [CSS Flexible Box Layout モジュール](http://www.w3.org/TR/css-flexbox-1/)
- [日本語訳](http://www.hcn.zaq.ne.jp/___/WEB/css-flexbox-ja.html)


## 15.1 Flexbox のモデルの定義

- 要素に `display: flex` を指定すると、`flex` コンテナが作成され、その子要素は `flex`
アイテムとなる

```css
E {
  display: flex;
}
```


## 15.2 Flexbox 内の配置

- Flexbox では2つの軸に基づいてレイアウトがおこなわれます
- メイン軸はアイテムが配置される方向（左から右、あるいは上から下）を表します
  - `flex-direction: row` なら縦方向、`flex-direction: column` なら横方向
- クロス軸はメイン軸に対して、直角に交わります

<img src="http://7xjtnb.com1.z0.glb.clouddn.com/flexbox_flex_direction.png" width="640" alt="flexアイテムの配置の方向を示すメイン軸とクロス軸">

- 軸の始点や終点という概念がよく使われます
- 軸の方向が横の場合は、始点が左で終点が右。縦方向の場合は、始点が上で終点が下。（反転していない場合）


## 15.3 配置順の反転

```css
E {
  flex-direction: row-reverse;
}
E {
  flex-direction: column-reverse;
}
```


## 15.4 任意の順で並べ替え

- `order` プロパティを使うと、並べ替えの順序を自由に指定できます
- flex コンテナではなく、flex アイテムに記述します
- 配置の変化は表示上だけのものであり、マークアップの中での順序は変わりません


__例__

```css
E {
  order: 2;
}
F, G {
  order: 3;
}
H {
  order: 1;
}
```


## 15.5 さらに柔軟な指定

- メイン軸方向の flex アイテムの長さの合計が flex コンテナの長さと一致しないことがほとんどです
- Flex アイテムを伸び縮みさせるためのプロパティが用意されています


### 15.5.1 `flex-glow` プロパティ

- flex アイテムを拡大する
- (flex コンテナの横幅 - flex アイテムの横幅の総和 = 余白) < 0
- 余白が余る場合、コンテナに合わせてアイテムの幅を広げるには `flex-glow` を指定します

```css
.flex-item {
  flex-grow: 1;
}

#b {
  flex-grow: 3; /* 1つだけ大きく */
}
```


### 15.5.2 `flex-shrink` プロパティ

- flex アイテムを縮小する
- flex コンテナの横幅 - flex アイテムの横幅の総和 = 余白 > 0

```css
.flex-item {
  flex-shrink: 1;
}

#b {
  flex-shrink: 3; /* 1つだけ小さく */
}
```


### 15.5.3 `flex-basis` プロパティ

- flex アイテムの幅は `width` の値やコンテンツの大きさによって決まります
- `flex-basis` が指定されると既存の `width` は無視されます
- `flex-basis` の値に対して拡大縮小が行われるようになります


```css
.flex-item {
  flex-basis: 100px;
}
```

### 15.5.4 `flex` を使った短縮記法

```css
E {
  flex: [grow] [shrink] [basis];
}
```


## 15.6 flex コンテナ内での配置

- 余白をよりよく利用する

### 15.6.1 `justify-content` を使ったメイン軸方向の配置

- メイン軸の配置の調整

<img src="http://image.slidesharecdn.com/putting-flexbox-into-practiceblend-conf130907-130908160522-/95/putting-flexbox-into-practice-59-638.jpg?cb=1383128890" width="640" alt="justify-content プロパティの効果">


__基本構文__

```css
.flex-container {
  justify-content: [keyword];
}
```


__例__

```css
E { justify-content: flex-start; }
E { justify-content: center; }
E { justify-content: space-around; }
```

### 15.6.2 `align-items` を使ったクロス軸方向の配置

- クロス軸の配置の調整

<img src="http://image.slidesharecdn.com/putting-flexbox-into-practiceblend-conf130907-130908160522-/95/putting-flexbox-into-practice-50-638.jpg?cb=1383128890" width="640" alt="align-items プロパティの効果">


__基本構文__

```css
.flex-container {
  align-items: [keyword];
}
```

__例__

```css
E { align-items: stretch; }
E { align-items: flex-end; }
E { align-items: center; }
```


### 15.6.3 `align-self` を使ったクロス軸方向の配置

- 個々の flex アイテムについてクロス軸方向の配置を指定したい場合に指定します

```css
E {
  align-self: [keyword];
}
```


### 15.6.4 折り返しとフロー

- flex アイテムが多くて flex コンテナの1行にうまく収まらない場合、`flex-wrap` で折り返しの指定ができます

```css
.flex-container {
  flex-wrap: wrap;
}
```


### 15.6.5 `flex-flow` を使った短縮記法

- `flex-direction` と `flex-wrap` の値を合わせて、`flex-flow` という短縮記法に記述できます

```css
E {
  flex-flow: [direction] [wrap]
}
```


### 15.6.6 `align-content` を使った複数行の flex アイテムの配置

- flex アイテムが複数行に折り返した場合、各行の配置は `align-content` を使って指定できます
- クロス軸方向の配置を行う `justify-content` のようなものです


## 15.7 利用可能なブラウザと古い構文

- IE10は古い構文でサポートされています


## 15.8 まとめ

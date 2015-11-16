# ブレンドモード、フィルター効果、マスキング

- CSSから利用できるSVGの機能が3つあります
- ブレンドモード、フィルター効果、マスキング
- これらは非破壊的な効果であり、元の画像を改変することなくページ上に対してのみ作用します


## 18.1 ブレンドモード

CSSで利用可能なブレンドモードのリストは [Compositing and Blending モジュール](https://drafts.fxtf.org/compositing/) で定義されています

- [Getting to Know CSS Blend Modes](https://dev.opera.com/articles/getting-to-know-css-blend-modes)


### 18.1.1 `background-blend-mode`

- デフォルト値: `normal`
- 要素の背景にあるレイヤーをブレンドするために使われます
- 対象の要素が持つ背景レイヤーだけがブレンドされます
- このプロパティは要素というコンテキストの中でのみ機能します
- 要素自体は他のどの部分ともブレンドされません

```css
E {
  background-blend-mode: multiply;
}
```

#### 18.1.1.1 背景画像と背景色のブレンド

背景画像と背景色を指定しブレンドモードを適用します。

```css
E {
  background: url(foo.png) #f00;
  background-blend-mode: screen;
}
```

#### 18.1.1.2 2つの画像のブレンド

複数の背景画像を指定しブレンドモードを適用します。

```css
E {
  background-color: transparent;
  background-image: url(foo.png), url(bar.png);
  background-blend-mode: multiply;
}
```

### 18.1.1.3 複数回のブレンド

`foo.png` に `multiply` が適用され、その後 `bar.png` に `screen` が適用される

```css
# {
  background-color: #fff;
  background-image: url(foo.png), url(bar.png);
  background-blend-mode: multiply, screen;
}
```

### 18.1.2 `mix-blend-mode`

- ある要素と別の要素をブレンドする
- 指定された要素の背後にあるすべての要素に対してコンテンツや背景がブレンドされます


```css
E {
  background-image: url(foo.png);
}
F {
  mix-blend-mode: multiply;
}
```

### 18.1.3 isolation

- デフォルト値: `auto`
- 対象の要素でスタックコンテキストを指定します（レイヤーの最背面をリセットする）
- [スタック文脈](https://developer.mozilla.org/ja/docs/Web/Guide/CSS/Understanding_z_index/The_stacking_context)
- 新しいスタックコンテキストを作成するには、`isolate` という値を指定します

```css
E {
  isolation: isolate;
}
```

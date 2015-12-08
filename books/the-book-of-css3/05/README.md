# Webフォント

## 5.1 `@font-face` ルール


```css
/*
 * Font Face
 * @font-family フォントの名前を指定（シングルクオートで囲めば複数指定可）
 * @src
    - local() フォントがユーザのマシンにインストール済みかどうかを調べます（非推奨）
    - url() インストールされていなかった場合に指定されたアドレスが使用されます
    - format() フォントの種類を指定
 */
@font-face {
  font-family: FontName;
  src: local(`fontname`), url('path/filename.otf') format('opentype');
}

E {
  font-family: FontName;
}
```

### 5.1.1 複数のフォントフェイスの定義

- 太字や斜体などの複数のフォントフェイスを使いたい場合には、それぞれのフォントフェイスを
個別に定義する必要があります

```css
@font-face {
  font-family: 'Getium Basic';
  src: url('Gentium Basic') format('woff');
}
@font-face {
  font-family: 'Getium Basic';
  font-style: italic;
  src: url('GenBasI.woff') format('woff');
}
h1 {
  font-family: 'Gentium Basic', sans-serif;
  font-style: italic;
}
```

## 5.1.2 実在するフォントフェイスと生成されたフォントフェイス

- Webフォントを使う場合、利用しようとしているすべてのフォントフェイスについてフォントファイル
を用意してリンクを記述する必要があります。そうしないと、ブラウザがフォントフェイスを自動生成
するため、多くの場合は見苦しい表示になってしまいます
- 斜体のスタイルを使う場合、`@font-face` の中でわすれずに斜体のフォントフェイスも定義しましょう



### 5.2.3 構文の詳細

```css
@font-face {
  font-family: 'Gentium Basic';
  src: url('GenBkBasR.eot');
  src: url('GenBasR.eot.?#iefix') format('embeded-opentype'),
       url('GenBkBasR.woff') format('woff'),
       url('GenBkBasR.ttf') format('truetype');
}
```

1. IE8以前のための`EOT`形式のフォントを指定
2. IE9での互換性の問題のために再び`EOT`形式のフォントを指定。
  （互換性の問題は重要ではなくなっているので各自の判断で削除してしまっても構わない）
3. 大多数のブラウザで使われる`WOFF`形式のフォントを指定
4. Android 4.3以前の古いブラウザ向けに`TTF`形式のフォントを指定


## 5.4 Webフォント

```css
@font-face {
  font-family: 'CartoonistHand';
  src: url('CartoonisHand.woff') format('woff');
}
@font-face {
  font-family: 'CartoonisHand';
  font-style: italic;
  src: url('CartoonisHand-Italic.woff') format('woff');
}
@font-face {
  font-family: 'CartoonisHand';
  font-weight: bold;
  src: url('CartoonistHand-Bold.woff') format('woff');
}
@font-face {
  font-family: 'AirstreamRegular';
  src: url('Airstream.woff') format('woff');
}
.font-face h1 { font-family: ChunkFiveRegular, sans-serif; }
.font-face h2 { font-family: AirstreamRegular, cursive; }
.font-face p { font-family: CartoonisHand, sans-serif; }
```


## 5.5 フォントの読み込みのコントロール

自分でフォントをホスティングしている場合には、[Web Font Loader](https://github.com/typekit/webfontloader)
などの利用を検討するとよいでしょう。ここではイベントハンドラが用意され、フォントの読み込みに
合わせてページの表示を動的にコントロールできるようになります


## 5.6 その他のプロパティ

### 5.6.1 `font-size-adjust`

- CSSのフォントスタックの最も大きな問題は、それぞれのフォントのサイズが大きく異なる可能性があるという点です
- `font-size-adjust` プロパティを使うと `font-size` を動的に変更でき、表示に一貫性を与えることができます

```css
E {
  font-size-adjust: [number];
}
```

ここでの `number` は、フォントの高さに対する小文字の `x` の高さ( `x-height` )の割合を表します。
例えば大文字の高さが `16px` の場合に小文字の `x` を高さ `8px` で表示したい場合、`font-size-adjust` は
16分の8つまり `0.5` を指定します

```css
p {
  font-size-adjust: 0.5;
}
```


### 5.6.2 `font-stretch`

- 一部のフォントファミリーでは、幅を伸縮できます

```css
E {
  font-stretch: [keyword];
}
```

`keyword` には幅の狭いものから順に `ultra-condensed` `extra-condensed` `condensed`
`semi-condensed` `normal` `semi-expanded` `expanded` `extra-expanded` `ultra-expanded`
のいずれかを指定できます。これらのキーワードはフォントのバリエーション名に対応指定います

```css
h1 {
  font-family: 'PT Sans', sans-serif;
}
h1.narrow {
  font-stretch: condensed;
}
```


## 5.7 OpenType の機能

- OpenType フォントを使うと、単なるフォントフェイスや太さのバリエーションをはるかに超えた設定を行えます
- リガチャー（合字）やスウォッシュ（一部を長く伸ばした装飾）、特殊な数字など。

これらの用語については Magnet Studio による [Beginners Guide to OpenType](http://www.magnetstudio.com/2014/03/22/beginners-guide-to-opentype/)
でわかりやすく解説されています


### 5.7.1 フォントの機能の有効化

```css
E {
  font-feature-settings: 'parameters';
}
```

`parameters` には、フォントの機能を表す略称と有効化と無効化のための真偽値を複数指定できます


__例) discretionary lightures（任意の合字）を表す `dlig` を有効化__

```css
E {
  font-feature-settings: 'dlig' on;
}
```

__例) スモールキャピタルの機能を無効化__

```css
E {
  font-fature-settings: 'smcp' off;
}
```

__例) 複数のパラメーターを指定__

```css
E {
  font-feature-settings: 'liga', 'tnum' off;
}
```


### 5.7.2 フォントの機能を指定するプロパティ

- `font-feature-settings` で有効化や無効化を行うそれぞれの機能は、`font-variant-*` と
呼ばれるプロパティを使って個別に指定することもできます

```css
E {
  font-variant-ligatures: no-discretionary-ligatures;
}
```


## 5.8 まとめ

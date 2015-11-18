# トランジションとアニメーション

## 14.1 トランジション

- [CSS Transitions](http://www.w3.org/TR/css3-transitions/)
- トランジションは暗黙のアニメーションです
- トランジションには、初期値と終了値とトランジション自体そしてトリガーという4つの設定項目が必要です

```css
E {
  transition-property: [keyword];
  transition-duration: [time];
  transition-timing-function: [keyword];
  transition-delay: [time];
}

E {
  transition: [property] [duration] [timing-function] [delay];
}
```

### 14.1.1 `transition-property`

```css
E {
  transition-property: [keyword];
}
```

- 複数指定可
-  [トランジションの対応しているプロパティのリスト](http://www.w3.org/TR/css3-transitions/#animatable-css)


|値|説明|
|:--|:--|
|`all`|トランジションに対応しているすべてのプロパティに適用します|
|`none`|トランジションしません|
|CSSのプロパティ|指定した任意のCSSプロパティに適用します|


### 14.1.2 `transition-duration`

```css
E {
  transition-duration: [time];
}
```

- トランジションの開始から完了までの時間を指定します
- トランジションを行うために指定が必須なのはこのプロパティだけです
- `time` の単位は `ms` (ミリ秒) また `s` (秒)です
- 負の値を指定すると `0` として扱われます


### 14.1.3 `transition-timing-function`

- トランジションの進み方を指定します
- キーワードか `cubic-bezier()` 関数または `steps()` 関数を記述します


#### 14.1.3.1 キーワードによる指定

- `ease` `linear` `ease-in` `ease-out` `ease-in-out`


#### 14.1.3.2 3次ベジェ曲線

```css
E {
  transition-timing-function cubic-bezier([x1], [y1], [x2], [y2]);
}
```

- 3次ベジェ曲線とは、4つの点を使って描かれるスムーズに連続した曲線のことです
- これらの点は `P0` `P1` `P2` `P3` と呼ばれます

![3次ベジェ曲線の例](https://d262ilb51hltx0.cloudfront.net/max/930/1*vWeVRPeCyo8Ul6G7CPibLA.png)

|点|座標値(x, y)|
|:--|:--|
|`P0`|`(0, 0)`|
|`P1`|`(0.6, 0.1)`|
|`P2`|`(0.15, 0.7)`|
|`P3`|`(1.0, 1.0)`|

|キーワード|`cubic-bezier()`での同等の値|
|:--|:--|
|`ease`|`0.25, 0.1, 0.25, 0.1`|
|`linear`|`0, 0, 1, 1`|
|`ease-in`|`0.42, 0, 1, 1`|
|`ease-out`|`0, 0, 0.58, 1`|
|`ease-in-out`|`0.42, 0, 0.58, 1`|


#### 14.1.3.3 `steps()` 関数

```css
E {
  transition-timing-function: steps([count], [direction]);
}
```

- `count` はアニメーションを分割する数を表し、整数で指定します
- `direction` は、省略可能で `start` または `end` (デフォルト)のいずれかを指定します

![トランジション - steps](http://www.w3.org/TR/css3-transitions/step.png)


__サンプル__

```css
E {
  transition-timing-function: steps(4, start);
}

E {
  transition-timing-function: steps(4, end);
}
```

### 14.1.4 `transition-delay`

```css
E {
  transition-delay: [time];
}
```

- トランジションを開始する時間を指定します
- `time` の単位は `ms` (ミリ秒)か `s` (秒)です
- デフォルトは `0`
- マイナスの指定をした場合は、指定した時間を差し引いて再生されます

```css
E {
  transition-duration: 4s;
  transition-delay: -2s;
}
/* 後半の2秒分だけが表示されます */
```


#### 14.1.5 `transition` を使った省略記法

```css
E {
  transition: [property] [duration] [timing-function] [delay];
}
```

- 時間の指定が2回行われるため注意が必要です
- 1回目が `duration` 2回目が `delay` を表します
- 1つだけ時間の指定がある場合は、`duration` であるとみなされます


### 14.1.6 全体のコード

```css
E {
  font-size: 150%;
  transition: font-size 2s ease-out 250ms;
}

E:hover {
  font-size: 600%;
}
```

### 14.1.7 複数のトランジション

- 個々のプロパティや短縮記法の中で、値をコンマで区切って記述すると複数のトランジションを
指定できます


```css
/* 以下の2つのルールは同じ効果 */
E {
  transition-property: border-width, height, padding;
  transition-duration: 4s, 500ms, 4s;
}
E {
  transition: border-width 4s, height 500ms, padding 4s;
}
```

## 14.2 アニメーション

- [CSS Animations](http://www.w3.org/TR/css3-animations/)


```css
E {
  animation-name: [name];
  animation-duration: [time];
  animation-timing-function: [value];
  animation-delay: [time];
  animation-iteration-count: [count];
  animation-direction: [keyword];
  animation-fill-mode: [keyword];
  animation-play-state: [keyword];
}
```

### 14.2.1 キーフレーム

- CSSでのアニメーションは、複数のトランジションが続けて発生するものとして捉えられます
- アニメーションの作成の第一歩として、トランジションの開始と終了の時点を表すキーフレーム
を定義します
- 同じ時点を表すキーフレームが重複している場合、後で宣言されたものが有効となります


```css
@keyframes [name] {
  [selector] {
    [property]: [value];
  }
}
```

__例) シンプルなキーフレーム__

```css
@keiframes expand {
  from { border-width: 4px; } /* アニメーションの開始時点 */
  50% { border-width: 12px; } /* アニメーションの中間地点 */
  to { /* 終了時点 */
    border-width: 4px;
    height: 100%;
    width: 100%;
  }
}
```

__例) セレクターを重ねて書く__

```css
@keyframes expand {
  from, to { border-width: 4px; }
  50% { border-width: 12px; }
  to {
    height: 100%;
    width: 100%;
  }
}
```

### 14.2.2 `animation-name`

```css
E {
  animation-name: [name];
}
```

- `@keyframes` ルールで定義した名前を参照するために使われます
- `none` を指定するとアニメーションは行われません


### 14.2.3 `animation-duration`

```css
E {
  animation-duration: [time];
}
```

- 構文は `transition-duration` と同一です


### 14.2.4 `animation-timing-function`

```css
E {
  animation-timing-function: [value];
}
```

- 構文は `transition-timing-function` と同一です


### 14.2.5 `animation-delay`

```css
E {
  animation-delay: [time];
}
```
- 構文は `transition-delay` と同一です


### 14.2.6 `animation-iteration-count`

```css
E {
  animation-iteration-count: [count];
}
```

- 繰り返しの回数を指定する
- デフォルトは `1`
- `infinite` が指定された場合ずっと繰り返されます
- `0` や負の値が指定された場合、アニメーションは1回も実行されません


### 14.2.7 `animation-direction`

```css
E {
  animation-direction: [keyword];
}
```

- アニメーションは先頭から末尾に発生しますが、この方向を反転させることもできます

|値|説明|
|:--|:--|
|`normal`|デフォルト|
|`alternate`|最後まで到達したあと逆方向に実行して先頭に戻ります。奇数回目のアニメーションは順方向、偶数回目のアニメーションは逆方向|


### 14.2.8 `animation-fill-mode`

```css
E {
  animation-fill-mode: [keyword];
}
```

- 有限回数のアニメーションでは、アニメーションが実行されてないときの表示を指定できます

|値|説明|
|:--|:--|
|`none`|デフォルト|
|`backwards`|アニメーションの開始前の要素には `0%` `from` のスタイルが適用されます |
|`forwards`|アニメーションの終了後も `100%` `to` のスタイルが引き続き適用されます|
|`both`|`backwards` と `forwards` の効果がともに発生します|


### 14.2.9 `animation-play-state`

```css
E {
  animation-play-state: [keyword];
}
```

- アニメーションがアクティブな状態かどうかを指定する

|値|説明|
|:--|:--|
|`running`|アニメーションが実行中|
|`paused`|アニメーションが実行中ではない|


### 14.2.10 `animation` を使った短縮記法

```css
E {
  animation: [name] [duration] [timing-function] [delay] [iteration-count] [direction] [fill-mode] [play-stete]
}
```

### 14.2.12 複数のアニメーション

```css
E {
  animation-name: first-anim, second-anim;
  animation-duration: 6s, 1.25ms;
  animation-delay: 0, 750ms;
}
E {
  animation: first-anim 6s, second-anim 1.25ms 750ms;
}
```

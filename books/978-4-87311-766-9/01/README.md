# イントロダクション

## Web 標準は敵か？味方か？
### 標準化のプロセス
1. Edotor's Draft(ED): 
2. First Public Working Draft(FPWD):
3. Working Draft(WD):
4. Candidate Recommendation(CR):
5. Proposed Recommendation(PR):
6. Recommendation(REC)

### CSS3, CSS4,そしてその他の創造物たち
CSS2.1 で定義されている機能を拡張したものについては、3というレベル番号が与えられました
- [CSS Syntax](https://www.w3.org/TR/css-syntax-3)
- [CSS Cascading and Inheritance](https://www.w3.org/TR/css-cascade-3)
- [CSS Color](https://www.w3.org/TR/css3-color)
- [Selectors](https://www.w3.org/TR/selectors)
- [CSS  Backgrounds & Borders](https://www.w3.org/TR/css3-background)
- [CSS Values and Units](https://www.w3.org/TR/css-values-3)
- [CSS Text](https://www.w3.org/TR/css-text-3)
- [CSS Text Decoration](https://www.w3.org/TR/css-text-decor-3)
- [CSS Fonts](https://www.w3.org/TR/css3-fonts)
- [CSS Basic User Interface](http://www.w3.org/TR/css3-ui)

一方、まったく新しい概念を表すモジュールには1というレベル番号が与えられました
- [CSS Transforms](https://www.w3.org/TR/css-transform-1)
- [Compositiong and Blending](https://www.w3.org/TR/compositiong-1)
- [Filter Effects](https://www.w3.org/filter-effects-1)
- [CSS Masking](https://www.w3.org/TR/css-masking-1)
- [CSS Flexible Box Layout](https://www.w3.org/TR/css-flexbox-1)
- [CSS Grid Layout](https://www.w3.org/TR/css-grid-1)

__CSS 3という言葉は流行していますが、CSS3そのものを定義した仕様はどこにもありません__

### ベンダー接頭辞の物語

## CSS コーディングのコツ
### 重複を最小限に抑える
#### 保守の容易さと簡潔さの両立
#### currentColor
- [CSS Color Level3](https://www.w3.org/TR/css3-color)

#### 継承 _Inherit_
### 数字ではなく自分の眼に頼る
我々の眼には縦方向の中央に配置したものをずれて認識してしまうことがよく知られています。
中央にあると認識させるためには、計算上の中央よりも少し上に対象を配置する必要があります。

このような錯覚は、視覚的デザインの分野ではしばしば見られます。
我々には __錯覚を考慮に入れたデザイン__ が求められます。

### レスポンシブWebデザイン
- 幅は固定値ではなくパーセンテージで指定しましょう
- 高い解像度のデバイス上で固定幅の表示にしたい場合、`width` の代わりに `max-width` を使いましょう
- 置換要素(replaced element)では、`max-width` として忘れずに100%を指定しましょう
- 背景画像がコンテナ全体を覆う必要がある場合、`background-size: cover` と指定するとコンテナのサイズを記述する必要がなくなります
- グリッドのセルの中に画像やその他の要素を配置する際には、ビューポートの幅に従って列の数が増えるようにしましょう
- 段組を使ってテキストを配置する場合、小さな画面では1段組みで表示するようにしましょう `column-count` ではなく `column-width` を指定します

大まかに言うと、__メディアクエリでのブレークポイントの前後相対的なサイズ設定を保ち、リキッド（流動的）なレイアウトを実現しよう__ というのがここでの考え方です。

### 短縮気泡を賢く使う
```css
background: url(tr.png) top right,
            url(br.png) bottom right,
            url(bl.png) bottom left;
background-size: 2em 2em;
background-repeat: no-repeat;
```

### プリプロセッサを使うべきか
- CSSの __ファイルサイズや複雑さ__ をコントロールできなくなります
- ブラウザ上で解釈されたり開発者ツールに表示されたりするCSSは開発者自身がかいたものではないため __デバッグが難しくなります__ 
- 開発のプロセスが多少 __遅延__ することになります
- どんな種類の抽象化にも、作業をはじめるための苦労が伴います
- 不完全な抽象化の法則 (law of leaky Abstractions) に注意が必要です。これは「すべての抽象化には不完全さが伴う」というものです

保守の容易さが求められる場合にはプリプロセッサの利用は避けられず、むしろ積極的に利用するべきです。
DRY な状態を保てなくなってきたらプリプロセッサに切り替えるという方針をおすすめします。
過度にプリプロセッサに依存したり、不必要な箇所にもプリプロセッサを利用するのは避けるべきです。
プリプロセッサの導入には慎重な検討が必要であり、単に採用すればよいというものではありません。

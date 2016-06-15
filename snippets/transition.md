# Transition
- [CSS transition の使用](https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)

## Properties

```css
E {
  transition-property: [keyword, ..];
  transition-duration: [time];
  transition-timing-function: [keyword || cubic-bezeir()];
  transition-delay: [time];
}

/* short-hand */
E {
  transition: [property] [duration] [timing-function] [delay];
}
```
> `transition-delay` にマイナスの指定をした場合は、指定した時間を差し引いて再生されます

- [cubic-bezier.com](http://cubic-bezier.com/)


## with JavaScript
トランジションの完了を `transitionend` イベントで検出できます。
`transitionend` イベントは tansition した property の数発行されます。

```js
document.querySelector(element).addEventListener('transitionend', e => {
  console.log(e.propertyName);
});
```

- [transitionend](https://developer.mozilla.org/ja/docs/Web/Events/transitionend)

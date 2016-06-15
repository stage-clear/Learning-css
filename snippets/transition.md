# Transition

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

- [cubic-bezier.com](http://cubic-bezier.com/)


## with JavaScript
トランジションの完了を `transitionend` イベントで検出できます。
`transitionend` イベントは tansition した property の数発行されます。

```js
document.querySelector(element).addEventListener('transitionend', e => {
  console.log(e.propertyName);
});
```
- [](https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions) - トランジション完了の検出
- [transitionend](https://developer.mozilla.org/ja/docs/Web/Events/transitionend)

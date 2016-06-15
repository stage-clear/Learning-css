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

## JavaScript
`transitionend` イベントは tansition した property の数発行される

```js
document.querySelector(element).addEventListener('transitionend', e => {
  console.log(e.propertyName);
});
```

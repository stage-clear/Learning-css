# CSS Transitions
- [CSS Transitions](https://www.w3.org/TR/css3-transitions/)
- [CSS transition の使用](https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)

## Properties

```css
E {
  transition-property: none | <single-transition-property> [, <single-transition-property>];
  transition-duration: <time> [, <time>];
  transition-timing-function: <single-transition-timing-function> [, <single-transition-timing-function>];
  transition-delay: <time> [, <time>];
}

/* shorthand */
E {
  transition: <single-transtion> [, <single-transition>];
  transition: <[property] [duration] [timing-function] [delay]>;
}
```
> `transition-delay` にマイナスの指定をした場合は、指定した時間を差し引いて再生されます

- [`<single-transition-property>`](https://www.w3.org/TR/css3-transitions/#single-transition-property)
- [`<single-transition-timing-function>`](https://www.w3.org/TR/css3-transitions/#single-transition-timing-function)
- [`<single-transition>`](https://www.w3.org/TR/css3-transitions/#single-transition)
- [cubic-bezier.com](http://cubic-bezier.com/)


## with JavaScript
トランジションの完了を `transitionend` イベントで検出できます。
`transitionend` イベントは tansition した property の数だけ発行されます。

```js
document.querySelector(element).addEventListener('transitionend', e => {
  console.log(e.propertyName);
});
```

- [transitionend](https://developer.mozilla.org/ja/docs/Web/Events/transitionend)

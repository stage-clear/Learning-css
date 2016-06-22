# Animation
- [CSS Animation](https://www.w3.org/TR/css3-animations/) - W3
- [CSSアニメーション](https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Animations/Using_CSS_animations) - MDN
- [CSS Animatable Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties) - MDN
- [Animateble](http://leaverou.github.io/animatable/)

## Properties

```css
E {
  animation-name: <single-animation-name> [, <single-animation-name>]*;
  animation-duration: <time> [, <time>]*;
  animation-timing-function: <single-timing-function> [, <single-timing-function>]*;
  animation-iteration-count: <single-animation-iteration-count> [, <single-animation-iteration-count>]*;
  animation-direction: <single-animation-direction> [, <single-animation-direction>]*;
  animation-play-state: <single-animation-play-state> [, <single-animation-play-state>]*;
  animation-delay: <time> [, <time>]*;
  animation-fill-mode: <single-animation-fill-mode> [, <single-animation-fill-mode>]*;
}

/* short-hand */
E {
  animation: <single-animation> [, <single-animation>]*;
  animation: [name] [duration] [timing-function] [delay] [iteration-count] [direction] [fill-mode] [play-state];
}
```

- [`<single-animation-name>`](https://www.w3.org/TR/css3-animations/#single-animation-name) - W3
- [`<single-animation-iteration-count>`](https://www.w3.org/TR/css3-animations/#single-animation-iteration-count) - W3
- [`<single-animation-direction>`](https://www.w3.org/TR/css3-animations/#single-animation-direction) - W3
- [`<single-animation-play-state>`](https://www.w3.org/TR/css3-animations/#single-animation-play-state) - W3
- [`<single-animation-fill-mode>`](https://www.w3.org/TR/css3-animations/#single-animation-fill-mode) - W3
- [`<single-animation>`](https://www.w3.org/TR/css3-animations/#single-animation) - W3

## with JavaScript - event

```js
let el = document.querySelector(ELEMENT);
let button = document.querySelector(BUTTON);

el.addEventListener('animationstart', listener, false);
el.addEventListener('animationiteration', listener, false);
el.addEventListener('animationend', listener, false);
button.addEventListener('click', toggleAnim, false);

function listener(e) {
  let msg = '';
  switch(e.type) {
    case 'animationstart': 
      msg = 'Started: elapsed time is' + e.elapsedTime;
      break;
    case 'animationend': 
      msg = 'Ended: elapsed time is' + e.elapsedTime;
      break;
    case 'animationiteration': 
      msg = 'New loop started at time ' + e.elapsedTime;
      break;
  }
  console.log(`[${e.type}]: ${msg}`);
}

function toggleAnim(e) {
  let state = el.style.animationPlayState;
  if (state === '' || state === 'running') {
    state = 'paused';
  } else {
    state = 'running';
  }
  el.style.animationPlayState = state;
}
```

- [AnimationEvent - MDN](https://developer.mozilla.org/en-US/docs/Web/API/AnimationEvent)
- [animationstart - MDN](https://developer.mozilla.org/en-US/docs/Web/Events/animationstart)
- [animationiteration - MDN](https://developer.mozilla.org/en-US/docs/Web/Events/animationiteration)
- [animationend - MDN](https://developer.mozilla.org/en-US/docs/Web/Events/animationend)
- [animation-play-state - MDN](https://developer.mozilla.org/ja/docs/Web/CSS/animation-play-state)


## with JavaScript - CSSKeyframesRule

- [Sample](https://jsfiddle.net/walfo/ju4tbe3w/)

```html
<style>
.box {
  /* style */
}
@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
</style>
```

```js
var anim = document.styleSheets[1].cssRules[1];

// findRule
console.log(findRule());
// appendRule
aButton.addEventListener('click', appendRule, false);
// deleteRule
bButton.addEventListener('click', deleteRule, false);

function findRule() {
  return anim.findRule('100%');
}

function appendRule() {
  anim.appendRule('50% {transform: rotate(60deg)} ');
}

function deleteRule() {
  anim.deleteRule('50%');
}
```

- [StyleSheet - MDN](https://developer.mozilla.org/en-US/docs/Web/API/StyleSheet)
- [CSSStyleSheet - MDN](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleSheet)
- [CSSKeyframesRule - MDN](https://developer.mozilla.org/ja/docs/Web/API/CSSKeyframesRule)


## Control CSSAnimation by JavaScript
- if the `display` property is set to `none`, the `animation-iteration-count` property is reset.

[Sample](https://jsfiddle.net/walfo/2bwf8uo4/)

### Start
- `animation-play-state: running`
- `animation-*` を設定したクラスを付与する

### Pause and Resume
- Pause: `animation-play-state: paused` , Resume: `animation-play-state: running`

### Stop and Start
- Stop: `display: none` , to Start `dispaly: block`
- Stop: `classList.remove('.animate')`, `classList.add('.animate')`

### Hidden, keep to be animated
- `visibility: hidden` or `opacity: 0`



# Animation
- [CSSアニメーション](https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Animations/Using_CSS_animations)
- [CSS Animatable Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties)
- [Animateble](http://leaverou.github.io/animatable/)

## Properties

```css
E {
  animation-name: [name, ...];
  animation-duration: [time, ...];
  animation-timing-function: [value, ...];
  animation-delay: [time, ...];
  animation-iteration-count: [count, ...];
  animation-direction: [keyword, ...];
  animation-fill-mode: [keyword, ...];
  animation-play-state: [keyword, ...]
}

/* short-hand */
E {
  animation: [name] [duration] [timing-function] [delay] [iteration-count] [direction] [fill-mode] [play-state];
}
```

## with JavaScript

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

- [animationstart](https://developer.mozilla.org/en-US/docs/Web/Events/animationstart)
- [animationiteration](https://developer.mozilla.org/en-US/docs/Web/Events/animationiteration)
- [animationend](https://developer.mozilla.org/en-US/docs/Web/Events/animationend)
- [animation-play-state](https://developer.mozilla.org/ja/docs/Web/CSS/animation-play-state)

# Animation

## Keyframes
## Setting Up Your Keyframe Animation
## Animated Elements
### The `animation-name` Property
### The `animation-duration` Property
### The `animation-iteration-count` Property
### The `animation-direction` Property
### The `animation-delay` Property
### Animation Events
#### Animation chaining

```css
.rainbow {
  animation-name: red, orange, yellow, blue, green;
  animation-duration: 1s, 3s, 5s, 7s, 11s;
  animation-delay: 3s, 4s, 7s, 12s, 19s;
}
```

Animation chaining with JS

```js
document.querySelectorAll('li')[0].addEventListener('animationend', e => {
  document.querySelectorAll('li')[1].style.animationName = 'orange';
}, false);
document.querySelectorAll('li')[1].addEventListener('animationend', e => {
  document.querySelectorAll('li')[2].style.animationName = 'yellow';
}, false);
document.querySelectorAll('li')[2].addEventListener('animationend', e => {
  document.querySelctorAll('li')[3].style.animationName = 'green';
}, false);
```

```css
li:first-of-type {
  animation-name: red;
  animation-duration: 1s;
}
li:nth-of-type(2) {
  animation-duration: 3s;
}
li:nth-of-type(3) {
  animation-duration: 5s;
}
li:nth-of-type(4) {
  animation-duration: 7s;
}
```

## Animation, Specificity, and Precedence Order
## Animation Events and Prefixing
### `animationstart`
- `animation-delay` が設定されている場合は、delay 時間が経過後にイベントが発行されます
- `animation-name` が複数ある場合は、値の数だけイベントが発行されます

### `animationend`

> (animation-duration * animation-iteration-count) + animation-delay = time

### `animationiteration`
- イテレートする毎にイベントを発行します
- `animationstart` および `animationend` 時には、イベントは発行されません
- `animation-iteration-count` が存在しない場合や、その値が `<= 1` の場合はイベントが発行されません
- `animation-duration: 0s` の場合はイベントは発行されません

## Ohter Considerations

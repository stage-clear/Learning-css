# Animation

## Keyframes
## Setting Up Your Keyframe Animation
## Animated Elements
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

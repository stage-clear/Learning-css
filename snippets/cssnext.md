# cssnext 

__custom property & var()__

```css
:root {
  --main-color: red;
  --gradation: linear-gradient(top, var(--main-color), white);
}
a {
  color: var(--main-color);
}
div {
  background: var(--gradation);
}
```

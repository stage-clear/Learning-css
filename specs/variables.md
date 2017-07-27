# Custom properties and Variables

```css
:root {
  --background: #fff;
}

div {
  --background: #ccc;
  background-color: var(--background);
}

div:hover {
  --background: #555;
}
```

```html
<div id="empty-box"></div>
<button id="set">Set value</button>
<button id="remove">Remove value</button>
<input type="color" id="color-picker" value="#ccc">
```

```js
const root = document.documentElement
const el = document.querySelector('#empty-box')
const style = window.getComputedStyle(style)
const value = style.getPropertyValue('--background')
// el.style.setProperty('--background')
// el.style.removeProperty('--background')
```

## Use with JavaScript
### Get the value of a Custom Property

```js
const el = document.querySelector('#id')
const style = window.getComputedStyle(el /* [, pseudoElm] */)
const value = style.getPropertyValue('--background')
```

### Set the value of a Custom Property

```js
el.style.setProperty('--background', 'red' /*, priority */)
```

### Remove the Value of a Custom Property

```js
el.style.removeProperty('--background')
```

### Change the Value of a Custom Property with Color picker

```js
const picker = document.querySelector('#color-picker')
picker.addEventListener('change', function() {
  el.style.setProperty('--background', this.value)
}, false)
```

## References
- [CSS Custom Properties - Dynamic Change With And Without JavaScript](http://vanseodesign.com/css/custom-properties-and-javascript/)

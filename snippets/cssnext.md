# cssnext 

__custom property & var()__

- [CSS Custom Properties for Cascading Variables](http://www.w3.org/TR/css-variables/)
- [postcss-custom-properties](https://github.com/postcss/postcss-custom-properties)

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

__custom media queries__

- [W3C CSS Custom Media Queries](https://drafts.csswg.org/mediaqueries/#custom-mq)
- [postcss-custom-media](https://github.com/postcss/postcss-custom-media)

```css
@custom-media --small-viewport (max-width: 320px);

@media (--small-viewport) {
  .container {
    width: 100%;
  }
}
```

__custom selectors__

- [postcss-custom-selectors](https://github.com/postcss/postcss-custom-selectors)
- [W3C CSS Extensions(Custom Selectors)](https://drafts.csswg.org/css-extensions/#custom-selectors)

```css
@custom-selector :--heading h1, h2, h3, h4, h5, h6;

article :--heading {
  font-weight: normal;
}

article :--heading + p {
  font-size: 13px;
}
```


__matches pseudo-class__

- [The Matches-any Pseudo-class: :matches()](https://drafts.csswg.org/selectors-4/#matches)
- [postcss-selector-matches](https://github.com/postcss/postcss-selector-matches)

```css
p:matches(:first-child, .special) {
  color: red;
}
```

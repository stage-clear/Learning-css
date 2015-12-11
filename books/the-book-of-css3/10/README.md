# 色と不透明度

## 10.1 `opacity` プロパティ

```css
E {
  opacity: [number];
}
```


## 10.2 色の記法に対する拡張と追加

### 10.2.1 アルファチャンネル

```css
E {
  color: rgba([red], [green], [blue], [alpha]);
}
```

### 10.2.2 色相、彩度、明度

![HSLでの色の表現方法](https://upload.wikimedia.org/wikipedia/commons/c/cb/HSL_color_solid_cylinder_alpha_lowgamma.png)

```css
/*
 * hsl
 */
E {
  color: hsl([hue], [saturation], [lightness]);
}
```


### 10.2.3 HSLA

```css
E {
  color: hsl([hue], [saturation], [lightness], [alpha]);
}
```

### 10.2.4 色を表す変数 `currentColor`

- CSS3 では色を表す `currentColor` というキーワードも追加されました
- 要素の `color` プロパティに指定されている値が、その要素の `currentColor` にセットされます

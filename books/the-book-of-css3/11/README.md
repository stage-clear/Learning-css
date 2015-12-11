# グラデーション

## 11.1 線形グラデーション

```css
E {
  background-image: linear-gradient([start], [end]);
}
```

### 11.1.1 グラデーションの方向

```css
/*
 * @value {direction} keyword [to top | to right bottom... | deg]
 * @value {start} color
 * @value {end} color
 */
E {
  background-image: linear-gradient([direction], [start], [end]);
}
```

__例__

```css
E { background-image: linear-gradient(to left, black, white); }
E { background-image: linear-gradient(to top right, black, white); }
E { background-image: linear-gradient(120deg, black, white); }
```


### 11.1.2 カラーストップの追加

```css
E {
  background-image: linear-gradient([start], [color-stop], [end]);
}
```

__例__

```css
E { background-image: linear-gradient(black, white 75%, black); }
E { background-image: linear-gradient(to right, black, white 75%); }
E { background-image: linear-gradient(to right, black 50%, white); }
E { background-image: linear-gradient(to right, black, white 50%, black 1px); }
```


### 11.1.3 線形グラデーションの繰り返し

- `repeating-linear-gradient()` 関数を使うと要素全体に同じグラデーションが繰り返し描画
されるようになります

```css
E { background-image: repeating-linear-gradient(white, black 25%); }
```

__いろいろな例__

```css
.gradient-1 {
  background-image: repeating-linear-gradient(to left, black, white, black 25%);
}
.gradient-2 {
  background-image: repeating-linear-gradient(45deg, black, white 2px, black 10px);
}
.gradient-3 {
  background-image: repeating-linear-gradient(315deg, black, black 2px, white 2px, white 4px);
}
```


## 11.2 円形グラデーション

- `radial-gradient()` 関数で円形グラデーションを定義します

```css
E {
  background-image: radial-gradient([circle], [start], [end]);
}
```

__いろいろな例__

```css
E { background-image: radial-gradient(circle at 100% 50%, white, black); }
E { background-image: radial-gradient(circle 50px, black, white); }
E { background-image: radial-gradient(circle closest-corner at 10% 60%, white, black); }
E { background-image: radial-gradient(circle closest-side at 10% 60%, white, black); }
E { background-image: radial-gradient(circle farthest-corner at 0% 100%, white, black, white, black); }
E { background-image: radial-gradient(circle farthest-side at 0% 100%, white, black, white, black); }
```


### 11.2.2 複数のカラーストップ

```css
E { background-image: radial-gradient(circle farthest-side, black, white, black); }
E { background-image: radial-gradient(circle farthest-side, black, white 25%, black); }
E { background-image: radial-gradient(circle farthest-side at left, white, black 25%, white 75%, black); }
E { background-image: radial-gradient(circle closest-side at 40% 50%, white, white 25%, black 50%, white 75%, black); }
```

### 11.2.3 円形グラデーションの繰り返し

- `repeating-radial-gradient()` を使うとグラデーションを繰り返すことができます

__基本構文__

```css
E {
  background-image: repeating-radial-gradient(circle, [start], [end]);
}
```

__いろいろな例__

```css
E { background-image: repeating-radial-gradient(circle farthest-corner at right top, black, white 10%, black 15%); }
E { background-image: repeating-radial-gradient(circle farthest-corner at left, white, white 10px, black 15px); }
E { background-image: repeating-radial-gradient(circle farthest-corner, white, black 1px, white 2px); }
```


## 11.3 複数のグラデーション

- CSS3 では背景画像を複数指定することができます。つまり、グラデーションもコンマで区切って
複数指定することが可能です

```css
.linears {
  background-image:
    linear-gradient(to right bottom, black, white 50%, transparent 50%),
    linear-gradient(to left bottom, black, white 50%, black 50%);
}

.radials {
  background-image:
    radial-gradient(closest-side circle at 20% 50%, white, black 95%, transparent),
    radial-gradient(closest-side circle at 50% 50%, white, black 95%, transparent),
    radial-gradient(closest-side circle at 80% 50%, white, black 95%, transparent);
}
```


## 11.4 まとめ

- [CSS3 Patterns Gallery](http://lea.verou.me/css3patterns/)

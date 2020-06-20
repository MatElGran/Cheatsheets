# CSS

## Font size dependant line height

Unitless value is the most recommended way to handle line-height

However, it sets too much line height in larger font sizes,
and in order to establish an optimal readability, we must manually
tweak it on every font-size increment, down to 1.1 on very large font sizes.

Instead, we can use a smaller relative size and add fixed "paddings" (called leading)
that will have a decreasing importance as the font size increases

```css
.parent * {
  line-height: calc(2px + 2ex + 2px);
}
```

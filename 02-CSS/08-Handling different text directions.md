# 08-Handling different text directions

> To understand the importance of writing modes to modern CSS.

---

## What are writing modes?

A writing mode in CSS refers to whether the text is running **horizontally** or **vertically**. The `writing-mode` property lets us switch from one writing mode to another.

The three possible values for the `writing-mode` property are:

- `horizontal-tb`: Top-to-bottom **block** flow direction. Sentences run horizontally.
- `vertical-rl`: Right-to-left **block** flow direction. Sentences run vertically.
- `vertical-lr`: Left-to-right **block** flow direction. Sentences run vertically.

---

## Writing modes and block and inline layout

Block and inline is tied to the writing mode of the document, and not the physical screen. When we switch the writing mode, we are changing which direction is **block** and which is **inline**.

This figure shows the two dimensions when in a horizontal writing mode:

![](../_assets/_images/horizontal-tb.png ':size=450')

This figure shows the two dimensions in a vertical writing mode:

![](../_assets/_images/vertical.png ':size=300')

---

## Logical properties and values

The property mapped to `width` when in a horizontal writing mode is called `inline-size` — it refers to the size in the **inline dimension**.

The property for `height` is named `block-size` and is the size in the **block dimension**. 

### Logical margin, border, and padding properties

The `margin-top` property is mapped to `margin-block-start` — this will always refer to the margin at the start of the block dimension.

The `padding-left` property maps to `padding-inline-start`, the padding that is applied to the start of the inline direction.

The `border-bottom` property maps to `border-block-end`, which is the border at the end of the block dimension.

### Logical values

There are also some properties that take physical values of `top`, `right`, `bottom`, and `left`. These values also have mappings, to logical values — `block-start`, `inline-end`, `block-end`, and `inline-start`.

```css
.box {
    inline-size: 200px;
    writing-mode: vertical-rl;
}

img {
    float: inline-start;
    margin-inline-end: 10px;
    margin-block-end: 30px;
}
```



---

?> {docsify-updated}
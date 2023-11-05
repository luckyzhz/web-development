# 10-CSS values and units

> To learn about the different types of values and units used in CSS properties.

---

## What is a CSS value?

**Value types** will be surrounded by **angle brackets**, such as `<color>` or `<length>`. A value type in CSS is a way to define a **collection** of allowable values.

When you see the value type `<color>` as valid for a particular property, that means you can use any valid color as a value for that property, as listed on the [`<color>`](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value) reference page.

---

## Numbers and lengths

### Numeric value types

| Data type | Description |
| :--- | :--- |
| `<integer>` | An `<integer>` is a whole number such as `1024` or `-55`. |
| `<number>` | A `<number>` represents a decimal number — it may or may not have a decimal point with a fractional component. For example, `0.255`, `128`, or `-1.2`. |
| `<dimension>` | A `<dimension>` is a `<number>` with a **unit** attached to it. For example, `45deg`, `5s`, or `10px`. `<dimension>` is an umbrella category that includes the `<length>`, `<angle>`, `<time>`, and `<resolution>` types. |
| `<percentage>` | A `<percentage>` represents a fraction of some **other** value. For example, `50%`. Percentage values are always relative to another quantity. For example, an element's length is         relative to its parent element's length. |

### Lengths

The **numeric type** you will come across most frequently is `<length>`. For example, `10px` (pixels) or `30em`. There are two types of lengths used in CSS — **relative** and **absolute**.

#### Absolute length units

| Unit | Name                | Equivalent to            |
| ---- | ------------------- | ------------------------ |
| `cm` | Centimeters         | 1cm = 37.8px = 25.2/64in |
| `mm` | Millimeters         | 1mm = 1/10th of 1cm      |
| `Q`  | Quarter-millimeters | 1Q = 1/40th of 1cm       |
| `in` | Inches              | 1in = 2.54cm = 96px      |
| `pc` | Picas               | 1pc = 1/6th of 1in       |
| `pt` | Points              | 1pt = 1/72nd of 1in      |
| `px` | Pixels              | 1px = 1/96th of 1in      |

#### Relative length units

Relative length units are relative to something else, perhaps the size of the parent element's font, or the size of the viewport. Some of the most useful units for web development are listed in the table below:

| Unit | Relative to |
|---|---|
| `em` | Font size of the **parent**, in the case of **typographical** properties like `font-size`;<br> or font size of the element **itself**, in the case of **other properties** like `width`. |
| `ex` | x-height of the element's font. |
| `ch` | The advance measure (width) of the glyph "0" of the element's font. |
| `rem` | Font size of the **root element**. |
| `lh` | Line height of the element. |
| `rlh` | Line height of the **root element**. |
| `vw` | 1% of the viewport's width. |
| `vh` | 1% of the viewport's height. |
| `vmin` | 1% of the viewport's smaller dimension. |
| `vmax` | 1% of the viewport's larger dimension. |
| `vb` | 1% of the size of the initial containing block in the direction of the root element's block axis. |
| `vi` | 1% of the size of the initial containing block in the direction of the root element's inline axis. |
| `svw`, `svh` | 1% of the small viewport's width and height, respectively. |
| `lvw`, `lvh` | 1% of the large viewport's width and height, respectively. |
| `dvw`, `dvh` | 1% of the dynamic viewport's width and height, respectively. |

---

## Color

- Keywords:
  - `color: greenyellow;`, `background-color: antiquewhite;`
- Hexadecimal RGB values (An *optional* alpha component represents the color's **opacity**):
  - `color: #02798b;`, `background-color: #128a7d;`
  - `background: #128a7d5e;`
- RGB values (An *optional* alpha component represents the color's **opacity**):
  - `color: rgb(31 120 50);`
  - `background: rgb(30% 20% 50%);`
  - `color: rgb(255 122 127 / 80%);`
  - `background: rgb(255 122 127 / 0.1);`
- HSL values (hue, saturation, and lightness. An *optional* alpha component represents the color's **opacity**):
  - `color: hsl(50 80% 40%);`
  - `background: hsl(150deg 30% 60%);`
  - `color: hsl(0.3turn 60% 45% / .7);`
  - `background: hsl(0 80% 50% / 25%);`

?> ⚠️ **Note**: Setting an alpha channel on a color has one key difference to using the `opacity` property. When you use `opacity` you make the element and everything inside it opaque, whereas using RGB with an alpha parameter colors only makes the color you are specifying opaque.

---

## Images

The `<image>` value type is used wherever an image is a valid value. This can be an **actual image** file pointed to via a `url()` function, or a **gradient**.

```css
.image {
    background-image: url(star.png);
}

.gradient {
    background-image: linear-gradient(90deg, rgb(119, 0, 255, 1) 39%, rgb(0, 212, 255, 1) 100%);
}
```

---

## Position

The `<position>` value type represents a set of **2D coordinates**, used to position an item such as a background image (via `background-position`). It can take **keywords** such as `top`, `left`, `bottom`, `right`, and `center` to align items with specific bounds of a **2D box**, along with **lengths**, which represent **offsets** from the top and left-hand edges of the box.

A typical position value consists of two values — the first sets the position horizontally, the second vertically. If you only specify values for one axis the other will default to `center`.

```css
.box {
    height: 300px;
    width: 400px;
    background-image: url(star.png);
    background-repeat: no-repeat;
    background-position: right 40px;
}
```

---

## Functions

CSS also has [functions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions), which work in a similar way to functions in other languages. In fact, we've already seen CSS functions in the [Color](#color) section above with `rgb()` and `hsl()` functions. 

### Math functions

 One of the most common [math functions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions#math_functions) is `calc()` which lets you do operations like addition, subtraction, multiplication, and division.

 ```css
 .wrapper {
    width: 400px;
}

.box {
    width: calc(20% + 100px);
}
```

There are many other math functions that you can use in CSS, such as `min()`, `max()`, and `clamp()`; respectively these let you pick the **smallest**, **largest**, or **middle** value from a set of values.

You can also use *Trigonometric* functions like `sin()`, `cos()`, and `tan()` to calculate angles for rotating elements around a point, or choose colors that take a hue angle as a parameter.

*Exponential* functions might also be used for animations and transitions, when you require very specific control over how something moves and looks.



---

?> {docsify-updated}
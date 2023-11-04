# 07-Backgrounds and borders

> To learn how to style the background and border of boxes.

---

## Styling backgrounds in CSS

The CSS `background` property is a shorthand for a number of background longhand properties. If you discover a complex background property in a stylesheet, it might seem a little hard to understand as so many values can be passed in at once.

### Background colors

The `background-color` property defines the background color of any element in CSS. The property accepts any valid `<color>`. A background-color extends underneath the content and **padding** box of the element.

```css
.box {
    background-color: #567895;
}

h2 {
    background-color: black;
    color: white;
}

span {
    background-color: rgba(255, 255, 255, .5);
}
```

### Background images

The `background-image` property enables the display of an image in the background of an element.

```css
.box {
    background-image: url(star.png);
}
```

?> ⚠️ **Note**: If you specify a background color in addition to a background image then the image displays on top of the color.

#### Controlling background-repeat

The `background-repeat` property is used to control the tiling behavior of images. The available values are:

- `no-repeat` — stop the background from repeating altogether.
- `repeat-x` — repeat horizontally.
- `repeat-y` — repeat vertically.
- `repeat` — the default; repeat in both directions.

#### Sizing the background image

We could use the `background-size` property to size the image to fit inside the background.

The available values are:

- [`<length>`](https://developer.mozilla.org/en-US/docs/Web/CSS/length)
- [`<percentage>`](https://developer.mozilla.org/en-US/docs/Web/CSS/percentage)
- Keywords:
  - `cover` — the browser will make the image just large enough so that it completely covers the box area while still **retaining its aspect ratio**. In this case, part of the image is likely to end up **outside the box**.
  - `contain` — the browser will make the image the right size to fit inside the box. In this case, you may end up with **gaps** on either side or on the top and bottom of the image.

#### Positioning the background image

The [`background-position`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-position) property allows you to choose the position in which the background image appears on the box it is applied to. This uses a coordinate system in which the **top-left-hand** corner of the box is `(0, 0)`, and the box is positioned along the horizontal (`x`) and vertical (`y`) axes.

The default `background-position` value is `(0, 0)`.

The most common `background-position` values take two individual values — a **horizontal** value followed by a **vertical** value.

The available values are:

- [`<length>`](https://developer.mozilla.org/en-US/docs/Web/CSS/length)
- [`<percentage>`](https://developer.mozilla.org/en-US/docs/Web/CSS/percentage)
- Keywords:
  - `top`, `bottom`, `left`, `right`, `center`
- Edge offsets values:
  - for example `background-position: bottom 10px right 20px;`

?> ⚠️ **Note**: `background-position` is a shorthand for `background-position-x` and `background-position-y`, which allow you to set the different axis position values individually.

### Gradient backgrounds

A **gradient** — when used for a background — acts just like an image and is also set by using the `background-image` property.

You can read more about the different types of gradients and things you can do with them on the MDN page for the [`<gradient>`](https://developer.mozilla.org/en-US/docs/Web/CSS/gradient) data type. A fun way to play with gradients is to use one of the many **CSS Gradient Generators** available on the web, such as <https://cssgradient.io/>.

### Multiple background images

You specify **multiple** `background-image` values in a **single** property value, separating each one with a comma (`,`).

The backgrounds will layer with the **last listed** background image at the **bottom** of the stack, and each previous image stacking on top of the one that follows it in the code.

The other `background-*` properties can also have **comma-separated** values in the same way as `background-image`:

```css
.box {
    background-image:
        url(image1.png),
        url(image2.png),
        url(image3.png),
        url(image4.png);
    background-repeat:
        no-repeat,
        repeat-x,
        repeat;
    background-position:
        10px 20px,
        top right;
}
```

**Each value of the different properties will match up to the values in the same position in the other properties**. Above, for example, `image1`'s `background-repeat` value will be `no-repeat`.

However, what happens when **different properties have different numbers of values**? The answer is that **the smaller numbers of values will cycle** — in the above example there are four background images but only two `background-position` values. The first two position values will be applied to the first two images, then they will cycle back around again — `image3` will be given the first position value, and `image4` will be given the second position value.

### Background attachment

Another option for backgrounds is specifying how they scroll when the content scrolls. This is controlled using the `background-attachment` property, which can take the following values:

- `scroll`: causes the element's background to scroll when the **page** is scrolled. If the *element* content is scrolled, the background *does not move*. In effect, the background **is fixed to the same position on the page**, so it scrolls as the page scrolls.
- `fixed`: causes an element's background to be fixed to the viewport so that it doesn't scroll when the page or element content is scrolled.
- `local`: fixes the background to the element it is set on, so when you scroll the element, the background scrolls with it.

Here is a live example: <https://mdn.github.io/learning-area/css/styling-boxes/backgrounds/background-attachment.html>

### Using the background shorthand property

Using the `background` property, we can set all of the different properties at once.

If using multiple backgrounds, you need to specify all of the properties for the first background, then add your next background after a comma (`,`).

There are a few rules that need to be followed when writing background image shorthand values:

- A `background-color` may only be specified after the final comma.
- The value of `background-size` may only be included immediately **after** `background-position`, separated with the `/` character, like this: `center / 80%`.

```css
.box {
    background:
        linear-gradient(105deg, rgba(255, 255, 255, .2) 39%, rgba(51, 56, 57, 1) 96%) center center / 400px 200px no-repeat,
        url(big-star.png) center no-repeat,
        rebeccapurple;
}
```

---

## Borders

Typically when we add borders to an element with CSS we use a shorthand property that sets the color, width, and style of the `border` in one line of CSS.

We can set a border for all four sides of a box with `border`:

```css
.box {
    border: 1px solid black;
}
```

Or we can target one edge of the box, for example:

```css
.box {
    border-top: 1px solid black;
}
```

The individual properties for these shorthands would be:

```css
.box {
    border-width: 1px;
    border-style: solid;
    border-color: black;
}
```

And for the longhands:

```css
.box {
    border-top-width: 1px;
    border-top-style: solid;
    border-top-color: black;
}
```

### Rounded corners

Rounding corners on a box is achieved by using the `border-radius` property and associated longhands which relate to each corner of the box.

Two lengths or percentages may be used as a value, the **first** value defining the **horizontal** radius, and the **second** the **vertical** radius. In a lot of cases, you will only pass in one value, which will be used for both.

For example, to make all four corners of a box have a 10px radius:

```css
.box {
    border-radius: 10px;
}
```

Or to make the top right corner have a horizontal radius of 1em, and a vertical radius of 10%:

```css
.box {
    border-top-right-radius: 1em 10%;
}
```

**Longhand property should be placed after the associate shorthand property**. Otherwise, the effect of longhand properties will be covered:

```css
.box {
    border: 10px solid rebeccapurple;
    border-radius: 1em;
    border-top-right-radius: 10% 30%;
}
```



---

?> {docsify-updated}
# 06-The box model

>  To learn about the **CSS Box Model**, what makes up the box model and how to switch to the alternate model.

---

## Block and inline boxes

In CSS we have several types of boxes that generally fit into the categories of **block boxes** and **inline boxes**. The type refers to how the box behaves in terms of page flow and in relation to other boxes on the page. Boxes have an **inner display type** and an **outer display type**.

In general, you can set various values for the display type using the `display` property, which can have various values.

---

## Outer display type

If a box has an outer display type of `block`, then:

- The box will break onto a new line.
- The `width` and `height` properties are respected.
- **Padding**, **margin** and **border** will cause other elements to be pushed away from the box.
- If `width` is not specified, the box will extend in the inline direction to fill the space available in its container. In most cases, the box will become as wide as its container, *filling up 100% of the space available*.

Some HTML elements, such as `<h1>`, `<p>`, and `<div>` use `block` as their outer display type by default.

If a box has an outer display type of `inline`, then:

- The box will **not** break onto a new line.
- The `width` and `height` properties will **not apply**.
- **Top** and **bottom** padding, margins, and borders will **apply** but will **not** cause other inline boxes to **move away** from the box.
- **Left** and **right** padding, margins, and borders will **apply** and will cause other inline boxes to **move away** from the box.

Some HTML elements, such as `<a>`, `<span>`, `<em>` and `<strong>` use `inline` as their outer display type by default.

---

## Inner display type

Boxes also have an **inner** display type, which dictates **how elements inside that box are laid out**.

By default, the elements inside a box are laid out in *normal flow* and behave as **block** or **inline** boxes.

You can change the inner display type for example by setting `display: flex;`. The element will still use the outer display type `block` but this changes the inner display type to `flex`. Any *direct children* of this box will become *flex items*.

---

## What is the CSS box model?

### Parts of a box

- **Content** box: The area where your content is displayed; size it using properties like `inline-size` and `block-size` or `width` and `height`.
- **Padding** box: The padding sits around the content as white space; size it using `padding` and related properties.
- **Border** box: The border box wraps the content and any padding; size it using `border` and related properties.
- **Margin** box: The margin is the outermost layer, wrapping the content, padding, and border as whitespace between this box and other elements; size it using `margin` and related properties.

![](../_assets/_images/box-model.png ':size=500')

### The standard CSS box model

In the **standard box** model, if you give a box an `inline-size` and a `block-size` (or `width` and a `height`) attributes, this defines the inline-size and block-size (width and height in horizontal languages) of the **content box**.

If we assume that a box has the following CSS:

```css
.box {
    width: 350px;
    height: 150px;
    margin: 10px;
    padding: 25px;
    border: 5px solid black;
}
```

The actual space taken up by the box will be 410px wide (350 + 25 + 25 + 5 + 5) and 210px high (150 + 25 + 25 + 5 + 5):

![](../_assets/_images/standard-box-model.png ':size=500')

?> ⚠️ **Note**: The *margin* is **not** counted towards the actual size of the box — sure, it affects the total space that the box will take up on the page, but only the space outside the box. The **box's area stops at the border** — it does not extend into the margin.

### The alternative CSS box model

In the **alternative box** model, any width is the width of the **visible box** on the page. The content area width is that width **minus** the width for the padding and border (see image below).

To turn on the alternative model for an element, set `box-sizing: border-box;` on it.

If we assume the box has almost the same CSS as above:

```css
.box {
    box-sizing: border-box; /* turn on the alternative box model */
    width: 350px;
    height: 150px;
    margin: 10px;
    padding: 25px;
    border: 5px solid black;
}
```

Now, the actual space taken up by the box will be 350px in the inline direction and 150px in the block direction.

![](../_assets/_images/alternate-box-model.png ':size=500')

### Set alternative box model for all elements

To use the alternative box model for *all of your elements* (which is a common choice among developers), set the `box-sizing` property on the `<html>` element and set all other elements to `inherit` that value:

```css
html {
    box-sizing: border-box;
}

*,
*::before,
*::after {
    box-sizing: inherit;
}
```

?> ⚠️ **Note**: `::before` creates a pseudo-element that is the *first* **child** of the selected element. `::after` creates a pseudo-element that is the *last* **child** of the selected element.

---

## Margins, padding, and borders

### Margin

The margin is an invisible space around your box. It pushes other elements away from the box. Margins can have positive or *negative* values. Setting a negative margin on one side of your box can cause it to *overlap* other things on the page.

We can control all margins of an element at once using the `margin` property, or each side individually using the equivalent longhand properties:

- `margin-top`
- `margin-right`
- `margin-bottom`
- `margin-left`

#### Margin collapsing

Depending on whether two elements whose *margins touch* have **positive** or **negative** margins, the results will be different:

- **Two positive** margins: The **largest** individual margin.
- **Two negative** margins: The **smallest** (**furthest from zero**) individual margin.
- **One positive and one negative** margins: Their **sum**.

### Borders

For styling borders, there are a large number of properties — there are four borders, and each border has a `style`, `width`, and `color` that we might want to manipulate.

You can set the `width`, `style`, or `color` of all four borders at once using the `border` property.

To set the properties of each side individually, use:

- `border-top`
- `border-right`
- `border-bottom`
- `border-left`

To set the `width`, `style`, or `color` of a single side:

- `border-top-width`
- `border-top-style`
- `border-top-color`
- ...

### Padding

Unlike margins, you **cannot have a negative padding**. Any background applied to your element will display behind the padding.

The `padding` property controls the padding on all sides of an element. To control each side individually, use these longhand properties:

- `padding-top`
- `padding-right`
- `padding-bottom`
- `padding-left`

---

## Using display: inline-block

`display: inline-block;` is a special value of `display`, which provides a middle ground between `inline` and `block`. Use it if you do not want an item to break onto a new line, but do want it to respect `width` and `height` and avoid the overlapping.



---

?> {docsify-updated}
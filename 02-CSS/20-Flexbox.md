# 20-Flexbox

> To learn how to use the Flexbox layout system to create web layouts.

---

## Introducing a simple example

Here is the html used to demonstrate flexbox:

```html
<style>
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    .container {
        border: 1px red solid;
    }

    .item {
        border: 1px blue solid;
    }
</style>

<section class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3.1<br>3.2</div>
</section>
```

---

## Specifying what elements to lay out as flexible boxes

In this case we want to lay out the `<div>` elements, so we set the `display` property of their **parent element**:

```css
.container {
    display: flex;
}
```

This causes the `<section>` element to become a **flex container** and its children to become **flex items**.

The element we've given a `display` value of `flex` to is acting like a **block-level** element in terms of how it interacts with the rest of the page, but its **children** are laid out as **flex items**.

Note also that you can use a `display` value of `inline-flex` if you wish to lay out an element's children as flex items, but have that element behave like an inline element.

---

## The flex model

When elements are laid out as flex items, they are laid out along two axes:

![](../_assets/_images/flex_terms.png ':size=500')

---

## Columns or rows?

Flexbox provides a property called `flex-direction` that specifies which direction the main axis runs (which direction the flexbox children are laid out in).

```css
.container {
    display: flex;
    flex-direction: row;
}
```

The value of `flex-direction` can be:

- `row`
- `row-reverse`
- `column`
- `column-reverse`

---

## Wrapping

We can set fixed width for flex items. But they may **overflow** the flex container if there are too many flex items within it.

```css
.container {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}
```

The `flex-wrap` property sets whether flex items are forced onto one line or can wrap onto multiple lines. Property `flex-wrap` should be set in the **flex container**, and its value can be:

- `nowrap`
- `wrap`
- `wrap-reverse`

?> ⚠️ **Note**: `flex-flow` is the shorthand property for `flex-direction` and `flex-wrap`. For example, `flex-flow: row wrap;`.

---

## Flexible sizing of flex items

We can control what proportion of space **flex items** take up compared to the other flex items:

```css
.item {
    flex: 1;
}

.item:nth-child(3) {
    flex: 2;
}
```

The space of the flex container will be divide into 4 equal parts (since 1 + 1 + 2 = 4). The first and second flex item get 1 part respectively, and the third flex item occupies 2 parts.

The **unitless proportion value** (like `1`, `2` above) can *optionally* be followed by a **basic size** value (like `200px`) within the `flex` value:

```css
.item {
    flex: 1 200px;
}

.item:nth-child(3) {
    flex: 2 200px;
}
```

The CSS above basically states, "Each flex item will **first be given 200px** of the available space. After that, the **rest** of the available space will be shared according to the proportion units."

?> ⚠️ **Note**: `flex` is the shorthand property for `flex-grow`, `flex-shrink` and `flex-basis`.

---

## Horizontal and vertical alignment

You can also align flex items along the main or cross axis:

```css
.container {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
}
```

Property `justify-content` controls where the flex items sit on the **main axis**. Its common values:

- `flex-start`
- `flex-end`
- `center`
- `space-evenly`
- `space-around`
- `space-between`

Property `align-items` controls where the flex items sit on the **cross axis**. Its common values:

- `stretch`
- `center`
- `flex-start`
- `flex-end`

You can override the `align-items` behavior for individual **flex items** by applying the `align-self` property to them:

```css
.item:nth-child(1) {
    align-self: flex-end;
}
```

---

## Ordering flex items

Flexbox also has a feature for changing the **layout order of flex items** without affecting the source order.

```css
.item:nth-child(1) {
    order: 1;
}
```

You'll see that the first `<div>` element has been moved to the end of the main axis. Let's talk about how this works in a bit more detail:

- By default, **all** flex items have an `order` value of `0`.
- Flex items with **higher** specified order values will appear **later** in the display order than items with lower order values.
- Flex items with the same order value will appear in their source order.
- You can set **negative** order values to make items appear earlier than items whose value is 0.

---

## Nested flex boxes

It's perfectly OK to set a flex item to also be a flex container, so that its children are also laid out like flexible boxes.



---

?> {docsify-updated}
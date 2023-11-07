# 23-Positioning

> To learn how CSS positioning works.

---

## Static positioning

Static positioning is the **default** that every element gets. It just means "put the element into its normal position in the document flow — nothing special to see here."

```css
.positioned {
    position: static;
}
```

---

## Relative positioning

```css
.positioned {
    position: relative;
    top: 30px;
    left: 30px;
}
```

The element is positioned according to the normal flow of the document, and then **offset relative to itself** based on the values of `top`, `right`, `bottom`, and `left`.

---

## Absolute positioning

```css
.positioned {
    position: absolute;
    top: 30px;
    left: 30px;
}
```

The element is **removed from the normal document flow**, and **no space** is created for the element in the page layout. The element is positioned **relative to its closest positioned ancestor** (if any) or to the **initial containing block**. Its final position is determined by the values of `top`, `right`, `bottom`, and `left`.

?> ⚠️ **Note**: You can use `top`, `bottom`, `left`, and `right` to **resize** elements if you need to. Try setting `top: 0;` `bottom: 0;` `left: 0;` `right: 0;` and `margin: 0;` on your positioned elements.

?> ⚠️ **Note**: The **initial containing block** has the **dimensions of the viewport** and is also the block that contains the `<html>` element. In other words, the absolutely positioned element may be displayed outside of the `<html>` element and be positioned relative to the initial viewport.

### Introducing z-index

The `z-index` CSS property sets the **z-order** of a **positioned element** and its descendants or **flex** and **grid** items. Overlapping elements with a larger z-index cover those with a smaller one.

```css
.box1 {
    position: absolute;
    z-index: 2;
}

.box2 {
    position: absolute;
    z-index: 1;
}
```

The `.box1` element has a higher `z-index` value, so it will cover the `.box2` element.

---

## Fixed positioning

```css
.positioned {
    position: fixed;
    top: 0;
    right: 0;
}
```

The element is **removed from the normal document flow**, and **no space** is created for the element in the page layout. The element is positioned **relative to its initial containing block**, which is the **viewport** in the case of visual media. Its final position is determined by the values of `top`, `right`, `bottom`, and `left`.

?> ⚠️ **Note**: Just like the absolute positioning, you can use `top`, `bottom`, `left`, and `right` to **resize** elements if you need to. Try setting `top: 0;` `bottom: 0;` `left: 0;` `right: 0;` and `margin: 0;` on your positioned elements.

---

## Sticky positioning

Sticky positioning is basically a **hybrid** between **relative** and **fixed** position. It allows a positioned element to act like it's relatively positioned until it's scrolled to a certain **threshold** (e.g., 10px from the top of the viewport), after which it becomes fixed.

```css
.positioned {
    position: sticky;
    top: 30px;
    left: 30px;
}
```

The element is positioned according to the normal flow of the document, and then offset relative to its **nearest scrolling ancestor** and **containing block** (nearest block-level ancestor), including table-related elements, based on the values of `top`, `right`, `bottom`, and `left`.

### Scrolling index

An interesting and common use of `position: sticky;` is to create a scrolling index page where different headings stick to the top of the page as they reach it.

```html
<div class="scrolling-ancestor">
    <h1>Sticky positioning</h1>
    <dl>
        <dt>A</dt>
        <dd>Apple</dd>
        <dd>Ant</dd>
        <dd>Altimeter</dd>
        <dt>B</dt>
        <dd>Bird</dd>
        <dd>Buzzard</dd>
        <dd>Bee</dd>
        <dt>C</dt>
        <dd>Calculator</dd>
        <dd>Cane</dd>
        <dd>Camera</dd>
    </dl>
</div>
```

```css
/* Make the container become a scrolling ancestor */
.scrolling-ancestor {
    width: 300px;
    height: 10em;
    border: 1px green solid;
    margin: 50px auto;
    overflow: auto;
}

.scrolling-ancestor::after {
    content: "";
    display: block;
    height: 20em;
}

/* containing block (nearest block-level ancestor) */
dl {
    width: 80%;
    margin: 0 auto;
    padding: 0;
    border: 1px red solid;
}

/* sticky element */
dt {
    position: sticky;
    top: 0;
    margin: 0;
    background-color: rgb(138, 43, 226, 0.6);
}
```



---

?> {docsify-updated}
# 11-Sizing items in CSS

> To understand the different ways we can size things in CSS.

---

## min- and max- sizes

In addition to giving things a fixed size, we can ask CSS to give an element a **minimum** or a **maximum** size.

For example, if you have a box that might contain a variable amount of content, and you always want it to be *at least* a certain height, you could set the `min-height` property on it. This is very useful for dealing with variable amounts of content while avoiding overflow.

```css
.box {
    border: 5px solid darkblue;
    width: 200px;
    min-height: 150px;
}
```

A common use of `max-width` is to cause images to scale down if there is not enough space to display them at their intrinsic width while making sure they don't become larger than that width.

For example, if you were to set `max-width: 100%;` on an image, and its intrinsic width is smaller than its container, the image will not be forced to stretch and become larger, thus preventing pixelation.

```css
img {
    max-width: 100%;
}
```

Sizing things according to the viewport can be useful in your designs. For example, if you want a full-page hero section to *show before the rest of your content*, making that part of your page 100vh high will push the rest of the content below the viewport, meaning that it will only appear once the document is scrolled.



---

?> {docsify-updated}
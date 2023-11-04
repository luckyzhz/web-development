# 09-Overflowing content

> Overflow is what happens when there is too much content to fit in an element box.

---

## The overflow property

Using the `overflow` property, you can convey to a browser how it should handle overflow content.

`overflow` can take these values:

- `visible`: This is the default value. With it, users can see content when it overflows.
- `hidden`: Overflow content is clipped at the element's **padding** box.
- `clip`: Overflow content is clipped at the element's overflow clip edge that is defined using the `overflow-clip-margin` property.
- `scroll`: Overflow content is clipped at the element's padding box, and overflow content can be scrolled into view using **scroll bars**.
- `auto`: Overflow content is clipped at the element's padding box, and overflow content can be scrolled into view. Unlike `scroll`, user agents **display scroll bars only if the content is overflowing** and hide scroll bars by default.

?> ⚠️ **Note**: If we want the scrollbar to appear in just one axis, we can use the longhand properties, like `overflow-x: scroll`, `overflow-y: auto`.

?> ⚠️ **Note**: You can specify x- and y-axis scrolling using the `overflow` property, **passing two values**. The first value applies to `overflow-x` and the second applies to `overflow-y`. For example, `overflow: hidden scroll`.



---

?> {docsify-updated}
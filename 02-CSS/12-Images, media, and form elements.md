# 12-Images, media, and form elements

> To understand the way that some elements behave unusually when styled with CSS.

---

## object-fit

The `object-fit` CSS property sets how the content of a [replaced element](https://developer.mozilla.org/en-US/docs/Web/CSS/Replaced_element), such as an `<img>` or `<video>`, should be resized to fit its container.

The `object-fit` property is specified as a single keyword chosen from the list of values below:

- `contain`
  - The replaced content is scaled to **maintain its aspect ratio** while **fitting within the element's content box**. The entire object is made to fill the box, while preserving its aspect ratio, so the object will be "**letterboxed**" if its aspect ratio does not match the aspect ratio of the box.
- `cover`
  - The replaced content is sized to **maintain its aspect ratio** while **filling the element's entire content box**. If the object's aspect ratio does not match the aspect ratio of its box, then the object will be **clipped** to fit.
- `fill`
  - The replaced content **is sized to fill the element's content box**. The entire object will completely fill the box. If the object's aspect ratio does not match the aspect ratio of its box, then the object will be **stretched** to fit.
- `none`
  - The replaced content is not resized.
- `scale-down`
  - The content is sized as if `none` or `contain` were specified, whichever would result in a **smaller** concrete object size.

---

## Replaced elements in layout

[Replaced elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Replaced_element), when they become part of a **grid** or **flex** layout, have different default behaviors, essentially to avoid them being stretched strangely by the layout.

To force the image to stretch to fill the grid cell it is in, you'd have to do something like the following:

```css
img {
    width: 100%;
    height: 100%;
}
```

---

## Form elements

The default styling of form elements varies depending on the operating system and browser your user is using to access the site. The following "**form reset**" provide a consistent base to work from:

```css
button,
input,
select,
textarea {
    font-family: inherit;
    font-size: 100%;
    box-sizing: border-box;
    padding: 0;
    margin: 0;
}

textarea {
    overflow: auto;
}
```



---

?> {docsify-updated}
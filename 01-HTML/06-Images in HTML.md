# 06-Images in HTML

> If an image has meaning, in terms of your content, you should use an HTML image. If an image is purely decoration, you should use CSS background images.

---

## Annotating images with figures and figure captions

`<figure>` and `<figcaption>` elements are created to provide a semantic container for figures, and to clearly link the figure to the caption.

```html
<figure>
  <img
    src="images/dinosaur.jpg"
    alt="The head and torso of a dinosaur skeleton;
            it has a large head with long sharp teeth"
    width="400"
    height="341">

  <figcaption>
    A T-Rex on display in the Manchester University Museum.
  </figcaption>
</figure>
```

A figure doesn't have to be an image. It is an **independent unit of content** that expresses your meaning in a compact, easy-to-grasp way.
A figure could be several **images**, a **code snippet**, **audio**, **video**, **equations**, a **table**, or something else.

---

?> {docsify-updated}
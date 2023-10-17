# 09-Responsive images

> Learn how to use features like `srcset` and the `<picture>` element to implement responsive image solutions on websites. 

---

## Resolution switching: Different sizes

We can use two attributes — `srcset` and `sizes` — to provide several additional source images along with hints to help the browser pick the right one.

```html
<img
  srcset="elva-fairy-480w.jpg 480w, elva-fairy-800w.jpg 800w"
  sizes="(max-width: 600px) 480px,
         800px"
  src="elva-fairy-800w.jpg"
  alt="Elva dressed as a fairy">
```

`srcset` defines the set of images we will allow the browser to choose between, and what size each image is. Each set of image information is separated from the previous one by a comma. For each one, we write:
1. An **image filename** (`elva-fairy-480w.jpg`)
2. A space
3. The image's **intrinsic width in pixels** (`480w`) — note that this uses the `w` unit, not `px`. An image's intrinsic size is its real size.

`sizes` defines a set of **media conditions** (e.g. screen widths) and indicates what image size would be best to choose. In this case, before each comma we write:
1. **A media condition** (`(max-width:600px)`) — a media condition describes a possible state that the screen can be in. In this case, we are saying "*when the viewport width is 600 pixels or less*".
2. A space
3. The **width of the slot** the image will fill when the media condition is true (`480px`)

?> ⚠️ **Note**: For the slot width, rather than providing an absolute width (for example, `480px`), you can alternatively provide a width relative to the viewport (for example, `50vw`) — but not a percentage. You may have noticed that **the last slot width has no media condition** (this is the **default** that is chosen when none of the media conditions are true). The browser ignores everything after the first matching condition, so **be careful how you order the media conditions**.

So, with these attributes in place, the browser will:
1. Look at its device width.
2. Work out which media condition in the `sizes` list is the first one to be true.
3. Look at the **slot size** given to that media query.
4. Load the image referenced in the `srcset` list that has the same size as the slot or, if there isn't one, the first image that is **bigger** than the chosen slot size.

Older browsers that don't support these features will just ignore them. Instead, those browsers will go ahead and load the image referenced in the `src` attribute as normal.

---

## Resolution switching: Same size, different resolutions

If you're supporting multiple display resolutions, but everyone sees your image at the same real-world size on the screen, you can allow the browser to choose an appropriate resolution image by using `srcset` with `x`-descriptors and without `sizes`:

```html
<style>
  /* In this example, the following CSS is applied to the image so that it will have a width of 320 pixels on the screen (also called CSS pixels) */
  img {
    width: 320px;
  }
</style>

<img
  srcset="elva-fairy-320w.jpg, elva-fairy-480w.jpg 1.5x, elva-fairy-640w.jpg 2x"
  src="elva-fairy-640w.jpg"
  alt="Elva dressed as a fairy">
```

If the device accessing the page has a standard/low resolution display, with one device pixel representing each CSS pixel, the `elva-fairy-320w.jpg` image will be loaded (**the 1x is implied**, so you don't need to include it.) If the device has a high resolution of two device pixels per CSS pixel or more, the `elva-fairy-640w.jpg` image will be loaded.

---

## Art direction

The **art direction problem** involves wanting to change the image displayed to suit different image display sizes. For example, a web page includes a large landscape shot with a person in the middle when viewed on a desktop browser. When viewed on a mobile browser, that same image is shrunk down, making the person in the image very small and hard to see. It would probably be better to show a smaller, portrait image on mobile, which zooms in on the person. The `<picture>` element allows us to implement just this kind of solution.

```html
<picture>
  <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
  <source media="(min-width: 800px)" srcset="elva-800w.jpg">
  <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
</picture>
```

?> ⚠️ **Note**: You should use the `media` attribute only in art direction scenarios; when you do use `media`, don't also offer media conditions within the `sizes` attribute.

---

## Why can't we just do this using CSS or JavaScript?

When the browser starts to load a page, it starts to download (**preload**) any images before the main parser has started to load and interpret the page's CSS and JavaScript. That mechanism is useful in general for reducing page load times, but it is not helpful for responsive images — hence the need to implement solutions like `srcset`. For example, you couldn't load the `<img>` element, then detect the viewport width with JavaScript, and then dynamically change the source image to a smaller one if desired. By then, the original image would already have been loaded, and you would load the small image as well, which is even worse in responsive image terms.

---

?> {docsify-updated}
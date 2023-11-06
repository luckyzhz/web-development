# 16-Fundamental text and font styling

> To learn the fundamental properties and techniques needed to style text on web pages.

---

The CSS properties used to style text generally fall into two categories:

- **Font styles**: Properties that affect a text's font, e.g., which font gets applied, its size, and whether it's bold, italic, etc.
- **Text layout styles**: Properties that affect the spacing and other layout features of the text, allowing manipulation of, for example, the space between lines and letters, and how the text is aligned within the content box.

---

## Fonts

### Color

The `color` property sets the color of the **foreground content** of the selected elements, which is usually the *text*, but can also include a couple of other things, such as an *underline* or *overline* placed on text using the `text-decoration` property.

`color` can accept any `<color>` value type. For example:

```css
p {
    color: red;
}
```

### Font families

`font-family` property allows you to specify a font (or list of fonts). The browser will only apply a font if it is available on the machine the website is being accessed on; if not, it will just use a browser default font.

```css
p {
    font-family: Arial;
}
```

#### Web safe fonts

Web safe fonts are fonts that are **pre-installed** by many operating systems.

<https://www.cssfontstack.com/> maintains a list of web safe fonts available on Windows and macOS operating systems.

#### Default fonts

CSS defines five **generic names** for fonts: `serif`, `sans-serif`, `monospace`, `cursive`, and `fantasy`. These are very generic and the exact typefaces used from these generic names can vary between each browser and each operating system. It represents a worst case scenario where the browser will try its best to provide a font that looks appropriate.

#### Font stacks

Since you can't guarantee the availability of the fonts you want to use on your webpages (even a web font could fail for some reason), you can supply a **font stack** so that the browser has multiple fonts it can choose from.

```css
p {
    font-family: "Trebuchet MS", Verdana, sans-serif;
}
```

It is a good idea to **provide a suitable generic font name at the end of the stack** so that if none of the listed fonts are available, the browser can at least provide something approximately suitable.

### Font size

Most common units for `font-size` property:

- `px`
  - The number of pixels **high** you want the text to be.
- `em`
  - `1em` is equal to the font size set on the **parent element** of the current element we are styling (more specifically, the **width** of a capital letter **M** contained inside the parent element).
- `rem`
  - Works just like `em`, except that `1rem` is equal to the font size set on the **root element** of the document (i.e. `<html>`), not the parent element.

The `font-size` of an element is **inherited** from that element's parent element. This all starts with the **root element** of the entire document — `<html>` — the standard `font-size` of which is set to `16px` across browsers.

It is best to use `rem` where you can to keep things simple.

### Font style, font weight, text transform, and text decoration

CSS provides four common properties to alter the visual weight/emphasis of text:

- `font-style`:
  - `normal`: Sets the text to the normal font (turns existing italics off).
  - `italic`: Sets the text to use the italic version of the font, if available; if not, it will simulate italics with oblique instead.
  - `oblique`: Sets the text to use a simulated version of an italic font, created by slanting the normal version.
- `font-weight`:
  - `normal`, `bold`
  - `lighter`, `bolder`: Sets the current element's boldness to be **one step** lighter or heavier than its **parent** element's boldness.
  - `100` – `900`: Numeric boldness values that provide finer grained control than the above keywords.
- `text-transform`:
  - `none`, `uppercase`, `lowercase`, `capitalize`
  - `full-width`: Transforms all glyphs to be written inside a fixed-width square, similar to a monospace font, allowing aligning of, e.g., Latin characters along with Asian language glyphs (like Chinese, Japanese, Korean).
- `text-decoration`:
  - `none`
  - `underline`
  - `overline`
  - `line-through`

?> ⚠️ **Note**: `text-decoration` can accept multiple values at once if you want to add multiple decorations simultaneously, for example, `text-decoration: underline overline;`. Also note that `text-decoration` is a shorthand property for `text-decoration-line`, `text-decoration-style`, and `text-decoration-color`. You can use combinations of these property values to create interesting effects, for example: `text-decoration: line-through red wavy;`.

### Text drop shadows

The `text-shadow` CSS property adds shadows to text. This takes up to four values, e.g., `text-shadow: 4px 4px 5px red;`.

The four properties are as follows:

1. The **horizontal offset** of the shadow from the original text — positive values move the shadow **right**, and negative values **left**.
2. The **vertical offset** of the shadow from the original text — positive values move the shadow **up**, and negative values **down**.
3. The **blur radius**: a higher value means the shadow is dispersed more widely. If this value is not included, it defaults to 0, which means no blur.
4. The **base color** of the shadow. If not included, it defaults to `currentcolor`, i.e. the shadow's color is taken from the element's `color` property.

#### Multiple shadows

You can apply multiple shadows to the same text by including multiple shadow values separated by commas (`,`), for example:

```css
h1 {
    text-shadow:
        1px 1px 1px red,
        2px 2px 1px red;
}
```

?> ⚠️ **Note**: You can see more interesting examples of `text-shadow` usage in <https://www.sitepoint.com/moonlighting-css-text-shadow/>

---

## Text layout

### Text alignment

The `text-align` property is used to control how text is aligned within its containing content box. The available values are listed below:

- `left`, `right`, `center`
- `justify`: Use this carefully — it can look terrible, especially when applied to a paragraph with lots of long words in it. If you are going to use this, you should also think about using something else along with it, such as `hyphens`, to break some of the longer words across lines.

### Line height

The `line-height` property sets the height of each line of text. This property can not only take most length and size units, but can also take a **unitless value**, which acts as a **multiplier** and is generally considered the **best option**.

With a **unitless value**, the `font-size` gets multiplied and results in the `line-height`.

The recommended line height is around **1.5 – 2**. To set our lines of text to 1.6 times the height of the font, we'd use:

```css
p {
    line-height: 1.6;
}
```

### Letter and word spacing

The `letter-spacing` and `word-spacing` properties allow you to set the spacing between letters and words in your text.

```css
p::first-line {
    letter-spacing: 4px;
    word-spacing: 4px;
}
```

---

## Font shorthand

Many font properties can also be set through the shorthand property `font`. These are written in the following order: `font-style`, `font-variant`, `font-weight`, `font-stretch`, `font-size`, `line-height`, and `font-family`.

Among all those properties, only `font-size` and `font-family` are required when using the font shorthand property.

A forward slash (`/`) has to be put in between the `font-size` and `line-height` properties.

A full example would look like this:

```css
h1 {
    font:
        italic normal bold normal 3em/1.5 Helvetica,
        Arial,
        sans-serif;
}
```



---

?> {docsify-updated}
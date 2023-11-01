# 01-Introduction to CSS

> CSS (Cascading Style Sheets) is used to style and lay out web pages.

---

## CSS syntax

```css
h1 {
    color: red;
    font-size: 5em;
}
```

- In the above example, the CSS rule opens with a **selector**. This selects the HTML element that we are going to style. In this case, we are styling level one headings (`h1`).
- We then have a set of curly braces `{ }`.
- Inside the braces will be one or more **declarations**, which take the form of **property** and **value** pairs.
- CSS properties and values are **case-insensitive**. The property and value in a property-value pair are separated by a colon (`:`).
- This example contains two declarations, one for `color` and the other for `font-size`.

!> **Warning**: In CSS (and other web standards), it has been agreed that **US** spelling is the standard where there is language variation or uncertainty. For example, `colour` should be spelled `color`, as `colour` will not work.

---

## Applying CSS to HTML

There are three methods of applying CSS to a document: with an **external** stylesheet, with an **internal** stylesheet, and with **inline** styles.

### External stylesheet

An external stylesheet contains CSS in a separate file with a `.css` extension. This is the most common and useful method of bringing CSS to a document. You can link a single CSS file to **multiple web pages**, styling all of them with the same CSS stylesheet.

To link `styles.css` to `index.html`, add the following line somewhere inside the `<head>` of the HTML document:

```html
<link rel="stylesheet" href="styles.css">
```

This `<link>` element tells the browser that we have a stylesheet, using the `rel` attribute, and the location of that stylesheet as the value of the `href` attribute.

### Internal stylesheet

An internal stylesheet resides within an HTML document. To create an internal stylesheet, you place CSS inside a `<style>` element contained inside the HTML `<head>`.

```html
<style>
    h1 {
        color: blue;
        background-color: yellow;
        border: 1px solid black;
    }

    p {
        color: red;
    }
</style>
```

### Inline styles

Inline styles are CSS declarations that affect a single HTML element, contained within a `style` attribute.

```html
<h1 style="color: blue; background-color: yellow; border: 1px solid black;">
    Hello World!
</h1>
<p style="color: red;">This is my first CSS example</p>
```

---

## @rules

CSS [@rules](https://developer.mozilla.org/en-US/docs/Web/CSS/At-rule) provide instruction for what CSS should perform or how it should behave. Some @rules are simple with just a keyword and a value. For example, `@import` imports a stylesheet into another CSS stylesheet:

```css
@import "styles2.css";
```

One common @rule that you are likely to encounter is `@media`, which is used to create [media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries). Media queries use conditional logic for applying CSS styling.

In the example below, the stylesheet defines a default pink background for the <body> element. However, a media query follows that defines a blue background if the browser viewport is wider than 30em.

```css
body {
    background-color: pink;
}

@media (min-width: 30em) {
    body {
        background-color: blue;
    }
}
```



---

?> {docsify-updated}
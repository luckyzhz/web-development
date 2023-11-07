# 25-Beginner's guide to media queries

> To understand how to use media queries, and the most common approach for using them to create responsive designs.

---

## Media Query Basics

The simplest media query syntax looks like this:

```css
@media media-type and (media-feature-rule) {
    /* CSS rules go here */
}
```

It consists of:

- A **media type**, which tells the browser what kind of media this code is for (e.g. *print*, or *screen*).
- A **media expression**, which is a **rule**, or **test** that must be passed for the contained CSS to be applied.
- A set of **CSS rules** that will be applied if the test passes and the media type is correct.

### Media types

The possible types of media you can specify are:

- `all`
- `print`
- `screen`

The following media query will only set the font size to `12pt` if the page is printed. It will not apply when the page is loaded in a browser:

```css
@media print {
    body {
        font-size: 12pt;
    }
}
```

?> ⚠️ **Note**: Media types are **optional**; if you do not indicate a media type in your media query, then the media query will default to being for all media types.

### Media feature rules

#### Width and height

```css
@media screen and (max-width: 600px) {
    body {
        color: blue;
    }
}
```

We can use the following media feature to test the dimension of viewport:

- `width`
- `min-width`
- `max-width`
- `height`
- `min-height`
- `max-height`

In practice, using minimum or maximum values is much more useful for responsive design so you will rarely see `width` or `height` used alone.

#### Orientation

`orientation` allows us to test for **portrait** or **landscape** mode.

```css
@media (orientation: landscape) {
    body {
        color: rebeccapurple;
    }
}
```

#### Use of pointing devices

`hover` can test if the user has the ability to hover over an element, which essentially means they are using some kind of **pointing device**; touchscreen and keyboard navigation does not hover.

```css
@media (hover: hover) {
    body {
        color: rebeccapurple;
    }
}
```

---

## More complex media queries

With all of the different possible media queries, you may want to combine them, or create lists of queries — any of which could be matched.

### "and" logic in media queries

Use `and` to combine the rules.

```css
@media screen and (min-width: 600px) and (orientation: landscape) {
    body {
        color: blue;
    }
}
```

### "or" logic in media queries

Use comma (`,`) to denote logic "or".

```css
@media screen and (min-width: 600px),
screen and (orientation: landscape) {
    body {
        color: blue;
    }
}
```

### "not" logic in media queries

Use `not` to reverse the rules.

```css
@media not all and (orientation: landscape) {
    body {
        color: blue;
    }
}
```

---

## How to choose breakpoints

The points at which a media query is introduced are known as **breakpoints**.

The [Responsive Design Mode](https://firefox-source-docs.mozilla.org/devtools-user/responsive_design_mode/index.html) in Firefox DevTools is very useful for working out where these breakpoints should go.

---

## The viewport meta tag

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

This is the [viewport meta tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Viewport_meta_tag) — it exists as a way to control how mobile browsers render content.



---

?> {docsify-updated}
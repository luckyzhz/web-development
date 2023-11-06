# 18-Styling links

> To learn how to style link states, and how to use links effectively in common UI features like navigation menus.

---

## Link states

Different states of links can be styled using different pseudo-classes:

- **Link**: A link that has a destination (i.e., not just a named anchor), styled using the `:link` pseudo class.
- **Visited**: A link that has already been visited (exists in the browser's history), styled using the `:visited` pseudo class.
- **Hover**: A link that is hovered over by a user's mouse pointer, styled using the `:hover` pseudo class.
- **Focus**: A link that is focused (e.g., moved to by a keyboard user using the <kbd>Tab</kbd> key or something similar, or programmatically focused using `HTMLElement.focus()`) — this is styled using the `:focus` pseudo class.
- **Active**: A link that is activated (e.g., clicked on), styled using the `:active` pseudo class.

---

## Default styles

The default styles of links can be turned off/changed using the following CSS properties:

- `color`: for the text color.
- `cursor`: for the mouse pointer style.
- `outline`: for the text outline. Outline is a line outside of the element's border. Unlike other areas of the box, outlines don't take up space, so they don't affect the layout of the document in any way.

---

## Pseudo-class order matters

```css
a {}

/* order: LoVe Fears HAte */

a:link {}

a:visited {}

a:focus {}

a:hover {}

a:active {}
```

This order is important because link styles build on one another. For example, the styles in the first rule will apply to all the subsequent ones. When a link is activated, it's usually also hovered over.

To remember the order, you could try using a mnemonic like **L**o**V**e **F**ears **HA**te.

---

## Including icons on links

A common practice is to include icons on links to provide more of an indicator as to what kind of content the link points to.

```css
/* box-sizing: content-box */
a[href^="http"] {
    background: url("external-link-52.png") no-repeat 100% 0;
    background-size: 16px 16px;
    padding-right: 19px;
}
```

We're using the `background` shorthand instead of the individual properties. We set the path to the image we want to insert, specify `no-repeat` so we only get one copy inserted, and then specify the position as `100%` of the way to the right of the *text content*, and `0` pixels from the top.

---

## Styling links as buttons

A website navigation menu can be marked up as a set of links, and this can be styled to look like a set of control buttons or tabs that provide the user with access to other parts of the site.

First, some HTML:

```html
<nav class="container">
    <a href="#">Home</a>
    <a href="#">Pizza</a>
    <a href="#">Music</a>
    <a href="#">Wombats</a>
    <a href="#">Finland</a>
</nav>
```

And now our CSS:

```css
body,
html {
    margin: 0;
    font-family: sans-serif;
}

.container {
    display: flex;
    gap: 0.625%;
}

a {
    flex: 1;
    text-decoration: none;
    outline: none;
    text-align: center;
    line-height: 3;
    color: black;
}

a:link,
a:visited,
a:focus {
    background: palegoldenrod;
    color: black;
}

a:hover {
    background: orange;
}

a:active {
    background: darkred;
    color: white;
}
```



---

?> {docsify-updated}
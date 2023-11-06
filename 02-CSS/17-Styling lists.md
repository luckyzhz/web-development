# 17-Styling lists

> To become familiar with the best practices and properties related to styling lists.

---

## List-specific styles

There are three properties you should know about to start with, which can be set on `<ul>` or `<ol> `elements:

- `list-style-type`: Sets the type of bullets for the list.
- `list-style-position`: Sets whether the bullets, at the start of each item, appear inside or outside the lists.
- `list-style-image`: Allows you to use a custom image for the bullet.

### Bullet styles

```css
ol {
    list-style-type: upper-roman;
}
```

You can find a lot more options by checking out the [`list-style-type`](https://developer.mozilla.org/en-US/docs/Web/CSS/list-style-type) reference page.

### Bullet position

The `list-style-position` property sets whether the bullets appear **inside** the list items, or **outside** them before the start of each item.

```css
ul {
    list-style-position: inside;
}

ol {
    list-style-position: outside;
}
```

### Using a custom bullet image

```css
ul {
    list-style-image: url(star.svg);
}
```

However, this property is a bit limited in terms of controlling the **position**, **size**, etc. of the bullets. You are better off using the `background` family of properties, like this:

```css
ul {
    padding-left: 2rem;
    list-style-type: none;
}

/* Use `background` family to set bullets. */
ul li {
    padding-left: 2rem;
    background-image: url(star.svg);
    background-position: 0 0;
    background-size: 1.6rem 1.6rem;
    background-repeat: no-repeat;
}
```

### list-style shorthand

The three properties mentioned above can all be set using a single shorthand property, `list-style`. For example:

```css
ul {
    list-style: square url(example.png) inside;
}
```

The values can be listed in any order, and you can use one, two, or all three. If both a `type` and an `image` are specified, the type is used as a **fallback** if the image can't be loaded for some reason.

---

## Controlling list counting

Sometimes you might want to count differently on an ordered list — e.g., starting from a number other than 1, or counting backwards, or counting in steps of more than 1.

### start

The `start` attribute allows you to start the list counting from a number other than 1.

```html
<ol start="4">
    <li>Football</li>
    <li>Basketball</li>
    <li>Volleyball</li>
</ol>
```

### reversed

The `reversed` attribute specifies that the list's items are in reverse order. Items will be numbered from high to low.

```html
<ol start="4" reversed>
    <li>Football</li>
    <li>Basketball</li>
    <li>Volleyball</li>
</ol>
```

### value

The `value` attribute allows you to set your list items to specific numerical values.

```html
<ol>
    <li value="2">Football</li>
    <li value="4">Basketball</li>
    <li value="6">Volleyball</li>
</ol>
```



---

?> {docsify-updated}
# 03-Common HTML elements

> Introduce some basic HTML elements.

---

## Heading and paragraph

There are six heading elements: `h1`, `h2`, `h3`, `h4`, `h5`, and `h6`. Each element represents a different level of content in the document; `<h1>` represents the main heading, `<h2>` represents subheadings, `<h3>` represents sub-subheadings, and so on. Besides, `<p>` element was used to wrap paragraphs.

Here is an example:

```html
<h1>I am the title of the story</h1>

<p>I am a paragraph.</p>

<p>I am another paragraph.</p>
```

A few best practices:
- Use a **single `<h1>`** per page — this is the top level heading, and all others sit below this in the hierarchy.
- Use the headings in the **correct order**. Don't use `<h3>` to represent subheadings, followed by `<h2>` to represent sub-subheadings.
- Of the six heading levels available, you should aim to use **no more than three** per page. If you use too many levels of headings, it is advisable to spread the content over multiple pages.

---

## List

It is OK to nest one list inside another one.

### Unordered

```html
<ul>
    <li>milk</li>
    <li>eggs</li>
    <li>bread</li>
</ul>
```

### Ordered

```html
<ol>
    <li>Drive to the end of the road</li>
    <li>Turn right</li>
    <li>Go straight across the first two roundabouts</li>
</ol>
```

---

## Emphasis and importance

### Emphasis

```html
<!-- sarcastic or passive-aggressive -->
<p>I am <em>glad</em> you weren't <em>late</em>.</p>
```

### Strong importance

```html
<p>This liquid is <strong>highly toxic</strong>.</p>
```

---

?> Update on: 📅 {docsify-updated}
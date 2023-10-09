# 01-Introduction to HTML

> Introduce some basic and important concepts of HTML.

---

## Semantic

***HTML*** is the abbreviation of HyperText Markup Language. HTML determines the **structure** of web pages. HTML use a series of **semantic** *elements* to describe the structure of web pages.

---

## Anatomy of an HTML element

```html
<p class="editor-note">My cat is very grumpy</p>
```

- **The opening tag**: `<p>` means paragraph, is an opening tag, which marks where the element begins.
- **The attribute**: There are many optional attributes for elements to add extra information. The `class` attribute is often used to target many elements sharing common characteristics.
- **The content**: Contents are put between the opening and closing tag.
- **The closing tag**: `</p>` is a closing tag, which marks the where the element ends.

---

## Void elements

Not all elements follow the pattern of an opening tag, content, and a closing tag. Some elements consist of a **single tag**, which is typically used to **insert/embed** something in the document.

 For example, the `<img>` element embeds an image file onto a page:

 ```html
<img
  src="https://raw.githubusercontent.com/mdn/beginner-html-site/gh-pages/images/firefox-icon.png"
  alt="Firefox icon">
 ```

---

 ## Boolean attributes

 Some attributes are written without value. These are called **Boolean attributes**. The occurrence of a Boolean attribute implies that the corresponding property is *true*.

Here, `disabled` is a Boolean attribute:

```html
<input type="text" disabled>
```

---

## Entity references: Including special characters in HTML

In HTML, the characters `<`, `>`, `"`, `'`, and `&` are special characters. They are parts of the HTML syntax itself. If we want to show these special characters in our text, we should use *character entity references*.

Each character reference starts with an ampersand (`&`), and ends with a semicolon (`;`):

| Literal character | Character reference | Meaning |
| :---: | :---: | :---: |
| < | `&lt;` | less than |
| > | `&gt;` | great than |
| " | `&quot;` | quote |
| ' | `&apos;` | apostrophe |
| & | `&amp;` | ampersand |

?> **Note**: You don't need to use entity references for any other symbols, as modern browsers will handle the actual symbols just fine as long as your HTML's character encoding is set to **UTF-8**.

---

?> Update on: 📅 {docsify-updated}
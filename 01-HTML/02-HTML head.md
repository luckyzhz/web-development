# 02-HTML head

> HTML head contains metadata about the document.

---

## Anatomy of an HTML document

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="icon" href="./favicon.svg">
</head>

<body>
    <!-- The body part is visible to the readers. -->
</body>

</html>
```

1. `<!DOCTYPE html>`: This is the document type declaration. It tells the web browser that the document is written in HTML5, the latest version of HTML.
2. `<html lang="en"></html>`: The root element `<html>` wraps all the contents on the page. `lang="en"` indicates that the document is primarily written in English.
3. `<head></head>`: The `<head>` element is used to contain meta-information about the document.
4. `<body></body>`: The `<body>` element contains the visible content of the web page.

---

## Metadata in the head

### Charset

`<meta charset="UTF-8">`: This `<meta>` element specifies the character encoding of the document as **UTF-8**, which is a widely used character encoding that supports a wide range of characters from different languages.

!> ⚠️ **Note**: Please always use **UTF-8** character encoding for the best compatibility.

### Viewport

`<meta name="viewport" content="width=device-width, initial-scale=1.0">`: This <meta> element is often used for **responsive** web design. It sets the viewport width to the device's width and sets the initial scale to 1.0. This helps ensure that the web page displays properly on different devices and screen sizes.

### Title

`<title>Document</title>`: This `<title>` element sets the title of the web page to "Document." The text inside this element will typically appear in the browser's tab.

### Icon

`<link rel="icon" href="./favicon.svg">`: This `<link>` element can be used to specify the favicon for the web page. The `href` attribute points to `./favicon.svg`, which is a relative URL. Favicon typically appear in the browser's tab.

### Author and description

Many `<meta>` elements include `name` and `content` attributes:

- `name`: specifies the type of meta element; what type of information it contains.
- `content`: specifies the actual meta content.

For example, we can specify the author and add some description of the website:

```html
<meta name="author" content="John">
<meta name="description" content="This is my study notes">
```

---

?> Update on: 📅 {docsify-updated}
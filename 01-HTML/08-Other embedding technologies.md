# 08-Other embedding technologies

> To learn how to embed items into web pages using `<object>` and `<iframe>`, like PDF documents and other webpages.

---

## Embed PDF documents — `<object>`

```html
<object data="mypdf.pdf" type="application/pdf" width="800" height="1200">
  <p>
    You don't have a PDF plugin, but you can
    <a href="mypdf.pdf">download the PDF file. </a>
  </p>
</object>
```

It is much better to link to PDF so they can be downloaded or read on a separate page, rather than embedding them in a webpage.

---

## Embed other web documents — `<iframe>`

```html
<head>
  <style>
    iframe {
      border: none;
    }
  </style>
</head>
<body>
  <iframe
    src="https://developer.mozilla.org/en-US/docs/Glossary"
    width="100%"
    height="500"
    allowfullscreen
    sandbox>
    <p>
      <a href="/en-US/docs/Glossary">
        Fallback link for browsers that don't support iframes
      </a>
    </p>
  </iframe>
</body>
```

Try loading the above example in browser. Instead of the page you expected, you'll probably see some kind of message to the effect of "I can't open this page", and if you look at the Console in the browser developer tools, you'll see a message telling you why.
In Firefox, you'll get told something like *The loading of "https://developer.mozilla.org/en-US/docs/Glossary" in a frame is denied by "X-Frame-Options" directive set to "DENY".*

Just as we can see, not all websites allow you to embed them. We often use `<iframe>` to embed online video (like YouTube) or map:

```html
<iframe width="420" height="315" src="https://www.youtube.com/embed/QH2-TGUlwu4" frameborder="0" allowfullscreen>
</iframe>
```

---

?> {docsify-updated}
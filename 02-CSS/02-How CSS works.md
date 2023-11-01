# 02-How CSS works

> To understand the basics of how CSS and HTML are parsed by the browser.

---

## How does CSS actually work?

When a browser displays a document, it must combine the document's content with its style information. It processes the document in a number of stages, which we've listed below:

1. The browser loads the HTML (e.g. receives it from the network).
2. It converts the HTML into a **DOM** (*Document Object Model*). The DOM represents the document in the computer's memory.
3. The browser then fetches most of the resources that are linked to by the HTML document, such as embedded images, videos, and even linked CSS!
4. The browser parses the fetched CSS, and sorts the different rules by their selector types into different "buckets", e.g. element, class, ID, and so on. Based on the selectors it finds, it works out which rules should be applied to which nodes in the DOM, and attaches style to them as required (this intermediate step is called a render tree).
5. The render tree is laid out in the structure it should appear in after the rules have been applied to it.
6. The visual display of the page is shown on the screen (this stage is called painting).

![Rendering process overview](../_assets/_images/rendering.svg ':size=600')

## About the DOM

A DOM has a tree-like structure. Each element, attribute, and piece of text in the markup language becomes a [DOM node](https://developer.mozilla.org/en-US/docs/Glossary/Node/DOM) in the tree structure. The nodes are defined by their relationship to other DOM nodes. Some elements are parents of child nodes, and child nodes have siblings.

Understanding the DOM helps you design, debug and maintain your CSS because the DOM is where your CSS and the document's content meet up. When you start working with browser DevTools you will be navigating the DOM as you select items in order to see which rules apply.

## A real DOM representation

Take the following HTML code:

```html
<p>
    Let's use:
    <span>Cascading</span>
    <span>Style</span>
    <span>Sheets</span>
</p>
```

In the DOM, the node corresponding to our `<p>` element is a parent. Its children are a text node and the three nodes corresponding to our `<span>` elements. The `SPAN` nodes are also parents, with text nodes as their children:

```
P
├─ "Let's use:"
├─ SPAN
|  └─ "Cascading"
├─ SPAN
|  └─ "Style"
└─ SPAN
    └─ "Sheets"
```



---

?> {docsify-updated}
# 13-Manipulating documents

> To gain familiarity with the core DOM APIs, and the other APIs commonly associated with DOM and document manipulation.

---

## Getting html elements

We can use methods whose parameter is a **CSS selector** to get html elements:

- `document.querySelector()`: selects the **first** element matching the **CSS selector** you pass into.
- `document.querySelectorAll()`: selects **every** elements matching the **CSS selector** you pass into, and stores references to them in an array-like object called a `NodeList`.

For example:

```js
const header = document.querySelector("header");
const cards = document.querySelectorAll(".card");
```

---

## Creating and placing new nodes

We can use methods `document.createElement()` or `document.createTextNode()` to create new nodes, and then, use method `.appendChild()` to append the nodes to elements. 

For example:

```js
const sect = document.querySelector("section");

// Create a new paragraph.
const para = document.createElement("p");
para.textContent = "MDN Web Docs";

// Append the paragraph node to the `section` element.
sect.appendChild(para);

// Create a text node.
const text = document.createTextNode(
    " — the premier source for web development knowledge.",
);

// Append the text node to the paragraph node.
para.appendChild(text);
```

---

## Moving and removing elements

Suppose we have some html code like this:

```html
<section>
    <p>1</p>
    <p>2</p>
    <p>3</p>
</section>
```

We can move the first paragraph to the bottom of the section:

```js
const sect = document.querySelector("section");
const para1 = document.querySelector("p:nth-child(1)");
sect.appendChild(para1);
```

Here, `para1` is just like a **pointer** in C++. So the above operation will **not** generate a second copy of the paragraph node. If you wanted to make a copy and add that as well, you'd need to use `Node.cloneNode()` instead.

We can use method `.removeChild()`  to remove elements' child nodes:

```js
sect.removeChild(para1);
```

We can use method `.remove()` to remove a node based only on a reference to itself:

```js
sect.remove();
```

---

## Manipulating styles

### inline styles

We can add **inline styles** directly onto elements. This is done with the `HTMLElement.style` property.

```js
const para = document.querySelector("p");

// Set inline styles.
para.style.color = "white";
para.style.backgroundColor = "black";
para.style.padding = "10px";
para.style.width = "250px";
para.style.textAlign = "center";
```

?> ⚠️ **Note**: Notice how the JavaScript property versions of the CSS styles are written in **lower camel case** whereas the CSS versions are hyphenated (**kebab-case**) (e.g. `backgroundColor` versus `background-color`).

### Using class attribute to toggle styles

This is our html code:

```html
<style>
    .highlight {
        color: white;
        background-color: black;
        padding: 10px;
        width: 250px;
        text-align: center;
    }
</style>

<section>
    <p>1</p>
    <p>2</p>
    <p>3</p>
</section>
```

We write the styles given to a specific class in advance. This way, as soon as that class is added to an element, the element renders with our predefined style.

We can use method `.setAttribute()` to set classes:

```js
const paras = document.querySelectorAll("p");
for (para of paras) {
    para.setAttribute("class", "highlight");
}
```



---

?> {docsify-updated}
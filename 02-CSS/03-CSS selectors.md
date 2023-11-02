# 03-CSS selectors

> To learn how CSS selectors work in detail.

---

## Selector lists

If you have more than one thing which uses the same CSS then the individual selectors can be combined into a **selector list** so that the rule is applied to all of the individual selectors.

Use commas (`,`) to separate every *selector* of the *selector list*:

```css
h1,
.special {
    color: blue;
}
```

!> **Warning**: If **any** selector of the selector list is syntactically invalid, the **whole** rule will be ignored.

---

## Type, class, and ID selectors

### Type selectors

A **type selector** is sometimes referred to as a *tag name selector* or *element selector* because it selects an HTML tag/element in your document.

```css
span {
    background-color: yellow;
}

strong {
    color: rebeccapurple;
}

em {
    color: rebeccapurple;
}
```

### The universal selector

The **universal selector** is indicated by an asterisk (`*`). It selects everything in the document (or inside the parent element if it is being chained together with another element and a descendant combinator).

```css
* {
    margin: 0;
}
```

One use of the universal selector is to make selectors easier to read and more obvious in terms of what they are doing.

For example, if we wanted to select any descendant elements of an `<article>` element that are the first child of their parent, including direct children, and make them bold, we could use the `:first-child` pseudo-class.

```css
article :first-child {
    font-weight: bold;
}
```

However, this selector could be confused with `article:first-child`, which will select any `<article>` element that is the first child of another element.

To avoid this confusion, we can add the universal selector to the `:first-child` pseudo-class, so it is more obvious what the selector is doing:

```css
article *:first-child {
    font-weight: bold;
}
```

### Class selectors

The class selector starts with a dot (`.`) character. It will select everything in the document with that class applied to it.

```css
.highlight {
    background-color: yellow;
}
```

#### Targeting classes on particular elements

You can create a selector that will target specific elements with the class applied. We do this by using the type selector for the element we want to target, with the class appended using a dot, with **no** white space in between.

```css
span.highlight {
    background-color: yellow;
}

h1.highlight {
    background-color: pink;
}
```

#### Target an element if it has more than one class applied

You can apply multiple classes to an element and target them individually, or only select the element when all of the classes in the selector are present.

We can tell the browser that we only want to match the element if it has two classes applied by chaining them together with **no** white space between them.

```css
.notebox.warning {
    border-color: orange;
    font-weight: bold;
}

.notebox.danger {
    border-color: red;
    font-weight: bold;
}
```

### ID selectors

An ID selector begins with a `#` rather than a dot character, but is used in the same way as a class selector. However, an ID can be used only once per page, and elements can only have a single id value applied to them.

```css
#one {
    background-color: yellow;
}

h1#heading {
    color: rebeccapurple;
}
```

---

## Attribute selectors

### Presence and value selectors

These selectors enable the selection of an element based on the presence of an attribute alone (for example `href`), or on various different matches against the value of the attribute.

| Selector | Example | Description |
| :--- | :--- | :--- |
| `[attr]` | `a[title]` | Matches elements with an *attr* attribute (whose name is the value in square brackets). |
| `[attr=value]` | `a[href="https://example.com"]` | Matches elements with an *attr* attribute whose value is exactly *value* — the string inside the quotes. |
| `[attr~=value]` | `p[class~="special"]` | Matches elements with an *attr* attribute whose value is exactly *value*, or contains *value* in its (**space separated**) list of values. |
| `[attr\|=value]` | `div[lang\|="zh"]` | Matches elements with an *attr* attribute whose value is exactly *value* or **begins** with *value* immediately followed by a **hyphen** (`-`). |

### Substring matching selectors

These selectors allow for more advanced matching of substrings inside the value of your attribute.

| Selector | Example | Description |
| :--- | :--- | :--- |
| `[attr^=value]` | `li[class^="box-"]` | Matches elements with an *attr* attribute, whose value **begins with** *value*. |
| `[attr$=value]` | `li[class$="-box"]` | Matches elements with an *attr* attribute whose value **ends with** *value*. |
| `[attr*=value]` | `li[class*="box"]` | Matches elements with an *attr* attribute whose value **contains** *value* |

?> ⚠️ **Note**: If you want to match attribute values **case-insensitively** you can use the value `i` (means ignore) before the closing bracket, like `li[class^="a" i]`.

---

## Pseudo-classes and pseudo-elements

### What is a pseudo-class?

A pseudo-class is a selector that selects elements that are in a **specific state**, e.g. they are the first element of their type, or they are being hovered over by the mouse pointer. They tend to act **as if** you had applied a **class** to some part of your document, often helping you cut down on excess classes in your markup, and giving you more flexible, maintainable code.

Pseudo-classes are keywords that start with a colon (`:`). Here are some commonly used pseudo-classes:
- `:first-child`
- `:last-child`
- `:only-child`
- `:invalid`
- `:hover`
- `:focus`
- `:link`
- `:visited`

?> ⚠️ **Reference**: Learn more kinds of pseudo-classes in https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes.

### What is a pseudo-element?

Pseudo-elements act **as if** you had added a whole **new HTML element** into the markup, rather than applying a class to existing elements.

Pseudo-elements start with a double colon `::`. Here are some commonly used pseudo-elements:
- `::first-line`
- `::before `
- `::after`

?> ⚠️ **Reference**: Learn more kinds of pseudo-elements in https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements.

---

## Combinators

### Descendant combinator

The **descendant combinator** — typically represented by a single space (` `) character — combines two selectors such that elements matched by the second selector are selected if they have an ancestor (parent, parent's parent, parent's parent's parent, etc.) element matching the first selector.

In the example below, we are matching only the `<p>` element which is inside an element with a class of `.box`:

```css
.box p {
    color: red;
}
```

### Child combinator

The child combinator (`>`) is placed between two CSS selectors. It matches only those elements matched by the second selector that are the **direct children** of elements matched by the first.

```css
article>p {
    color: red;
}
```

### Next-sibling combinator

The **next-sibling combinator** (`+`) is placed between two CSS selectors. It matches only those elements matched by the second selector that are the **next sibling** element of the first selector. For example, to select all `<p>` elements that are **immediately** preceded by a `<h1>` element:

```css
h1+p {
    background-color: #333;
    color: #fff;
}
```

### Subsequent-sibling combinator

If you want to select siblings of an element even if they are not directly adjacent, then you can use the **subsequent-sibling combinator** (`~`).

```css
h1~p {
    background-color: #333;
    color: #fff;
}
```

### Creating complex selectors with nesting

The CSS nesting module allows you to write nested rules that use combinators to create complex selectors.

```css
p {
    ~img {}
}

/* This is parsed by the browser as */
p~img {}
```

```css
parent {
    /* parent styles */
    & child {
        /* child of parent styles */
    }
}

/* the browser will parse both of these as */
parent {
    /* parent styles */
}

parent child {
    /* child of parent styles */
}
```

### Using combinators

You can combine any of the selectors that we discovered in previous lessons with combinators in order to pick out part of your document. For example, to select list items with a class of "a" which are direct children of a `<ul>`, try the following:

```css
ul>li[class="a"] {
    color: red;
}
```



---

?> {docsify-updated}
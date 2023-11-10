# 04-Introduction to events

> To understand the fundamental theory of events, how they work in browsers.

---

## addEventListener()

`addEventListener()`

Some common events:

- `click`
- `dblclick`
- `focus`
- `blur`
- `mouseover`
- `mouseout`

```js
const btn = document.querySelector("button");
btn.addEventListener("click", function1);

const input = document.querySelector(`input[type="text"]`);
input.addEventListener("blur", function2);

const image = document.querySelector("img");
image.addEventListener("mouseover", function3);

const video = document.querySelector("video");
video.addEventListener("dblclick", function4);
```

---

## Removing listeners

`removeEventListener()`

```js
btn.removeEventListener("click", function1);
```

Event handlers can also be removed by passing an `AbortSignal` to `addEventListener()` and then later calling `abort()` on the controller owning the `AbortSignal`.

```js
const controller = new AbortController();

btn.addEventListener(
    "click",
    function1,
    { signal: controller.signal } // pass an AbortSignal to this handler
);

// removes all event handlers associated with this controller
controller.abort();
```

---

## Event objects

Sometimes, inside an event handler function, you'll see a parameter specified with a name such as `event`, `evt`, or `e`. This is called the **event object**, and it is automatically passed to event handlers to provide extra features and information.

```js
// The background color of the button changes when clicked
const btn = document.querySelector("button");

function random(number) {
    return Math.floor(Math.random() * (number + 1));
}

function bgChange(e) {
    const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
    e.target.style.backgroundColor = rndCol;
    console.log(e);
}

btn.addEventListener("click", bgChange);
```

The `target` property of the **event object** is always a reference to the element the event occurred upon.

Most event objects have a standard set of properties and methods available on the event object; see the [`Event`](https://developer.mozilla.org/en-US/docs/Web/API/Event) object reference for a full list.

---

## Preventing default behavior

Sometimes, you'll come across a situation where you want to prevent an event from doing what it does by default.

The most common example is that of a web form, for example, a custom registration form. When the user clicks the submit button, you may want to prevent the form from being submitted to the server if the information in the form is incorrect.

Here is a simple check inside a handler for the `submit` event (the `submit` event is fired on a form when it is submitted) that tests whether the text fields are empty. If they are, we call the `preventDefault()` function on the event object — which stops the form submission — and then display an error message in the paragraph below our form to tell the user what's wrong:

```html
<form>
    <div>
        <label for="fname">First name: </label>
        <input id="fname" type="text">
    </div>
    <div>
        <label for="lname">Last name: </label>
        <input id="lname" type="text">
    </div>
    <div>
        <input id="submit" type="submit">
    </div>
</form>
<p></p>
```

```js
const form = document.querySelector("form");
const fname = document.getElementById("fname");
const lname = document.getElementById("lname");
const para = document.querySelector("p");

form.addEventListener("submit", (e) => {
    if (fname.value === "" || lname.value === "") {
        e.preventDefault();
        para.textContent = "You need to fill in both names!";
    }
});
```

---

## Event bubbling

Event bubbling describes how the browser handles events targeted at nested elements.

### Bubbling example

```html
<div id="container">
    <button>Click me!</button>
</div>
<pre id="output"></pre>
```

```js
const output = document.querySelector("#output");
function handleClick(e) {
    output.textContent += `You clicked on a ${e.currentTarget.tagName} element\n`;
}

const container = document.querySelector("#container");
const button = document.querySelector("button");

container.addEventListener("click", handleClick);
button.addEventListener("click", handleClick);
```

You'll see that all two elements fire a click event when the user clicks the button:

```
You clicked on a BUTTON element
You clicked on a DIV element
```

In this case:

- the click on the `button` fires first
- followed by the click on its parent (the `<div>` element)

This makes sense: the `button` is inside the `<div>`, so when you click the button you're also implicitly clicking the element it is inside. We describe this by saying that the event **bubbles up** from the innermost element that was clicked.

### stopPropagation()

The `Event` object has a function available on it called `stopPropagation()` which, when called inside an event handler, prevents the event from bubbling up to any other elements.

```js
const output = document.querySelector("#output");
function handleClick(e) {
    e.stopPropagation(); // prevents the event from bubbling up
    output.textContent += `You clicked on a ${e.currentTarget.tagName} element\n`;
}

const container = document.querySelector("#container");
const button = document.querySelector("button");

container.addEventListener("click", handleClick);
button.addEventListener("click", handleClick);
```

Now, you'll see that only the innermost elements fire a click event when the user clicks the button:

```
You clicked on a BUTTON element
```

### Event capture

An alternative form of event propagation is **event capture**. This is like event bubbling but the order is **reversed**: the event fires first on the *least* nested element, and then on successively more nested elements, until the target is reached.

Event capture is disabled by default. To enable it you have to pass the `capture` option in `addEventListener()`.

```js
const output = document.querySelector("#output");
function handleClick(e) {
    output.textContent += `You clicked on a ${e.currentTarget.tagName} element\n`;
}

const container = document.querySelector("#container");
const button = document.querySelector("button");

container.addEventListener("click", handleClick, { capture: true });
button.addEventListener("click", handleClick);
```

In this case, the order of messages is reversed: the `<div>` event handler fires first, followed by the `<button>` event handler:

```
You clicked on a DIV element
You clicked on a BUTTON element
```

By default almost all event handlers are registered in the bubbling phase, and this makes more sense most of the time.

---

## Event delegation

Sometimes, we want some code to run when the user interacts with any one of *a large number of child elements*; we **set the event listener on their parent**, rather than set on every child individually.

```html
<div id="container">
    <div class="tile"></div>
    <div class="tile"></div>
    <div class="tile"></div>
    <div class="tile"></div>
</div>

<style>
    .tile {
        outline: 1px red dotted;
        height: 100px;
        width: 25%;
        float: left;
    }
</style>
```

We set the click event handler on the parent, and rely on **event bubbling** to ensure that the handler is executed when the user clicks on a tile:

```js
function random(number) {
    return Math.floor(Math.random() * (number + 1));
}

function bgChange(e) {
    const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
    e.target.style.backgroundColor = rndCol;
    console.log(e);
}

const container = document.querySelector("#container");
container.addEventListener("click", bgChange);
```

?> ⚠️ **Note**: `event.target` points **innermost** element. If we want to access the element that handle the event (in this case the **container**) we could use `event.currentTarget`.



---

?> {docsify-updated}
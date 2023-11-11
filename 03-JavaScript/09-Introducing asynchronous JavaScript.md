# 09-Introducing asynchronous JavaScript

> To gain familiarity with what asynchronous JavaScript is, how it differs from synchronous JavaScript, and why we need it.

---

Asynchronous programming is a technique that enables your program to start a potentially long-running task and still be able to be responsive to other events while that task runs, rather than having to wait until that task has finished. Once that task has finished, your program is presented with the result.

What asynchronous functions can do:

1. Start a **long-running operation** by calling a function.
2. Have that function start the operation and **return immediately**, so that our program can still be responsive to other events.
3. **Notify us with the result** of the operation when it eventually completes.

Many functions provided by browsers, especially the most interesting ones, can potentially take a long time, and therefore, are asynchronous. For example:

- Making HTTP requests using `fetch()`
- Accessing a user's camera or microphone using `getUserMedia()`
- Asking a user to select files using `showOpenFilePicker()`

---

## Event handlers

**Event handlers** are really a form of asynchronous programming: you provide a function (the event handler) that will be called, not right away, but whenever the event happens.

If "**the event**" is "**the asynchronous operation has completed**", then that event could be used to notify the caller about the result of an asynchronous function call.

For example, we can create a new `XMLHttpRequest` and listen for its `loadend` event.

```html
<button id="xhr">Click to start request</button>
<button id="reload">Reload</button>

<pre readonly class="event-log"></pre>
```

```js
const log = document.querySelector(".event-log");

document.querySelector("#xhr").addEventListener("click", () => {
    log.textContent = "";

    const xhr = new XMLHttpRequest();

    // `loadend` will not happen immediately
    xhr.addEventListener("loadend", () => {
        log.textContent = `${log.textContent}Finished with status: ${xhr.status}`;
    });

    xhr.open(
        "GET",
        "https://raw.githubusercontent.com/mdn/content/main/files/en-us/_wikihistory.json",
    );
    xhr.send();
    log.textContent = `${log.textContent}Started XHR request\n`;
});

document.querySelector("#reload").addEventListener("click", () => {
    log.textContent = "";
    document.location.reload();
});
```

After adding the event listener we send the request. Note that **after this, we can log "Started XHR request"**: that is, **our program can continue to run while the request is going on**, and our event handler will be called when the request is complete.

---

## Callbacks

An event handler is a particular type of callback. A **callback** is just **a function that's passed into another function**, with the expectation that the callback will be called at the appropriate time.

However, callback-based code can get hard to understand when the callback itself has to call functions that accept a callback.

For these reasons, most modern asynchronous APIs don't use callbacks. Instead, the foundation of asynchronous programming in JavaScript is the `Promise`.



---

?> {docsify-updated}